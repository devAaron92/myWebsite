---
layout: post
title: "Reaper Automation"
date: 2026-03-18
video: /videos/addAutomation2.mp4
---
> Automation in REAPER can feel confusing at first, but it’s very flexible once you get the hang of it — here are some tips I picked up today.

## Adding and removing automation lanes fast in REAPER

REAPER allows you to add many automation lanes at once. 

First you'll want to make sure to add your track.

Then, Just click Trim to open the automation window. 

![Trim](/myImages/reaperAutomationImages/trim.png)

After you click 'Trim' you wil lsee the envelopes window open. You can select one parameter at a time or as many as you'd like all at once. 

There, you can hold the shift key and select as many parameters as you want to enable them all at once. I find this especially helpful when working with plugins that have many parameters.


<video width="100%" controls>
  <source src="/videos/addAutomation2.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

The same convenience applies when removing automation lanes. Instead of removing them individually—which can be time-consuming—you can open the Trim window, hold Shift, select the parameters you want to remove, right-click, and choose Hide All.


## Improper Gain Staging: Clipping

As I had the audio and midi for a couple of tracks I started working on automating. I suddenly noticed there was no sound coming from my speakers. When I checked REAPER, I saw that the master track had muted itself. This happened when the master gain was set to +12 dB. When I lowered it, the problem went away.

At first, I thought the issue might be related to the automation I was working with. I had several automation lanes open and was experimenting with filter cutoff modulation. But that didn’t really make sense.

Then I wondered if I had simply opened too many automation lanes on the guitar track. But that couldn’t be the problem either. Many projects have dozens or even hundreds of automation lanes across tracks, and my CPU usage was very low. So it wasn’t a performance issue.

Eventually I noticed that the master gain was set to +12 dB. When I lowered it to around +6 dB, the master track stopped muting itself. I did not properly manage gain staging by pushing the master gain to +12dB, which likely caused clipping during playback.

![Gain Staging](/myImages/reaperAutomationImages/gainStaging.png)

## Watch out for Bypassing Parameter

I also ran into an unexpected issue while using Valhalla Supermassive. I opened the automation window, selected several parameters, and drew some automation. Then I wondered why I wasn’t hearing anything. I checked the FX window and saw that the plugin wasn’t enabled. When I tried to click the checkbox, it wouldn’t let me enable it. I then looked at the plugin window itself and noticed it said “Bypassed” at the top.

When I went back to the automation window, I realized there was a parameter controlling the plugin’s bypass state. Once I removed that automation, the plugin worked normally again.

## Audio Routing Confusion

When I plugged in my headphones I couldn't hear any audio coming through.

I checked my track settings, monitoring, and routing, and everything looked fine. It turned out the fix was straightforward: go to Options → Preferences → Audio → Device, and enable external headphones. Once I switched that on, the audio came through immediately.

<style>
  a.boombox-link {
    display: inline-block;
    padding: 10px 20px;
    background-color: #1db954;
    color: white;
    text-decoration: none;
    border-radius: 8px;
    transition: transform 0.1s;
  }
  a.boombox-link:hover {
    transform: scale(1.05);
  }
</style>

## Multitrack on BoomBox
<p>
  <strong> I’ve attached the multi-track I developed during this project </strong>  
  <a class="boombox-link" href="https://app.boombox.io/app/file/f7GYRKMP29zqmgNm7W9KrLEdenAjQ316a" target="_blank" rel="noopener noreferrer">
    Check it out on Boombox
  </a>
</p>

<div class="bg-gray-800 border-l-4 border-green-400 p-6 rounded-lg mt-10 mb-10">
  <p class="text-green-300 font-semibold text-lg mb-2">Final Thoughts</p>
  <p class="text-gray-300 leading-relaxed">
    Today’s session reinforced just how powerful REAPER’s automation system can be — once you understand the shortcuts and workflow, you can work much faster and more efficiently.

    If you're a plugin devleoporor company who needs an extra hand with QA, reach out to Aaron at aaron@pluginproof.com. Thanks for reading, and have a great day!

  </p>
</div>

<div id="comments-container">
  <h3>Comments</h3>

  <!-- Comment form -->
  <form id="comment-form">
    <input type="text" id="comment-name" placeholder="Your name (optional)" />
    <textarea id="comment-message" placeholder="Write a comment..." required></textarea>
    <button type="submit">Post Comment</button>
  </form>

  <!-- Display comments -->
  <div id="comments-list"></div>
</div>

<script type="module">
  import { createClient } from 'https://cdn.jsdelivr.net/npm/@supabase/supabase-js/+esm'

  // ---- Replace these with your Supabase project values ----
  const supabaseUrl = 'https://aeffcodmwsxhjseferdf.supabase.co'
  const supabaseKey = 'sb_publishable_zb3sXiUcvLA1oZW4HmCSwQ_n_DcmTD0'
  const supabase = createClient(supabaseUrl, supabaseKey)

  const form = document.getElementById('comment-form')
  const nameInput = document.getElementById('comment-name')
  const messageInput = document.getElementById('comment-message')
  const list = document.getElementById('comments-list')

  // Fetch and display comments
  async function fetchComments() {
    const { data, error } = await supabase
      .from('comments')
      .select('*')
      .order('created_at', { ascending: true })
    if (error) {
      console.error(error)
      return
    }

    list.innerHTML = ''
    data.forEach(c => {
      const name = c.name || 'Anonymous'
      const div = document.createElement('div')
      div.innerHTML = `<p><strong>${name}:</strong> ${c.message}</p>`
      list.appendChild(div)
    })
  }

  // Submit new comment
  form.addEventListener('submit', async e => {
    e.preventDefault()
    const name = nameInput.value.trim()
    const message = messageInput.value.trim()
    if (!message) return

    const { error } = await supabase
      .from('comments')
      .insert([{ name, message }])
    if (error) {
      console.error(error)
      return
    }

    // Clear form
    messageInput.value = ''
    nameInput.value = ''

    fetchComments()
  })

  // Initial load
  fetchComments()
</script>