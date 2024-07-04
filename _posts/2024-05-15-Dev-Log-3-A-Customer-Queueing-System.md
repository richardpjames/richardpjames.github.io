---
layout: post
title: Dev Log 3 - A Customer Queueing System
author: Richard James
imageurl: /assets/images/dev-log-3/withmodels.png
---

After a few prototypes I have settled on an idea for my first small game. It revolves around running a series of food trucks nestled in a forest. A number of customers wander the paths and choose which food they want to buy. A number of factors influence this, with the weather and individual customer preferences being taken into account. With increasing rent to pay, and random events, you have to try an keep afloat for as long as possible.

The first mechanic that I really wanted to nail down was having the customers walk around the park and then queue for their food. The idea is that there is one person being served at a time, and the remaining customers queue up behind.

I don't want the queues to snake around forever, so they are capped at a small number (five) and then a label shows the actual length of the queue.

The final result is shown in a small gif below to give you an idea of what we are aiming for, and what we are going to build.

<img src="/assets/images/dev-log-3/animatedqueue.gif" class="img-fluid rounded mx-auto d-block px-5" />

## Step One: The NavMesh

The first challenge is setting up pathfinding for the customers. To do this we need to utilise the NavMash functionality within Godot. I only want customers to be able to walk along the paths, so I have set up a NavMesh node with a GridMap containing only the paths sitting beneath it as a child.

When baking the NavMesh - this means that our customers are only allowed to navigate around the paths in that particular GridMap.

<img src="/assets/images/dev-log-3/navmesh.png" class="img-fluid rounded mx-auto d-block px-5" />

A number of additional GridMap nodes (not underneath the NavMesh) and individual scenery pieces complete the rest of the park. Our customers will not be able to walk in any of these other areas.

<img src="/assets/images/dev-log-3/withmodels.png" class="img-fluid rounded mx-auto d-block px-5" />

The Park in TotalThe Godot Docs (which are excellent) have examples for integrating RigidBody and CharacterBody objects into the NavMesh. You can find the example for CharacterBody3D [here](https://docs.godotengine.org/en/stable/tutorials/navigation/navigation_introduction_3d.html)! I am using these examples largely as-is and they work perfectly.

## Step Two: Wandering

Now that we have a NavMesh and some boilerplate code for moving a character to a specific position, I needed to implement the wandering behaviour which would have the customers navigating around the park.

To do this I created a new Node3D and a number of Marker3D nodes as children. These represent random points on the path which a character will select from and walk towards. When they reach their destination, they will pick another new node and begin walking again.

The real challenge with this is picking a sensible number and position of points to give the customers believable behaviour and ensuring that they will pass all of the food stalls and not clump in certain areas. With my current POC only three stalls exist, but as this grows this could become a challenge (one to keep an eye on).

## Step Three: Queueing

So far, we're not doing anything too complicated or unique, we just have a number of characters wandering aimlessly around our level. Where we want to get to is that they can pass by a food stall and decide that they want to eat there.

In my intial design, I had the idea of utilising a "QueueManager" who would have visbility of all of the customers and the various queues and stalls and could then assign customers to queues as needed. I actually did an initial implementation with this approach, but it became very difficult to manage relatively quickly. Issues included:

* Complexity - having to keep track of all queues and customers within a single component, meant a complexity in the data structures needed.
* Separation of concerns - the QueueManager needed to have references to all of the customers, and all of the queues, so they became more tightly coupled.
* Having the customers behave naturally, as the QueueManager would override their state, having them make large trips to get to food and then having to manage which customers arrived first so that they didn't queue in an odd order.

Yet again - the value of trying something (and not getting bogged down in the design) shows through. By learning from an initial (quick) approach I was able to refine to the following:

* Each queue is an object in the game world. It has a point at which the customer being served stands, a point at which the queue forms and two Area3D nodes with collision shapes to detect a customer arriving at the counter, and to capture customers who are passing by.
* Customers continue to wander the level at random. They also have a number of properties that define how much they like each type of food (a random number from 0 to 1) and a "consider_queue" method which is called when they pass a stall.
* So - when a customer enters the Area3D for the queue, the customer is passed the product being sold and generates a random number to determine whether to join the queue (using our consider_queue method). A true/false is then passed back to the queue itself who can add the customer and move them to the right spot.

In this design there is no component that needs to know about all of the queues, or about all of the customers. They all exist independently but have a defined method for communicating. This removed a lot of the coupling and complexity from the approach, and gave a nicer result in terms of how the customers appear to behave.

## Step Four: The Maths

I'm not going to go through all of the maths to make the queues work and look nice, but here are some things to consider:
* How to make the queue point in the right direction (180 degrees away from the service hatch).
* How to make sure that customers don't queue up on top of each other and the length of the queue is capped.
* How to make sure that the label for the queue length is always in the right position and oriented towards the camera.

If you'd like to see my solutions here is the GDScript for the queue and for the customer:

### queue.gd:

```
extends Node

# We need to know which product we are selling and the area which triggers customers
@export var product: Constants.PRODUCT
@export var consideration_area: Area3D
@export var queue_size: int = 5
@export var queue_offset: float = 1

# The spacial points that represent the queue areas
@onready var serving_point = $ServingPoint
@onready var queue_point = $QueuePoint
@onready var serving_area = $ServingArea
# The timer for use when serving customers
@onready var serve_timer = $ServeTimer
# The label for the size of the queue
@onready var size_label = %SizeLabel

# States for the queue
enum STATES {WAITING, SERVING}
var current_state

# This holds the queue of customers
var queue = []
# Holds the current customer
var current_customer

# Called when the node enters the scene tree for the first time.
func _ready():
 # Connect our collision areas
 consideration_area.body_entered.connect(on_consideration_body_entered)
 serving_area.body_entered.connect(on_serving_area_body_entered)
 # Set the initial state to waiting
 current_state = STATES.WAITING

func _process(_delta):
 # First deal with the label for the queue size
 var camera = get_tree().get_root().get_camera_3d()
 # Find the position of the queue on the screen from the camera
 var screen_position = camera.unproject_position(queue_point.global_position)
 # Move the label to that position
 size_label.set_position(Vector2(screen_position.x, screen_position.y - 50))
 # Then process the queue
 if current_state == STATES.WAITING:
  if queue.size() > 0:
   # Get the first customer in the queue and move them to the serving point
   var customer = queue[0]
   customer.move_to_point(serving_point.global_position)
   # Remove the customer from the queue and recalculate positions
   queue.remove_at(0)
   update_label()
   calculate_queue_positions()
   # We are now serving and want to track our current customer
   current_state = STATES.SERVING
   current_customer = customer

func update_label() -> void:
 size_label.text = "%s" % queue.size()

func on_serving_area_body_entered(body) -> void:
 if body == current_customer:
  serve_timer.start()

func _on_serve_timer_timeout():
 if current_customer.has_method("serve"):
  current_customer.serve(product)
  SignalManager.on_product_sold.emit(product)
  current_state = STATES.WAITING

func on_consideration_body_entered(body) -> void:
 # If the body can consider joining the queue
 if body.has_method("consider_queue"):
  # and they decide that they do want to join
  if body.consider_queue(product):
   # Then add the body and recalculate positions
   queue.append(body)
   update_label()
   calculate_queue_positions()

# Move all of the queue members to the correct spot
func calculate_queue_positions():
 for i in range(queue.size()):
  queue[i].move_to_point(calculate_offset(i))

# Calculate the correct queue position based on start and offset
func calculate_offset(position: int) -> Vector3:
 position = clamp(position,0,queue_size)
 # Find the direction between the queue and the stand
 var direction = serving_point.global_position.direction_to(queue_point.global_position)
 # Deal with any tiny variances
 direction = direction.round()
 return queue_point.global_position + ((position - 1) * direction * queue_offset)
```
### customer.gd
```
extends CharacterBody3D
class_name Customer
# Reference to this object
@onready var customer = $"."
# Our navigation agent for moving around the scene
@onready var navigation_agent = $NavigationAgent
# Variable for speed
@export var movement_speed: float = 4.0
# Get a reference to the points we can wander
@export var wander_points: Node3D
# Track where the exit is
@export var exit_location: Area3D
# Minimum and maximum cash amounts
@export var min_money: int = 2
@export var max_money: int = 12
# Track the customer money
var money: int
# The avalable states for the customer
enum STATES {QUEUEING, WANDERING, LEAVING}
# The customers current state
var current_state: STATES
# Store which products the customer has already purchased
var already_purchased: Array[Constants.PRODUCT] = []
# Dictionary to hold all of the products with a random propensity
var product_propensity = {}

# Called when the node enters the scene tree for the first time.
func _ready():
 # Generate randomly how much a customer likes each product
 for i in Constants.PRODUCT:
  product_propensity[i] = randf()
 # Generate random monetary amount
 money = randi_range(min_money,max_money)
 wander()

# Physics function handles movement with the navigation agent
func _physics_process(delta):
 # If navigation is completed then no need to continue
 if navigation_agent.is_navigation_finished():
  # If wandering and we've reached the end, pick another point
  if current_state == STATES.WANDERING:
   wander()
  # Otherwise we are queueing so need to stand still
  else:
   return
 var next_path_position: Vector3 = navigation_agent.get_next_path_position()
 look_at(next_path_position)
 var new_velocity: Vector3 = global_position.direction_to(next_path_position) * movement_speed
 if navigation_agent.avoidance_enabled:
  navigation_agent.set_velocity(new_velocity)
 else:
  _on_velocity_computed(new_velocity)

# Callback from the navigation agent
func _on_velocity_computed(safe_velocity: Vector3):
 velocity = safe_velocity
 move_and_slide()

func move_to_point(point: Vector3):
 # Set the target position based on the marker passed in
 navigation_agent.set_target_position(point)
 
# What happens once the customer has been served
func serve(product: Constants.PRODUCT):
 # Pay for the product
 money -= GameManager.prices[product]
 # Keep a track of what the customer has purchased
 already_purchased.append(product)
 # If run out of money then leave the food court - or if we have purchased everything
 if money < 0 or already_purchased.size() == Constants.PRODUCT.size():
  leave()
 # Otherwise we just continue to wander
 else:
  wander()

func consider_queue(product: Constants.PRODUCT) -> bool:
 # Check if we have already purchased this product
 if not already_purchased.has(product):
  var rand = randf()
  # Check if the customer likes this enough to queue and isn't leaving
  if rand < product_propensity[Constants.PRODUCT.keys()[product]] and current_state == STATES.WANDERING:
   # If happy add to the queue and start queueing
   current_state = STATES.QUEUEING
   # Returns true to state that they want to join the queue
   return true
 # Returns false if not wanting to join a queue
 return false

func wander() -> void:
 # Select a random point to wander towards
 var point = wander_points.get_children().pick_random()
 move_to_point(point.global_position)
 # Set the state
 current_state = STATES.WANDERING

func leave() -> void:
 # Go to the exit and set the state
 move_to_point(exit_location.get_marker().global_position)
 current_state = STATES.LEAVING
 ```