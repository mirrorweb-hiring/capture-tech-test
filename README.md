# Product Engineer Tech Test - X Capture Pipeline

Welcome, and thanks for taking the time to work through this exercise with us!

## Background

This exercise mirrors a real project we work on at MirrorWeb: building **capture pipelines** that archive content from third-party platforms into a normalised, platform-agnostic format. Your task is to build a small **X capture pipeline** (X, formerly Twitter) that archives a user's posts from their X page.

## The task

Build a pipeline that, given an X user, captures their posts, transforms them into the **Output Format** described below and stores the transformed output.

Each captured post should include:

- The **post content** itself
- Any associated **replies**
- Any associated **likes**
- **Identifying user information** for the authors involved - at minimum **username** and **display name**

The output should conform to the **Output Format** described in [`OUTPUT_FORMAT.md`](./OUTPUT_FORMAT.md), which contains the full field definitions and an example of the expected JSON output. It's a deliberately simple, platform-agnostic structure - part of the exercise is working out how X's concepts map onto it.

## How this works

- **This is a pairing exercise.** We will work through it together on the day. **Asking questions is encouraged** - how you reason about and explore the problem is exactly what we want to see.
- **You won't need to provide your own X API credentials.** We'll provide credentials for a test account that already has posts, comments, likes, and replies for you to capture, so you have real data to work with.
- **Using AI tools is allowed and encouraged.** Use whatever you'd normally reach for. We're interested in how you think about and solve the problem, not in catching you out.

## What we're looking for

There are no trick requirements here. We're primarily interested in:

- How you **think about and break down** the problem
- How you **structure** the pipeline (fetching, transforming, and outputting data)
- How faithfully your output **maps to the Output Format** in [`OUTPUT_FORMAT.md`](./OUTPUT_FORMAT.md) - in particular how you model posts, replies (and the relationship between them), likes, and user identity
- How you **handle the data source** - connecting to the API, fetching the data, and dealing with the realities of it
- The **core engineering fundamentals** - code quality and readability, sensible error handling, security, and an awareness of performance
- The **questions you ask** and the trade-offs you talk through along the way

The solution should be written in **Go**. Beyond that, you're free to choose whatever libraries and tooling you're comfortable with.

## Getting started

A good first step is to read through [`OUTPUT_FORMAT.md`](./OUTPUT_FORMAT.md) and get a feel for the target structure - in particular how messages, replies, likes, and user identity are represented - before deciding how you'll approach the capture.

It's also worth a look over the X API documentation ahead of the session so you have a feel for what's available: https://docs.x.com/x-api/overview

## Outputs

By the end of the session we'd expect to see a working (or working-toward) pipeline that produces output in the Output Format for a user's posts, replies, and likes - and a good conversation along the way.

Good luck, and enjoy it - we're looking forward to building this with you.
