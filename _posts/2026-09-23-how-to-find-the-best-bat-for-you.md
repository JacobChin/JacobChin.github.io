---
layout: post
title: "How Do You Know Which Bat Is Best for You?"
description: "What existing bat research can—and cannot—tell us about fitting a hitter for the best tradeoff between exit velocity and barrel control."
author: Jacob Chin
note: "004"
hero: bat-fitting
math: true
topics: "Baseball · Bat Fitting · Physics"
read_time: "22 min read"
display_date: "September 2026"
permalink: /articles/how-to-find-the-best-bat-for-you/
---

## The Question

In [“Is Bat Speed Missing Something?”](https://jacobchin.github.io/Baseball-Projects/bat-speed-moi/), I argued that a public bat-speed reading is not an equipment-neutral description of a hitter. It tells us how fast a point on a particular bat moved, but not how difficult that bat was to accelerate or how its mass distribution affected the collision.

That analysis used Statcast data to study the relationship between bat speed and top-end exit velocity. It also showed where public data stop helping. Without measuring the bat itself—its length, mass, balance point, moment of inertia, and barrel properties—an unusual exit velocity cannot be assigned to equipment rather than impact quality, swing mechanics, or measurement noise.

This article starts where that one ended: **what would an evidence-based bat-fitting process actually need to measure?**

The goal is to turn a broad critique of bat-speed leaderboards into an individualized fitting question, then use the existing literature to design the study that could answer it.

For readers interested in the exploratory measurement attempt that preceded this review, I documented the three-bat pendulum and tee test in a separate [technical note (PDF)](https://jacobchin.github.io/Baseball-Projects/bat-speed-moi/exploratory-three-bat-moi-swing-speed-pilot.pdf){: .source-link }. Because those measurements were not laboratory-grade, I do not use that pilot as evidence for the hypothesis developed here.

> **Working question**
>
> How can an individual hitter identify the bat that provides the best tradeoff between exit velocity and barrel control?

For this article, **barrel control** means the ability to deliver the intended part of the barrel to the intended place at the intended time, especially when pitch speed and location vary. It is not simply how maneuverable a bat feels. It has to appear in measurable outcomes such as impact-location dispersion, timing error, swing-and-miss rate, foul rate, and squared-up-contact rate.

“Best” also needs a stated objective. Some hitters may prioritize two-strike adjustability, plate coverage, maximum peak exit velocity, durability, comfort, or another goal. This article makes one simplifying assumption: **most hitters being fitted for a bat want to produce the strongest possible contact without giving up the barrel control required to create that contact consistently.** The goal is therefore not maximum exit velocity or maximum control in isolation. It is the best tradeoff between them.

The useful version of the fitting question is not “heavy or light?” It is how bat MOI, angular speed, impact radius, collision efficiency, time to contact, and barrel accuracy interact for one hitter.

I also want to separate three targets that are often blended together:

- The bat that produces the highest bat speed.
- The bat that produces the best batted balls when contact is made.
- The bat that can be delivered accurately and adjusted under representative pitch variation.

Those do not have to be the same bat. The highest-exit-velocity bat is not automatically the best game bat if it widens the hitter's impact-location or timing errors. The easiest bat to control is not automatically best if its strongest contact is substantially weaker. This research review and proposed study are intended as a companion to the earlier Statcast article, not a replacement for it.

## What Current Research Says

### Weight and swing weight answer different questions

Total mass tells us how much matter is in the bat. MOI tells us how that mass resists rotation about a particular axis.

In simplified form,

$$
I = \int r^2\,dm
$$

where \\(I\\) is moment of inertia, \\(dm\\) is a small element of mass, and \\(r\\) is its distance from the axis. Moving the same amount of mass farther from the hands can therefore raise MOI substantially.

This is why the label on the knob is incomplete. A lighter, end-loaded bat can have a higher swing weight than a heavier bat whose mass is concentrated closer to the hands.

Standard laboratory practice commonly measures a bat's MOI about a pivot six inches from the knob. Some swing-speed research instead reports MOI about the knob. Those values should not be compared without converting them to a common axis using the bat's mass and center of mass.

[Dan Russell: Moment of Inertia of Baseball and Softball Bats](https://www.acs.psu.edu/drussell/bats/bat-moi-details.html){: .source-link }

### Lower MOI generally permits more swing speed

The clearest controlled evidence comes from a 2003 field study by Lloyd Smith, Jeff Broker, and Alan Nathan.

The study used specially weighted bats to separate total weight from MOI. One group of bats varied in weight while MOI was held constant. Another varied in MOI while weight was held constant. Fourteen male slow-pitch softball players hit pitched balls, and high-speed video measured bat motion.

The result matters for bat fitting: normalized swing speed was nearly independent of total bat weight when MOI was held constant, but it declined as MOI increased when weight was held constant.

The authors represented the relationship with a power law that can be written as

$$
\omega \propto I^{-n}
$$

where \\(\omega\\) is angular swing speed, \\(I\\) is bat MOI, and \\(n\\) describes how sensitive the hitter's swing speed is to increasing MOI.

The pooled result was approximately \\(n=0.25\\), while the player-level values ranged from about 0.08 to 0.37. A hitter near the low end retained speed relatively well as MOI increased. A hitter near the high end lost speed more quickly.

That range may be more important than the average. It suggests that a universal swing-weight recommendation would ignore meaningful differences among hitters.

The study was performed with slow-pitch softball players, not baseball hitters. Its experimental design is directly relevant, but its exact average exponent should not simply be assigned to every baseball player.

[Smith, Broker, and Nathan, 2003](https://baseball.physics.illinois.edu/SwingSpeed.pdf){: .source-link }

Later work using 19 baseball players hitting machine-pitched balls found an exponent of \\(0.29 \pm 0.04\\) for angular speed versus MOI about the knob. That study also estimated the instantaneous rotation axis near the hands shortly before impact and developed a model in which linear bat speed depends on both rotational speed and the distance from the rotation axis to the impact point.

[Nathan et al., 2011](https://www.acs.psu.edu/drussell/Publications/NathanCrisco-SportsEng.pdf){: .source-link }

### The MOI–speed result has been repeated, but not under one universal protocol

The Smith–Broker–Nathan power law is the most convenient result for this article because it produces a hitter-specific sensitivity term, \\(n\\). It is not the only evidence that bat inertia changes swing speed.

Fleisig and colleagues used three-dimensional motion tracking to study baseball and fast-pitch softball hitters swinging bats with different mass properties. Bat linear velocity was related to MOI in both groups, leading the authors to argue that MOI was more useful than total mass when the goal was to regulate bat velocity.

[Fleisig et al., 2002](https://doi.org/10.1046/j.1460-2687.2002.00096.x){: .source-link }

Koenig and colleagues tried to separate mass, center-of-mass position, and MOI more explicitly. Their first experiment included seven collegiate male baseball players and 13 production or adjustable test implements. Across their studies, swing speed generally decreased as bat inertia increased, but the relationship was not perfectly monotonic. Swings at pitched balls were slower and more variable than tee swings, which the authors connected to the additional decision-making and adjustment required to hit a moving ball.

That variation matters here. A laboratory relationship between MOI and maximum-effort speed does not automatically describe how the hitter will organize a swing when the pitch has to be recognized and intercepted.

[Koenig et al., 2004](https://people.stfx.ca/smackenz/courses/directedstudy/articles/koenig%202004%20the%20influence%20of%20moment%20of%20inertia%20on%20baseball%20and%20softball%20bat%20swing%20speed.pdf){: .source-link }

Smith and Kensrud later conducted a larger slow-pitch field study with 29 right-handed hitters. All five bats used the same 34-inch aluminum shell and were nearly equal in weight; inertia was changed by moving mass between the proximal and distal ends. Hitters faced a live pitcher and swung the bats in randomized order. The fitted power was \\(n=0.21\\) across all five bats and \\(n=0.24\\) after removing the unusually low-inertia bat.

That study is especially relevant to bat fitting because it used matched bats in randomized order and showed that the fitted exponent changed when the unusually low-inertia condition was excluded. It also provides a warning: the power law is a convenient local description, not a complete biomechanical model. It incorrectly predicts unbounded swing speed as bat MOI approaches zero because it omits the inertia of the hitter and the rest of the linked system.

[Smith and Kensrud, 2014](https://baseball.physics.illinois.edu/WSU-SwingSpeed.pdf){: .source-link }

Taken together, these studies establish the direction of the relationship more confidently than they establish one universal exponent. They used baseball and softball hitters, tee and pitched-ball tasks, different bat constructions, different assumed axes, and different definitions of the measured point on the bat. Those differences are not noise to ignore. They are reasons to estimate \\(n\\) for the actual hitter and tested range rather than importing a population average into a fitting decision.

### Mass placement can change swing organization and timing

Endpoint bat speed does not reveal how the hitter produced it.

Laughlin and colleagues compared 30 collegiate baseball hitters swinging a standard bat, a barrel-weighted bat, and a handle-weighted bat against pitched balls. The handle-weighted bat preserved equivalent swing kinematics within the study's equivalence bounds, while the barrel-weighted bat did not. Neither weighted bat preserved equivalence for the timing of all measured bat kinematics and some ground-reaction-force peaks.

This does not show that a handle-weighted bat is better. It shows that adding mass in two different places can alter the swing differently even when both changes make the bat heavier.

[Laughlin et al., 2016](https://pubmed.ncbi.nlm.nih.gov/26836969/){: .source-link }

Crisco, Osvalds, and Rainbow examined 306 swings from 22 male players aged 13–18 using three youth bats with different MOIs. Their inverse-dynamics analysis found that peak force increased with larger bat MOI and was strongly related to bat-tip speed. The force applied through most of the swing was dominated by a component along the bat's long axis, while the applied moment rose sharply only near impact.

The practical lesson is that a swing is not generated by one constant torque acting on a rigid lever. The hitter's forces, hand motion, segment coordination, and late rotational action all contribute. That is another reason a fitted \\(n\\) should be treated as an empirical response, not a complete explanation of the hitter.

[Crisco, Osvalds, and Rainbow, 2018](https://pubmed.ncbi.nlm.nih.gov/29651903/){: .source-link }

### Why more bat speed does not settle the fitting question

Bat speed is one input to batted-ball speed. It is not the only input.

In a one-dimensional description of the collision, the outgoing ball speed depends on the incoming pitch speed, the linear speed of the bat at the impact location, and a collision-efficiency term. That efficiency depends on the bat and ball's elastic properties, impact location, and the bat's inertial properties.

A lower-MOI bat gives the hitter an opportunity to swing faster. At the same time, lowering MOI can reduce the bat's effective resistance during impact. A higher-MOI bat can produce a more effective collision but may cost swing speed. Those effects oppose one another.

“The bat is harder for the ball to slow down” is a useful intuition, but it is not a complete physical model. A real bat is not a rigid point mass. It translates, rotates, bends, vibrates, and contacts the ball at a particular location. Bat construction and the ball-bat coefficient of restitution also matter.

[Dan Russell: Swing Weight of a Bat](https://www.acs.psu.edu/drussell/bats/bat-moi.html){: .source-link }

[Dan Russell: Regulating Bat Performance](https://www.acs.psu.edu/drussell/bats/bat-regulate.html){: .source-link }

The practical implication is modest but important: increasing bat speed by choosing a lower-MOI bat does not guarantee an equal increase in exit velocity. A higher-MOI bat may improve collision effectiveness while making it harder to arrive on time or adjust the barrel. The correct performance tradeoff has to be measured with the hitter and bat together.

### Length changes the speed at the impact point

Bat sensors often report linear barrel speed, while the underlying bat motion includes angular rotation. In the simplest rotational model,

$$
v = \omega r
$$

where \\(v\\) is linear speed at the impact point, \\(\omega\\) is angular velocity, and \\(r\\) is the distance from the rotation axis to that point.

If two bats could be swung with the same angular velocity and contacted the ball at different radii, the longer radius would have the greater linear speed. That is the theoretical appeal of a longer bat whose MOI can be kept manageable.

But *at equal MOI* does not automatically mean *at equal angular velocity*. Length and mass distribution may change the hitter's hand path, posture, timing, achievable torque, impact pattern, and instantaneous rotation axis. A longer radius can also make an equivalent angular error produce a larger spatial miss at the barrel. The possible linear-speed advantage is therefore a design consideration to examine, not a free benefit.

The 2011 baseball study supports including both MOI and impact radius in a swing-speed model. It does not prove that every hitter should use the longest bat that can be built to a target MOI.

### Barrel control does not yet have one accepted measurement

The phrase *barrel control* is common in baseball, but the research literature usually separates it into narrower spatial and temporal outcomes.

One study of 10 college baseball players measured variability in where and when the bat met launched balls while changing how much of the ball's flight the hitter could see. Contact error was separated into deviation along the bat, vertical deviation, and timing. Removing useful trajectory information increased some forms of impact variability. The experiment demonstrates that contact precision depends on the information available to the hitter, not only on the physical swing.

[Katsumata, 2016: Contribution of Visual Information About Ball Trajectory to Baseball Hitting Accuracy](https://pmc.ncbi.nlm.nih.gov/articles/PMC4743964/){: .source-link }

A later experiment examined how mixed pitch types and advance information influenced timing control. It defined timing error from the difference between the observed impact location and an estimated optimal impact location, adjusted for pitch speed. That is useful for this project because it turns “late” or “early” from a visual judgment into a continuous variable.

[Katsumata et al., 2020](https://pmc.ncbi.nlm.nih.gov/articles/PMC7077830/){: .source-link }

Recent computational work combined 18 pitch trajectories from 10 collegiate pitchers with 145 swing trajectories from 29 collegiate hitters. The calculated acceptable timing window averaged about 9.4 milliseconds but ranged from roughly 2.5 to 30.4 milliseconds depending on the swing trajectory. No single swing-path feature determined the window; the side-view path, top-view path, and bat angle at impact interacted.

[Nakashima et al., 2025](https://pmc.ncbi.nlm.nih.gov/articles/PMC11985794/){: .source-link }

These studies provide possible components of barrel control: impact-location error, timing error, their trial-to-trial dispersion, and the size of the acceptable contact window. They do not establish that one metric captures the whole idea. A hitter could be spatially precise but consistently late, make frequent contact away from the bat's best-performing region, or preserve accuracy only when the next pitch is known.

More importantly, these studies did not systematically vary bat MOI while measuring those outcomes. The MOI literature is strongest on swing speed and collision performance. The batting-control literature is strongest on perception, timing, and trajectory. The missing study is the one that joins them.

### Different changes can create the same “lighter” feeling

My earlier article discussed balance point, puck knobs, choking up, and torpedo bats in more depth. For this experiment, the important point is that they are not interchangeable.

Moving the center of mass toward the hands can change how a bat feels, but balance point alone does not determine MOI. Adding a puck knob can pull the balance point toward the grip while still adding a positive amount of MOI about a fixed pivot. Redistributing mass from the barrel toward the knob may reduce MOI. The result depends on what material moved, how far it moved, and where the comparison axis is located.

Choking up changes something else: the position of the hands on the existing bat. Relative to the hands, it generally shortens both the distance to the bat's mass and the distance to the impact point. That can reduce rotational demand while also reducing the radius available to create linear barrel speed. A real swing is not a bat rotating around one stationary hinge, so the size of either effect has to be measured with the hitter.

Torpedo bats illustrate a third option—redistributing barrel mass around a preferred impact region. A 2026 experiment by Alan Nathan, Lloyd Smith, and Daniel Russell tested two standard and two torpedo maple bats with broadly similar length, mass, and MOI. Peak BBCOR was similar across the bats, but the location of peak performance shifted; one torpedo specimen produced a modestly wider high-BBCOR region while the other did not. The difference between the two nominally identical torpedo shapes also showed why the finished bat's actual inertial and vibrational properties matter.

These examples do not establish one superior geometry. They establish why “weight,” “balance,” and “swing weight” cannot substitute for one another in a fitting experiment.

[Nathan, Smith, and Russell, 2026: Studies of the Torpedo Bat](https://baseball.physics.illinois.edu/ISEA2026-Torpedo-v7.pdf){: .source-link }

[MLB, 2026: Juan Soto's puck-knob experiment](https://www.mlb.com/news/juan-soto-switches-to-hockey-puck-knob-bat){: .source-link }

### A bat sensor is useful without being a laboratory reference

Commercial inertial sensors make repeated bat testing accessible, but their outputs should not be treated as interchangeable with high-speed optical tracking.

A validation study compared several commercially available bat sensors with motion capture. The devices generally showed moderate or high correlations for swing speed across players, but all displayed systematic or proportional errors. The authors specifically cautioned that the precision of several devices, including Blast Motion, was not sufficient for detecting small within-player differences reliably.

That distinction shapes the proposed study. Commercial sensors may be useful for accessible screening or repeated practice measurements, but they cannot establish that every small difference between bats represents a true biomechanical change. Optical tracking and direct impact measurements should supply the criterion outcomes, and device-reported acceleration, power, or time-to-contact values should be validated before receiving equal evidentiary weight.

[Nagami et al., 2022](https://pmc.ncbi.nlm.nih.gov/articles/PMC8879135/){: .source-link }

## Theoretical Ideal Study

The existing research determines what the next study must do.

- Because repeated studies show a general MOI–speed relationship but not one universal exponent, the study must estimate \\(n\\) separately for each hitter.
- Because collision efficiency changes with MOI, construction, and impact location, those bat properties must be measured rather than inferred from exit velocity.
- Because pitched-ball tasks are slower and more variable than tee swings, the test must include pitch uncertainty rather than treating maximum-effort tee speed as barrel control.
- Because spatial and temporal contact errors are different, the study must measure both instead of using one subjective control grade.
- Because commercial sensors may not resolve small within-hitter differences, optical tracking and direct impact measurement should provide the criterion measurements.

A useful study would therefore separate MOI, length, and construction instead of comparing three retail bats that vary in all three, then connect those controlled bat properties to both batted-ball speed and barrel control.

### Participants

Recruit a broad sample of hitters across skill levels, strength profiles, body sizes, swing styles, and baseline bat speeds. The sample should be large enough to estimate hitter-specific responses rather than only a pooled average.

Record relevant descriptive variables—height, mass, hand dominance, playing level, grip position, strength measures, and normal game-bat specifications—without assuming in advance that any one of them explains the result.

### Bat conditions

Use matched bats of the same material, construction, barrel performance, grip, and surface finish.

Run two controlled series:

1. **MOI series:** hold length and construction constant while systematically varying MOI through documented mass placement.
2. **Length series:** vary length while matching MOI as closely as engineering permits, then verify the actual MOI, mass, center of mass, and barrel performance of every bat.

A third redistribution series could compare conventional and torpedo-like geometries at matched length, total mass, MOI, and measured collision properties.

The bats should be visually masked where possible and presented in randomized, counterbalanced order. Familiarization swings should occur before data collection. Trial blocks should be short enough to manage fatigue, with rest and repeat sessions used to assess day-to-day reliability.

### Hitting task and measurement

Use a pitching machine to deliver representative pitch speeds and locations, then repeat key conditions with randomized pitch types and locations to test adjustability. The hitter should not know the next condition in advance. Tee swings can establish a low-variability baseline, but they cannot measure the pitch recognition, timing, and spatial adjustment that barrel control requires.

Synchronize:

- Optical bat and body tracking for angular velocity, hand motion, instantaneous rotation axis, and linear speed at the measured impact point.
- A validated launch monitor for exit velocity, launch angle, spray direction, and incoming pitch speed.
- Direct impact-location measurement along and around the barrel, including distance from the intended contact region.
- Bat-specific laboratory measurements of MOI, center of mass, coefficient of restitution or BBCOR where applicable, and vibration behavior.
- Sensor outputs such as time to contact only after comparing them with the synchronized optical record.
- Swing-and-miss, foul, fair-contact, and squared-up-contact rates for every bat condition.
- Timing-error and impact-location dispersion, not only each condition's best swing.

Every swing should retain both the process and the outcome. A high-MOI bat that produces one exceptional exit velocity but a wider spread of misses or off-center impacts may not be the best practical fit. A very low-MOI bat that reaches the ball reliably but produces weaker contact may not be best either.

### Analysis

Estimate \\(n\\) separately for each hitter using the bat-speed and MOI conditions. Then model both batted-ball speed and barrel control as functions of at least:

- Hitter.
- Bat MOI.
- Bat length and measured impact radius.
- Linear and angular bat speed immediately before impact.
- Incoming pitch speed.
- Impact location and contact orientation.
- Bat construction and measured collision efficiency.
- Trial order, session, and fatigue.
- Pitch speed, location, and whether the condition was known or randomized.

Barrel control should remain visible rather than being hidden inside a subjective score. For each bat, the study could report impact-location dispersion, timing dispersion, miss rate, and squared-up-contact rate beside the exit-velocity distribution.

The central output should not be one universal optimum. It should be an individualized **tradeoff frontier** across the tested MOI range. A bat belongs on that frontier when no other tested bat improves exit velocity without worsening barrel control, or improves barrel control without sacrificing exit velocity. If one recommendation is required, the fitter could choose the highest-performing bat that remains within a pre-specified acceptable range of impact and timing error. That decision rule is more transparent than arbitrarily declaring that one mph of exit velocity equals a particular percentage of additional control.

The strongest evidence would be out-of-sample: estimate a hitter's optimal region in one session, then test whether that recommendation improves both batted-ball results and barrel-control outcomes in a later blinded session.

## Limitations

The research reviewed here supports the components of the fitting problem more strongly than it supports the complete framework.

- No cited study directly maps a hitter's MOI sensitivity to that hitter's exit-velocity/barrel-control tradeoff across a controlled series of bats.
- Several of the strongest MOI studies used slow-pitch softball players, youth players, or small collegiate samples. Their exact estimates should not be assigned automatically to other populations.
- The power-law exponent \\(n\\) is a convenient description over a tested MOI range, not a law that should be extrapolated toward unrealistically light or heavy bats.
- *Barrel control* has no single accepted outcome. Impact-location error, timing error, swing-and-miss rate, foul rate, and squared-up contact describe related but different abilities.
- A Pareto frontier can show the available tradeoffs, but recommending one bat still requires a stated decision rule about how much control loss is acceptable for a possible gain in batted-ball speed.
- A pitching-machine study would improve experimental control while remaining less perceptually representative than facing live pitchers with realistic release cues and pitch sequencing.
- Length, total mass, MOI, balance point, barrel geometry, stiffness, and vibration cannot always be changed independently in a physical bat. “Holding everything else constant” may be only approximate.
- Natural wood variation can produce different collision behavior even among bats built to the same dimensions.
- Familiarity, learning, fatigue, and expectations about a bat may affect performance unless conditions are blinded, randomized, and repeated across sessions.
- Commercial sensors can make a study easier to run, but small within-hitter differences require criterion validation.

The framework also assumes that the fitting objective is a tradeoff between exit velocity and barrel control. That is a useful general objective, not a universal definition of the best bat. A particular hitter may reasonably prioritize two-strike adjustability, reach, injury history, league equipment rules, or another constraint.

## My Hypothesis

This article advances one hypothesis:

> **Hitters who retain bat speed as MOI increases—those with a lower MOI-sensitivity exponent \\(n\\)—will achieve their best exit-velocity/barrel-control tradeoff at a higher bat MOI than hitters whose bat speed declines more rapidly.**

This hypothesis does not assume that one MOI is best for every hitter. It predicts a relationship between two individualized measurements: the rate at which a hitter loses bat speed as MOI rises, and the MOI region where that hitter's batted-ball speed and barrel-control outcomes are jointly strongest.

Testing the hypothesis requires estimating \\(n\\) for each hitter and then independently mapping that hitter's batted-ball-speed and barrel-control outcomes across the bat conditions. The evidence would support the hypothesis if lower-\\(n\\) hitters consistently reached their best tradeoff at higher MOIs than higher-\\(n\\) hitters. It would weaken the hypothesis if \\(n\\) did not predict that region.

Bat length, choking up, puck knobs, and barrel mass redistribution remain possible mechanisms or design variables. They are not additional hypotheses in this article.

## Conclusion

Bat weight is an incomplete fitting variable.

The scale cannot tell a hitter how difficult a bat is to rotate. Balance point cannot reconstruct the full mass distribution. Bat speed alone cannot describe the collision. Maximum exit velocity alone cannot describe how often the hitter will deliver the useful part of the barrel on time.

The existing evidence supports several narrower conclusions.

MOI is a stronger description of rotational demand than total weight by itself. Increasing MOI generally reduces swing speed, but hitters differ in how sensitive they are to that increase. Length changes the relationship between angular speed and linear speed at the impact point. Collision effectiveness and impact location can offset—or reverse—the conclusion suggested by bat speed alone. Mass redistribution can change these variables without fitting neatly into “lighter” or “heavier.”

The next step is to test a controlled range of bats while measuring both sides of the fitting problem at the same time: the quality of the resulting contact and the hitter's ability to deliver the barrel accurately under pitch uncertainty.

The eventual fitting question should therefore be more specific than “What weight do you swing?”

It should be:

**How much rotational resistance can you carry while preserving the barrel control required to produce your best batted balls consistently?**
