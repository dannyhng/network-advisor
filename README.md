# Network Blueprint Advisor

**Live Demo:** https://dannyhng.github.io/network-advisor/

---

## Project Overview
The Network Blueprint Advisor is an interactive web tool I built to generate realistic network designs based on real-world constraints.
Instead of giving generic advice, the tool takes inputs like budget, device count, and use case, then builds a network design that reflects how someone would actually approach this in a real environment.

---

## Motivation and Philosophy

After studying for the CCNA and Security+, I realized something:

I could configure networks, but I wasn’t fully comfortable designing them.

Most learning materials focus on commands and protocols, but in real life, nobody hands you a perfect topology. You get vague requirements like:

- “We have 40 devices and some cameras”
- “We need it to be reliable”
- “Budget is limited”

I built this tool to practice turning those messy requirements into actual design decisions.

My philosophy is simple:

**Boring network design is good network design.**

If a network is predictable, stable, and easy to troubleshoot, it is already doing its job well. 

---

## Engineering Process: Challenges and Solutions

### Challenge 1: Learning JavaScript and State Management

This was my first time building a multi-step interactive application.

At the beginning, everything felt messy. I didn’t understand how to:
- Track user selections across multiple steps
- Update the UI without refreshing the page
- Keep everything from breaking when users clicked things out of order

**What I did:**

I learned how the DOM actually works and built a simple state object to store all user inputs.

Every button click updates that object, and the UI reacts based on it.

I also added localStorage after realizing how annoying it was to lose progress on refresh.

---

### Challenge 2: Designing Realistic Hardware and Topology Logic

At first, my recommendations were pretty unrealistic.

I was defaulting to higher-end hardware and more advanced designs, even when the scenario didn’t actually need it. It worked on paper, but it didn’t feel like something you would confidently deploy in a real environment.

The harder part wasn’t picking hardware, it was justifying *why* a certain design made sense given constraints like budget and device count.

**What I did:**

I started breaking decisions down into simple conditions.

For example:
- High budget + high device density → Layer 3 switching with SVIs  
- Lower budget or smaller networks → Router-on-a-Stick for simplicity  

I also added real-world considerations like licensing costs and workload-specific hardware (for example, different storage drives for surveillance vs NAS use).

This forced me to move away from “ideal designs” and start thinking in terms of practical tradeoffs.

---

### Challenge 3: Bridging Logical Design and Physical Reality

Early on, the tool looked good on paper.

It could generate VLANs, routing strategies, and security zones.

But then I realized something:

None of that matters if the power goes out or a surge kills the equipment.

That was a gap in my thinking.

**What I did:**

I added a physical layer component:
- UPS recommendations for power loss
- Rack suggestions for airflow and organization

This forced me to think beyond “network config” and start thinking in terms of full systems.

---

### Challenge 4: The Double NAT Problem

While testing different setups, I ran into a common issue:

Putting a new router behind an ISP router caused Double NAT.

This broke things like VPN access, even though everything looked “correct”.

**What I did:**

I added logic that explicitly tells users to set their ISP device to bridge mode.

This made the tool more realistic, because it accounts for how networks are actually deployed, not just how they look in diagrams..

---

### Challenge 5: UI Readability and Complexity

As I added more features, the interface started getting harder to read.

At one point:
- Text was too small
- Layout felt cramped
- Navigation started breaking as I added more steps

**What I did:**

I simplified the layout and improved spacing and font sizes.

I also reworked how navigation works so the flow stays consistent, even as more questions are added.

---

## What I Learned

### Systems Thinking Over Configuration

Studying for certifications taught me how to configure devices.

This project taught me how to think about systems.

I started considering things I used to ignore:
- Power stability
- Hardware limitations
- Failure scenarios
- Data protection

It changed how I approach network design completely.

---

### Translating Design Decisions into Code

One of the hardest parts was turning “engineering judgment” into actual logic.

For example:
When should a network use Router-on-a-Stick vs Layer 3 switching?

That is usually based on experience, not strict rules.

I had to break that down into conditions like:
- Device count
- Budget
- Traffic type

That process made me understand those decisions much more deeply.

---

### Thinking Beyond Initial Deployment

I used to think a network was “done” once everything worked.

This project forced me to think about what happens after:

- How do you monitor it?
- How do you troubleshoot it later?
- What happens when something fails?

That is where things like logging, backups, and documentation actually matter. 

---

## Tech Stack

- Logic and Interactivity: Vanilla JavaScript  
- Structure and Styling: HTML5 and CSS3  
- Framework: Astro  
- Libraries: jsPDF, html2canvas  

---

## Key Features

- Dynamic hardware recommendations based on budget and scale  
- Intelligent routing strategy selection (RoAS vs Layer 3 offload)  
- Automatic network segmentation using VLAN design  
- Homelab-focused software stack suggestions  
- Exportable architecture via PDF and Markdown  

---

## How to Run Locally

```bash
# Clone the repository
git clone https://github.com/dannyhng/network-advisor.git

# Navigate into the project directory
cd network-advisor

# Install dependencies
npm install

# Start the development server
npm run dev
```
