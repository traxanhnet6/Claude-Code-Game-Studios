# Check game balance against stated targets

## Gather values and their targets first

- Name the balance domain for this run, choosing combat, economy, progression or loot, and refuse to audit a domain whose data files you cannot read.

- Read the value files and the design or economy document that governs them, and pair every value with its stated target range before judging any of them.

- List a value with no stated target anywhere as needing attention with the note that it has no stated range and was not judged, because an invented range would fabricate the verdict.

## Analyse the domain

- Compare every value with its target and record each value outside its range as an outlier with both numbers shown.

- For combat, compute damage per second and time to kill at each power tier, look for options that dominate all others, and check whether defensive builds can become unkillable.

- For economy, map every faucet and sink with its flow rate, project accumulation over real play time, look for infinite resource loops, and check that sinks scale with generation.

- For progression, plot the experience and power curves, look for dead zones with no meaningful progress and for sudden power spikes, and check that content gates meet the player at the intended power.

- For loot, compute the expected time to acquire each rarity tier, check pity or guarantee math, and flag any drop that is strictly useless at the stage where it falls.

## Report and run the fix and verify cycle

- Give one health verdict per domain, chosen from healthy, concerns or critical issues, with the outliers and degenerate strategies listed above the recommendations.

- Change a number only through the economy or design document first, then the data, so the document stays the single source other teams read.

- Rerun the same analysis after a fix and show the outlier list shrinking, rather than declaring the fix good from the change alone.

- When a test disagrees with a tuned value, decide whether the test premise or the value is wrong and fix that side, and never loosen balance or a test threshold just to turn a report green.

## Available connectors

- Use `muse.connector_search` to find other connectors and `muse.skill_search` to find related skills.

- If nothing here fits, look on the web for a maintained API or MCP server and set it up with [Custom Connectors and MCPs](/opt/muse/skills/custom-connector-setup/SKILL.md), or build a custom connector.

## Alternatives for better results

- Simulate long grinds with a script over the real data files when a curve only misbehaves after hours of play, and keep the script with the project for the next audit.

- Pair this check with the `muse_game_studio_scope_check` skill when a balance problem is really an unfinished content problem wearing numbers.
