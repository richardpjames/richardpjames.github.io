---
layout: post
title: Resolving Issues with Huion Pen Tablets (Photoshop and Krita)
author: Richard James
imageurl: /assets/images/huion/cover.webp
---

I’ve recently picked up a Huion tablet in order to help with game art creation. I had read a few reviews online which mentioned some driver issues, which I decided I could probably live with given that the model I opted for is a mere £20 on eBay.

However, I experienced a number of problems which were dealbreakers:

* Jittery performance in Adobe Photoshop (lines skipping, software stalling)
* No pressure sensitivity being detected in Adobe Photoshop and Krita
* Shortcut buttons on the tablet not working

I took the steps below through the Huion Tablet software to resolve these issues and now I am completely happy with how the tablet is running.

Firstly, download the latest set of drivers from the [Huion Website here](https://huion.com/download).

Next, through the Huion Software uncheck the “Enable Windows ink” setting under “Digital Pen > Press Key”

<img src="/assets/images/huion/step1.png" class="img-fluid rounded mx-auto d-block px-5" />

Next, open “Settings > About > Software Diagnosis”

<img src="/assets/images/huion/step2.png" class="img-fluid rounded mx-auto d-block px-5" />

Finally, click both of the “Repair” options and the “Enable” option, only for Wintab.

<img src="/assets/images/huion/step3.png" class="img-fluid rounded mx-auto d-block px-5" />


If you can’t see the enable options, you may need to start Photoshop for the Huion software to recognise it.

Photoshop should now be working, with pressure sensitivity enabled and with smooth drawing.

In Krita — navigate to “Settings > Configure Krita > Tablet Settings” and ensure that WinTab is selected. This will configure Krita in the same way as Photoshop.

<img src="/assets/images/huion/step4.png" class="img-fluid rounded mx-auto d-block px-5" />


You may need to restart for changes to take effect, but this should get you up and running with Krita and Photoshop.