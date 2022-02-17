---
title: "Return Lane | Half Scale Pinball"
date: 2022-02-16 20:09:37 -0600
categories: system-shock-pinball
tags: pinball openscad
---

The prototype return lane is complete and I discuss some of the challenges of working exclusively in OpenSCAD.

## The prototype

I've completed a first draft of the return lane assembly; although, it's not fully tested at this time. The problem is I can't really test the lane without having the side wall and slingshot on either side to verify the ball behaves as I'd like. For the moment, I've just printed and installed a single lane on a test board.

![Lane prototype](/assets/posts/2022-02-16-return-lane-prototype.jpg)
*The left return lane assembly installed on a test board.*

The top plate of the assembly is largely cosmetic so for the final design I intend on making it more "blocky" to better fit with the 90's DOS shooter theme of the original System Shock. I also plan on constructing the bottom plate from metal to reduce wear. I'm considering building the top plate from clear acrylic; however, I don't have room under the playfield to add lights under it so that may be a waste.

![Lane render](/assets/posts/2022-02-16-return-lane-render.png)
*The right return lane assembly in the playfield render.*

## Challenges with designing in OpenSCAD

For prototyping, I heavily leverage OpenSCAD's Boolean operations to quickly create complex shapes; however, there is no direct way to create fillets. This posed a problem for the return lane prototype as the inlane has a concave fillet where the lane divider joins the flipper return lane.

There are a few ways to accomplish a concave fillet in OpenSCAD but they each have their drawbacks:
* You can programmatically draw the curve using the 2D subsystem but this is made difficult by the lack of a built-in Bezier curve library.
* You can subtract a circle from the corner but this gets more complex when the joint isn't 90 degrees.
* [Clever use of the offset module][fillets in openscad] can produce fillets but they will be applied to the entire object.
* You could draw the part in vector art software, export to SVG, and import into OpenSCAD; however, the part will no longer be parametric.

The dimensions of the machine are bound to keep changing as I refine my designs so I opted for the simplest route of simply subtracting a curve from the lane using a hard-coded ellipse. It's not elegant and it's not robust but it does get the job done quick so I can move on to more important assemblies.

![Lane construction](/assets/posts/2022-02-16-return-lane-construction.png)
*Each colored section represents a different primitive I union'd or difference'd to create the final part profile.*

For the final part, I'm considering writing a Bezier curve library to let me draw the curve directly in OpenSCAD. I know Bezier curve libraries already exist for OpenSCAD; however, I'm pretty opinionated with how I structure my scad files so I'd rather write the library myself to keep everything consistent. I also have bigger plans down the road to build a dependency manager for OpenSCAD so it would be helpful to have some of my own libraries I can test with.

[fillets in openscad]: http://www.neufeld.newton.ks.us/electronics/?p=1730
