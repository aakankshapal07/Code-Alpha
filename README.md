# Code-Alpha
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Language Translation Tool</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 30px; }
    textarea { width: 100%; height: 100px; margin: 10px 0; }
    select, button { margin: 5px; padding: 5px; }
    .output { margin-top: 15px; padding: 10px; border: 1px solid #ccc; background: #f9f9f9; }
  </style>
</head>
<body>
  <h2>🌍 Language Translation Tool</h2>
  
  <label>Enter text:</label>
  <textarea id="inputText"></textarea>
  
  <br>
  <label>From:</label>
  <select id="sourceLang">
    <option value="en">English</option>
    <option value="hi">Hindi</option>
    <option value="es">Spanish</option>
    <option value="fr">French</option>
  </select>
  
  <label>To:</label>
  <select id="targetLang">
    <option value="hi">Hindi</option>
    <option value="en">English</option>
    <option value="es">Spanish</option>
    <option value="fr">French</option>
  </select>
  
  <button onclick="translateText()">Translate</button>
  
  <div class="output" id="translatedText">Your translation will appear here...</div>
  
  <button onclick="copyText()">Copy</button>
  <button onclick="speakText()">🔊 Speak</button>
  
  <script>
    async function translateText() {
      const inputText = document.getElementById("inputText").value;
      const sourceLang = document.getElementById("sourceLang").value;
      const targetLang = document.getElementById("targetLang").value;
      
      const response = await fetch("https://libretranslate.de/translate", {
        method: "POST",
        body: JSON.stringify({
          q: inputText,
          source: sourceLang,
          target: targetLang,
          format: "text"
        }),
        headers: { "Content-Type": "application/json" }
      });
      
      const data = await response.json();
      document.getElementById("translatedText").innerText = data.translatedText;
    }

    function copyText() {
      const text = document.getElementById("translatedText").innerText;
      navigator.clipboard.writeText(text);
      alert("Copied to clipboard!");
    }

    function speakText() {
      const text = document.getElementById("translatedText").innerText;
      const speech = new SpeechSynthesisUtterance(text);
      speech.lang = document.getElementById("targetLang").value;
      window.speechSynthesis.speak(speech);
    }
  </script>
</body>
</html>
