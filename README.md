# translator-website 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>English-Bangla Translator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f0f2f5;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }
    .container {
      width: 90%;
      max-width: 600px;
      padding: 20px;
      background-color: white;
      border-radius: 8px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      text-align: center;
    }
    textarea {
      width: 100%;
      height: 100px;
      margin-bottom: 10px;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    .button-group button {
      margin: 10px;
      padding: 10px 15px;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
    button:hover {
      background-color: #0056b3;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>English-Bangla Translator</h1>
    
    <textarea id="inputText" placeholder="Enter text here..."></textarea>
    
    <div class="button-group">
      <button onclick="translateToBangla()">Translate to Bangla</button>
      <button onclick="translateToEnglish()">Translate to English</button>
    </div>
    
    <h2>Translation</h2>
    <p id="outputText"></p>
    
    <div class="button-group">
      <button onclick="pronounceEnglish()">Pronounce English</button>
      <button onclick="pronounceBangla()">Pronounce Bangla</button>
    </div>
  </div>

  <script>
    // Function to handle English to Bangla translation
    function translateToBangla() {
      const text = document.getElementById("inputText").value;
      fetchTranslation(text, "en", "bn", (translation) => {
        document.getElementById("outputText").textContent = translation;
      });
    }

    // Function to handle Bangla to English translation
    function translateToEnglish() {
      const text = document.getElementById("inputText").value;
      fetchTranslation(text, "bn", "en", (translation) => {
        document.getElementById("outputText").textContent = translation;
      });
    }

    // Function to fetch translation (Replace with an actual API endpoint)
    function fetchTranslation(text, fromLang, toLang, callback) {
      // Replace YOUR_API_KEY with your actual API key.
      const apiKey = "YOUR_API_KEY";
      const url = `https://translation.googleapis.com/language/translate/v2?key=${apiKey}&q=${encodeURIComponent(text)}&source=${fromLang}&target=${toLang}`;
      
      fetch(url)
        .then(response => response.json())
        .then(data => callback(data.data.translations[0].translatedText))
        .catch(error => console.error("Translation error:", error));
    }

    // Function for English pronunciation
    function pronounceEnglish() {
      const text = document.getElementById("outputText").textContent;
      const utterance = new SpeechSynthesisUtterance(text);
      utterance.lang = 'en-US';
      speechSynthesis.speak(utterance);
    }

    // Function for Bangla pronunciation
    function pronounceBangla() {
      const text = document.getElementById("outputText").textContent;
      const utterance = new SpeechSynthesisUtterance(text);
      utterance.lang = 'bn-BD';
      speechSynthesis.speak(utterance);
    }
  </script>
</body>
</html>
