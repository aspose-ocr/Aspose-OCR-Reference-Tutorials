---
category: general
date: 2026-05-25
description: استخراج النص من الصورة في جافا باستخدام OCR. تعلم كيفية تحميل الصورة
  للـ OCR، التعرف على النص من الصورة، والحصول على النص من OCR باستخدام مثال كود بسيط.
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: ar
og_description: استخراج النص من الصورة في جافا مع دليل خطوة بخطوة. تعلّم كيفية تحميل
  الصورة للتعرف الضوئي على الأحرف، التعرف على النص من الصورة، والحصول على النص من
  OCR بكفاءة.
og_title: استخراج النص من الصورة في جافا – الحصول على النص من التعرف الضوئي على الأحرف
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  headline: Extract Text from Image in Java – Get Text from OCR
  type: TechArticle
- description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  name: Extract Text from Image in Java – Get Text from OCR
  steps:
  - name: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
    text: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
  - name: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
    text: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
  - name: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
    text: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
  - name: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
    text: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
  - name: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
    text: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: استخراج النص من الصورة في جافا – الحصول على النص من OCR
url: /ar/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من صورة في جافا – الحصول على النص من OCR

هل احتجت يومًا إلى **استخراج النص من صورة** لكن لم تكن متأكدًا أي مكتبة جافا تختار؟ لست وحدك. سواءً كنت تقوم برقمنة الإيصالات، أو استخراج أرقام السيريال من صور المنتجات، أو مجرد تجربة مشروع جانبي ممتع، تحويل الصورة إلى نص قابل للتحرير هو عائق شائع.

في هذا الدرس سنستعرض مثالًا كاملاً جاهزًا للتنفيذ يوضح لك كيفية **تحميل الصورة لـ OCR**، وتكوين المحرك، وأخيرًا **التعرف على النص من الصورة** حتى تتمكن من **الحصول على النص من OCR** ببضع أسطر من الشيفرة فقط. لا مراجع غامضة—كل ما تحتاجه موجود هنا.

## ما ستتعلمه

* كيفية إعداد محرك OCR خفيف الوزن في جافا.  
* الخطوات الدقيقة لـ **تحميل الصورة لـ OCR** ومعالجة مسارات الملفات المختلفة.  
* لماذا يهم ضبط اللغة عندما تريد **استخراج النص من صورة** ليست بالإنجليزية.  
* كيفية إخراج النتيجة بأمان وماذا تفعل عندما لا يُرجع المحرك أي شيء.  
* مجموعة من النصائح الاحترافية لتجنب أكثر الأخطاء شيوعًا.

بنهاية هذا الدليل سيكون لديك برنامج مستقل يقرأ ملف JPEG (أو PNG) يحتوي على أحرف أوكرانية ويطبع السلسلة المعترف بها إلى وحدة التحكم. لا تتردد في تغيير اللغة أو الصورة—كل شيء مُصمم كوحدات قابلة للتبديل.

---

![Diagram showing the flow of extracting text from image using Java OCR engine](/images/extract-text-from-image-java.png)

*نص بديل: مخطط تدفق عملية استخراج النص من صورة باستخدام محرك OCR في جافا.*

## المتطلبات المسبقة

* **Java Development Kit (JDK) 11+** – يستخدم الكود نظام الوحدات الحديث، لكن الإصدارات الأقدم تعمل مع بعض التعديلات البسيطة.  
* **Maven أو Gradle** – لجلب مكتبة OCR (سنستخدم **Asprise OCR** كخيار خفيف ومجاني للتطوير).  
* ملف صورة تجريبي (مثلاً `ukrainian_sign.jpg`) موجود في مكان يمكن للبرنامج قراءته.  
* إلمام أساسي بطريقة `main` في جافا ومعالجة الاستثناءات.

إذا كان لديك كل ما سبق فأنت جاهز للبدء. وإلا، احصل على JDK من Oracle أو AdoptOpenJDK وأعد مشروع Maven بسيط—ليس هناك شيء معقد.

---

## الخطوة 1: إضافة تبعية OCR

أولًا، أخبر أداة البناء الخاصة بك بجلب محرك OCR. بالنسبة لـ Maven، ضع هذا داخل `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

إذا كنت تفضّل Gradle، فالمكافئ هو:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

هذه الإحداثيات تجلب ملف JAR مضغوط يحتوي على `OcrEngine`، `OcrLanguage`، والفئات المساعدة التي سنستخدمها. لا تحتاج إلى ملفات تنفيذية أصلية إضافية للخطوط اللاتينية والسيريلية الأساسية.

---

## الخطوة 2: إنشاء فئة جافا **استخراج النص من صورة**

الآن سنكتب البرنامج الفعلي. احفظ التالي باسم `ExtractTextDemo.java` داخل `src/main/java/com/example/ocr/`.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;

/**
 * Demonstrates how to extract text from image using Asprise OCR.
 * The example loads a JPEG, sets the language to Ukrainian,
 * runs recognition, and prints the result.
 */
public class ExtractTextDemo {

    public static void main(String[] args) {
        // ---- 1️⃣  Initialize the OCR engine ---------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---- 2️⃣  Configure the engine to recognize Ukrainian text -----------
        // This is crucial if your image contains non‑Latin characters.
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.UKRAINIAN);

        // ---- 3️⃣  Load the image that contains Ukrainian characters ----------
        // Replace the path with the location of your own picture.
        String imagePath = "YOUR_DIRECTORY/ukrainian_sign.jpg";
        try {
            ocrEngine.getImage().loadFromFile(imagePath);
        } catch (Exception e) {
            System.err.println("Failed to load image: " + e.getMessage());
            return;
        }

        // ---- 4️⃣  Perform OCR recognition and obtain the extracted text -------
        String recognizedText;
        try {
            recognizedText = ocrEngine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Recognition error: " + e.getMessage());
            return;
        }

        // ---- 5️⃣  Output the recognized text to the console -------------------
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### لماذا يعمل هذا الهيكل

* **كتل مرقمة منفصلة** تجعل التدفق سهل المتابعة، خاصةً عندما تبحث عن مكان **تحميل الصورة لـ OCR** أو **التعرف على النص من الصورة**.  
* الـ `try/catch` حول تحميل الصورة والتعرف يضمن فشل البرنامج بطريقة لطيفة—مفيد عندما يكون مسار الملف خاطئًا أو لا يجد محرك OCR بيانات اللغة.  
* ضبط اللغة مبكرًا (الخطوة 2) يحسن الدقة بشكل كبير للخطوط غير الإنجليزية. إذا احتجت لاحقًا إلى **java image to text** للغات أخرى، ما عليك سوى استبدال `OcrLanguage.UKRAINIAN` بـ `OcrLanguage.ENGLISH` أو `FRENCH`، إلخ.

---

## الخطوة 3: بناء وتشغيل البرنامج

من جذر المشروع، نفّذ:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

أو إذا كنت تستخدم Gradle:

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

بافتراض أن `ukrainian_sign.jpg` يحتوي على النص *«Ласкаво просимо»* (الأوكرانية لـ “Welcome”)، يجب أن ترى شيءًا مشابهًا لـ:

```
=== OCR Result ===
Ласкаво просимо
```

هذا الإخراج يؤكد أنك نجحت في **استخراج النص من صورة** و**الحصول على النص من OCR** في تشغيل واحد.

---

## الخطوة 4: تعديل سير العمل – من **Java Image to Text** في المشاريع الحقيقية

على الرغم من أن العرض التجريبي بسيط، فإن التطبيقات الواقعية غالبًا ما تحتاج إلى المزيد:

| السيناريو | ما الذي يجب تعديله | السبب |
|----------|-------------------|--------|
| **معالجة دفعات** | تكرار عبر `List<Path>` وتخزين كل نتيجة في قاعدة بيانات. | يقلل العمل اليدوي عندما يكون لديك مئات الصور. |
| **صيغ صور مختلفة** | استخدم `ImageIO.read(new File(path))` للمعالجة المسبقة، ثم مرّر `BufferedImage` إلى `ocrEngine.getImage().loadFromBufferedImage(bufImg)`. | يدعم PNG، BMP، أو حتى PDFs بعد التحويل. |
| **تحسين الأداء** | استدعِ `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)` إذا كنت تقبل دقة أقل قليلاً. | يسرّع التعرف على الأجهزة منخفضة المواصفات. |
| **ما بعد المعالجة** | قص الفراغات، استبدال الأخطاء الشائعة في OCR (`0` → `O`, `1` → `I`). | يحسّن جودة البيانات للخطوات اللاحقة. |

هذه التعديلات تحافظ على الفكرة الأساسية—**التعرف على النص من الصورة**—مع إتاحة مرونة أكبر للبيئات الإنتاجية.

---

## الأخطاء الشائعة ونصائح احترافية

1. **إعداد لغة خاطئ** – إذا نسيت الخطوة 2، سيستخدم المحرك الإنجليزية افتراضيًا، مما يحول الأحرف السيريلية إلى رموز غير مفهومة. تأكد دائمًا من رمز اللغة.  
2. **جودة الصورة مهمة** – الصور منخفضة الدقة أو الضبابية تقلل الدقة. عالج مسبقًا بزيادة التباين أو التحويل إلى أبيض وأسود إذا لزم الأمر.  
3. **مشكلات مسار الملف** – في Windows، يجب هروب الشرطات المائلة العكسية (`C:\\images\\file.jpg`). استخدام `Path.of(...)` من `java.nio.file` يتجاوز هذه المشكلة.  
4. **تسرب الذاكرة** – `OcrEngine` يحتفظ بموارد أصلية. استدعِ `ocrEngine.dispose()` عند الانتهاء، خاصةً في الخدمات طويلة التشغيل.  
5. **سلامة الخيوط** – المحرك غير آمن للاستخدام المتعدد الخيوط بشكل افتراضي. أنشئ نسخة منفصلة لكل خيط أو قم بمزامنة الوصول.

---

## مثال كامل يعمل (كل شيء في ملف واحد)

فيما يلي ملف واحد يمكنك نسخه ولصقه في أي بيئة تطوير. يتضمن استدعاء `dispose()` وطريقة مساعدة صغيرة لجعل الشيفرة أكثر نظافة.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;
import java.nio.file.Path;

/**
 * Complete, runnable demo that extracts text from an image using Java OCR.
 */
public class FullDemo {

    public static void main(String[] args) {
        // Path to the image – change this to your own file.
        Path imgPath = Path.of("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Run the OCR workflow and capture the output.
        String result = extractTextFromImage(imgPath, OcrLanguage.UKRAINIAN);
        if (result != null) {
            System.out.println("=== OCR Result ===");
            System.out.println(result);
        }
    }

    /**
     * Core method that encapsulates the 5‑step OCR process.
     *
     * @param imagePath Path to the image file.
     * @param language  Desired OCR language.
     * @return Recognized text, or {@code null} if something went wrong.
     */
    private static String extractTextFromImage(Path imagePath, OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        try {
            // 1️⃣ Set language
            engine.getEngineOptions().setLanguage(language);

            // 2️⃣ Load image
            engine.getImage().loadFromFile(imagePath.toString());

            // 3️⃣ Recognize and return text
            return engine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Error during OCR: " + e.getMessage());
            return null;
        } finally {
            // 4️⃣ Release native resources
            engine.dispose();
        }
    }
}
```

تشغيل هذا البرنامج ينتج نفس الإخراج الموضح سابقًا. لا تتردد في استبدال `OcrLanguage.UKRAINIAN` بـ `OcrLanguage.ENGLISH` أو أي لغة مدعومة أخرى لتلاحظ كيف يتكيف المحرك.

---

## الخلاصة

لقد استعرضنا كل ما تحتاجه لتقوم بـ **استخراج النص من صورة** باستخدام جافا: من إضافة تبعية OCR، إلى **تحميل الصورة لـ OCR**،

## دروس ذات صلة

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}