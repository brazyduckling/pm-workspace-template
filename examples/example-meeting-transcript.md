# Example Meeting Transcript

Use this as sample input for the `/onboard` wizard if you don't have your own meeting notes handy.

---

**Meeting: [URGENT] Checkout "Sticky Cart" vs. "Fast-Track" Logic Sync**
**Date:** March 6, 2026
**Time:** 10:00 AM – 10:30 AM
**Participants:** Sarah (Product Manager - Core UX), Dave (Senior Engineer - Backend/APIs), Meera (Lead Designer), Josh (Marketing/Growth), Marcus (QA/Testing)

---

[00:00:01] Sarah: Okay, can everyone hear me? I'm at the airport so sorry if there's an announcement. We need to lock the logic for the "Hungry Now" button before the sprint ends tonight.

[00:01:15] Dave: Wait, I thought we were calling it "Express Checkout"? The API docs I wrote last night say POST /v1/express-track. If we change the name again, the frontend hooks are going to break.

[00:02:10] Meera: It's "Hungry Now" in the UI. Marketing insisted. Josh?

[00:02:22] Josh: Yeah, "Express" felt too much like a shipping thing. "Hungry Now" tested 14% better in the London focus groups. But Sarah, did we decide if it bypasses the "Do you want a side of garlic bread?" cross-sell? Because if it does, the average order value (AOV) is going to tank.

[00:04:05] Sarah: That's the mess. If it's a "fast-track," it has to be fast. If we pop up three modals asking about dips and drinks, it's just the normal checkout with a different colored button.

[00:05:30] Marcus: Hey guys, jumping in — I found a bug in the staging build. If a user has an expired credit card but clicks "Hungry Now," the app just spins forever. It doesn't redirect to the payment update page. It just... hangs.

[00:06:45] Dave: That's because the fast-track endpoint assumes a valid payment_token is present. It doesn't have an error handler for 402 Payment Required. I can fix it, but I'll need another two hours.

[00:08:12] Meera: Also, Sarah, look at the Figma link I just sent. If the user is ordering from a place with "Customizable Toppings" (like a pizza place), the "Hungry Now" button is overlapping the "Add Extra Cheese" toggle. It looks like a total mess on iPhone SE screens.

[00:10:00] Sarah: Ugh, the SE users. Okay, can we hide the button if the screen height is below a certain pixel count?

[00:11:15] Josh: No way. A huge chunk of our late-night student demographic uses older iPhones. We can't cut them out of the "fast" experience. They're the ones most likely to use it!

[00:13:00] Dave: Can we go back to the "Sticky Cart" logic? If they have stuff in their cart from yesterday, and they hit "Hungry Now" on a new restaurant, what happens? Do we clear the old cart? Or merge them? Because we can't do multi-restaurant delivery yet.

[00:14:20] Sarah: It should definitely clear the old cart.

[00:14:35] Meera: Wait, if I'm halfway through a £50 family order and I accidentally tap "Hungry Now" on a burger place, I lose my whole cart? I'd delete the app.

[00:16:00] Josh: We need a "Are you sure?" modal.

[00:16:15] Sarah: NO. No more modals! The whole point of this feature is one-tap ordering. If we add an "Are you sure?" modal, we've just invented a very expensive "Checkout" button.

[00:18:45] Marcus: Guys, I'm still seeing the spinning wheel on the expired card thing. Dave, did you push the fix to dev-3?

[00:19:00] Dave: No, Marcus, I'm in this meeting. I can't code and talk at the same time. Also, Sarah, the legal team sent an email — apparently, we need to show the delivery fee before the tap. We can't just hide it until the receipt.

[00:21:10] Sarah: (Heavy sigh) Okay, so we need: the button to show the total price including fees, a way to handle expired cards without a "hang," a solution for the overlapping UI on small screens, and a decision on the "Clear Cart" catastrophe.

[00:23:30] Meera: What if the "Hungry Now" button only appears after you've selected your main items? Like, it replaces the "Go to Cart" button?

[00:24:50] Josh: That defeats the purpose. The "Hungry Now" should be on the home screen for "The Usual" order. Like, "Tap here to get your Friday Night Pad Thai."

[00:26:15] Dave: If we're doing "The Usual" from the home screen, that's a completely different API. That's a reorder logic, not a checkout logic. We haven't even scoped that.

[00:27:40] Sarah: Okay, we're spiraling. We have 2 minutes. Here's the deal:

Dave: Fix the 402 error hang. Just redirect to the standard checkout if the payment fails.

Meera: Shrink the button padding for SE users. Don't hide it.

Josh: We're keeping the cross-sells for now, but only ONE. Pick the best one.

Sarah (Me): I will talk to Legal about the "Price on Button" requirement.

[00:29:10] Marcus: And the cart clearing thing?

[00:29:45] Sarah: If they have a cart already, the "Hungry Now" button turns into "View Cart." We don't clear anything. It's safer.

[00:30:00] Dave: That's going to take until Tuesday.

[00:30:15] Sarah: Make it happen by Monday. Bye everyone, they're calling my group for boarding.
