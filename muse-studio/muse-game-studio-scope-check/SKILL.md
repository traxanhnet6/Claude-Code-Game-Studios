# Check a game batch against its original scope

## Find the original plan and the current state

- Locate the baseline for the work, meaning the user order, the queue item or the design note that enumerated what would be built, and list its items one by one.

- Read the current state from the real files, commits and queue marks, and list what exists now in the same units as the baseline.

- Stop and say which side is unreadable when either side cannot be read, because comparing a real baseline against a guess produces a number that means nothing.

## Compare and quantify

- List scope additions that were built but never planned, and scope removals that were planned but dropped, each in one line with its cost.

- Compute the net change as a percentage of the baseline item count only when the baseline enumerates real items and the current state was fully read.

- Treat additions without matching cuts or an extended timeline as creep, while still naming additions that turned out to be discovered requirements.

## Give the verdict

- Return PASS when the net change is at most 10 percent, CONCERNS between 10 and 25 percent, and FAIL above 25 percent, with FAIL above 50 percent meaning stop and replan before more building.

- Return NOT ASSESSED instead of any percentage when the baseline document exists but enumerates no items, when the current state cannot be determined, or when the denominator would be zero for any other reason.

- Rank NOT ASSESSED above PASS and below CONCERNS and FAIL, because a comparison that never happened has not shown the work is on track, while measured creep is more actionable than an unmeasurable baseline.

- End a NOT ASSESSED verdict with what would make the work assessable, and do not offer a rerun against the same inputs.

- Recommend cuts that preserve the core player experience over nice to have items, and name the two or three additions with the best cut ratio when the verdict is CONCERNS.

## Available connectors

- Use `muse.connector_search` to find other connectors and `muse.skill_search` to find related skills.

- If nothing here fits, look on the web for a maintained API or MCP server and set it up with [Custom Connectors and MCPs](/opt/muse/skills/custom-connector-setup/SKILL.md), or build a custom connector.

## Alternatives for better results

- Run this check before a batch starts when the user order is one short sentence, by writing the enumerated baseline yourself from the order and the project documents, so the end of the batch has something real to compare against.
