# Prove a game change with playtest evidence

## Write the acceptance criteria before touching the build

- List the criteria the change must prove, split by logic, integration, visual feel, interface and data, in the words a player would use.

- Name the critical path the playtest will walk, from entry to the changed feature and back, before the run starts.

- Record which account, character and starting position the playtest uses, and keep test credentials in the session so a retest does not fail as a process error.

## Run the automated checks and read the whole log

- Run the project test suite with `muse.exec` and write its output to a log file in the project scratch folder.

- Read the complete failure list from that log file before stating any result, because the exit code of a piped command belongs to the last command in the pipe and an empty output proves nothing.

- Report the exact pass and fail counts from the log, group the failures by name, and separate test premise errors from code errors with the reason for each call.

- Treat a check that did not run as NOT RUN, which yields NOT ASSESSED, and never report it as a pass or as a failure.

## Play the real build in a real browser

- Delegate the playtest to `browser.browse` on the exact build that will ship or is already live, with a self contained assignment that names the steps, the stop conditions and the verbatim texts to capture.

- Walk the critical path using only the guidance a player has, such as in game arrows, signs and quest text, when the change is about guidance or navigation.

- Capture screenshots at the moments that prove each visual or interface criterion, including the moment before and after the state change the feature is about.

- Record the first five minutes honestly, covering what worked, pain points, confusion points and bugs in the order they happened.

## Judge the evidence before closing the change

- Check every retained screenshot exists, shows the screen the criterion is about and is dated after the last code change it proves, because evidence older than its code is potentially stale.

- Refuse to close a visual or interface criterion on a written description alone, because a description is an assertion and a screenshot is evidence.

- Close the change only when automated counts, playtest steps and retained evidence agree, and name any criterion left unverified as a debt with its reason.

## Available connectors

- Use `muse.connector_search` to find other connectors and `muse.skill_search` to find related skills.

- If nothing here fits, look on the web for a maintained API or MCP server and set it up with [Custom Connectors and MCPs](/opt/muse/skills/custom-connector-setup/SKILL.md), or build a custom connector.

## Alternatives for better results

- Run the sibling skill `real_browser_playtest_gate` when the only question is whether a playable build may be sent, and keep this skill for the full evidence pack around a change.

- Retest from a harder starting state than the happy path, such as a saved position lost mid map, when a guidance fix claims to recover lost players.
