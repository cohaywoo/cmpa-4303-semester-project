# BlockCraft Companion

## What is this?

BlockCraft Companion is a responsive web app for Minecraft-inspired creative builds. Builders can create named projects, choose blocks from a large categorized catalog, set quantities, select a biome, upload screenshots, and share or print their build plans.

## Why does it exist?

I built this project for Minecraft builders who enjoy ambitious creations but need help organizing materials and ideas. The app turns an open-ended build into a named plan with blocks, quantities, recipes, storage estimates, a biome, and screenshots. It also serves as the first deployed milestone of my CMPA 4303 semester project.

## What tools did I use?

- **Code editor: VS Code** - I used VS Code to write, organize, and test the project files.
- **Languages: HTML, CSS, and vanilla JavaScript** - This lightweight stack is a good fit for a fast static project while still supporting responsive layouts, animations, filters, calculations, and interactive build management.
- **Browser localStorage** - I used localStorage to save named builds, block quantities, biome selections, descriptions, screenshots, and theme preferences between visits.
- **Hosting platform: GitHub Pages** - GitHub Pages provides free public hosting for this static site and deploys directly from the repository's main branch.
- **AI assistant: GitHub Copilot** - Copilot helped me brainstorm interface ideas, refine the responsive layout, and troubleshoot the JavaScript interactions.

## How to visit it

[Visit BlockCraft Companion](https://cohaywoo.github.io/cmpa-4303-semester-project/)

The source code is available in the [GitHub repository](https://github.com/cohaywoo/cmpa-4303-semester-project).

## Exercise 05 enhancement

The Build Hub now includes a persistent materials checklist and gathering progress bar. Builders can mark each saved material as collected, see the percentage completed for the active build, and resume that progress after switching builds or returning to the site. I chose this enhancement because the original planner could calculate what materials were needed but could not help track what had already been gathered. I implemented it with HTML, CSS, vanilla JavaScript, and localStorage, improving the P01 project from a planning list into a more useful build-progress tool.
