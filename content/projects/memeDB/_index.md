---
title: "Static Database On Github Pages"
date: 2025-03-10
description: ""
tags: ["database", "sql", "AI"]
---

## Idea

When I see memes online I like to save them to my phone and share them with people later.

However, the action of finding funny images online and sharing them with people typically don't happen at the same time.
Thus when I finally remembered to share an image with my friends, I always struggle to find the image I had in my head.

If there is a way for me to use an algorithm to figure out what's in each image I download,
I can create a database where I can then associate the text within the image with the image itself, thus making lookup a breeze.


## Experiments

The easiest option to look up an image I have in my head is using texts in these images.

A short search online indicates the problem of "identify text in image" is called Optical Character Recognition(OCR) and it has already been solved.
I narrowed down two options:
- [EasyOCR](https://github.com/JaidedAI/EasyOCR): One of the easiest to implement traditional method I can run locally.
- [Google Cloud Vision API](https://cloud.google.com/vision?hl=en): Google's production level OCR that is free as long as I make less than 1000 calls a month.

### Experiementation With Both OCR Tools

Selecting a random image with hand written characters, I got the following results:
```
@s"
lekJIilkec
Civlicws
call
Load
plaqve roonds
AUNNYC@
Mose
Good
Hne
```
From this image:
![test meme](test_meme.jpg)

Using the same image with Google's Vision API I got:
```
But sir! those look like
Civilians
Good call
Load the
plague rounds
ifunny.co
```

It seems for a small project Google's Cloud Vision API is the best way forward.

### Database On Github Pages

Now I need a database to be hosted online for me to do the lookup.
With this page being hosted on github, it means the database must be static. Since the backend of the page is a github repository,
everytime I modify the database I would need to push to it.

Given I've not touched databases that much in the past, SQLite seems the perfect place to get started.


## Plan

Thus far, it's pretty clear that I want to:
1. Create a static database with SQLite.
2. Fill the database with a script that called Google's cloud vision API to associate text with image.
3. Look up entries from said database on this website.

## Result

<form id="query-form">
  <textarea id="query-input" rows="1" cols="50" placeholder="Enter your text" style="background-color: black;color:#fff;"></textarea>
  <br>
  <button type="submit">Search</button>
</form>

<h2>Hits</h2>
<div id="query-output"></div>


## Problems

I've unfortunately came to the realization after completing this project that someone at Google (and most likely Apple as well) 
have thought about this exactly problem and implemented this exact feature in Google Photo.

I am the idiot who unfortunately did not find the feature until too late:
![me, the idiot](idiot.png)


## Future Ideas

Now although it seems I re-invented a feature that's in every single smartphone, I should be able to improve it with the help of more powerful AI APIs.

At least for now, I cannot index my local images with Google Photo by using names of the object or character in the image. But that's for next time.

<script src="/js/sql-wasm.js"></script>
<script src="/js/query.js"></script>