# Product Engineer Tech Test - MirrorWeb Social Capture Pipeline

Welcome, and thanks for taking the time to work through this exercise with us!

## Background

This exercise mirrors a real project we work on at MirrorWeb: building **capture pipelines** that archive content from third-party platforms into a normalised, platform-agnostic format. Your task is to build a small **capture pipeline** for **MirrorWeb Social**, a self-contained social platform we run for this exercise, that captures a user's posts and the activity around them.

## The task

Build a pipeline that, given a MirrorWeb Social user, captures their posts, transforms them into the **Output Format** described below and stores the transformed output.

Each captured post should include:

- The **post content** itself
- Any associated **replies**
- Any associated **reactions** (for example likes)
- **Identifying user information** for the authors involved - at minimum **username** and **display name**

The output should conform to the **Output Format** described in [`OUTPUT_FORMAT.md`](./OUTPUT_FORMAT.md), which contains the full field definitions and an example of the expected JSON output. It's a deliberately simple, platform-agnostic structure - part of the exercise is working out how MirrorWeb Social's concepts map onto it.

## How this works

- **This is a pairing exercise.** We will work through it together on the day. **Asking questions is encouraged** - how you reason about and explore the problem is exactly what we want to see.
- **You won't need to provide any credentials of your own.** We'll give you the API endpoint and an access token for a test instance on the day. It's preloaded with mock data - posts, replies, reactions, attachments, and the accounts behind them - crafted so that everything is properly related to the entities it belongs to, giving you a realistic, connected dataset to work with.
- **Using AI tools is allowed and encouraged.** Use whatever you'd normally reach for. How you **work with and guide an agent** - the way you direct it, review what it produces, and course-correct - interests us as much as your mastery of the language itself. We're interested in how you think about and solve the problem, not in catching you out.

## What we're looking for

There are no trick requirements here. We're primarily interested in:

- How you **think about and break down** the problem
- How you **structure** the pipeline (fetching, transforming, and outputting data)
- How faithfully your output **maps to the Output Format** in [`OUTPUT_FORMAT.md`](./OUTPUT_FORMAT.md) - in particular how you model posts, replies (and the relationship between them), reactions, and user identity
- How you **handle the data source** - connecting to the API, fetching the data, and dealing with the realities of it
- The **core engineering fundamentals** - code quality and readability, sensible error handling, security, and an awareness of performance
- The **questions you ask** and the trade-offs you talk through along the way

The solution should be written in **Go**. Beyond that, you're free to choose whatever libraries and tooling you're comfortable with.

## Getting started

A good first step is to read through [`OUTPUT_FORMAT.md`](./OUTPUT_FORMAT.md) and get a feel for the target structure - in particular how messages, replies, reactions, and user identity are represented - before deciding how you'll approach the capture.

It's also worth reviewing the MirrorWeb Social API spec in [`api/openapi.yaml`](./api/openapi.yaml) ahead of the session so you have a feel for what's available. That spec is the documentation for the platform - there's nothing external to look up.

## Outputs

By the end of the session we'd expect to see a working (or working-toward) pipeline that produces output in the Output Format for a user's posts, replies, and reactions - and a good conversation along the way.

Good luck, and enjoy it - we're looking forward to building this with you.
