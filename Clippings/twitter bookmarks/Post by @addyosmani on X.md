---
title: "Post by @addyosmani on X"
source: "https://x.com/addyosmani/status/2082723002836545641"
author:
  - "[[@addyosmani]]"
published: 2026-07-30
created: 2026-07-30
description: "Software quality now depends on the constraints you set around your agents. When humans manually wrote most of the code we could look at th"
tags:
  - "clippings"
---
Software quality now depends on the constraints you set around your agents.

When humans manually wrote most of the code we could look at the code itself for signs of quality. Is it clean? Is it thoughtful? Is it fast? Can another engineer understand it? Does it have tests?

Agents can now generate more code than people can read. When code generation scales beyond review, quality - checks for one or more of correctness, maintainability, security, performance etc - increasingly has to live somewhere else.

It moves into the harness, environment and operating system around the agent.

This can be the tests and deterministic checks that decide what the system is allowed to do (amongst others). Your constraints are what may eventually enable loops of agents to deliver production software reliably. They can include unit tests, property tests, acceptance tests, mutation testing and quality metrics.

This back-pressure lets the system resist bad work before it becomes somebody elses problem.

Set your constraints. They decide whether the code your agents generate is good enough to ship.

![set the constraints around your agents - correctness, security, maintainability and other dimensions.](https://pbs.twimg.com/media/HOdPzoWaYAA6dgQ?format=jpg&name=large)

---

## Comments

> **Mikhail Rogov @i\_mika\_el** · [2026-07-30](https://x.com/i_mika_el/status/2082723545965109720)
> 
> which constraint has actually caught the most bad agent code for you?
> 
> > **Addy Osmani @addyosmani** · [2026-07-30](https://x.com/addyosmani/status/2082725110885286388)
> > 
> > Performance (metrics, budgets). Most harnesses optimize for basic correctness but don't go too far on UX & perf being as good as they could be.

> **Vishal Singh @vishalsingh2972** · [2026-07-30](https://x.com/vishalsingh2972/status/2082723498137690490)
> 
> end of day agents are still dumb AI that needs lot of maneuvering lol
> 
> > **Addy Osmani @addyosmani** · [2026-07-30](https://x.com/addyosmani/status/2082725271917232312)
> > 
> > And constraints definitely help 😅

> **Cj @cjaythecreator** · [2026-07-30](https://x.com/cjaythecreator/status/2082724525788016844)
> 
> AI coding quality is increasingly just how difficult did you make it for the agent to ship garbage? 😅
> 
> > **Addy Osmani @addyosmani** · [2026-07-30](https://x.com/addyosmani/status/2082725662813761651)
> > 
> > How difficult you make it to \_not\_ ship slop 😂

> **Jan Amann @jamannnnnn** · [2026-07-30](https://x.com/jamannnnnn/status/2082728233703719113)
> 
> I totally agree, it’s what I’m working toward with \`eloqnt lint\` in the i18n space.
> 
> It’s tricky though finding a balance of what can be deterministically checked, and what requires more AI for verification. Or a mix of both? Still a lot to explore here I think!
> 
> > **Jan Amann @jamannnnnn** · 2026-07-14
> > 
> > Today, I'm launching eloqnt/studio.
> > 
> > An AI-based toolchain that helps you ship high-quality translations. All from the command line.
> > 
> > 𝚎𝚕𝚘𝚚𝚗𝚝 𝚕𝚒𝚗𝚝
> > 
> > 𝚎𝚕𝚘𝚚𝚗𝚝 𝚛𝚎𝚟𝚒𝚎𝚠
> > 
> > 𝚎𝚕𝚘𝚚𝚗𝚝 𝚝𝚛𝚊𝚗𝚜𝚕𝚊𝚝𝚎
> > 
> > With our hosted model, or bring your own. 🔗↓