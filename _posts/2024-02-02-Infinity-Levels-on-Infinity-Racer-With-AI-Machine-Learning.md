---
layout:     post
title:      Infinity Levels On Infinity Racer Using AI/Machine Learning With Tensorflow
date:       2024-02-03 13:24:03
summary:    Infinity Levels On Infinity Racer Using AI/Machine Learning With Tensorflow
categories: portfolio
---

Infinity Levels has arrived. Using Tensorflow, an open source Machine Leanring platform, I have setup a level generator which creates levels ondemand. Here is how I did it.

Looking at a screenshot here of the app, you can see a clear grid pattern. There is a 20X30 grid. Each cell is either a space, rock, or exit. The user draws lines with their finger to get the car to the exit. 

![gridExample](/assets/20240204/gridExample.png)

For this task I used a GAN or Generative Adversarial Network (GAN), which has two neural networks, a generator and a discriminator. These are trained simulaneously, through competition the Generator and Discriminator go back and forth. The Generator tries to make levels indistinguishable from the real thing. While the Discriminator tries to guess if a level is generated or fake. For 30,000 rounds the battle rages. Back and forth these two go at it. 

This all happens locally on my computer, other than pulling existing levels from the database, the training process does not require the internet. 

By the end both elements should be trained to do their job, both becoming better and better until the end when the model is saved.

Once the training process is complete the discriminator is not used in the level generator. It just sits dormant in the model.

Unlike ChatGPT where it gives a response based on a prompt, this level generator produces raw output, "noise vector" as it's called, it just imagines it, and tada, a level is born.

----

My initial sprint was just to get the level generator to produce BAD levels. I was sure if I could get bad levels, I could keep iterating and eventually produce good levels. 

My earliest attempt I mapped the grid down to the pixel. On my development phone a cell is 18.75 pixels. It seems obvious in retrospect, but when I produced my first level, it wasn't produced with a grid in mind. It was just a smattering of decimal numbers between 0 and 1. It seemed to give little consideration to the fact that these numbers were going to be groups with it's neighbors to become a cell in a grid.

It became clear that it would be better to simplify to a grid approach rather than mapping each pixel.

My next approach was to use 600 values to represent the 20X30 grid. I used `0` for space, `1` for rock, and `2` for exits. After recoding for this new approach the level started producing level with exits in the middle, on the top, all sort of places.

So I decided to just place the exits after the level was generated, now I was down to just `1`s and `0`s. Deciding where to place an exit has rules like, must be in the lower half of the screen, must be 2-3 cells all next to one another. I decided to use a pathfinding software and some regular software development to place an exit location after the level was generated.

Using a pathfinding module for npm, I started validating levels based on if there was a clear path to the bottom row.

Here would be an invalid level

```        
0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,
1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,
0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0     
```

This shows a row of rock making the pathway to the exit impossible.

Since the car is slighly taller than the width of one cell, a level also needs to have a path of 2 cells or more, making this invalid as well.

```        
0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,
1,1,1,1,1,1,1,1,1,0,1,1,1,1,1,1,1,1,1,1,
0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0     
```

The pathway software still counted this as valid, so came up with the concept of, 'solidifing' a level, if there was a cell with a `1` on each side, just change the `0` to a `1` since the pathway is invalid based on the size of the car. This allowed me to solidify a level and then run the pathway software to see if there was an exit.

Next came the concept of velocity, in plain language this means, the car cannot go far enough, it runs out of speed and stops. This example below shows an invalid level based on the car not having enough velocity.

```
0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,
0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,
1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,0,0,
0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,
0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0
```

Once a level is determined valid, I select a placement of the exit cell based on:

- velocity, making sure the user has enough speed to get to that cell
- pathway validation, making sure there is a valid path to the exit cell, for instance, it's not blocked by a rock
- too direct, making sure a user cannot just draw a simple diagonal line and beat the level

As it stand now, I have the level generator running daily, I'm doing slight edits and approving each level. Once approved, the brand new level is available to the those with Infinity Level on the Infinity Racer App.

In the last 15 levels created 9 were invalid, meaning there was no way to place an exit based on my level validation. Invalid levels get saved into the database too, I'm using them to further train the discriminator. These levels required some manual adjustments, in order to be valid and then released to the app. 

Going forward I'll be looking to train a new model regularly, adjusting configurations and input parameters in order to get the model to produce the highest quality levels possible.

Infinity Racer now with Infinity Levels is available [here](https://apps.apple.com/us/app/infinity-racer/id6464310248?uo=4)
