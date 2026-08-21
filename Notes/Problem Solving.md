## Problem Solving

**1. The Odd Weight Coin (your example)**
 You have 8 coins, identical in appearance. One is fake and weighs slightly less. Using a balance (weighing) scale only **twice**, find the fake coin.
 → Teaches divide-and-conquer (split into 3 groups, not 2 — a nice surprise for students who assume halving).

**2. 9 Balls, One Weighing**
 You have 9 balls, one heavier than the rest. Find it in just **1** weighing.
 → Simpler warm-up version of the above; good stepping stone.

**3. The Two Egg Drop**
 You have 2 identical eggs and a 100-floor building. You want to find the highest floor an egg can be dropped from without breaking, using the fewest possible drops in the worst case.
 → Great for showing "worst case" thinking — sets up algorithm complexity later.

**4. Three Switches, One Bulb**
 There are 3 switches outside a room, only one lights the bulb inside. You can flip switches as much as you like, but can enter the room only **once**. Find which switch controls the bulb.
 → Forces "creative" observation (uses heat, not just light) — fun twist.

**5. The Two Jugs Problem**
 You have a 4-litre jug and a 3-litre jug (no markings). Measure exactly 2 litres.
 → Classic state-space problem; can literally be drawn as a flowchart of states.

**6. Wolf, Goat, and Cabbage (River Crossing)**
 A farmer must cross a river with a wolf, a goat, and a cabbage, using a boat that carries only the farmer + one item at a time. Wolf eats goat, goat eats cabbage if left alone. Get everyone across safely.
 → Great for constraints + sequencing; students often "solve" it by trial and error, then you show them how to write it as a set of rules/steps.

**7. Poisoned Bottle**
 You have 1000 bottles of wine, one is poisoned. You have 10 test strips; poison takes effect only if consumed, and one strip can test multiple bottles at once (mixed). Find the poisoned bottle using the strips.
 → Advanced version of the coin problem; introduces binary encoding (great "aha" moment — 2^10 = 1024 > 1000).

**8. Fake Coin, Don't Know Heavier or Lighter**
 12 coins, one is fake (could be heavier OR lighter), 3 weighings to find it AND say if it's heavier or lighter.
 → Harder follow-up to puzzle 1; good bonus/challenge problem for fast finishers.

**How to run it in class:**

- Give the coin puzzle (#1) first as the flagship — most students have some intuition already.
- Ask them to write their solution as **numbered steps** (not vague reasoning) — that's the actual C-programming-relevant skill you're building (sequencing + decisions).
- Then ask: "What if I gave you 27 coins instead of 8 — how many weighings now?" — this nudges them toward spotting the log₃ pattern without you stating it outright.

That's the classic **burning rope puzzle**. Here it is:

**The Puzzle**
 You have two ropes. Each takes exactly 60 minutes to burn completely, but they burn unevenly — so you can't assume half the rope burns in 30 minutes (one half might burn fast, the other slow). Using just these two ropes and a lighter, measure exactly **45 minutes**.

**The Solution**

1. Light **Rope A from both ends** at the same time, and **Rope B from one end only**, at the same time (t = 0).
2. Rope A, burning from both ends, will finish in **30 minutes** — no matter how unevenly it burns, the two flames meet halfway through the total burn time.
3. The instant Rope A finishes (at the 30-minute mark), light **Rope B's other end too**.
4. Rope B has been burning for 30 minutes from one end, so it has "30 minutes worth" of rope left. Now burning from both ends, that remaining portion finishes in half the time — **15 minutes**.
5. Total time elapsed: 30 + 15 = **45 minutes**.



**Everyday life problems (easiest, good for warm-up)**

1. Making a cup of tea/coffee — good for showing sequence and decisions ("if no milk, use black tea")
2. Tying a shoelace — great for showing how hard it is to describe something "obvious" precisely
3. Crossing a busy road safely — introduces conditions and repetition ("look left, look right, repeat until safe")
4. Getting ready for college in the morning — shows ordering matters (can't wear shoes before socks)
5. Making Maggi/instant noodles — clean sequential steps with a timer (loop concept)

**Decision-heavy problems (good for if-else thinking)**

6. Deciding what to wear based on weather — introduces conditionals naturally
7. Withdrawing cash from an ATM — has validation steps (wrong PIN, insufficient balance) — great lead-in to error handling
8. Ordering food on Swiggy/Zomato — has choices, confirmation, payment failure retries
9. Deciding whether to carry an umbrella — simple if-else

**Search / sort / optimization problems (fun, sets up later units)**

10. Finding a friend's name in a phone contact list — leads into searching
11. Arranging a shuffled deck of playing cards by rank — leads into sorting
12. Finding the shortest route from hostel to canteen avoiding a closed gate — leads into pathfinding intuition
13. Splitting a mess/canteen bill fairly among 4 friends — division + rounding edge cases

**Group/creative problems (good for teams, more discussion)**

14. Planning a birthday party on a fixed budget — resource allocation
15. Making a timetable for exam study across 5 subjects in 5 days — scheduling
16. Packing a suitcase for a 3-day trip with a weight limit — constraints
17. Organizing a cricket/kabaddi tournament for the class — combinatorics, brackets

**Classic CS-flavored fun ones**

18. Guessing a number between 1-100 in fewest tries — leads beautifully into binary search later
19. Sorting a mixed pile of coins by denomination — sorting/counting
20. Giving correct change for a purchase using minimum notes/coins — greedy algorithm intuition