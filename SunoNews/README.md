# सुनो न्यूज़ — Android प्रोजेक्ट

यह एक असली Android Gradle प्रोजेक्ट है (WebView में चलने वाला ऐप), जिसे आपके
"Accessible GitHub APK Builder" टूल से सीधे APK में बनाया जा सकता है।

## तरीका

1. "Accessible GitHub APK Builder" खोलें, अपना GitHub token डालकर Connect करें।
2. एक नई repository बनाएं (जैसे `SunoNews`)।
3. "Upload files" में यह पूरा ZIP चुनें और अपलोड करें — यह अपने-आप सही
   फ़ोल्डर structure में extract हो जाएगा।
4. "Add Android build workflow" पर टैप करें — यह `.github/workflows/build.yml`
   बना देगा (JDK 17 + Gradle के साथ)।
5. "Start APK build" दबाएं और कुछ मिनट इंतज़ार करें।
6. बिल्ड पूरा होने पर "Download APK" से APK उतार लें और फ़ोन में install करें।

## अंदर क्या है

- `MainActivity.kt` — बस एक WebView खोलता है जिसमें पूरा न्यूज़ ऐप (HTML/JS) चलता है।
- `assets/www/index.html` — असली ऐप: भाषा (हिंदी/English/मराठी/اردو) और विषय
  (टेक ज्ञान, ऑटो, मनोरंजन, मसाला, जरा हटके) चुनने के विकल्प, और खबरें।
- खबरें अभी NDTV/India Today जैसे भरोसेमंद public feed से आती हैं। अगर आप
  दैनिक जागरण या किसी और अखबार की सही category RSS/API link दें, तो
  `index.html` के अंदर `FEEDS` वाले हिस्से में वह जोड़ी जा सकती है।
- ऐप को इंटरनेट परमिशन चाहिए (खबरें लाने के लिए) — बस यही एक परमिशन मांगी गई है।

## TalkBack के साथ इस्तेमाल

ऐप में कोई अलग text-to-speech कोड नहीं है — पूरा भरोसा आपके फ़ोन के TalkBack
पर है। हर खबर पर सही भाषा का टैग (`lang` attribute) लगाया गया है, ताकि
TalkBack खुद सही उच्चारण में पढ़े।
