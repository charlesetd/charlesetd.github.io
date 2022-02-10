---
title:  "Half Scale Pinball Slingshot"
date:   2022-02-09 19:56:16 -0600
categories: system-shock-pinball
tags: pinball video
---

This week I show off a video of the functioning prototype slingshot assembly complete with multi-colored LED lighting.

## Testing

Last post I said I'd be working on the in/out-lanes next but I finally got all the parts in to run a full test on my slingshot assembly and just couldn't wait. The video below demonstrates the assembly with a few different general illumination colors and explains how it all works.

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/bvdvDqhvvm8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

For this test, I just used an [Arduino 4 Relays Shield](https://store-usa.arduino.cc/products/arduino-4-relays-shield) and some simple code to fire the solenoid for 1/10th of a second when either sensor triggered. I also wrote in a delay forcing the solenoid to remain off for at least one second after firing to give it time to cool down (not that it gets that hot from the short burst anyways). I don't plan on using relays to drive the solenoids in the final machine as most will require PWM signals but the Arduino is sufficient for prototyping.

Overall, I'm really happy with how the assembly turned out. That said, this is by no means the final version as there are a few quirks I need to work out.

## Areas for Improvement

### Unnecessary Return Spring

In the video, you can see a return spring around solenoid plunger. Theoretically, this shouldn't be needed as the slingshot rubber can also reset the plunger; however, I found it was needed in the prototype as the slot for the slingshot actuator is slightly too short causing the actuator to get stuck without the spring.

The only reason I want to remove the spring is because it's reducing the solenoid's power by a fair bit. I was originally running the solenoid at 15v; however, the addition of the spring required I increase the voltage to 18v to kick the ball with the same force. Running the coil at a higher voltage isn't ideal as it both puts more wear on the coil and requires that I run all coils at the higher voltage as well (since I do not want multiple coil voltages in the machine).

### Wobbly LEDs

To make the LEDs easily replaceable, I designed custom quick-change sockets to accept standard 5mm LEDs. These sockets are great for prototyping but they don't grip the leads tight enough resulting in the lights flickering when the solenoid kicks. This is largely because the sockets are really just holders for 2-pin Dupont connectors and the connectors I have aren't particularly strong.

Additionally, the Dupont connectors are only friction-fit into the sockets and do fall out over time. This could be fixed with some hot glue but I'm still considering other options such as different connectors.

### Deadzones

The prototype uses a pair of LJ8A3-2-Z/BY inductive probes running at 5v to detect the ball (see my [previous post]({% post_url 2022-02-04-testing-inductive-probes %}) for more technical details). The probes are compact, easy to use, and easy to mount; however, they have a fairly small detection radius which leaves quite a few deadzones along the slingshot. The most egregious deadzone is directly in front of the kicker which means the assembly is unlikely to ever kick the ball with full force.

Unfortunately, I cannot just put another sensor in the center deadzone as the solenoid plunger would block it. I could try mounting the solenoid vertically like on a full-sized machine but even then I doubt I'd have enough space for the probe.

One option I'm considering is to shift the solenoid closer to the flippers thus giving more room for sensors; although, this would require repositioning the lower sensor further up so I'd really only be moving the deadzone. Ultimately, I don't want to change the sensor positions just yet though as where the ball contacts each slingshot will depend greatly on the upper playfield and may make the deadzones moot (or at least move them).
