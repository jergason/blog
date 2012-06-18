---

title: Turning Off GPU Acceleration In Google Chrome
date: '2012-05-04'
categories: coding
tags: [chrome]
permalink: post/22387219496/turning-off-gpu-acceleration-in-google-chrome

---

I am currently working on a strange device that has a frankenstein
mutated version of WebKit. The browser doesn’t support hardware
acceleration, so I was looking for a way to turn it off in Google Chrome
for debugging purposes.

I ran into
[this](http://peter.sh/experiments/chromium-command-line-switches/)
excellent site that lists all of the command-line arguments that
Chromium takes, and a few of them apply to turning off the GPU:

-   `--blacklist-accelerated-compositing`: Blacklist the GPU for
    accelerated compositing.
-   `--blacklist-webgl`: Blacklist the GPU for WebGL
-   `--disable-accelerated-2d-canvas`: Disable gpu-accelerated 2d canvas
-   `--disable-accelerated-compositing`: Disables accelerated
    compositing
-   `--disable-accelerated-layers`: Disables the hardware acceleration
    of 3D CSS and animation

Launching Chrome with these options gave me an experience more like the
device I am working on, which greatly helped in performance
optimization.
