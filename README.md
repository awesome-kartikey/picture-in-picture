# Awesome Kartikey Picture-in-Picture

A web-based application demonstrating various Picture-in-Picture (PiP) functionalities, from basic screen sharing PiP to advanced features like custom PiP windows, video filters, and YouTube playback.

This project includes several versions showcasing progressive feature implementation:

- **`index.html`**: The basic implementation using native browser PiP for screen sharing.
- **`advanced-pip-app v1.html`**: Adds video file upload capability alongside screen sharing.
- **`advanced-pip-app v2.html`**: Introduces a custom, movable, and resizable PiP window, video filters, and a timer.
- **`advanced-pip-app v3.html`**: The most feature-rich version, adding YouTube URL playback, dark/light theme toggle, keyboard shortcuts, fullscreen, volume/speed controls, and screenshot capability.

## Features

**Core (`index.html`)**

- Select a screen or application window to share.
- Initiate native browser Picture-in-Picture for the shared screen.

**Advanced (`advanced-pip-app*.html`)**

- **Screen Sharing:** Capture and display screen content. (v1+)
- **Video File Upload:** Play local video files. (v1+)
- **Native PiP:** Utilize the browser's built-in PiP functionality. (v1+)
- **Custom PiP:** A custom-built, movable, and resizable PiP window implemented with HTML/CSS/JS. (v2+)
- **Video Filters:** Apply CSS filters (grayscale, sepia, blur, etc.) to the video. (v2+)
- **Playback Timer:** Display elapsed playback time. (v2+)
- **YouTube Playback:** Load and play videos directly from YouTube URLs. (v3)
- **Theme Toggle:** Switch between light and dark modes. (v3)
- **Tooltips:** Helpful hints on button functionality. (v3)
- **Keyboard Shortcuts:** Control basic functions using keyboard commands (Ctrl+P, Ctrl+C, Ctrl+S, Esc). (v3)
- **Fullscreen Mode:** View the main video in fullscreen. (v3)
- **Volume & Playback Speed Control:** Adjust audio volume and video playback speed. (v3)
- **Screenshot:** Capture a frame from the currently playing video. (v3)

## Tech Stack

- **Frontend:** HTML5, CSS3, JavaScript (ES6+)
- **APIs:**
  - WebRTC (`navigator.mediaDevices.getDisplayMedia`) for screen capture.
  - Picture-in-Picture API (`video.requestPictureInPicture`) for native PiP.
  - Fullscreen API
  - DOM Manipulation
- **Libraries:** Font Awesome (for icons)

## Setup Instructions

No complex setup is required. The project consists of static HTML, CSS, and JavaScript files.

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/awesome-kartikey/picture-in-picture.git
    cd picture-in-picture
    ```
2.  **Open the HTML files:**

    - For the basic version, open `index.html` in your web browser.
    - For advanced versions, open `advanced-pip-app v1.html`, `advanced-pip-app v2.html`, or `advanced-pip-app v3.html` directly in your browser.

    _Note:_ Due to security restrictions, `navigator.mediaDevices.getDisplayMedia()` typically requires the page to be served over HTTPS or from `localhost`. Simply opening the file via `file:///` might work in some browsers for basic testing but is not guaranteed for all features. Using a simple local web server is recommended.

    _Example using Python's built-in server:_

    ```bash
    # If you have Python 3
    python -m http.server
    # If you have Python 2
    python -m SimpleHTTPServer
    ```

    Then navigate to `http://localhost:8000` (or the port specified) in your browser and click on the desired HTML file.

## Usage

**Basic Version (`index.html`)**

1.  Open `index.html`.
2.  Your browser will likely prompt you to select a screen, window, or tab to share. Choose one and click "Share".
3.  The shared content will appear in the hidden `<video>` element (though you won't see it on the main page).
4.  Click the "START" button to activate the native Picture-in-Picture window displaying your shared screen.

**Advanced Versions (`advanced-pip-app*.html`)**

1.  Open the desired `advanced-pip-app vX.html` file.
2.  **Share Screen:** Click "Share Screen" and select the content to share.
3.  **Upload Video:** Click "Upload Video" and choose a local video file.
4.  **Play YouTube (v3 only):** Enter a YouTube video URL in the input field and click "Play YouTube".
5.  Once content is playing in the main video player:
    - Click "Start PiP" for the native browser PiP.
    - Click "Custom PiP" (v2+) to toggle the custom, movable/resizable PiP window.
    - Use filter dropdown (v2+), theme toggle (v3), volume/speed controls (v3), screenshot (v3), or fullscreen (v3) as needed.
    - Use "Stop" to end the screen share or clear the video source.
    - Explore tooltips (v3) and keyboard shortcuts (v3) for more interaction options.
