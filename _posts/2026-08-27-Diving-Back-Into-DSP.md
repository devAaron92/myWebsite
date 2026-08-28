---
layout: post
title: "Diving back into DSP – Exponential Decay Envelope"
date: 2026-08-27
---

Today I dove back into DSP for a moment. I wanted to keep it simple and focus on the fundamentals.

A fundamental concept in digital audio is representing a continuous-time signal as a discrete sequence of samples. The project I worked on today was a simple implementation of an exponential decay function. I wanted to understand how something as basic as an envelope can be represented mathematically and then implemented digitally.

The first step was to establish Euler's number:

```python
e = 2.718281828459045

The exponential decay function I'm using is:

e-kt

where k is the decay-rate constant and t is time.

For k, I picked an arbitrary value of 5. At this point, I hadn't calculated t yet.

At first, I thought I could just create a list to represent our discrete sequence. But a loop made more sense because I didn't just want to create a list of numbers. I wanted to understand what was actually happening as we moved through the sequence and calculated the envelope.

So I created a variable called n to represent the sample index.

The goal was simple: iterate through the sample index so that I could calculate the corresponding point in time and then calculate the exponential decay at that point.

Because the first index in a discrete sequence is 0, the first calculation occurs at:

n = 0

With a sample rate of 10 samples per second (fs = 10), we calculate time from the sample index:

t = n / fs

So for the first sample:

t = 0 / 10 = 0

We then evaluate the exponential decay function at that time:

e-5(0) = e0 = 1

So the first envelope value is 1.

On the next iteration, n is incremented from 0 to 1.

Now:

t = 1 / 10 = 0.1

So we're evaluating the same exponential decay function at 0.1 seconds:

e-5(0.1) = e-0.5 ≈ 0.6065

So our first two envelope values are approximately:

1, 0.6065

This was where the distinction between the sample index, time, and envelope value became much clearer to me.

n tells us which sample we're at. The sample rate tells us how many samples occur per second. From those two things, we can determine the time represented by that sample:

t = n / fs

Then we use that time in the exponential decay function to calculate the envelope value.

So the basic chain is:

n → t → e-kt

Working through this program made me realize that there's quite a bit more going on underneath what initially looks like a simple sequence of numbers.