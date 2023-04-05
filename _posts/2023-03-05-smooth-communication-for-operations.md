---
layout: post
title: Smooth communication for operations
---

In our day-to-day work we use a lot of services to facilitate communication about operations. The goal is to keep applications and services running as smoothly as possible. For each available channel of communication someone needs to respond at the right time with the correct urgency to fix problems or prevent issues from escalating.

For the rest of the discussion we would like to use the following conceptual definitions, they might be different than what you are used to.

* *Notifications*: messages meant to interrupt a person
* *Errors*: messages describing unexpected or unhandled situations in an application
* *Metrics*: numeric data which allows you to inspect running systems
* *Events and logs*: semistructured or unstructured text describing application progress in a stream of consciousness manner

Any of these may end up on the an engineer's plate, and they have to decide on the urgency and manner of response. You can easily overburden an engineer by using the wrong communication channel, over-signaling, or not having clear responsibilities.

Improving communication is a constant process. Engineering management should keep time reserved to allow for improvement in a way that fits their management concepts.

From experience we can suggest a number of practical tips to improve operations.

Every one of the categories described above must have a **single dedicated communication channel**. People on the teams must understand the purpose of each channel. Engineers always send messages to the appropriate channel.

**Prevent signal exhaustion** by keeping the rate of messages on any communication channel to an appropriate level. 

Only have one person *on call* at any time, they are responsible for sorting out all **notifications** and choosing appropriate action. Engineers should only use notifications to this person when immediate action is likely required, the criterium is: would you want to wake up at 3:00 AM for this?

Applications must use **error reporting** and have a single generic way for dealing with errors and exceptions. The error reporting service must trigger a notification to the on call engineer when the error rate is abnormally high. Engineers should actively keep errors to a minimum by fixing issues with unexpected conditions. Errors may only be raised when the situation can't be resolved automatically or when it's an unknown error condition.

**Metrics** must be centralized as much as possible and key metrics must be presented on categorized dashboards to identify abnormal situations at a glance.

Engineers should use application metrics sparingly. A useful analog is to envision parts of your application as stations on a factory floor, you need a metric when you can't tell if any of the stations are working as intended.

Metric services must trigger a notification to the on call engineer when key indicators are outside of expected boundaries. Not every metric needs a trigger.

Sometimes it helps to introduce a temporary metrics when exploring a new feature, make sure they are removed once they are no longer used to prevent signal exhaustion.

Make sure there is a process for inspecting the dashboards, they are useless when nobody looks at them.

Use **events and logs** for all other signals and messages. The goal is to provide contextual clues for ad-hoc problem solving. Events and logs can be written to a remove logging service, a local logging service, and directly to disk. Certain events, like deployment markers, can also be useful in metrics and error reporting. Engineers should write to the log when the application:

1. Transfers to a different state: start, pause, reload, and stop, usually at info level
2. Starts or ends an action, usually below info level
2. Handles an *expected error* successfully, where level depends on severity of the error
3. Encounters an *unhandled error*, using the highest level and duplication to error reporting is fine

For very large systems it can be interesting to implement a way to control the verbosity of running applications so you can increase and the level of details only when investigating an issue. Most error reporting and metrics services have a way to control the reporting rate through sampling. Logging usually has levels and can be configured to only show everything above a certain threshold.
