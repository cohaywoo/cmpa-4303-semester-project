# BlockCraft Companion: P02 Iteration Plan

## 1. P01 Evaluation

### What works well

- **The core workflow is functional.** A visitor can open the Build Hub, create a named build, choose blocks from a large catalog, adjust quantities, and see storage estimates in real time. The search field and category filters make a catalog of more than a simple handful of blocks usable.
- **The project has meaningful persistence.** Build names, block quantities, biome selections, descriptions, screenshots, theme preference, and the new collected-material checklist are stored in `localStorage`. A visitor can leave and return without losing a build plan.
- **The enhancement added real utility.** The materials checklist and progress bar turn the app from a static shopping list into a tool for tracking a build over time. The progress is isolated by active build and survives a reload.
- **The visual direction is coherent.** The green, stone, and gold palette communicates the Minecraft-inspired subject without requiring a large image-heavy interface. The dark/light theme toggle, cards, responsive grid, texture images, screenshot lightbox, and print stylesheet show attention to different ways a builder might use the tool.
- **The app has useful outputs.** Users can copy a shopping list, print a checklist, share build details, upload reference screenshots, and load starter templates. Those features give the planner value beyond simply displaying a block catalog.

### What does not work well yet

- **The page hierarchy is still prototype-like.** The landing content says “First Deployment,” repeats broad feature claims, and hides the main Build Hub behind a button. A returning builder has to scroll and click before reaching the primary task. P02 should make the planner the clear first action while retaining a concise introduction.
- **The interface is becoming too dense.** The Build Hub contains project creation, two selects, deletion, uploads, sharing, search, nine categories, a large palette, saved materials, storage calculations, export actions, and progress tracking in one section. On a phone this is usable but long and requires substantial scrolling; the controls need clearer grouping and prioritization.
- **The data model is fragile.** Plans are stored only in browser `localStorage`, so they are not available across devices or browsers. Large screenshot data URLs can also consume storage quickly. There is no export/import backup for a user who wants to move or protect a build.
- **Some interactions need stronger feedback and accessibility polish.** The app relies heavily on small buttons, selects, and live replacement of saved-material rows. It needs clearer focus states, more explicit empty/error messages, confirmation feedback for destructive actions, and testing with keyboard navigation and a screen reader. The current page also depends on remote texture images, so a blocked network can leave the palette without useful visuals.
- **The content is not yet a complete product experience.** The catalog and recipes are useful, but the app does not explain a recommended planning workflow, distinguish a material quantity from a recipe input consistently, or provide a concise project summary suitable for sharing outside the app.
- **The code is difficult to extend.** Almost all markup, styling, data, and behavior live in one `index.html` file. This was efficient for P01, but it makes changes harder to test and increases the chance that unrelated interactions affect one another.

### Comparison to the proposal

The proposal was to build a Minecraft-inspired creative-build companion that helped builders organize ideas, materials, and project goals. P01 delivered that central concept: named build plans, a categorized block catalog, quantities, storage calculations, biomes, descriptions, screenshots, templates, sharing, and printing all support the proposed use case.

The implementation expanded beyond a basic idea organizer into a more capable material-planning tool. The original concept did not require the screenshot gallery, starter templates, recipes, or persistent collection progress, but those additions came from evaluating what a builder needs after creating a plan. The main gap is that P01 is still a polished prototype rather than a dependable finished product: it has no cross-device data strategy, no import/export safety net, and no separated project structure. P02 should focus on reliability and clarity instead of continuing to add an unlimited catalog of features.

## 2. Changes for P02

### Fixes

- **Add import and export for build data.** Provide a JSON export for the active build or all builds, plus an import flow with validation and a confirmation step. This fixes the risk of losing plans when `localStorage` is cleared and gives users a practical way to move data between browsers.
- **Handle storage and image failures.** Detect invalid saved JSON, quota errors, and failed screenshot/image loads instead of silently failing. Show a useful message and keep the rest of the build usable when a texture or upload cannot be saved.
- **Improve keyboard and assistive-technology behavior.** Audit heading order, focus visibility, labels, live regions, modal focus, Escape behavior, and keyboard access to every interactive control. This is necessary for the app to function as a finished tool rather than only a mouse-and-touch prototype.
- **Add destructive-action safeguards.** Make clear which build is active, require intentional confirmation before clearing or deleting, and provide success/error feedback for share, copy, import, and upload actions.

### Improvements

- **Rework the page hierarchy around the Build Hub.** Make “Create or continue a build” the primary first-viewport action, reduce the amount of promotional copy, and keep the overview/features content secondary. This will reduce the number of clicks between arrival and the main task.
- **Group and simplify Build Hub controls.** Separate project management, reference media, material selection, and progress/output actions into labeled groups. On small screens, preserve comfortable touch targets and make the saved-material summary easier to scan.
- **Clarify planning language and calculations.** Explain the difference between planned blocks, crafted blocks, recipe inputs, stacks, and inventory slots. The summary should communicate what the number means without requiring a user to infer it from several lines of text.
- **Improve the build summary and sharing output.** Include the build description, biome, progress percentage, material quantities, and a compact screenshot/preview choice in the printable and shareable output. This makes the result useful outside the website.
- **Make the visual system more consistent.** Replace repeated inline styles and undefined/fallback color assumptions with a smaller documented set of design variables, then test dark mode, light mode, print, tablet, and phone layouts together.

### Additions

- **Build backup and restore.** Import/export is the highest-value addition because it makes the existing local-first approach safer without requiring a backend.
- **A build dashboard or saved-build overview.** Add a compact view showing each build's biome, number of materials, collection progress, and last updated state. This gives users a useful way to choose what to resume instead of relying only on a select menu.
- **Optional material notes and categories.** Let users attach a short note to a material, such as where to gather it or which room uses it, while retaining the existing quantity controls.
- **Basic automated interaction checks.** Add a small browser test workflow for creating a build, adding a material, changing quantity, collecting it, reloading, and exporting. This protects the most important user path as the project becomes more complex.

### Cuts

- **Cut the fixed “24 plans / 8 biomes / 3 tools” snapshot numbers.** They read like product claims rather than useful live information and can become inaccurate as the app changes. Replace them with live counts or remove the snapshot if it does not help a builder make a decision.
- **Cut or limit low-value catalog expansion.** I will not spend P02 time trying to include every possible block variant. A smaller, reliable catalog with accurate textures, categories, and recipes is more valuable than a huge list with inconsistent coverage.
- **Cut decorative motion that does not support a task.** Keep transitions that communicate opening, closing, or progress, but remove visual effects that compete with material selection or make the interface feel slower on mobile.

## 3. Priority and Timeline

### Must complete

**Estimated effort: most of one weekend, approximately 8–12 hours.**

1. Reorganize the first-viewport navigation so the Build Hub is clearly the primary workflow.
2. Add validated JSON export/import and storage error handling.
3. Fix accessibility fundamentals: keyboard navigation, visible focus, labels, modal behavior, and clear status messages.
4. Test the full critical path on desktop, tablet, and phone: create, save, reload, switch builds, collect materials, print, and restore a backup.
5. Split the largest data and UI responsibilities out of the single inline script enough to make the final changes maintainable.

### Should complete

**Estimated effort: another 6–10 hours.**

1. Add a saved-build dashboard with live progress and biome information.
2. Improve the printable/shareable summary and clarify storage/recipe terminology.
3. Add material notes and stronger empty/error states.
4. Replace fixed snapshot statistics with live information and refine the responsive layout after testing real content lengths.

### If time allows

**Estimated effort: 4–8 additional hours, only after the must-complete work is stable.**

1. Add lightweight browser smoke tests for the core workflow.
2. Add sorting or filtering for saved materials by category, collected state, or quantity.
3. Add optional build milestones, such as foundation, walls, and finishing, without turning the project into a full task-management app.
4. Improve offline resilience by bundling a small set of fallback textures or displaying a consistent generated swatch when remote assets fail.

## 4. Updated Tools and Approach

I will keep the static HTML/CSS/vanilla JavaScript approach for P02. It is appropriate for a GitHub Pages deployment and keeps the project easy to run, but I will separate the large inline script into focused JavaScript modules or clearly separated data/rendering sections instead of introducing a framework solely for structure. I will continue using `localStorage` for the MVP, adding JSON import/export rather than taking on a backend before the core workflow is reliable.

VS Code, GitHub, GitHub Pages, browser DevTools, and GitHub Copilot were effective during P01 and will remain part of the workflow. Copilot was most useful when working iteratively against a concrete feature, while browser testing exposed interaction bugs that static inspection missed. For P02 I will make browser checks more deliberate: test the critical path after each major change, use responsive viewport checks, inspect keyboard focus, and verify both a clean browser and a browser with existing saved data.

If I were starting over, I would define the saved-build data shape and separate UI state from persistent state before building the interface. I would also establish the primary user journey first, then add the catalog, screenshots, recipes, and sharing around that journey. That would have prevented the page from accumulating many useful features inside one increasingly dense file and would make the final MVP easier to prioritize and maintain.
