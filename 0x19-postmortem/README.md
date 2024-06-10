<<<<<<< HEAD
=======
0x19. Postmortem

>>>>>>> 17524514cc03f9e764277d245f1ffd92fc0922e5
### Postmortem: June 2, 2024 Outage

---

#### Issue Summary

![Cat Pulling Cables](https://media.giphy.com/media/xT0GqFv2Rm5RBfZfnO/giphy.gif)

*Sometimes, it feels like our servers are held together by cat hair and good intentions.*

**Duration:** June 2, 2024, 14:00 - 16:30 UTC

**Impact:** The entire web application was down. Users were met with a 503 Service Unavailable error. Approximately 100% of users were affected, which is like closing the doors to an all-you-can-eat buffet during lunchtime.

**Root Cause:** A misconfiguration in the load balancer caused all incoming traffic to flood a single server, which inevitably waved a white flag and crashed.

---

#### Timeline

- **14:00 UTC:** Issue detected via monitoring alert. Cue panic music.
- **14:05 UTC:** On-call engineer received alert, put on the superhero cape, and started investigating.
- **14:10 UTC:** Assumed backend server had a meltdown; performed a quick server restart (IT's equivalent of turning it off and on again).
- **14:20 UTC:** Server restart didn’t help. Problem escalated to the SRE team. "We need backup!"
- **14:30 UTC:** SRE team dove into logs and load balancer configurations like Sherlock Holmes with coffee.
- **14:45 UTC:** Traffic misrouting identified. "Elementary, my dear Watson!"
- **15:00 UTC:** Brief wild goose chase suspecting a DDoS attack. Turns out the internet was not out to get us this time.
- **15:15 UTC:** Realization hit—load balancer configuration was the real culprit.
- **15:30 UTC:** Corrected the load balancer settings. Order restored.
- **15:45 UTC:** System began to stabilize. Time to exhale.
- **16:30 UTC:** Confirmed all systems were operational and threw a tiny, socially-distanced celebration.

---

#### Root Cause and Resolution

**Root Cause:**
A well-meaning maintenance update accidentally changed the load balancer configuration, directing all web traffic to a single, unsuspecting server. This was like sending all the shoppers in a mall to one checkout counter on Black Friday. Overwhelmed, the server crashed.

**Resolution:**
The SRE team heroically reverted the load balancer settings to their original state, spreading the traffic evenly across all servers. This allowed the overwhelmed server to recover, and the site gradually returned to normal, much like traffic after a jam clears up.

---

#### Corrective and Preventative Measures

**Improvements/Fixes:**
1. Tighten change control processes to avoid unexpected "fun" like this in the future.
2. Enhance monitoring to catch traffic distribution issues quicker than a cat catching a laser pointer.
3. Boost team knowledge on load balancer configuration with training sessions, preferably with snacks.

**Tasks:**
- **Patch Load Balancer Configuration:**
  - Conduct a thorough review and ensure best practices are adhered to. No more rogue settings!
- **Enhance Monitoring:**
  - Implement alerts specifically for uneven traffic distribution.
  - Introduce more detailed monitoring on server load and performance.
- **Change Control Process:**
  - Develop a comprehensive checklist for configuration changes, including peer reviews and pre-deployment testing.
  - Organize regular training sessions on load balancer management. (Optional: offer motivational cookies.)
- **Documentation Update:**
  - Create and distribute detailed documentation on correct load balancer configuration.
  - Ensure all team members are familiar with and understand this documentation.

---

**And remember, folks, while our servers might sometimes behave like temperamental pets, we’re committed to keeping them well-trained and purring along smoothly.**
