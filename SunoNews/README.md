# Suno News — Android प्रोजेक्ट

WebView में चलने वाला न्यूज़ ऐप, जिसे "Accessible GitHub APK Builder" से सीधे APK बनाया जा सकता है।

## इस वर्ज़न में क्या बदला

1. **ऐप न खुलने की दिक्कत ठीक की।** `styles.xml` की थीम AppCompat वाली कर दी गई है
   (`MainActivity` AppCompatActivity है, इसलिए पुरानी थीम से ऐप खुलते ही क्रैश हो जाता था)।
2. **पूरा इंटरफ़ेस अंग्रेज़ी में है** — बटन, मेन्यू, स्टेटस मैसेज, फ़ुटर, AI सेक्शन, ऐप का नाम।
3. **न्यूज़ की भाषा चुनने की ड्रॉप-डाउन लिस्ट** ("News reading language"): Hindi / English / Marathi / Urdu।
   भाषा बदलने पर सिर्फ़ खबरें और उनके category के नाम बदलते हैं (दैनिक जागरण की तरह),
   इंटरफ़ेस अंग्रेज़ी में ही रहता है। चुनी हुई भाषा और category फ़ोन में याद रहती है।
4. **हर खबर पर उसकी असली भाषा का टैग** लगता है, ताकि TalkBack सही उच्चारण में पढ़े।
   अगर किसी भाषा की खबर अनुवाद के बिना अंग्रेज़ी में ही आई है, तो उस पर `en` टैग लगेगा
   और ऊपर स्टेटस में साफ़ बताया जाएगा।

## भाषा के हिसाब से खबरें कैसे आती हैं

- **English:** सीधे अंग्रेज़ी फ़ीड से।
- **Hindi / Marathi / Urdu:**
  1. पहले उस भाषा की अपनी फ़ीड (`NATIVE_FEEDS`) आज़माई जाती है — अभी सिर्फ़ Hindi के Movies के लिए एक पुरानी सार्वजनिक लिस्ट वाला लिंक है, जो चलना बंद भी हो सकता है।
  2. फ़ीड न हो या न चले तो अंग्रेज़ी फ़ीड आती है, और **AI key डाली हो** तो वह चुनी हुई भाषा में अनुवाद होकर दिखती है।
  3. AI key न हो तो अंग्रेज़ी खबरें ही दिखती हैं (सही टैग के साथ)।
- AI key डालने की जगह: ऐप में "AI options (API key)"। OpenRouter या Google Gemini की key चलती है।
- किसी भाषा/category की असली फ़ीड जोड़नी हो तो `assets/www/index.html` में `NATIVE_FEEDS` के अंदर लिंक डालें, जैसे `NATIVE_FEEDS.hi.tech = "https://..."`।

## APK बनाने का तरीका

1. "Accessible GitHub APK Builder" खोलें, GitHub token से Connect करें।
2. नई repository बनाएं (जैसे `SunoNews`)।
3. "Upload files" में यह पूरा ZIP चुनें — यह सही फ़ोल्डर structure में extract हो जाएगा।
4. "Add Android build workflow" दबाएं (JDK 17 + Gradle वाला `build.yml` बनेगा)।
5. "Start APK build" दबाएं, कुछ मिनट रुकें, फिर "Download APK" से APK उतारकर इंस्टॉल करें।

## अंदर क्या है

- `MainActivity.kt` — सिर्फ़ एक WebView खोलता है जिसमें पूरा ऐप (HTML/JS) चलता है।
- `assets/www/index.html` — असली ऐप।
- ऐप को सिर्फ़ इंटरनेट की परमिशन चाहिए।
