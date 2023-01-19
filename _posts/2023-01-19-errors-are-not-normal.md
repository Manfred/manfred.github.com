---
layout: post
title: Errors are not normal
---

I've seen a few projects where the error reporting service for the web application was flooded with unhandled exceptions and errors. Sometimes up to the point where they were hitting the maximum quota for the service. I'm not sure who needs to hear this, but this is not normal.

Errors reported by a web application are supposed to give off a strong signal that something is broken. When they are buried under a mountain of noise that is no longer the case.

Non-intermittent exceptions coming from your ‘own’ code should be resolved as soon as possible, especially when they affect users. Depending on priorities in the project this may take a while, in which case you want to leave the exceptions as a signal that things are bad.

Intermittent issues are usually caused by networking problems or error responses from other applications. If these are structural in nature, you could report them as a metric instead and show it on a dashboard to keep track of their impact.
