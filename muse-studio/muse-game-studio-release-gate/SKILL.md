# Gate a game release for web and Android

## Freeze and verify the batch

- List every agent and scheduled job still writing to the tree, and start only when each writer has finished or paused, following the sibling skill `quiet_tree_integration_check`.

- Snapshot the hashes of every file in the batch, rerun the full suite yourself from a separate process, and read the complete failure list from the log file.

- Compare the hashes again after the run and discard the whole verification when any shipped file changed during it.

- Confirm the batch contains no half finished files from other teams, no temporary bake outputs and no assets that nothing references yet.

## Check content and quality gates

- Confirm zero open blocking bugs for the paths this release touches, and list the known non blocking issues that ship as accepted risks.

- Confirm no placeholder art, no unfinished feature surface and no player facing text with unresolved markers reaches the build, with unfinished features hidden instead of shown.

- Confirm version numbers agree across the repo, the live site and any APK in the same release, and that the release note names the commit being shipped.

## Prove the live web build

- Push the batch and wait for the host to finish deploying, then fetch each shipped file from the live site with `curl` and compare its hash with the local file, following the sibling skill `verify_static_deploy`.

- Open the live entry point and confirm the page actually loads the new files, because a file present on the server is not proof the game runs it.

- Run the acceptance playtest in a real browser on the live build, walking the critical path this batch touched, before any link goes to the user.

## Prove the Android build when the release includes one

- Build the APK only from the verified staging tree at a named commit, in the declared variant, and bundle exactly one graphics tier for an offline build.

- Verify signing with `apksigner verify`, read package id, version and permissions with `aapt dump badging`, and report the final size in bytes with its dominant content named.

- Install and launch the APK on a real device or an emulator, observe the first playable screen and retain a screenshot, and state plainly in the first lines of the report when this step could not run.

## Give the verdict

- Return READY only when every section above passed on evidence you produced in this run.

- Return NOT READY with the failing section named when any gate failed, and NOT ASSESSED when a section could not be run, with what would unblock it.

- Close with one short release report covering the commit, the file list, the live hash results, the playtest result and the part that remains unverified.

## Available connectors

- [GitHub](/opt/hatch/connectors/github/CONNECTOR.md) for the push and remote verification of the release commits.

- Use `muse.connector_search` to find other connectors and `muse.skill_search` to find related skills.

- If nothing here fits, look on the web for a maintained API or MCP server and set it up with [Custom Connectors and MCPs](/opt/muse/skills/custom-connector-setup/SKILL.md), or build a custom connector.
