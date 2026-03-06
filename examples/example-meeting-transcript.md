# Example Meeting Transcript

Use this as sample input for the `/onboard` wizard if you don't have your own meeting notes handy.

---
Meeting: 🚨 URGENT: "Where's my Food" / Driver Tracker
Date: March 6, 2026
Platform: Google Meet
Participants: 6 (Sarah, Dave, Meera, Josh, Marcus, +1)

[00:00:12] Sarah: Is everyone in? I can’t see Meera. Oh, there you are. Okay, look, the Support Slack is blowing up. Ever since the v4.2 push, the "Where is my driver?" button is basically a random number generator.

[00:01:05] Josh: It’s worse than that. I just tried to order a burrito and the map showed my driver in the middle of the Atlantic Ocean. Like, off the coast of Africa.

[00:01:45] Dave: (Chewing) Sorry, finishing lunch. That’s a coordinate flip. The new API is swapping latitude and longitude for certain Android builds. It’s an easy fix, but—

[00:02:15] Meera: It’s not just the coordinates, Dave. The button itself is disappearing. If a user backgrounds the app to check TikTok and comes back, the "Track Driver" button just... vanishes. They have to kill the app to see where their pizza is.

[00:03:40] Sarah: Wait, why is it vanishing? Meera, is that the new "Minimalist Overlay" you guys pushed?

[00:04:10] Meera: No! Don't pin that on Design. We specifically said the button should stay pinned to the bottom nav. But Marcus said the "Live Activity" widget was conflicting with the in-app button.

[00:05:22] Marcus: (Heavy interference/wind noise) Can you hear me? I’m walking to the lab. Yeah, the Live Activity is hogging the refresh token. So when the app comes back to the foreground, the API thinks the session is dead. It’s not "vanishing," it’s failing to authenticate.

[00:06:55] Josh: Guys, customers don't care about "refresh tokens." They care that they spent £40 on Thai food and now they’re staring at a blank home screen. Our "Where is my driver" CSAT score dropped from 4.8 to 1.2 in three hours.

[00:08:15] Sarah: Okay, stop. Dave, can we just roll back to the old "Where is my driver" logic? The one that just showed the static map?

[00:08:45] Dave: I mean, I could, but we’d lose the "Estimated Time to Door" (ETD) logic. And the old map didn't show if the driver was on a bike or a car. Remember how much Marketing complained about "misleading vehicle icons"?

[00:10:05] Josh: (Sighs) If the choice is "Wrong Icon" or "Atlantic Ocean," I choose the wrong icon.

[00:11:30] Meera: Also, I just noticed something in the Figma. Who changed the button color to light gray? It looks like it’s disabled. I’ve had three DMs from the UX researchers saying people aren’t even clicking it because they think it’s broken.

[00:12:45] Sarah: I thought we changed it to "Ghost Grey" to match the "Order History" page?

[00:13:10] Meera: No! It’s an action button. It needs to be "Hunger Orange." If it’s gray, it looks like the driver hasn’t even picked up the food yet.

[00:15:20] Marcus: (Sound of a door slamming) Okay, I’m in the lab. I’m looking at the logs. It’s not just Android. iOS is also failing because of the "Driver Chat" integration. If the driver sends a message like "I'm outside," it blocks the map view.

[00:16:45] Sarah: You’re kidding. So they get the food, but they can’t see the map to know it’s there?

[00:17:10] Marcus: Basically. The "Where is my driver" button is being hidden by the "Chat" notification, and the notification won't swipe away.

[00:19:00] Dave: That’s because the z-index on the chat modal is set to 9999. I told the frontend guys that was a bad idea.

[00:20:30] Sarah: (Background noise of a dog barking) Quiet, Buster! Okay, look. We have 10 minutes before the CTO asks for an update. Dave, fix the Lat/Long flip. Meera, send Marcus the hex code for the orange button—DO NOT use gray. Marcus, can we just kill the chat integration for today? Just hide the chat feature until we fix the map?

[00:22:15] Josh: If we kill chat, how do they tell the driver the doorbell is broken? We’ll get a surge in "Order Not Delivered" tickets.

[00:23:45] Sarah: Then we’re screwed either way.

[00:25:00] Meera: Wait, I have an idea. Can we just put a giant "Call Driver" button at the top? If the map is broken, at least they can talk to a human.

[00:26:30] Dave: No. GDPR. We use an anonymized VoIP bridge. If I try to spin that up now, the whole "Where is my driver" system will crash the auth server.

[00:27:50] Marcus: I’m seeing a spike in "App Not Responding" errors. I think everyone is refreshing the map at the same time because it’s not updating.

[00:28:40] Sarah: Great. We’re DDOS-ing ourselves.

[00:29:15] Sarah: Okay, new plan. Dave, hotfix the coordinates ONLY. Marcus, force-refresh the map every 30 seconds instead of every 5 to save the server. Josh, tell Support to send a generic "We’re having map issues" push notification so people stop clicking the button.

[00:30:05] Dave: I’ll try, but no promises on the Atlantic Ocean thing for another hour.

[00:30:25] Sarah: I have another meeting. Just... make the button orange. Please.