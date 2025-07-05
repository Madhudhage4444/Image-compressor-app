<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="description" content="Resize, enhance, and compress your images online. Free, fast, and easy tools for JPG, PNG, and WebP." />
  <title>🧠 Smart Image Tools - Resize | Compress | Enhance</title>
  <style>
    :root {
      --primary: #4f46e5;
      --accent: #22d3ee;
      --dark-bg: #1a1a1a;
      --light-bg: #fdfbfb;
      --font-color: #333;
      --font-dark: #eee;
    }

    body {
      font-family: 'Segoe UI', sans-serif;
      margin: 0;
      padding: 0;
      background: linear-gradient(to right, var(--light-bg), #e2e8f0);
      color: var(--font-color);
      transition: all 0.3s ease-in-out;
    }
    .dark-mode {
      background: var(--dark-bg);
      color: var(--font-dark);
    }
    header, footer {
      padding: 1rem;
      text-align: center;
      background-color: var(--primary);
      color: white;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
    }
    main {
      padding: 2rem;
      max-width: 700px;
      margin: auto;
      text-align: center;
      background-color: rgba(255,255,255,0.9);
      border-radius: 12px;
      box-shadow: 0 4px 20px rgba(0,0,0,0.05);
    }
    .dark-mode main {
      background-color: rgba(34,34,34,0.85);
    }
    input[type="file"], input[type="number"] {
      margin: 1rem 0;
      padding: 0.5rem;
      border: 1px solid #ccc;
      border-radius: 8px;
    }
    #output {
      margin-top: 1.5rem;
    }
    button {
      padding: 0.6rem 1.2rem;
      background-color: var(--primary);
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      margin: 0.5rem;
      transition: background 0.3s;
    }
    button:hover {
      background-color: #3730a3;
    }
    .toggle {
      position: absolute;
      top: 1rem;
      right: 1rem;
      background-color: var(--accent);
      color: black;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <header>
    <h1>🧠 Smart Image Tools</h1>
    <p>Resize • Enhance • Compress (Free & Instant)</p>
  </header>
  <button onclick="toggleDarkMode()" class="toggle">🌓 Mode</button>
  <main>
    <p><strong>Upload your image (JPG, PNG, WebP):</strong></p>
    <input type="file" id="imageInput" accept="image/*" />
    <p>
      <label><strong>Resize Width (px):</strong></label>
      <input type="number" id="resizeWidth" placeholder="e.g. 800" />
    </p>
    <button onclick="processImage()">🚀 Compress & Resize</button>
    <div id="output"></div>
  </main>
  <footer>
    © 2025 Smart Tools by Madhukar | <a href="https://vercel.com" style="color: #a5f3fc; text-decoration: underline;">Deploy on Vercel</a>
  </footer>

  <script src="https://cdn.jsdelivr.net/npm/browser-image-compression@2.0.2/dist/browser-image-compression.js"></script>
  <script>
    async function processImage() {
      const fileInput = document.getElementById("imageInput");
      const resizeWidth = parseInt(document.getElementById("resizeWidth").value);
      const file = fileInput.files[0];
      if (!file) return alert("Please upload an image first.");

      const options = {
        maxSizeMB: 1,
        maxWidthOrHeight: resizeWidth || 1024,
        useWebWorker: true,
      };

      try {
        const compressedFile = await imageCompression(file, options);
        const beforeSize = (file.size / 1024).toFixed(2);
        const afterSize = (compressedFile.size / 1024).toFixed(2);
        const downloadUrl = URL.createObjectURL(compressedFile);

        document.getElementById("output").innerHTML = `
          <p>✅ Process completed</p>
          <p><strong>Before:</strong> ${beforeSize} KB | <strong>After:</strong> ${afterSize} KB</p>
          <a href="${downloadUrl}" download="smart-image.jpg">
            <button>⬇️ Download Final Image</button>
          </a>
        `;
      } catch (e) {
        alert("❌ Processing failed. Try again.");
        console.error(e);
      }
    }

    function toggleDarkMode() {
      document.body.classList.toggle("dark-mode");
    }
  </script>
</body>
</html>
