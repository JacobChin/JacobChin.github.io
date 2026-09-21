---
layout: post
title: "What Would the Most Productive Offensive Lineup Look Like?"
description: "A research-based framework for simulating baseball lineups, testing nine copies of one hitter, and building the best nine-player offense while accounting for baserunning."
author: Jacob Chin
note: "003"
topics: "Baseball · Simulation · Lineup Optimization"
read_time: "26 min read"
display_date: "September 2026"
permalink: /articles/optimizing-offensive-lineups/
---

## The Question

What would happen if one hitter occupied all nine positions in a batting order?

Would the best version be built around the player with the most home-run power? Would an elite contact hitter create longer innings and eventually score more runs? Or would the best nine-copy lineup belong to a hitter who combines on-base ability, power, and enough speed to create value after reaching base?

That is the first question I want to answer.

The second is more realistic and more difficult:

> **Working question**  
> Using the 2025 pool of qualified Major League hitters, which combination of nine unique players—and which batting order—would produce the most runs in a neutral offensive environment?

The roster would not need to field a defense. There would be no catcher requirement, no positional restrictions, and no concern about salary or roster construction. This is strictly an offensive thought experiment.

However, *offense* cannot mean batting statistics alone. A hitter continues affecting the inning after reaching base. He may steal second, take third on a single, score from first on a double, advance on a fly ball, avoid a force out, or turn a potential double play into one out. He may also run into an out and end a promising inning.

Speed and baserunning therefore need to be part of the question—not added as a footnote after the lineup has already been selected.

This article does not claim to have found the winning lineup. It establishes what previous simulations have done, what their internal logic included, where they simplified the game, and what a more complete simulation would need before its answer should be trusted.

## What Current Research Says

Baseball lineup simulation has a long history. Some models were designed to evaluate one hitter in isolation. Others compared batting orders for a fixed roster. More ambitious models selected players, optimized in-game strategy, or estimated the interaction between batting and baserunning.

These methods should not be grouped together simply because they all involve probabilities.

A model can use a mathematically exact Markov-chain calculation while relying on unrealistic runner-advancement rules. Another can use millions of Monte Carlo games but repeat the same oversimplified assumptions millions of times. Conversely, either method can produce useful results when its transitions are estimated well and match the question being asked.

The important issue is not just *how* the calculation is performed. It is what information enters the calculation.

For every simulation, the relevant questions are:

- Which plate-appearance outcomes are distinguished?
- Does the model remember the identity of each runner?
- How are first-to-third and second-to-home decisions handled?
- Are stolen-base attempts separated from stolen-base success?
- Are double plays, sacrifice flies, wild pitches, errors, and other events included?
- Does the model use observed strategy or choose an optimal strategy?
- Does it maximize average runs, the probability of scoring at least one run, or the probability of winning?
- How does it search the enormous set of possible lineups?
- Does it validate only the mean, or the complete distribution of scoring?

The history of lineup research becomes much clearer when organized around those choices.

### The original nine-copy lineup

The first part of this project has a direct historical precedent.

In 1977, Thomas Cover and Carroll Keilers published an **Offensive Earned-Run Average**, or OERA. The interpretation was exactly the proposed clone-lineup experiment: how many runs per game would a lineup score if the same player occupied all nine positions?

The model represented an inning using 24 possible base-out states: eight combinations of occupied bases at zero, one, or two outs. Each plate appearance became one of six outcomes: an out, walk, single, double, triple, or home run. The hitter's observed frequencies supplied the probability of each outcome.

The calculation was elegant, but its baseball rules were intentionally simple:

- Sacrifices were ignored.
- Errors counted as outs.
- Runners did not advance on outs.
- Every single advanced existing runners two bases.
- Every double scored a runner from first.
- Double plays did not occur.

Those conventions made the result deterministic once the batting event was known. They also removed most of what we now think of as baserunning.

OERA remains important because it formalized the repeated-hitter question and showed why a hitter cannot be evaluated by batting average or slugging percentage alone. Hits and walks interact across an inning. Avoiding outs allows the lineup to turn over, while extra-base hits convert accumulated runners into runs.

It should not, however, be mistaken for a complete description of what nine copies of a modern player would do on the bases.

[Cover and Keilers, 1977](https://isl.stanford.edu/~cover/papers/paper43.pdf){: .source-link }

### Adding stolen bases to the clone model

Later research extended the repeated-hitter framework to include steals.

Kiyoshi Ano's modified OERA incorporated stolen-base effects into a stationary Markov chain. This was an important step because it acknowledged that two hitters with similar batting lines could create different run values after reaching first.

The extension also illustrates a recurring limitation. Adding a stolen-base transition is not the same as building a full baserunning model. Stealing second is only one component of running value. A complete model would also distinguish the decision to attempt a steal from the physical probability of success and include advancement on balls in play, tagging, force plays, pickoffs, and other runner-dependent outcomes.

[Ano, 2001](https://www.sciencedirect.com/science/article/pii/S0096300399002805){: .source-link }

### Early Monte Carlo batting-order experiments

Monte Carlo simulation approaches the problem differently. Instead of solving directly for the expected value of every state, the computer plays the game repeatedly and averages the results.

Richard Freeze used more than 200,000 simulated games in a 1974 study of batting order. The simulation was based on the programmed *Sports Illustrated* baseball game and examined league-average production associated with batting-order positions.

This was an early demonstration that repeated game simulation could compare lineup strategies. It was not yet a player-level model of nine distinct hitters with individualized baserunning. Its inputs were closer to average lineup-slot profiles than to the complete abilities of a specific roster.

That distinction matters. A simulation cannot discover the interaction between a particular leadoff hitter and cleanup hitter if it begins by treating the positions as generic offensive types.

[Freeze, 1974](https://pubsonline.informs.org/doi/abs/10.1287/opre.22.4.728){: .source-link }

### Markov chains with nine different hitters

The clone-lineup calculation becomes more difficult when the nine batting positions contain different players. The probability of the next event now depends on both the base-out state and which hitter is due to bat.

Bukiet, Harold, and Palacios developed a Markov-chain model that allowed non-identical hitters. Batter-specific probabilities could be placed into the transition structure, allowing the model to generate inning and game run distributions, estimate wins, compare trades, and evaluate batting orders.

The framework was flexible enough to accept more detailed runner advancement. In practical applications, however, it often used simplified advancement conventions descended from earlier scoring-index models. Later research reported that those simplified rules understated league scoring by approximately seven percent.

This exposes an important divide between a model's *architecture* and its *implementation*. A framework may be capable of detailed baseball logic without the published version actually using that detail.

[Bukiet, Harold, and Palacios, 1997](https://pubsonline.informs.org/doi/abs/10.1287/opre.45.1.14){: .source-link }

### A richer event model—and the problem of uncertainty

Joel Sokol developed a more detailed Markov model and a fast heuristic for constructing near-optimal lineups.

The batting inputs extended beyond hits, walks, and generic outs. They included hit by pitch, strikeouts, flyouts, groundouts, caught stealing and pickoffs, double plays, sacrifice flies, and stolen bases. League-average rates supplied several rare events, including errors, balks, wild pitches, and passed balls.

Runner advancement on a single from first was divided into three possibilities: stopping at second, reaching third, or being thrown out at third. That was considerably more realistic than assuming every single advances every runner exactly two bases.

The model still did not preserve the complete identity and running ability of every person on base. Most advancement logic came from aggregate rates. Steals of third and home were omitted, and several rare events were excluded.

Sokol's other major contribution was to treat lineup optimization as a problem under uncertainty. A player's observed frequencies are estimates, not permanent true probabilities. Using bootstrap samples, the study showed that the exact best lineup can change across plausible versions of the same player data even when a group of near-optimal lineups remains consistently strong.

That is an essential warning for this project. Reporting one order to three decimal places would create false certainty if several lineups are separated by only a few runs over an entire season.

[Sokol, 2003](https://www2.isye.gatech.edu/~jsokol/boouu.pdf){: .source-link }

### Potential value and realization value

One useful idea in Sokol's work is the distinction between **potential value** and **realization value**.

A hitter creates potential value when he reaches base and gives future hitters something to convert. He realizes value when his own event advances or scores runners already on base.

The same player can do both, but the distinction helps explain why ordering is not reducible to ranking nine hitters from best to worst. A walk with the bases empty creates an opportunity. A home run realizes its own value immediately. A single can do either depending on who is on base and how far that runner advances.

This framework also provides a more useful version of the contact-versus-power discussion. The issue is not whether a lineup needs a ceremonial "contact hitter" and "power hitter." It is whether the nine selected players create enough opportunities, preserve enough outs, and convert enough of those opportunities into runs.

### Search methods do not determine baseball realism

Even with a fixed group of nine players, there are 362,880 possible batting orders. If the model may also choose nine hitters from the entire pool of qualified players, the problem becomes much larger.

Researchers have used several methods to manage that search:

- **Exhaustive enumeration** evaluates every permitted order and guarantees the best answer under the model, but becomes expensive when player selection is also open.
- **Rules and heuristics** construct a strong lineup using baseball-informed shortcuts, sacrificing a guarantee of perfection for speed.
- **Random search** evaluates a sample of possible lineups and establishes a useful baseline.
- **Metropolis–Hastings and simulated annealing** propose changes—often swapping two hitters—and sometimes retain worse intermediate lineups to escape local optima.
- **Genetic algorithms** retain strong candidates and create new lineups through swaps or recombination.
- **Dynamic programming** solves recursively for the best decision when the complete state and available actions can be represented.

Schorsch and Valera, for example, combined a 24-state offensive model with a Metropolis–Hastings search over batting orders. Their plate-appearance outcomes included home runs, triples, doubles, singles, walks, and outs. Runners could sometimes take an extra base, but the probability did not depend on who the runner was. The authors identified richer baserunning as a more important improvement than replacing the optimizer.

That is the correct priority. An advanced search method can locate the exact best lineup inside an unrealistic baseball model. It cannot repair the model's transitions.

[Schorsch and Valera, 2018](https://www.researchgate.net/publication/328529782_Baseball_Lineup_Optimization){: .source-link }

### Strategic models answer a different question

Some baseball models optimize decisions rather than just batting order.

Early dynamic-programming work represented stealing, sacrificing, and swinging as offensive actions. Later models expanded the state to include inning, score, lineup position, and game situation. Turocy treated baseball as a zero-sum Markov game in which both teams maximize their probability of winning. Kira and colleagues developed an even larger non-zero-sum framework in which the offense could hit, steal, or bunt while the defense could pitch or issue an intentional walk.

These models can answer questions that an expected-runs lineup simulation cannot. A strategy that maximizes the probability of scoring one run in the bottom of the ninth may differ from the strategy that maximizes average runs over a neutral game. A lineup that maximizes run differential may not be arranged identically to one that maximizes win probability against a particular opponent.

Their state spaces are also enormous. Adding strategic decisions, score, inning, batting order, and the opposing team's choices can create millions of states before player-specific sprint speed or batted-ball geometry is considered.

For the proposed experiment, expected runs should remain the primary objective. Bunting, intentional walks, and score-dependent strategy would answer a broader question than the one posed here.

[Kira et al., 2019](https://orsj.org/wp-content/or-archives50/pdf/e_mag/Vol.62_02_064.pdf){: .source-link }

### Baserunning requires both ability and choice

Ben Baumer's simulation research focused directly on the part of offense that many lineup models compress into fixed transition probabilities.

The work considered stolen bases, taking extra bases on balls in play, tagging, and avoiding double plays. Later work with Jon Terlecky separated how often a runner attempted an extra base from how often he succeeded given an attempt. Bayesian shrinkage helped prevent a runner with only a few opportunities from appearing unrealistically excellent or poor.

This separation is fundamental:

- **Physical ability** affects whether a runner can reach safely.
- **Decision behavior** affects whether he tries.
- **Opportunity** determines whether the choice exists at all.

Sprint speed is therefore not identical to baserunning value. A fast player may make poor decisions or run conservatively. A slower runner may anticipate the play, take an efficient route, and choose opportunities well.

Baumer, Piette, and Null later examined batting and baserunning together. Their simulation showed why baserunning value is contextual. A runner's opportunity to advance depends on the hitters behind him, and the value of gaining a base depends on what those hitters are likely to do next.

This is directly relevant to a nine-copy lineup. Nine copies of a high-on-base hitter create many baserunning opportunities for one another. Nine copies of a home-run-dependent hitter may generate fewer discretionary advancement plays because home runs clear the bases without requiring a running decision.

[Baumer, Piette, and Null, 2012](https://scholarworks.smith.edu/sds_facpubs/40/){: .source-link }

### More realistic simulation still requires decisions about context

Beaudoin developed a simulator using batter and pitcher statistics, nine possible plate-appearance outcomes, and runner-advancement probabilities estimated from a large dataset. The model could study player ability, stolen-base and bunt strategies, and lineup order.

Including the pitcher makes the simulated plate appearance more realistic, but it introduces another choice. Should a theoretical lineup be judged against a league-average opponent, the actual schedule each hitter faced, a fixed distribution of left- and right-handed pitchers, or a sequence of specific pitchers?

There is no context-free answer. A neutral comparison requires the same opponent environment for every lineup. Otherwise, differences in simulated scoring could reflect the pitchers assigned to each candidate rather than the quality of the offense.

[Beaudoin, 2013](https://www.degruyterbrill.com/journal/key/jqas/9/3/html){: .source-link }

### Recent simulations are getting closer to the proposed question

A recent project by Evan Schaeffer used a 24-state Monte Carlo framework to optimize Major League lineups. Its public code and data documentation describe player probabilities for strikeouts, walks, singles, doubles, triples, home runs, groundouts, flyouts, and lineouts, with separate estimates against left- and right-handed pitchers.

The simulator also included stolen-base attempts, caught stealing, double plays, wild pitches, passed balls, errors, and a simplified bullpen. It compared lineups ordered by wRC+, a two-dimensional potential-versus-realization method, random permutations, cloned hitters, and synthetic contact and power rosters.

This is unusually close to the proposed project. It also reveals how much depends on the transition layer. Many runner movements are governed by fixed probabilities rather than the identity of the specific runner. The presence of a stolen-base rule does not mean a fast and slow runner are fully distinguished in every advancement situation.

[Schaeffer, 2025](https://repository.lib.ncsu.edu/items/11c82287-452b-409a-89c6-015c99d889e5){: .source-link }

[Schaeffer simulation data and code](https://datadryad.org/dataset/doi:10.5061/dryad.s4mw6m9kf){: .source-link }

### Speed-stratified advancement is the clearest modern direction

Surya Tallavarjula's 2026 offensive simulation addresses runner identity more directly.

The model estimates each hitter's probabilities of singles, doubles, triples, home runs, walks, hit by pitch, strikeouts, flyouts, and groundouts from Retrosheet data. It then places runners into five sprint-speed groups and estimates advancement matrices for those groups. The specific runner's speed is interpolated within the relevant situation.

Runner speed affects more than stolen bases. The model applies it to advancement on balls in play and to double-play probabilities. Stolen-base and caught-stealing estimates are shrunk toward the rate of the player's speed group, which reduces the influence of small samples. Steals of both second and third are represented.

The study also validates more than average runs. Team and player results are compared using error, bias, correlation, and agreement measures, while complete scoring distributions are examined with distributional statistics. Its lineup optimization uses a genetic-style local search, more disruptive swaps early in the search, smaller adjacent changes later, cached estimates, and extensive final simulations with uncertainty intervals.

Important pieces remain outside the model. The example does not fully condition every event on the pitcher, defense, ball trajectory, fielder positioning, fielder arm, lead size, jump quality, or coaching aggressiveness. Some of those effects are absorbed into historical rates rather than generated explicitly.

Still, the basic direction is right: once a player reaches base, the simulation must remember who he is.

[Tallavarjula, 2026](https://journals.sagepub.com/doi/10.1177/22150218251410737){: .source-link }

### What Statcast adds to the baserunning question

Statcast's baserunning framework reinforces the difference between speed and complete running value.

For extra-base opportunities, MLB's model considers factors including the runner's speed and starting position, the outfielder's arm strength, and the distances between the runner, ball, fielder, and relevant base. Each opportunity is classified by whether the runner attempted to advance and whether he was safe or out.

Stolen-base value is evaluated separately using information about the runner, pitcher, and catcher. The public Baserunning Run Value leaderboard combines value from stolen bases and advancement on balls in play.

A public lineup simulation will not have every internal feature used by Statcast. But its conceptual structure should be preserved: opportunity, attempt, and success are different events, and the runner is only one part of the play.

[MLB Statcast: Baserunning](https://www.mlb.com/glossary/statcast/baserunning){: .source-link }

[MLB Statcast: Sprint Speed](https://www.mlb.com/glossary/statcast/sprint-speed){: .source-link }

### What the methods collectively show

The literature does not support one universal answer about contact, power, speed, or lineup order. It does support several methodological conclusions:

- A repeated-hitter lineup is a useful measure of complete offensive interaction, not just individual rate statistics.
- Avoiding outs and producing extra bases interact nonlinearly across an inning.
- The precise best batting order is often less stable than a group of near-optimal orders.
- Baserunning value depends on both the runner and the hitters surrounding him.
- A model that tracks occupied bases but forgets runner identity cannot fully account for speed.
- Search algorithms determine how efficiently the model finds a lineup; transition rules determine what kind of baseball it is optimizing.
- Mean runs alone are insufficient validation. The simulated frequency of scoreless innings, big innings, and complete game totals should also resemble real baseball.

These findings shape the proposed study.

## A Better Study

The study should be divided into two experiments using the same offensive engine.

The first would allow duplicated players and evaluate every qualified 2025 hitter as a nine-copy lineup. The second would require nine unique hitters and jointly optimize both player selection and batting order.

Both experiments should use a neutral environment so that every candidate faces the same assumptions.

### Player pool and objective

The player pool would contain all hitters who qualified for the 2025 Major League batting title. Restricting the sample to qualified hitters reduces the most severe small-sample problems and makes the initial comparison reproducible.

This restriction does not imply that the true best offensive roster could never include a part-time player. It defines the scope of this first experiment.

The primary objective would be expected runs per 27 outs. This avoids complications caused by home teams sometimes batting only eight innings or skipping the bottom of the ninth. Full nine-inning games would still be simulated to examine the distribution of team scoring.

Secondary results would include:

- Runs per game
- Probability of scoring zero, one, or multiple runs in an inning
- Probability of scoring at least three, five, or ten runs in a game
- Plate appearances per game
- Runners left on base
- Outs made on the bases
- Runs attributable to steals and other advancement
- Double plays created or avoided

The best lineup by average runs may not have the same scoring distribution as the runner-up. One may produce runs more consistently while another creates more extreme high-scoring games.

### The offensive state

The minimum state would include:

- Number of outs
- Identity of the runners on first, second, and third
- Batter due to hit
- Current position in the batting order

The identity requirement is the largest departure from a basic 24-state model. First base occupied by an elite runner is not the same state as first base occupied by a slow runner, even though both appear identical in a conventional base-out table.

For a neutral run-production model, score, inning, and opposing lineup do not need to change offensive decisions. They can be added for bookkeeping and distributional validation without controlling strategy.

### Plate-appearance outcomes

Each hitter would receive a probability distribution for mutually exclusive offensive events. At minimum, the model should distinguish:

- Unintentional walk
- Hit by pitch
- Strikeout
- Single
- Double
- Triple
- Home run
- Ground-ball out
- Air out
- Double-play opportunity or outcome
- Reached on error
- Fielder's choice
- Sacrifice fly opportunity

Separating groundouts from air outs is necessary because their runner consequences differ. Treating every out as one event would eliminate double plays, force advancement, tagging, and sacrifice flies.

The probabilities should be estimated from 2025 event-level data, with shrinkage toward appropriate league averages. Qualified hitters have substantial samples, but triples, steals of third, advancement outs, and several other events remain sparse.

A neutral version could apply the 2025 league distribution of left- and right-handed pitching to every lineup. A more advanced version could estimate hitter outcomes against standardized pitcher-quality distributions. The same opponent environment must be used for all candidates.

### Avoiding double counting

Player speed already influences observed batting statistics.

A fast hitter may beat out more infield ground balls, turn hits into doubles or triples, and avoid some double plays. If a simulation begins with his observed single, triple, and grounded-into-double-play rates, those speed effects are already partially embedded in the plate-appearance probabilities.

The model should not then award an additional speed adjustment to the same event.

There are two defensible approaches:

1. **Observed-outcome approach:** Use each hitter's actual event rates, then apply player-specific speed only to events occurring after the batter has reached base. Grounded-into-double-play rate remains part of the batter's observed outcome distribution.
2. **Generative approach:** Begin with batted-ball type and location, then generate infield hits, extra-base hits, and double plays using batter speed, runner speed, defensive context, and ball characteristics.

The second approach is more complete but requires much more data and modeling. The first is appropriate for an initial retrospective study as long as its boundary is stated clearly.

### The baserunning layer

The model should separate four components.

**Opportunity** determines whether advancement is possible. Examples include a runner on first when a single reaches the outfield or a runner on second with fewer than two outs when a fly ball is caught.

**Attempt probability** estimates whether the runner tries to take the additional base. It should depend on the runner's historical aggressiveness, speed, the number of outs, and available information about the play.

**Success probability** estimates whether the runner reaches safely given an attempt. It should depend on runner ability and, where public data allow, the type and location of the batted ball and the fielder involved.

**Run consequence** is not assigned manually. It emerges from the new base-out state and what the subsequent hitters do.

The simulation should include, at minimum:

- Stolen-base attempts at second and third
- Caught stealing and pickoffs
- First-to-third advancement on singles
- Second-to-home advancement on singles
- First-to-home advancement on doubles
- Tagging from second or third on air outs
- Advancement and outs on ground balls
- Batter and runner effects on double plays
- Wild pitches and passed balls at league-average rates

Rare events such as triple plays, steals of home, catcher's interference, and runners being struck by batted balls could be excluded initially, documented, and tested for materiality.

### Observed running versus optimal running

Two baserunning policies should be reported.

The first would preserve each player's observed 2025 attempt tendencies. This answers a retrospective question: how would these hitters have performed together if they continued making decisions like the ones observed during the season?

The second would hold physical success probabilities fixed but choose the action with the highest expected run value in the current state. This answers a counterfactual question: what could the lineup produce if every runner made the run-maximizing decision?

The difference between the two is decision value. It prevents a player's physical speed and strategic aggressiveness from being collapsed into one rating.

### Experiment 1: nine copies of one hitter

Every qualified hitter would be placed into all nine batting positions and simulated under identical conditions.

The primary ranking would compare expected runs per 27 outs. The analysis would also report:

- Batting-only production with neutral league-average running
- Production with the player's own baserunning profile
- Production with optimal baserunning decisions
- The change created by removing home runs
- The change created by replacing the player's running with league-average running

These controlled versions would show *why* the leading clone wins.

A hitter could rank first because he almost never makes outs, because he frequently clears the bases, because he combines both skills, or because his running creates extra value in the large number of opportunities generated by nine copies of himself.

### Experiment 2: nine unique hitters

The unrestricted experiment would choose nine different players and arrange them in an order.

This is both a selection problem and a sequencing problem. Choosing the nine highest individual clone scores would not necessarily produce the best mixed lineup. Clone value measures how a player interacts with copies of himself. A unique-player lineup may benefit from complementary profiles.

The search should occur in stages:

1. Use individual and pairwise results to create a broad candidate set.
2. Generate thousands of plausible nine-player rosters.
3. Optimize the order within each roster using swaps and larger lineup changes.
4. Allow occasional worse moves early in the search to avoid local optima.
5. Re-simulate the strongest candidates with much larger samples.
6. Compare finalists using common random-number streams so that identical random circumstances are applied to competing lineups.
7. Bootstrap player probabilities to determine whether the apparent winner remains strong under sampling uncertainty.

For the final candidates, all 362,880 orders could be evaluated with a faster expected-value engine or screened before large Monte Carlo confirmation.

The reported result should include a *near-optimal set*, not only one winner. If several lineups differ by less than the uncertainty interval, the honest conclusion is that the data do not identify one definitive order.

### Contact, power, and mixed-lineup comparisons

The contact-versus-power question must be defined before it is tested.

A "contact lineup" should not simply mean the nine players with the highest batting averages. Batting average combines contact, batted-ball quality, speed, and luck. A more defensible contact classification would emphasize strikeout avoidance and in-zone or overall contact rate while retaining a minimum standard of on-base ability.

A "power lineup" should emphasize isolated power, extra-base-hit rate, barrel rate, or expected slugging rather than raw home-run total, which depends on playing time.

The study should compare:

- The unrestricted optimized lineup
- A contact-restricted optimized lineup
- A power-restricted optimized lineup
- An on-base-restricted optimized lineup
- The nine best clone hitters
- A conventional lineup ordered by an overall statistic such as wRC+
- Thousands of random qualified-hitter lineups

Each restricted roster must still have its batting order optimized. Otherwise, the comparison would confound roster type with poor sequencing.

The categories should also be tested at several thresholds. A conclusion that changes when "power hitter" moves from the top 20 percent to the top 25 percent is not a robust conclusion.

### Validation

Before optimizing hypothetical lineups, the engine should reproduce known 2025 baseball.

Actual team rosters and batting orders would be simulated using the same event and advancement logic. The model should be compared with observed team results for:

- Runs per game
- Plate appearances per game
- Singles, doubles, triples, and home runs
- Walk and strikeout rates
- Stolen-base attempts and success
- Double plays
- Outs on the bases
- Runners left on base
- The distribution of runs per inning and per game

Agreement in league-average runs is not enough. A model could reach the correct mean by producing too many scoreless innings and too many extreme innings. The shape of the distribution matters.

Sensitivity tests should then remove or simplify one component at a time:

- Replace all baserunners with league-average runners.
- Remove stolen bases.
- Replace player-specific advancement with fixed league rates.
- Use deterministic advancement like the original OERA.
- Remove handedness splits.
- Replace detailed outs with one generic out.

The changes in rankings and run estimates would reveal which assumptions materially affect the answer.

## My Hypothesis

### H1: The best clone will have a complete offensive profile

I do not expect the best nine-copy lineup to belong automatically to the hitter with the most home runs, the highest batting average, or the lowest strikeout rate.

I expect it to belong to a hitter who combines elite on-base ability with substantial extra-base damage.

Nine copies of a pure slugger may strand too many opportunities if the hitter also makes outs frequently. Nine copies of a pure contact hitter may extend innings without converting enough runners. Walk-heavy players may repeatedly fill the bases but depend on later events to move everyone home.

The leading clone should be a hitter who creates potential value and realizes it within the same offensive profile.

### H2: The unrestricted unique-player lineup will beat either pure archetype

I suspect the best nine-player lineup will contain a mixture of skills rather than nine players selected from one narrow offensive category.

That does not mean the optimizer will intentionally choose one stereotypical leadoff hitter, one bat-control hitter, and one cleanup hitter. Traditional roles should not be imposed on the result.

The predicted mixture may instead contain several players who are individually well-rounded, with variation at the margins: some especially effective at avoiding outs, some especially effective at generating extra-base damage, and some who add running value without sacrificing too much hitting.

The important test is whether unrestricted optimization consistently selects a more varied set of profiles than the contact- or power-restricted experiments.

### H3: Baserunning will matter most among otherwise close choices

Batting will probably determine most of the separation between strong and weak offensive candidates. An elite runner cannot compensate for making far more outs or producing far less damage than the hitters he replaces.

I expect baserunning to become most important when the batting choices are already close.

It may also matter more in high-on-base lineups. More runners and longer innings create more opportunities to steal, take an extra base, tag, avoid a double play, or make a damaging out. The same running ability can therefore have different value depending on the eight hitters surrounding it.

I expect player-specific advancement to change some roster and ordering decisions even if it does not overturn the offensive hierarchy.

### H4: A mixed lineup is plausible, but the model should be allowed to reject it

My prior belief is that a combination of on-base ability, contact, power, and baserunning will produce the most runs.

That belief should not be encoded as a roster-building rule.

If the unrestricted optimizer selects nine power-heavy hitters, that is evidence against the original expectation. If nine elite contact hitters win, that result should also be accepted. The purpose of the simulation is not to construct a numerical defense of a preferred baseball philosophy.

The model should define the environment, represent the relevant events, validate its behavior, and allow the lineup composition to emerge.

> **Predicted pattern**  
> The best clone should combine on-base ability and power. The best unique-player lineup should favor complete hitters while using complementary differences in power, contact, and baserunning. Speed should influence close selections and sequencing rather than substitute for elite batting.

## Conclusion

The question "What is the best offensive lineup?" sounds simpler than it is.

The original OERA framework showed how to evaluate a lineup containing nine copies of one hitter. Later Markov and Monte Carlo models allowed different hitters, more plate-appearance outcomes, faster lineup searches, strategic decisions, and uncertainty analysis. Baserunning research then showed that reaching base does not end a player's offensive contribution—and that speed, judgment, opportunity, and success should not be treated as the same thing.

The history also shows how easily precision can exceed realism.

A simulation may evaluate hundreds of thousands of lineups while assuming that every runner advances identically. It may include stolen bases while ignoring first-to-third decisions. It may identify one order as "optimal" even though several alternatives are statistically indistinguishable. It may reproduce average league scoring while generating the wrong kinds of innings.

A stronger model would remember the identity of every runner, separate opportunities from decisions and outcomes, use the same neutral environment for every lineup, and validate both average scoring and its distribution.

Only then should it answer the two central questions:

1. Which 2025 qualified hitter would produce the most runs if he occupied all nine lineup positions?
2. Which nine unique hitters, in which order, would produce the most runs together?

The comparison between contact and power should emerge from those experiments. It should not be decided by labeling players in advance or assuming that baseball requires one particular mixture.

My expectation is that the optimum will reward hitters who preserve outs and create damage, with baserunning separating some of the closest candidates. But the most valuable result may not be the name at the top of the ranking.

It may be understanding *why* that lineup wins—and which assumptions cause the answer to change.

> The best lineup is not merely the collection of the nine best batting lines. It is the combination of hitters, runners, and sequence that creates the greatest number of runs before making 27 outs.

## Reading List

1. [Cover and Keilers — An Offensive Earned-Run Average for Baseball](https://isl.stanford.edu/~cover/papers/paper43.pdf)
2. [Freeze — An Analysis of Baseball Batting Order by Monte Carlo Simulation](https://pubsonline.informs.org/doi/abs/10.1287/opre.22.4.728)
3. [Bukiet, Harold, and Palacios — A Markov Chain Approach to Baseball](https://pubsonline.informs.org/doi/abs/10.1287/opre.45.1.14)
4. [Ano — Modified OERA with Steal Effect](https://www.sciencedirect.com/science/article/pii/S0096300399002805)
5. [Sokol — A Robust Heuristic for Batting Order Optimization Under Uncertainty](https://www2.isye.gatech.edu/~jsokol/boouu.pdf)
6. [Baumer — Using Simulation to Estimate the Impact of Baserunning Ability in Baseball](https://www.degruyterbrill.com/document/doi/10.2202/1559-0410.1174/html)
7. [Baumer and Terlecky — Improved Estimates for the Impact of Baserunning in Baseball](https://www.researchgate.net/publication/265059918_Improved_Estimates_for_the_Impact_of_Baserunning_in_Baseball)
8. [Baumer, Piette, and Null — Parsing the Relationship Between Baserunning and Batting Abilities Within Lineups](https://scholarworks.smith.edu/sds_facpubs/40/)
9. [Beaudoin — Various Applications to a More Realistic Baseball Simulator](https://www.degruyterbrill.com/journal/key/jqas/9/3/html)
10. [Schorsch and Valera — Baseball Lineup Optimization](https://www.researchgate.net/publication/328529782_Baseball_Lineup_Optimization)
11. [Kira et al. — Dynamic Programming and Game-Theoretic Baseball Models](https://orsj.org/wp-content/or-archives50/pdf/e_mag/Vol.62_02_064.pdf)
12. [Rublewski — Optimizing Batting Lineups Through Monte Carlo Simulation](https://digitalcommons.lib.uconn.edu/srhonors_theses/962/)
13. [Schaeffer — Using Simulation to Optimize Batting Lineups in Major League Baseball](https://repository.lib.ncsu.edu/items/11c82287-452b-409a-89c6-015c99d889e5)
14. [Schaeffer — Public Simulation Data and Code](https://datadryad.org/dataset/doi:10.5061/dryad.s4mw6m9kf)
15. [Tallavarjula — A Monte Carlo Simulation of Baseball Offense With Speed-Stratified Baserunning and Distributional Validation](https://journals.sagepub.com/doi/10.1177/22150218251410737)
16. [MLB Statcast — Baserunning](https://www.mlb.com/glossary/statcast/baserunning)
17. [MLB Statcast — Sprint Speed](https://www.mlb.com/glossary/statcast/sprint-speed)
18. [Chadwick Bureau — Retrosheet Event Fields](https://github.com/chadwickbureau/chadwick/blob/master/doc/cwevent.rst)

*This article is an analytical framework, not a completed simulation. Proposed lineup results and relationships are identified as hypotheses unless directly supported by the cited research.*
