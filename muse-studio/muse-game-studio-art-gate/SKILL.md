# Gate game art against the reference standard

## Fix the standard before judging anything

- Name the reference set for this judgement, meaning the user supplied images and videos plus the anchor pieces the user already praised, and open them before opening the new art.

- Pull the project art bible points that apply, covering style statement, shape language, color system, character direction, environment direction and asset standards for size and format.

- Judge the new art against that reference set only, and never against the previous version of the same art.

## Audit the asset files with real measurements

- Measure file sizes, dimensions and formats with `muse.exec` and tools such as `stat`, `file` and `du`, and compare them with the budgets in the art bible.

- Search the codebase for references to each new asset and list assets that nothing references, plus references whose file is missing.

- Write NOT ASSESSED in any cell you could not measure, because a budget table filled from guesses looks like evidence and is worse than an empty cell.

## Inspect the art the way a player sees it

- View the art at full map or scene scale and again at 100 percent crops on seams, gates, joins and every area a previous round got wrong.

- Check detail density between the core and the rim of a scene, and fail the piece when the rim reads flat, patched or repetitive next to the core.

- Check the piece inside the real game render when it is meant to run there, because a painting that reads well alone can still fight the logic grid, the signs or the HUD.

- List every mismatch in plain words before writing any verdict, and claim a match only for the elements that actually match.

## Apply the harsh gate before anything reaches the user

- Send failing art back inside the team with the mismatch list and regenerate it, for as many rounds as the piece needs.

- Never send the user an image that failed this gate and never ask the user to judge one, because the user standing order is that ugly images are fixed internally and not asked about.

- Hide a feature whose art is unfinished rather than shipping a placeholder, following the project rule that unfinished art stays invisible.

- When a piece passes, attach the panorama and the 100 percent crops, label each image as an in game capture, a render from real game data or a layout mockup, and name the remaining weakness in one sentence.

## Available connectors

- Use `muse.connector_search` to find other connectors and `muse.skill_search` to find related skills.

- If nothing here fits, look on the web for a maintained API or MCP server and set it up with [Custom Connectors and MCPs](/opt/muse/skills/custom-connector-setup/SKILL.md), or build a custom connector.

## Alternatives for better results

- Run the sibling skill `preview_fidelity_check` when the question is whether one preview matches its reference and the live render, and keep this gate for whole asset batches and style drift.

- Split a failing scene into named regions and re-judge region by region, because one global verdict hides the one flat corner that ruins the piece.
