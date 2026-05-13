# DartsXL Counter

**A dart counter and checkout route analyzer for all major dartboard types — built on a novel real-time combinatorial algorithm.**

Live app: [dartsxl.com](https://dartsxl.com) · [Google Play](https://play.google.com/store/apps/details?id=com.dartsxl.counter)

---

## What it is

DartsXL Counter is a dart scoring counter with an integrated checkout route analyzer. It supports the classic dartboard, quad-boards and the DartsXL Dartboards. The DartsXL Counter runs in the browser and as an Android app.

The counter itself is straightforward. The checkout route analyzer is not.

---

## The algorithm problem

In 501-rules darts, a "checkout" is the sequence of throws needed to reach exactly zero from a given remaining score. For any given score, there are many possible routes, and they are not equal — some require fewer total darts, some leave better or worse options if you miss.

Every existing dart counter application has solved this by brute force editorial work: someone manually enumerated the accepted "best" routes for every possible remaining score, entered them as hard-coded lookup tables, and manually ranked them. This is the universal prior art in the field.

The combinatorial space is large enough that a naive recursive solution exploring all cases will freeze a regular device. That's why no one had written a live algorithm before — it simply wasn't fast enough to be practical.

---

## The DartsXL solution

The DartsXL Counter computes checkout routes live using a heavily optimized recursive algorithm. After optimization work, the algorithm produces results in **double-digit milliseconds** on typical devices — fast enough to be invisible to the user during normal counter use.

This is not just a performance improvement. It means:

- Checkout routes are computed rather than looked up, making the system correct by construction rather than by editorial completeness
- The ranking of routes is itself algorithmic rather than manually ordered
- The approach generalizes to any dartboard geometry, including non-standard boards, without requiring new lookup tables

---

## The Checkout Routes Analyzer

Built on top of the core algorithm, the Analyzer is the key novel feature of DartsXL. It goes substantially beyond what a dart counter normally does.

**Match replay and branching.** From any state in a real recorded match, the user can branch off a simulated "what if" match — exploring what the checkout options would have looked like if different throws had been made, or what the future options look like from the current position.

**Neighbour analysis.** For any checkout route, the Analyzer also computes routes for all *neighbouring segments* — the segments physically adjacent to the target on the board. This answers a question no standard dart app addresses: if you miss your target and hit a neighbour instead, does that hurt you, help you, or make no difference?

The Analyzer grades neighbours as "good" (same or fewer darts needed) or "bad" (more darts needed), giving the user a genuine strategic picture of each throw, not just a recommended target. Because it computes routes for the main target plus all neighbours simultaneously, it runs in the **100–200ms range** on older devices — still fast enough to feel immediate.

---

## Technical overview

- **Design of the dartboards:** Python — used to mathematically describe and validate the geometry of the DartsXL dartboard and the classic dartboard. Used as the design basis for the physical DartsXL dartboards and for defining the segment polygons making up the graphical dartboards in the DartsXL Counter.
- **Web and Android app:** ES6 JavaScript — a single codebase serving both the web app (hosted via GitHub Pages, live at dartsxl.com) and the Android app (Google Play Store)
- **Algorithm producing checkout routes:** Written in JavaScript and is included in the application without any network calls necessary.
- **Physical products:** Custom-designed physical dartboard accessories manufactured to spec and sold via Amazon, designed to the same geometric specifications developed in the Python phase
- **Code:** The deployed app is obfuscated. The repository hosts the production build.

---

## Why this exists

This started as a problem I wanted to solve correctly. The hard-coded lookup table approach used everywhere else felt like an editorial patch over a computational problem. I wanted an actual algorithm.

The project ended up spanning mathematical modeling in Python, a full web and Android application in JavaScript, physical product design, manufacturing, and retail. It's live, it works, and the core algorithm does something that wasn't being done before.

---

## Links

- Live web app: [dartsxl.com](https://dartsxl.com)
- Google Play: [DartsXL Counter](https://play.google.com/store/apps/details?id=com.dartsxl.counter)


---

## DartsXL Dartboards

The DartsXL dartboards are physical sisal dartboards designed from scratch using the same geometric models built in Python for the counter app. All boards extend the standard doubles and trebles with a quad-scoring ring — with custom ring proportions (quads being the thinnest ring) that differ from any standard dartboard.

**Heptaboard** — A heptagonal (seven-sided) sisal dartboard with a custom 20-segment layout adapted to the shape. See product images for the geometry. Available in two variants — Full (all 20 segments) and Open (a subset of segments):
- [Heptaboard Full](https://www.amazon.co.uk/DartsXL-Dartboard-Heptaboard-Sisal-Quads/dp/B0FN82SHW5) *(Amazon UK)*
- [Heptaboard Open](https://www.amazon.co.uk/DartsXL-Dartboard-Heptaboard-Sisal-Quads/dp/B0FN83N625) *(Amazon UK)*

**XLBoard** — A classic round dartboard with the standard 20-segment layout, extended with a quad-scoring ring. Doubles, trebles and quads have custom proportions:
- [XLBoard — Classic round board with quad-ring, custom ring proportions.](https://www.amazon.co.uk/DartsXL-Dartboard-XLBoard-Sisal-Quads/dp/B0FNNBS5Y1/) *(Amazon UK)*