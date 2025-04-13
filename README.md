<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>100 YouTube Screen Simulation</title>
  <style>
    body {
      font-family: sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f5f5f5;
      text-align: center;
    }

    header {
      padding: 20px;
      background-color: #1e3a8a;
      color: white;
    }

    .controls {
      margin: 20px 0;
    }

    button {
      padding: 10px 15px;
      margin: 0 10px;
      font-size: 16px;
      cursor: pointer;
      border: none;
      border-radius: 5px;
      background-color: #2563eb;
      color: white;
    }

    button:hover {
      background-color: #1d4ed8;
    }

    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
      gap: 10px;
      padding: 20px;
    }

    iframe {
      width: 100%;
      height: 180px;
      border: none;
    }
  </style>
</head>
<body>

  <header>
    <h1>📺 100 YouTube Screens Simulation</h1>
  </header>

  <div class="controls">
    <button onclick="playAll()">▶️ Play All</button>
    <button onclick="toggleMute()">🔇 Mute / Unmute</button>
    <button onclick="stopAll()">⏹️ Stop All</button>
  </div>

  <div class="grid" id="videoGrid"></div>

  <script>
    const videoIds = [
      "Ria5YlK2Afo", "aLFMkJaURUI", "hjGgK935eaA", "vr70Upcgl2k",
      "TbvZ7BfhKoE", "rdwoNFwkRF0", "BsyY02ioWrI", "xjxkMiK4igk",
      "8OEAtVMCJUU", "UYqnKDBvYFo"
    ];

    const videoGrid = document.getElementById('videoGrid');
    let players = [];
    let isMuted = true;

    function createVideoFrames() {
      for (let i = 0; i < 100; i++) {
        const videoId = videoIds[i % videoIds.length];
        const iframe = document.createElement('iframe');
        iframe.src = `https://www.youtube.com/embed/${videoId}?enablejsapi=1&rel=0&mute=1`;
        iframe.id = `player${i}`;
        iframe.allow = "autoplay; encrypted-media";
        videoGrid.appendChild(iframe);
      }
    }

    function playAll() {
      for (let i = 0; i < 100; i++) {
        const iframe = document.getElementById(`player${i}`);
        iframe.contentWindow.postMessage('{"event":"command","func":"playVideo","args":""}', '*');
      }
    }

    function stopAll() {
      for (let i = 0; i < 100; i++) {
        const iframe = document.getElementById(`player${i}`);
        iframe.contentWindow.postMessage('{"event":"command","func":"stopVideo","args":""}', '*');
      }
    }

    function toggleMute() {
      isMuted = !isMuted;
      const command = isMuted ? "mute" : "unMute";
      for (let i = 0; i < 100; i++) {
        const iframe = document.getElementById(`player${i}`);
        iframe.contentWindow.postMessage(`{"event":"command","func":"${command}","args":""}`, '*');
      }
    }

    createVideoFrames();
  </script>
</body>
</html>
