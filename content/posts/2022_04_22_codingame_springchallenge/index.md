+++
title = "Codingame - Spring Challenge"
date = 2022-05-13
+++

Last week [CodinGame.com](https://www.codingame.com/home) hosted a Spring Challenge, it's a 10-day bot programming
competition that I gave a try and wanted to share my thoughts.

The contest is held yearly and this time about ~8000 people participated with at least a single submission. The idea revolves
around creating an AI for a game - in this particular case the goal is trivial: protect your base and outlive your
opponent.
Players start at opposite corner of the map and control a team of 3 heroes while monsters randomly spawn at the edges
and regularly attack bases, if a monster reaches one's base it deals damage. Heroes can kill monsters, gain 'mana' for
each damage dealt and can cast a few spells.

{{ image(src="play-opt.gif", alt="Spring Challenge 2022 Playing") }}

I always wanted to do something similar locally, i.e. code a simple game and create an AI for that, ideally
leveraging massive number of simulations. Except for controlling the environment itself, CodinGame checks pretty much all required
boxes, and it works in a multiplayer mode! I intended to spend only a few hours to find out how polished the
platform is - **to my surprise when 3 days later I clocked in ~10h+.** Delight at its finest.

**This was my first try at such type of contests so whatever you read here should be taken a with a grain of salt.**
Having said that, let me describe the road I took to get to Gold league - it should be quite representative of what
one can expect from such events.

### Wood leagues

I started with the simplest tactic one can imagine: find the closest monster to my base and attack it with all we got.
Hard to get simpler... yet it turned out to be an effective approach. My take on that is that everyone
already moved to more efficient approaches but haven't managed to fully implement them yet.

Let's improve it and assign a single hero to a single monster. I also noticed a pretty severe bug in my trivial implementation -
turns out that when sides are changed (roughly half matches) own hero identifiers change i.e. 0-2 on Blue side and 3-5
on Red side. *Yes, it meant that I was loosing half games instantly [cough, cough].*

*This got me into Bronze, ~TOP 2500*

### Bronze leagues

New league, new toys. They gave us a few spells and introduced a fog of war. Because both bases were always out of fog
of war and my brave heroes were always going for the closed 'visible' monster... they tended to run mindlessly into
enemy base if all monsters on my side were killed. Additionally, enemies started using spells and more sophisticated
tactics e.g. 2 defenders and 1 attacker. The first shift of meta.

Another set of naive improvements - let's ignore enemies further than X distance from my base.

This improved my score only slightly, I jumped about 200 positions and noticed that some games end with timeout where
player with higher 'wild mana' wins (wild mana - mana gathered outside own base), given that my folk usually stay within
base it's hard to win anything that ended due to round limit.

*Bronze, TOP ~2300*

Coded basic 2-defender-1-attacker tactic, Also started using 'Control' spell on all monsters within range that are not
heading towards enemy base and have more than 14 health points (Control spell forces a unit to move towards a given
direction). Ignore fog of war for now.

{{ image(src="full_game.png", alt="Spring Challenge 2022 Playing") }}

*Submitted a new version, got to Bronze ~1500 and went to sleep. Got promoted to Silver overnight.*

### Silver leagues and the road to Gold

About 2000 players were moved to Silver with me, not bad. My solution was very hacky at this point, and opponents were
getting fancier with their solutions all the time. After fixing a few more issues with defenders (e.g. they tended to
stick a little too close to the middle, wasting too much time on random monsters spawning next to my base). This didn't
do much for my overall score, top ~1300.

I decided that it's time for a big bang rewrite as the approach is not too flexible. After another hour I was in
slightly better shape with fewer magic ifs, functions and random numbers. Got back to working
on strategy and tactics again, this time I wanted to invest more upfront before submitting my version for evaluation.

Major changes:

- Introduced 'stances', so that I could dynamically change behaviour e.g. DEFENDER, MIDDLE ROAM, ATTACKER, DIVE etc.
- My 'Attacker' started farming in the middle and only around 80th turn moved into an offensive position.
- Attacker learned new tricks:
    - e.g. Wind + Shield spell combo
    - Shield monsters aggressively if they are healthy and close to enemy base (so that enemies can't Wind them anymore)
- Defender improvements:
    - use Wind a lot more, prioritize it over everything else if monster is not shielded
    - use Control very aggressively, turned out that if I'm Controlling my side of map well enough then opponents can't
      utilize their offensive positions

This got me into top 70 (TOP 7 in Poland) and Gold league was opened on the following day!
Seemed very promising given that I still could think of plenty improvements on both def and off sides (better combos,
better farming, less reliant on magic numbers, better timing for offense, take enemy position into account when
defending, number of enemies, simulations, local-system parameter evaluation etc.), plus my implementation was... less
than ideal.

Then I had to take a break for a few days. In fact that was my final submission.

*Day 3/4: Top 70*

Over time my AI started loosing its appeal, people caught up and even surpassed my score. Eventually, I ended the
competition in top 800 a week later without any additional submissions.

{{ image(src="chrome_lGriSiCTFb.png", alt="Spring Challenge 2022 Playing 2") }}

### Post-mortem

This was a very interesting venture into the classic engineering loop:

**observe -> think/measure -> improve -> observe**

Enjoyment was absurdly high. Albeit, I felt a little disappointed when my AI got demoted into TOP 800 (out
of ~8k participants) during my absence - I was hoping for a better final placement despite my inactivity!
Anyway, probably still a reasonable placement for a first timer.

It scratched my competitive side a lot. Next time I need to set up a better schedule so that I have enough time to at 
least give it a full try.

**A few final thoughts about the game itself:**

- Importance of time, especially during the finish, meta changes and converges only at the end and the best
  implementation wins, almost all people from Top 20 ended up using the same tactic.
- The 'problem' that current meta impacts our evaluation hugely, i.e. an approach that does well right now vs currently
  dominant tactics will do bad job 3 days later when people switch.
  - So maybe it's not worth investing into specific tactics initially and only fine-tune it during later stages?
- Talking about meta and strategy, this went unexpectedly complex very quickly:
    - Attacking is easier than defending, it's also easier to execute properly and yields better results quickly
    - Have a funky tactic and win 70%+ games because you abuse some mechanic or try to create a more general approach
      that, if executed well, technically, could beat everyone?
        - What about CG matchmaking system? Which approach is more valued there? Win 70% vs general population vs win
          80% against top players but only 60% vs general population?
    - But that well-executed general approach would be complex - do I have enough time to do it? Is it possible during a
      10-day contest at all?
