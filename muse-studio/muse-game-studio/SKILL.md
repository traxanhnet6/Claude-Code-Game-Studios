# Run the Muse game studio

## Treat yourself as the studio, not as a lone coder

- Run game work as a small studio where you hold the producer and technical director seats yourself and delegate specialist work to child agents with written role briefs.

- Convert each Claude Code Game Studios agent into a self contained brief you paste into a `subagent.spawn` call, because Muse has no slash commands, no agent registry and no commit blocking hooks.

- Keep the rigor at minimal by default, because the source framework measured its own heavier process modes and found they produced more documents without producing a better game.

- Raise rigor for one system only when that system carries real risk, such as a save migration, a payment path or a release build, and record the exception in the project notes.

## Pick a role before you delegate

- Read the matching brief in `references/roles/` and paste its duties, output standard and prohibitions into the child agent task, together with the concrete facts of the job.

- Use the creative director brief when two specialist directions conflict or a choice changes the identity of the game.

- Use the art director brief for anything the player sees, and pair it with the `muse_game_studio_art_gate` skill before any art reaches the user.

- Use the QA lead brief to own the test plan, the evidence folder and the release quality verdict for a batch.

- Use the economy designer brief for prices, rewards, drop rates and progression curves, and treat the project economy document as the only source of numbers.

- Use the systems designer brief when a mechanic needs explicit formulas, edge cases and worked values before code exists.

- Use the gameplay programmer brief to implement designed mechanics as data driven code with its own test section.

- Use the UI programmer brief for HUD, panels and screen flow, with phone readability and safe areas checked on real screenshots.

- Use the world builder brief for maps and lore together, so layout, gates, spawns and signs stay consistent with the story bible.

- Use the writer brief for player facing text, with one voice per character and no invented proper names presented as settled.

- Use the Android specialist brief for every APK build, and pair it with the `muse_game_studio_release_gate` skill before a file is handed over.

- Use the release manager brief to run the deploy sequence for web builds on git plus Render and for APK releases.

## Run one work loop

- Start from the user order and restate it as one closable outcome with a named proof, such as a passing test count, a live screenshot or a verified file hash.

- Split the work into independent pieces and spawn the role agents in parallel in one block, each with a self contained brief that names its files, its limits and its prohibitions.

- Keep work that touches the same files in one agent, because parallel writers on one tree corrupt each other and waste the whole batch.

- Verify every returned claim yourself by reading the files, rerunning the checks and looking at the images, because a child report is a claim and not evidence.

- Deploy only a batch that passed every hard gate below, then prove the live build and run the acceptance playtest on the live build itself.

- Report to the user only when an outcome closes, with the proof attached and the honest weakness named in one sentence.

## Hold the image evidence gate

- Close nothing that changes what the player sees until the real game has been run, the result looked at with your own eyes and a screenshot retained as evidence.

- Treat a green automated test count as proof of code logic only, and never as proof of how a screen, a map or an animation looks.

- Compare new art against the user reference images and the project art bible, never against the previous version of the art.

- Label every preview honestly as an in game capture, a render from real game data or a layout mockup, and never present a mockup as game art.

## Hold the harsh art gate

- Fix art that falls short of the reference standard inside the team and regenerate it until it passes, without sending the failing rounds to the user.

- Never ask the user to judge an image you already know is below the standard, and never ask about an ugly image at all.

- Send the user only art that passed your own harshest review, and name its remaining weakness plainly when you send it.

- Hide any feature whose art is unfinished instead of showing a placeholder, an emoji or a flat color block in its place.

## Hold the quiet tree and independent suite gate

- List every agent and scheduled job still writing to the tree before you verify or deploy, and wait until each writer finishes or pauses.

- Snapshot hashes of the files you will ship before the verification run and compare them after, and discard the run when the tree moved during it.

- Rerun the full suite yourself in a separate process and read the complete failure list from the log file, because the exit code of a piped or tailed command belongs to the last command in the pipe and not to the suite.

- Separate test premise errors from code errors when a failure appears, fix the wrong premise in the test, and never loosen game balance or a check to make a claim turn green.

## Hold the live match gate

- Push the verified batch, then fetch the live files and compare their hashes with the local build before you say the deploy landed.

- Treat a file that merely exists on the server as unproven until the running page actually loads it.

- Run the acceptance playtest in a real browser on the live build after the hashes match, walking the critical path the batch touched.

- Send the user a playable link only after the live playtest passes, and say plainly which part remains unverified when one does.

## Hold the token discipline gate

- Write briefs that carry every fact a child agent needs, because a child that has to rediscover context burns the budget twice.

- Prefer one sharp agent with a narrow brief over several overlapping agents, and prefer doing a small job yourself over spawning a team for it.

- Send no progress filler to the user, and let silence mean the work is still running rather than narrating it.

- Record decisions in the project documents and memory as you close them, so the next session starts from facts instead of re-deriving them.

## Replace the Claude Code machinery honestly

- Replace hooks with the gates in this skill plus a `cron.add` job only when a check truly must repeat on a schedule, and never claim a commit or push was blocked by a hook.

- Replace the project.yaml modes block with the standing orders already recorded for the user and the project, and check those before asking any question.

- Ask the user only when a real decision is missing and no standing order covers it, and then ask the one pinpointing question that unblocks the work.

- Keep the Android track from the fork as the android specialist brief in `references/roles/android-specialist.md`, covering WebView APK packaging, signing verification and device evidence.

## Available connectors

- [GitHub](/opt/hatch/connectors/github/CONNECTOR.md) for reading and updating the user repositories that hold the game and this studio package.

- Use `muse.connector_search` to find other connectors and `muse.skill_search` to find related skills.

- If nothing here fits, look on the web for a maintained API or MCP server and set it up with [Custom Connectors and MCPs](/opt/muse/skills/custom-connector-setup/SKILL.md), or build a custom connector.

## Alternatives for better results

- Reuse the older learned skills beside this package instead of duplicating them, namely `preview_fidelity_check` for preview honesty, `real_browser_playtest_gate` for the playtest gate, `suite_green_claim_check` for green claims, `quiet_tree_integration_check` for tree freezing and `verify_static_deploy` for live bytes.

- Merge two roles into one brief when a job is small, such as writer plus world builder for a single village, and split them again when the job grows.

- Downgrade a batch to a partial report when one gate cannot pass today, naming the exact gate and what would unblock it, instead of shipping around it.
