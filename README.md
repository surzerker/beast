# Beast Tracker Fork

This is a fork of the [original Beast Tracker](https://beastracker.s3.amazonaws.com/index.html) for the Goldblum Goo and Deformed Wing quests in Race War Kingdoms. It adds quality-of-life (QoL) improvements to enhance usability and reliability, maintained by [Surzerker](https://github.com/surzerker).

## Credits

- **Original Author**: Anubis (assumed), for creating the original Beast Tracker.
- **JimCav.com**: For providing detailed information about the quests, which informed the tracker’s instructions and strategies.
- **Alex (Cagedangel)**: For identifying the need for a Web Worker to ensure the timer works when the tab is out of focus.
- **Sebs (Niizandar)**: For the original request that inspired this fork’s development.
- **Maintainer**: [Surzerker](https://github.com/surzerker), for implementing and maintaining the QoL improvements.

## Purpose

This tool assists players in completing the Goldblum Goo (Nightmare Fly) and Deformed Wing (Dragonling Zombie) quests in Race War Kingdoms. These quests involve tracking a target kingdom on a 300x300 grid by messaging the Shrine Keeper every 5 minutes for directional clues, costing ash or runes. The tracker logs movements, suggests coordinates, and manages a 5-minute timer, improving efficiency over the original.

## Improvements and Features

### 1. Web Worker for Reliable Timer (Out-of-Focus Functionality)
- **Problem**: The original tracker’s timer, likely using `setInterval`, could be throttled or paused by browsers when the tab was inactive, disrupting the 5-minute tracking cycle.
- **Solution**: Implemented a Web Worker to run the 300-second (5-minute) timer in a separate thread, unaffected by browser throttling in inactive tabs.
- **How It Works**:
  - A Web Worker script (embedded as a Blob) counts down from 300 seconds, sending updates to the main thread every second via `postMessage`.
  - The main thread updates the UI (`Timer` display) and page title (e.g., "Beast Tracker: 295s"), ensuring the remaining time is visible even when the tab is not focused.
  - The timer starts when the user sets a starting position (via "Set All Values" or "Set X/Y Location") and stops on reset or when it reaches 0, with an alert for completion.
- **Benefit**: Players can switch tabs or minimize the browser without losing track of the 5-minute cycle, critical for messaging the Shrine Keeper on time.

### 2. Dark Theme Styling
- **Improvement**: Added a dark theme for better readability and modern aesthetics.
- **How It Works**:
  - Uses a dark gray background (`#1e1e1e`), light text (`#e0e0e0`), and green accents (`#4CAF50`) for headings and links.
  - Buttons and containers have darker shades (`#3a3a3a`, `#2a2a2a`) with hover effects (`#4a4a4a`) and rounded borders for a cohesive look.
  - The footer and collapsible sections blend seamlessly, with green highlights when expanded.
- **Benefit**: Reduces eye strain during long tracking sessions and improves visual clarity, especially in low-light environments.

### 3. Collapsible Quest Overview and Instructions
- **Improvement**: Added detailed, collapsible sections for quest overview and tracker usage, collapsed by default to reduce clutter.
- **How It Works**:
  - Uses HTML `<details>` and `<summary>` elements for native browser collapsing, styled as buttons with dark backgrounds and green highlights when open.
  - **Quest Overview**: Explains the Goldblum Goo and Deformed Wing quests, including costs (5,000+ ash or 999 runes), item acquisition, trading, tracking, and rewards (non-consumed card chances).
  - **How to Use the Tracker**: Guides users through the TL;DR strategies (start at (150,150,Surface), move 75 units, wait 5 minutes, handle conflicts with an 8x8 grid) and tool usage (setting positions, logging moves, monitoring timer).
  - Sections are toggled via clear "Show Quest Overview" and "Show How to Use the Tracker" buttons.
- **Benefit**: Keeps the interface clean for experienced users while providing accessible, detailed guidance for newcomers, with information sourced from [JimCav.com](https://jimcav.com) and the [Reddit post](https://www.reddit.com/r/a:t5_3k1hf/comments/6ndq4z/card_quests_new_surface_beasts/).

### 4. Enhanced Instructions and Quest Integration
- **Improvement**: Integrated specific instructions for the quests, replacing generic references with tailored guidance based on provided strategies.
- **How It Works**:
  - Instructions detail the quest process: killing beasts, trading with the Shrine Keeper, tracking every 5 minutes, and killing an enemy in the target kingdom.
  - Incorporates TL;DR strategies:
    - Start at map center (150,150,Surface).
    - Move half the distance to the edge (75 units) based on Keeper clues.
    - Wait 5 minutes, repeat tracking, or check the same kingdom.
    - Resolve conflicts by killing enemies in an 8x8 grid.
  - Tracker supports these via:
    - **Set All Values**: Initializes at (150,150,Surface) and starts the timer.
    - **Set X/Y Location**: Allows custom coordinates (1-300), validating input and starting the timer if no prior moves.
    - **Direction Buttons**: Log moves (North, East, South, West), suggest new coordinates (e.g., (225,150,Surface) for East), and store up to 5 recent tracks.
    - **Reset**: Clears all data and stops the timer.
- **Benefit**: Aligns the tool with the quests’ specific mechanics, making it easier to follow the strategic approach while logging progress accurately.

## How to Use

1. Visit the [GitHub Pages site](https://surzerker.github.io/beast-tracker) (replace with your actual URL after enabling GitHub Pages).
2. Expand the "Quest Overview" or "How to Use the Tracker" sections for guidance.
3. Click **Set All Values** to start at (150,150,Surface) or **Set X/Y Location** for a custom position, which starts the 5-minute timer.
4. Message the Shrine Keeper in-game with "track" to get a direction, then click the corresponding direction button (e.g., North) to log the move.
5. Update your position with **Set X/Y Location** based on suggested coordinates in **Map Data**.
6. Monitor the timer in the UI or page title, waiting 5 minutes before tracking again.
7. Use **Reset** to clear data and restart.
8. For conflicting clues, note your position and kill enemies in an 8x8 grid, updating coordinates as needed.

## Setup with GitHub Pages

To host this tracker:
1. Ensure `index.html` is in the repository’s root.
2. Go to **Settings** > **Pages** in your repository.
3. Set **Source** to **Deploy from a branch**, select `main` and `/ (root)`, then **Save**.
4. Wait 1–5 minutes, then visit `https://surzerker.github.io/beast-tracker` (adjust for your repository name).
5. The site is now publicly accessible.

## Contributing

Feel free to fork this repository or submit pull requests with improvements. Issues or suggestions can be reported via [GitHub Issues](https://github.com/surzerker/beast-tracker/issues).

## License

This project is open-source under the [MIT License](LICENSE), with respect to the original Beast Tracker’s terms (if applicable).
