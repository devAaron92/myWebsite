---
layout: post
title: "Reaper Automation"
date: 2026-03-18
---

> I had a good session in REAPER today after getting the hang of automation, here is what I learned in the process.

## Adding and removing automation lanes fast in REAPER


Automation is really flexible in REAPER as you get the hang of it. I found that it is convenient, you can add many automation lanes at once. Just click Trim to open the automation window. From there, you can hold the shift key and select as many parameters as you want to enable them all at once. I find this especially helpful when working with plugins that have many parameters.

![Trim](/myImages/reaperAutomationImages/trim.png)


The same convenience applies when removing automation lanes. Instead of removing them individually—which can be time-consuming—you can open the Trim window, hold Shift, select the parameters you want to remove, right-click, and choose Hide All.

![Add Automation](/myImages/reaperAutomationImages/addAutomation.png)

## Improper Gain Staging: Clipping

As I had the audio and midi for a couple of tracks I started working on automating. I suddenly noticed there was no sound coming from my speakers. When I checked REAPER, I saw that the master track had muted itself. This happened when the master gain was set to +12 dB. When I lowered it, the problem went away.

At first, I thought the issue might be related to the automation I was working with. I had several automation lanes open and was experimenting with filter cutoff modulation. But that didn’t really make sense.

![Filter Cutoff](/myImages/reaperAutomationImages/filterCutoff.png)

Then I wondered if I had simply opened too many automation lanes on the guitar track. But that couldn’t be the problem either. Many projects have dozens or even hundreds of automation lanes across tracks, and my CPU usage was very low. So it wasn’t a performance issue.

Eventually I noticed that the master gain was set to +12 dB. When I lowered it to around +6 dB, the master track stopped muting itself. I did not properly manage gain staging by pushing the master gain to +12dB, which likely caused clipping during playback.

![Gain Staging](/myImages/reaperAutomationImages/gainStaging.png)

## Watch out for Bypassing Parameter

I also ran into an unexpected issue while using Valhalla Supermassive. I opened the automation window, selected several parameters, and drew some automation. Then I wondered why I wasn’t hearing anything. I checked the FX window and saw that the plugin wasn’t enabled. When I tried to click the checkbox, it wouldn’t let me enable it. I then looked at the plugin window itself and noticed it said “Bypassed” at the top.

When I went back to the automation window, I realized there was a parameter controlling the plugin’s bypass state. Once I removed that automation, the plugin worked normally again.

## Audio Routing Confusion

When I plugged in my headphones I couldn't hear any audio coming through.

I checked my track settings, monitoring, and routing, and everything looked fine. It turned out the fix was straightforward: go to Options → Preferences → Audio → Device, and enable external headphones. Once I switched that on, the audio came through immediately.

<div class="bg-gray-800 border-l-4 border-green-400 p-6 rounded-lg mt-10 mb-10">
  <p class="text-green-300 font-semibold text-lg mb-2">Final Thoughts</p>
  <p class="text-gray-300 leading-relaxed">
    Today’s session reinforced just how powerful REAPER’s automation system can be — once you understand the shortcuts and workflow, you can work much faster and more efficiently.

    If you're a plugin devleoporor company who needs an extra hand with QA, reach out to Aaron at aaron@pluginproof.com. Thanks for reading, and have a great day!

  </p>
</div>