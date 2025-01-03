---
title: MaixCDK
id: home_page
---

<div>
<script src="/static/css/tailwind.css"></script>
</div>

<style>
h2 {
    font-size: 1.6em;
    font-weight: 600;
    font-weight: bold;
}
#page_wrapper
{
    background: #f2f4f3;
}
.dark #page_wrapper
{
    background: #1b1b1b;
}
.md_page #page_content
{
    padding: 1em;
}
.md_page #page_content > div
{
    width: 100%;
    max-width: 100%;
    text-align: left;
}
h1 {
    font-size: 3em;
    font-weight: 600;
    margin-top: 0.67em;
    margin-bottom: 0.67em;
}
#page_content h2 {
    font-size: 1.6em;
    font-weight: 600;
    margin-top: 1em;
    margin-bottom: 0.67em;
    font-weight: bold;
    text-align: center;
    margin-top: 3em;
    margin-bottom: 1.5em;
}
#page_content h3 {
    font-size: 1.5em;
    font-weight: 400;
    margin-top: 0.5em;
    margin-bottom: 0.5em;
}
#tags > p {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    padding: 1em;
}
#tags > p a {
    margin: 0.2em 0.2em;
}
#feature video, #feature img {
    height: 15em;
}
.feature_item {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    margin: 1em;
    border: 1em solid white;
    background: white;
    border-radius: 0.5em;
    overflow: hidden;
    max-width: 20em;
    box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
}
.dark .feature_item {
    border: 1em solid #2d2d2d;
    background: #2d2d2d;
}
.feature_item .feature {
    font-size: 1.2em;
    font-weight: 600;
}
.feature_item .description {
    font-size: 0.8em;
    font-weight: 400;
}
.feature_item video, .feature_item img {
    width: 100%;
    object-fit: cover;
}
.feature_item .img_video {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}
.feature_item > div {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
}
.feature_item p {
    padding: 0.5em;
}
#page_content li {
    margin: 0.5em;
    list-style-type: disc;
}
.white_border {
    border: 1em solid white;
}
.dark .white_border {
    border: 1em solid #2d2d2d;
}
.code-toolbar pre {
    margin: 0;
}
.code_wrapper {
    overflow: auto;
}
@media screen and (min-width: 1280px) {
    .md_page #page_content > div
    {
        width: 1440px;
        max-width: 1440px;
    }
}
@media screen and (max-width: 768px) {
    .code_wrapper {
        font-size: 0.6em;
    }
}
</style>

<!-- wrapper -->
<div class="flex flex-col justify-center items-center">

<div class="w-full flex flex-col justify-center text-center">
    <div class="flex justify-center">
        <img src="/static/image/maixcams.png" alt="MaixPy Banner">
    </div>
    <h1><span>MaixCDK</span></h1>
    <h3>Fast implementation of AI vision and auditory applications</h3>
</div>

<div id="big_btn_wrapper" class="flex flex-wrap justify-center items-center">
    <a class="btn m-1" href="/doc/">Quick Start 🚀📖</a>
    <a class="btn m-1" href="/api/">API Reference 📚</a>
    <a class="btn m-1" target="_blank" href="https://wiki.sipeed.com/maixcam-pro">Hardware Platform: MaixCAM 📷</a>
    <a class="btn m-1" target="_blank" href="https://github.com/sipeed/MaixCDK">Open Source Code ⭐️</a>
    <a class="btn m-1" target="_blank" href="https://maixhub.com/app">App Store 📦</a>
</div>

<div id="tags">

[![GitHub Repo stars](https://img.shields.io/github/stars/sipeed/MaixCDK?style=social)](https://github.com/sipeed/MaixCDK)[![Apache 2.0](https://img.shields.io/badge/license-Apache%20v2.0-orange.svg)]("https://github.com/sipeed/MaixCDK/blob/main/LICENSE.md)[![GitHub downloads](https://img.shields.io/github/downloads/sipeed/maixcdk/total?label=GitHub%20downloads)](https://github.com/sipeed/MaixCDK) [![Build MaixCAM](https://github.com/sipeed/MaixCDK/actions/workflows/build_maixcam.yml/badge.svg)](https://github.com/sipeed/MaixCDK/actions/workflows/build_maixcam.yml)[![Trigger wiki](https://github.com/sipeed/MaixCDK/actions/workflows/trigger_wiki.yml/badge.svg)](https://github.com/sipeed/MaixCDK/actions/workflows/trigger_wiki.yml)

</div>

<div class="text-center">

English | [中文](./zh/)

</div>


<div class="mt-16"></div>

<div class="text-gray-400 text-center">


If you like MaixCDK or MaixPy, please give a star ⭐️ to the [MaixPy](https://github.com/sipeed/MaixPy) and [MaixCDK](https://github.com/sipeed/MaixCDK) open source project to encourage us to develop more features.

</div>


<div class="mt-6"></div>

<h2 class="text-center font-bold">Simple API Design, AI Image Recognition within 20 Lines of Code</h2>
<div id="id1" class="flex flex-row justify-center items-end flex-wrap max-w-full">
<div class="shadow-xl code_wrapper">

```cpp
#include "maix_nn.hpp"
#include "maix_camera.hpp"
#include "maix_display.hpp"

int main()
{
    nn::Classifier classifier("/root/models/mobilenetv2.mud");
    image::Size input_size = classifier.input_size();
    camera::Camera cam = camera::Camera(input_size.width(), input_size.height(), classifier.input_format());
    display::Display disp = display::Display();

    char msg[64];
    while(!app::need_exit())
    {
        image::Image *img = cam.read();
        auto *result = classifier.classify(*img);
        int max_idx = result->at(0).first;
        float max_score = result->at(0).second;
        snprintf(msg, sizeof(msg), "%5.2f: %s", max_score, classifier.labels[max_idx].c_str());
        img->draw_string(10, 10, msg, image::COLOR_RED);
        disp.show(*img);
        delete result;
        delete img;
    }
    return 0;
}
```

</div>
<video playsinline controls autoplay loop muted preload  class="p-0 mx-2 rounded-md shadow-xl white_border" src="https://wiki.sipeed.com/maixpy/static/video/classifier.mp4" type="video/mp4">
Classifier Result video
</video>
</div> <!-- id1 -->


<h2 class="text-center font-bold">Same simple Python API binding</h2>
<div id="id2" class="flex flex-row justify-center items-end flex-wrap max-w-full">
<div class="shadow-xl code_wrapper">

```python
from maix import camera, display, image, nn

classifier = nn.Classifier(model="/root/models/mobilenetv2.mud")
cam = camera.Camera(classifier.input_width(), classifier.input_height(), classifier.input_format())
disp = display.Display()

while 1:
    img = cam.read()
    res = classifier.classify(img)
    max_idx, max_prob = res[0]
    msg = f"{max_prob:5.2f}: {classifier.labels[max_idx]}"
    img.draw_string(10, 10, msg, image.COLOR_RED)
    disp.show(img)
```

</div>
<video playsinline controls autoplay loop muted preload  class="p-0 mx-2 rounded-md shadow-xl white_border" src="https://wiki.sipeed.com/maixpy/static/video/classifier.mp4" type="video/mp4">
Classifier Result video
</video>
</div> <!-- id2 -->

<!-- div start-->
<div class="text-center flex flex-col justify-center items-center">
<h2>Variety of built-in functions</h2>

<p>The functionality of MaixCDK is kept in sync with MaixPy, and the MaixPy documentation is also applicable to MaixCDK.</p>

<div style="display: flex; justify-content: left">
    <a target="_blank" style="margin: 1em;color: white; font-size: 0.9em; border-radius: 0.3em; padding: 0.5em 2em; background-color: #a80202" href="https://wiki.sipeed.com/maixpy/">Please Visit MaixPy learn more features</a>
</div>

</div>
<!-- div end-->



<!-- div start-->
<div class="flex flex-col justify-center items-center max-w-full">
<h2>Add Python binding in one second</h2>

Just add comments, then you can use this API in MaixPy!

<div class="flex flex-row justify-center items-center flex-wrap mt-3 max-w-full">
<div class="mr-4 mt-4 shadow-xl code_wrapper flex flex-col justify-center items-center">

Python demo code:

```python
from maix import uart


devices = uart.list_devices()
print(devices)



```

</div>
<div class="max-w-full">
<div class="mt-4 shadow-xl code_wrapper flex flex-col justify-center items-center">

MaixCDK implemention in `maix_uart.hpp`:

```cpp
namespace maix::uart {
    /**
     * List all UART devices can be directly used.
     * @return All device path, list type, element is string type
     * @maixpy maix.uart.list_devices
     */
    std::vector<std::string> list_devices();
}
```

</div>
</div>
</div>
</div>
<!-- div end-->

<!-- start -->
<div class="flex flex-col justify-center items-center">
<h2>Online AI Training Platform MaixHub</h2>

No need for AI expertise or expensive training equipment, train models with one click, deploy to MaixCAM with one click.

<div class="mt-3"></div>

<img class="shadow-xl white_border" src="/static/image/maixhub.jpg">
</div>
<!-- end -->

## Maix Ecosystem

<img src="/static/image/maix_ecosystem.png" class="white_border shadow-xl rounded-md">


## Community {#community}

<div class="max-w-full">
<div class="overflow-auto">

| Community | Address |
| --- | ---- |
| **MaixCDK Documentation**| [MaixCDK Documentation](https://wiki.sipeed.com/maixcdk/) |
| **MaixPy Documentation**| [MaixPy Documentation](https://wiki.sipeed.com/maixpy/) |
| **App Store**| [maixhub.com/app](https://maixhub.com/app) |
| **Project Sharing**| [maixhub.com/share](https://maixhub.com/share) |
| **Bilibili**| Search for `MaixCAM` or `MaixPy` on Bilibili |
| **Discussion**| [maixhub.com/discussion](https://maixhub.com/discussion) |
| **MaixCDK issues**| [github.com/sipeed/MaixPy/issues](https://github.com/sipeed/MaixCDK/issues) |
| **Telegram**| [t.me/maixpy](https://t.me/maixpy) |
| **QQ Group**| 862340358 |

</div>
</div>

</div>
<!-- wrapper end -->
