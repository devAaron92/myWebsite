---
layout: post
title: Exploring 'Environments' Through Risk-Based Testing
date: 2026-08-25
---

### Risk-Based Testing

Today, I tested Environments. It's a recently released plugin by AudioThing. AudioThing descrbes it as convolution engine that combines multiple impulse responses, while allowing the user to move through the captured environment and apply modulation. 

Testing audio plugins requires developers to focus on areas that are high risk. It’s not feasible to test everything in a plugin, release times and budgets are a thing.

That’s why we prioritize failures where we think they are most likely to occur.


### Identifying the Risk

What failure here would actually matter to the user, and why do we have reason to believe it could happen?

This isn't a utility plugin where an occasional click might be annoying but peripheral.

Environments is fundamentally about transforming an incoming musical signal through changing acoustic spaces.

 **-> The manual repeatedly emphasizes:**
 **-> Movement through space**
 **-> Changing spatial character**
 **-> Modulation and motion**
 **-> Multiple impulse responses**
 **-> An additional convolution layer**

### Risk Hypothesis

Continuous movement through the captured environment could produce discontinuities or other unwanted audible artifacts as the spatial characteristics change.

The plugin describes a convolution engine that combines multiple impulse responses, while allowing the user to move through the captured environment and apply modulation. The resulting audio therefore changes as the spatial parameters change over time. That creates a plausible opportunity for discontinuities or other unwanted artifacts to occur during those transitions.

A conventional convolution reverb might essentially be:
        
# -> Input → fixed impulse response → output

Environments is describing something more like:
       
# -> Input → changing spatial position / changing IR characteristics → output

That means the processing system has to handle changing convolution states over time.

### Test

# -> Put the sustained Surge XT pad through Environments.

# -> Pick one Environment and leave it unchanged.

# -> Listen for any clicks, pops, glitches, sudden level changes, or anything that could be an audio artifact.

# -> Automate X position steadily from one side to the other.

<video controls width="100%" style="margin: 20px 0;">
  <source src="/videos/environmentsVidsMp4/xSteady.mp4" type="video/mp4">
</video>

# -> Automate Y position steadily from top to bottom.

<video controls width="100%" style="margin: 20px 0;">
  <source src="/videos/environmentsVidsMp4/ySteady.mp4" type="video/mp4">
</video>


# -> Automate X + Y steadily from one side/top to the other side/bottom.

<video controls width="100%" style="margin: 20px 0;">
  <source src="/videos/environmentsVidsMp4/ySteady.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

# -> Automate X position rapidly from one side to the other.

<video controls width="100%" style="margin: 20px 0;">
  <source src="/videos/environmentsVidsMp4/xRapid.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

# -> Automate Y position rapidly from top to bottom.

<video controls width="100%" style="margin: 20px 0;">
  <source src="/videos/environmentsVidsMp4/yRapid.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

# -> Automate X + Y rapidly from one side/top to the other side/bottom.

<video controls width="100%" style="margin: 20px 0;">
  <source src="/videos/environmentsVidsMp4/xRapid+yRapid.mp4
" type="video/mp4">
  Your browser does not support the video tag.
</video>

# -> Automate X steadily + Y rapidly simultaneously.

<video controls width="100%" style="margin: 20px 0;">
  <source src="/videos/environmentsVidsMp4/xSteady+yRapid.mp4
" type="video/mp4">
  Your browser does not support the video tag.
</video>

# -> Automate X rapidly + Y steadily simultaneously.

<video controls width="100%" style="margin: 20px 0;">
  <source src="/videos/environmentsVidsMp4/xRapid+ySteady.mp4
" type="video/mp4">
  Your browser does not support the video tag.
</video>

### Result & Interpretation

**Result:** I did not observe any clicks, pops, glitches, sudden level changes, or other audible discontinuities during any of the tested movements.

**Interpretation:** The hypothesized failure was not exposed under these test conditions. This does not establish that the plugin is free of artifacts; it means that this particular attack did not reveal one.
