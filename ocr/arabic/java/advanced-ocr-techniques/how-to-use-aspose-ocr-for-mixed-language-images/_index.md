---
category: general
date: 2026-05-06
description: كيفية استخدام Aspose OCR للتعرف على النص من الصورة، وتمكين الكشف التلقائي
  عن اللغة، وتحسين سرعة OCR في Java.
draft: false
keywords:
- how to use aspose
- recognize text from image
- improve ocr speed
- load image for ocr
- enable automatic language detection
language: ar
og_description: كيفية استخدام Aspose OCR للتعرف بسرعة على النص من الصورة، وتمكين الكشف
  التلقائي عن اللغة، وتحسين سرعة OCR في Java.
og_title: كيفية استخدام Aspose OCR للصور متعددة اللغات
tags:
- Aspose
- OCR
- Java
- Image Processing
title: كيفية استخدام Aspose OCR للصور متعددة اللغات
url: /ar/java/advanced-ocr-techniques/how-to-use-aspose-ocr-for-mixed-language-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام Aspose OCR للصور متعددة اللغات

هل تساءلت يومًا **كيف تستخدم Aspose** لاستخراج النص من صورة تحتوي على عدة لغات في آن واحد؟ لست وحدك—فالمطورون غالبًا ما يواجهون صعوبة عندما تمزج الصورة بين الإنجليزية، الروسية، الهندية أو أي نص آخر. الخبر السار هو أن Aspose OCR يتعامل مع ذلك بسلاسة، ويمكنك حتى **التعرف على النص من الصورة** بشكل أسرع عن طريق تضييق مجموعة اللغات.

في هذا الدرس سنستعرض مثالًا كاملًا وجاهزًا للتنفيذ بلغة Java **يقوم بتحميل الصورة للـ OCR**، ويُفعّل **الكشف التلقائي عن اللغة**، ويظهر حيلة بسيطة لـ **تحسين سرعة OCR**. في النهاية ستحصل على برنامج مستقل يطبع النص المستخرج إلى وحدة التحكم، وستفهم لماذا كل إعداد مهم.

> **المتطلبات المسبقة** – تثبيت Java 17+، Maven أو Gradle لإدارة الاعتمادات، ورخصة Aspose OCR (الإصدار التجريبي المجاني يكفي للتقييم). لا توجد مكتبات أخرى مطلوبة.

---

## الخطوة 1 – إضافة Aspose OCR إلى مشروعك

قبل أن تتمكن من **استخدام Aspose**، تحتاج إلى إضافة المكتبة إلى مسار الفئات الخاص بك. مع Maven يبدو ذلك هكذا:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

إذا كنت تفضل Gradle:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **نصيحة احترافية:** التزم بأحدث إصدار ثابت؛ الإصدارات الأحدث غالبًا ما تتضمن تحسينات في الأداء تؤثر مباشرةً على **تحسين سرعة OCR**.

---

## الخطوة 2 – إنشاء مثيل محرك OCR  

قلب كل سير عمل Aspose OCR هو `OcrEngine`. إنشاءه بسيط، لكن يجدر الإشارة إلى أن المحرك يحتفظ بذاكرات داخلية. إعادة استخدام نفس المثيل عبر عدة صور يمكن أن **يحسن سرعة OCR** لأن المكتبة تتجنب التهيئة الأصلية المتكررة.

```java
import com.aspose.ocr.*;

public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialise the OCR engine – one instance per application is ideal
        OcrEngine ocrEngine = new OcrEngine();
```

---

## الخطوة 3 – **تحميل الصورة للـ OCR**  

Aspose يدعم العديد من صيغ الصور (PNG، JPEG، TIFF، BMP). هنا نوضح تحميل صورة PNG تحتوي على نص بالإنجليزية، الروسية، والهندية. المساعد `ImageStream.fromFile` يج abstracts تفاصيل إدخال/إخراج الملفات ويضمن تدفق الصورة بشكل صحيح إلى المحرك.

```java
        // Step 3: Load the picture that holds mixed languages
        // Replace the path with the actual location of your image file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));
```

> **ماذا لو كانت الصورة في الذاكرة؟** استخدم `ImageStream.fromByteArray(byte[])` بدلاً من ذلك—مثالي لخدمات الويب التي تستقبل الصور كتيارات بايت.

---

## الخطوة 4 – تفعيل الكشف التلقائي عن اللغة  

بشكل افتراضي، يفترض Aspose OCR لغة واحدة، مما قد يؤدي إلى ناتج مشوش في الصور متعددة اللغات. تشغيل الكشف التلقائي يخبر المحرك بفحص نص كل كتلة قبل التعرف.

```java
        // Step 4: Turn on auto‑detect – this is the key to handling mixed‑language images
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

---

## الخطوة 5 – **تحسين سرعة OCR** عن طريق تقليل مجموعة اللغات  

الكشف التلقائي الكامل يفحص كل لغة يدعمها Aspose (أكثر من 70). إذا كنت تعرف اللغات المحتملة مسبقًا، يمكنك إعطاء المحرك إشارة. توفير مصفوفة أصغر يقلل مساحة البحث وبالتالي **يحسن سرعة OCR**.

```java
        // Step 5 (optional but recommended): Limit detection to known languages
        // "en" = English, "ru" = Russian, "hi" = Hindi
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });
```

> **لماذا يساعد ذلك؟** يتخطى المحرك نماذج اللغات التي لا يحتاجها، مما يوفر دورات المعالج والذاكرة. إذا أضفت لغات أخرى لاحقًا، ما عليك سوى تحديث المصفوفة—دون الحاجة لإعادة كتابة الكود.

---

## الخطوة 6 – تنفيذ التعرف و **التعرف على النص من الصورة**  

الآن يبدأ الجزء الثقيل. `recognize()` تُعيد كائن `OcrResult` يحتوي على النص العادي، درجات الثقة، وحتى معلومات التخطيط إذا احتجتها لاحقًا.

```java
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 7: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### ناتج وحدة التحكم المتوقع

```
=== Extracted Text ===
Hello world!
Привет мир!
नमस्ते दुनिया!
```

إذا كانت الصورة تحتوي على ضوضاء إضافية أو نص مائل، قد ترى ثقة أقل لتلك الأسطر. في هذه الحالة، فكر في معالجة مسبقة للصورة (إزالة الميل، التحويل إلى ثنائي) قبل تمريرها إلى Aspose.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو كانت الصورة ضخمة (مثلاً >10 MP)؟

الصور الكبيرة تستهلك المزيد من الذاكرة ويمكن أن تبطئ المعالجة. طريقة سريعة لـ **تحسين سرعة OCR** هي تقليل حجم الصورة مع الحفاظ على قابلية القراءة:

```java
// Example using java.awt for simple resizing (optional)
BufferedImage original = ImageIO.read(new File("large.png"));
int targetWidth = 2000; // adjust based on your needs
BufferedImage resized = new BufferedImage(targetWidth,
        (original.getHeight() * targetWidth) / original.getWidth(),
        BufferedImage.TYPE_INT_RGB);
Graphics2D g = resized.createGraphics();
g.drawImage(original, 0, 0, targetWidth, resized.getHeight(), null);
g.dispose();
ocrEngine.setImage(ImageStream.fromImage(resized));
```

### كيف أتعامل مع النصوص من اليمين إلى اليسار مثل العربية؟

Aspose OCR يحترم تلقائيًا اتجاه النص، لكن قد ترغب في ضبط علامة `RightToLeft` للمعالجة اللاحقة:

```java
ocrEngine.getSettings().setRightToLeft(true);
```

### هل يمكن استخراج النص من ملفات PDF بدلاً من الصور؟

نعم—حوّل كل صفحة PDF إلى صورة (باستخدام Aspose PDF أو أي أداة تحويل) ومرّر النتيجة إلى نفس خط أنابيب OCR. منطق **التعرف على النص من الصورة** يبقى نفسه.

---

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

```java
import com.aspose.ocr.*;
import java.io.File;

/**
 * Demonstrates how to use Aspose OCR to recognize text from an image
 * that contains multiple languages, with automatic language detection
 * and a speed‑optimising language whitelist.
 */
public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine – reuse this instance for many images
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that holds mixed languages (replace with your path)
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));

        // Enable automatic detection of language per text block
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // OPTIONAL: Restrict detection to English, Russian, and Hindi to boost speed
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });

        // Run OCR and capture the result
        OcrResult ocrResult = ocrEngine.recognize();

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

احفظ الملف باسم `MixedLanguageDemo.java`، ثم قم بتجميعه باستخدام `javac`، وشغّله بـ `java MixedLanguageDemo`. إذا تم إعداد كل شيء بشكل صحيح، سترى النص متعدد اللغات مطبوعًا في وحدة التحكم.

---

## الخلاصة

أنت الآن تعرف **كيف تستخدم Aspose** لـ **التعرف على النص من الصورة** التي تحتوي على عدة لغات، وكيفية **تفعيل الكشف التلقائي عن اللغة**، ونصيحة عملية لـ **تحسين سرعة OCR** عن طريق تقليل مجموعة اللغات. الكود الكامل أعلاه جاهز للنسخ‑اللصق، والتوضيحات ستمنحك الثقة لتكييف الحل—سواء كنت تحتاج إلى **تحميل الصورة للـ OCR** من تدفق، أو مصفوفة بايت، أو حتى لقطة من كاميرا ويب.

الخطوات التالية؟ جرّب التجربة مع:

* إضافة معالجة مسبقة للصور (إزالة الضوضاء، التحويل إلى ثنائي) للمسحات ذات الجودة المنخفضة.  
* تصدير `OcrResult` كـ JSON للخدمات اللاحقة.  
* دمج المحرك في نقطة نهاية REST باستخدام Spring Boot بحيث يمكن للعملاء رفع الصور واستلام النص المستخرج فورًا.

برمجة سعيدة، ولتكن خطوط أنابيب OCR الخاصة بك سريعة، دقيقة، ومتعددة اللغات!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}