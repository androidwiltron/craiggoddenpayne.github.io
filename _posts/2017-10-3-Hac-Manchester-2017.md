---
layout: post
title: HacManchester 2017
---

### We won the GCHQ challenge!!

This year I entered the HacManchester competition again, with 2 other people at Zuto. 

We decided to go for the GCHQ challenge, since it sounded to us like the most interesting challenge. The challenge was to create a product that could be used to contact the emergency services in a different way.

What we created was "Beacon". Beacon is a device (we prototyped on a raspberry pi) which is constantly listening out for a preset keyword. When it detects the keyword, it will contact the emergency services. This sounds incredibly simple (the concept really is), but the actual implementation involves many parts!

First of all we built the raspberry pi, and loaded raspian. We added the microphone module and we used the library ### to start recording data. We then chunked the audio into segments and when we detected audio data, we sent this data to Amazon Lex for analysis. We set up a trigger on Lex when a keyword is said. We chose "Help" and "I'm on fire", but we would have eventually given the oppotunity for the user to set these keywords. 
When the keyword was triggered, we sent a notification via an sns topic, which called an api gateway, which called into our PoliceHQ application. This sent the clientIp of the original request along with the type of emergemncy, which the PoliceHQ application showed on a map with a list of outstanding jobs.
We also created an android application, using Xamarin, which sent a notification if the keyword was triggered, and also allowed the customer to cancel the notification, if they said the keyword by mistake.

Not bad for 24 hours worth of work!

## diagram

## video

# Tags: HacManchester, Zuto, GCHQ, Winners, 2017