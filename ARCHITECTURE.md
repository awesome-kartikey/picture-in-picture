# System Architecture

This project is a purely **client-side web application**. It runs entirely within the user's web browser and does not require any backend server for its core functionality. It leverages modern browser APIs to achieve screen capture and Picture-in-Picture display.

## Architecture Style

- **Client-Side Rendering:** All UI rendering and logic execution happen in the browser.
- **Event-Driven:** The application responds to user interactions (button clicks, file uploads, dropdown changes) and browser events (video metadata loaded, PiP exit).
- **API-Reliant:** Heavily depends on browser-provided JavaScript APIs (`MediaDevices`, `PictureInPictureWindow`, `Fullscreen`, DOM APIs).

## Project Folder Structure

```
picture-in-picture/
├── advanced-pip-app v1.html  # Self-contained demo: Screen Share + File Upload + Native PiP
├── advanced-pip-app v2.html  # Self-contained demo: Adds Custom PiP, Filters, Timer
├── advanced-pip-app v3.html  # Self-contained demo: Adds YouTube, Themes, Shortcuts, Volume, etc.
├── index.html                # Core/Basic HTML structure (Screen Share + Native PiP)
├── script.js                 # JavaScript logic for index.html
└── style.css                 # CSS styling for index.html
```

- **`index.html`, `script.js`, `style.css`**: Form the basic version of the application. `index.html` provides the structure, `style.css` the presentation, and `script.js` the core logic for screen capture and native PiP initiation.
- **`advanced-pip-app*.html`**: These are self-contained HTML files that include their own embedded CSS (`<style>`) and JavaScript (`<script>`). Each file represents a more advanced version or a specific feature set demonstration, building upon the concepts of the basic version.

## Major Components

1.  **HTML Structure (`.html` files):**

    - Defines the user interface elements: video player (`<video>`), buttons (`<button>`), file input (`<input type="file">`), dropdowns (`<select>`), text inputs (`<input type="text">`), status display (`<div>`).
    - In advanced versions, includes the structure for the custom PiP window (`<div id="custom-pip">`).

2.  **CSS Styling (`style.css`, embedded `<style>`):**

    - Provides visual presentation, layout, and theming (including dark mode in v3).
    - Styles the main UI, buttons, video player, and the custom PiP window.
    - Used for applying video filters (`filter` property).
    - Enables resizing for the custom PiP window (`resize: both`).

3.  **JavaScript Logic (`script.js`, embedded `<script>`):**

    - **Event Handling:** Listens for user actions (clicks, changes, file selections, key presses).
    - **API Interaction:**
      - `navigator.mediaDevices.getDisplayMedia()`: Initiates screen capture.
      - `videoElement.requestPictureInPicture()`: Requests native browser PiP.
      - `document.exitPictureInPicture()`: Exits native PiP (implicitly handled by browser controls).
      - `URL.createObjectURL()`: Creates a URL for uploaded local files.
      - DOM Manipulation: Selects elements, updates text content (status, timer), changes styles (filters, themes), adds/removes elements dynamically (v3 controls).
      - Fullscreen API: Requests/exits fullscreen mode (v3).
    - **State Management:** Manages application state (e.g., `mediaStream` object, `isCustomPipActive` flag, button disabled states).
    - **Custom PiP Logic (v2+):** Handles dragging (mousedown, mousemove, mouseup events) and toggling resizability for the custom PiP element. Copies the video stream/source to the PiP video element.
    - **Feature Logic:** Implements timer updates, filter application, theme switching, YouTube URL parsing/loading, keyboard shortcut handling, volume/speed control, and screenshot generation (v3).

4.  **Browser APIs:**
    - **MediaDevices API:** Provides access to media input devices (screen capture).
    - **Picture-in-Picture API:** Allows websites to create a floating video window.
    - **HTMLMediaElement API:** Controls video playback (`play()`, `pause()`), source (`srcObject`, `src`), events (`onloadedmetadata`, `leavepictureinpicture`), volume, playback rate.
    - **DOM API:** Used extensively for selecting and manipulating UI elements.
    - **Fullscreen API:** Controls browser fullscreen mode.

## Data Flow

**Basic Screen Share + Native PiP (`index.html`)**

1.  **User Action:** Page loads.
2.  **JS (`selectMediaStream`):** Calls `navigator.mediaDevices.getDisplayMedia()`.
3.  **Browser:** Prompts user to select screen/window.
4.  **User Action:** Selects content and grants permission.
5.  **Browser:** Returns a `MediaStream` object to JS.
6.  **JS:** Sets `videoElement.srcObject = mediaStream`. Attaches `onloadedmetadata` listener.
7.  **Video Element:** Fires `loadedmetadata` event.
8.  **JS (`onloadedmetadata`):** Calls `videoElement.play()`. (Video remains hidden in `index.html`).
9.  **User Action:** Clicks the "START" button.
10. **JS (Button Listener):** Calls `videoElement.requestPictureInPicture()`.
11. **Browser:** Displays the native PiP window showing the `MediaStream`.
12. **User Action:** Closes PiP window using browser controls.
13. **Video Element:** Fires `leavepictureinpicture` event (handled in advanced versions).

**Advanced Flow Example - Custom PiP with File Upload (v2/v3):**

1.  **User Action:** Clicks "Upload Video" label.
2.  **Browser:** Opens file selection dialog.
3.  **User Action:** Selects a video file.
4.  **JS (File Input Listener):**
    - Gets the `File` object.
    - Creates an object URL: `fileURL = URL.createObjectURL(file)`.
    - Sets `videoElement.src = fileURL`.
    - Updates button states (enable PiP, Stop, etc.).
    - Starts timer (if applicable).
5.  **Video Element:** Loads and potentially autoplays the video.
6.  **User Action:** Clicks "Custom PiP" button.
7.  **JS (`toggleCustomPiP`):**
    - Checks if custom PiP is already active. If not:
    - Sets `pipVideo.src = videoElement.src` (or `pipVideo.srcObject = videoElement.srcObject` if screen sharing).
    - Calls `pipVideo.play()`.
    - Makes the custom PiP div visible (`customPip.style.display = 'block'`).
    - Sets `isCustomPipActive = true`.
    - Updates button text/state and enables move/resize buttons.
8.  **User Action:** Drags the custom PiP window.
9.  **JS (Mouse Listeners):** Tracks mouse movement while dragging flag is true, updating `customPip.style.left` and `customPip.style.top`.

## Design Decisions

1.  **Client-Side Only:** Keeps the project simple, easy to deploy (static hosting), and leverages powerful built-in browser capabilities. No need for server infrastructure.
2.  **Multiple HTML Files:** Chosen to demonstrate features progressively. While good for demos, a production app would likely consolidate into a single application with modular JS.
3.  **Embedded CSS/JS (Advanced Versions):** Simplifies distribution of each demo version as a single file. However, for larger projects, external CSS and JS files are preferred for better organization, caching, and maintainability.
4.  **Native PiP vs. Custom PiP:** Both are included to showcase the different approaches. Native PiP is simpler to implement but less flexible. Custom PiP offers flexibility at the cost of increased implementation complexity.
5.  **Progressive Enhancement:** The advanced versions build upon the core concepts, adding features like filters, themes, and more controls, demonstrating how the basic functionality can be extended.
6.  **Use of Font Awesome:** Provides easy access to icons for buttons, improving the UI without requiring custom image assets.
