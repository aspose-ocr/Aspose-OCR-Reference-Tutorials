---
category: general
date: 2026-04-29
description: تعلم كيفية التعرف الضوئي على الحروف (OCR) لملفات TIFF باستخدام وضع البث
  في Aspose OCR. يوضح لك هذا الدليل كيفية استخراج مربعات النص من صور TIFF المتقطعة
  بكفاءة.
draft: false
keywords:
- how to ocr tiff
- extract text tiles
language: ar
og_description: كيفية إجراء OCR لملفات TIFF باستخدام Aspose OCR Streaming. كود خطوة
  بخطوة لاستخراج قطع النص من صور TIFF الكبيرة.
og_title: كيفية التعرف الضوئي على الأحرف في ملفات TIFF – دليل البث الكامل
tags:
- OCR
- Java
- Aspose
- TIFF
title: كيفية إجراء OCR لملفات TIFF – بث ملفات TIFF الكبيرة واستخراج قطع النص في جافا
url: /ar/java/advanced-ocr-techniques/how-to-ocr-tiff-stream-large-tiffs-and-extract-text-tiles-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف الضوئي على النص في ملفات TIFF – بث ملفات TIFF الكبيرة واستخراج قطع النص في Java

هل تساءلت يومًا **how to ocr tiff** عن ملفات TIFF الكبيرة جدًا بحيث لا يمكن تحميلها في الذاكرة دفعة واحدة؟ لست وحدك. يواجه العديد من المطورين عقبة عندما تُقسم صور TIFF إلى عشرات القطع، وتفشل المكالمة المعتادة `ocrEngine.recognize()`.

الأخبار السارة؟ وضع البث في Aspose OCR يتيح لك إمداد كل قطعة كتيار منفصل، بحيث يمكنك **extract text tiles** دون استهلاك الذاكرة بالكامل. في هذا الدرس سنستعرض مثالًا كاملاً وجاهزًا للتنفيذ بلغة Java، نشرح لماذا كل سطر مهم، ونشير إلى الأخطاء التي يجب تجنبها.

> **ما ستحصل عليه:** برنامج قابل للتنفيذ يدمج ملفات TIFF المجزأة أثناء التشغيل، يطبع النص المدمج، ويظهر لك كيفية تعديل الكود للغات أو صيغ صور أخرى.

---

## المتطلبات المسبقة

- **Java 17** أو أحدث (الكود يستخدم `try‑with‑resources`، لذا يعمل على JDK 8+، لكن JDK 17 هو الإصدار طويل الأمد الحالي).
- مكتبة **Aspose.OCR for Java** (الإصدار v23.10 أو أحدث). أضفها عبر Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- مجلد يحتوي على قطع TIFF الفردية (مثال: `tile_0.tif`, `tile_1.tif`, …).  
- اختياريًا: بيئة تطوير متكاملة مثل IntelliJ IDEA أو VS Code – لكن محرر نصوص بسيط يكفي.

---

## الخطوة 1 – إعداد مسارات القطع (لماذا هذا مهم)

قبل أن يتمكن محرك OCR من فعل أي شيء، يحتاج إلى معرفة مكان كل جزء من الصورة. كتابة المسارات يدوياً مقبولة للعرض التجريبي، لكن في الإنتاج قد تحتاج إلى مسح دليل أو قراءة ملف بيان.

```java
// Define the absolute or relative paths to each TIFF tile
String[] tilePaths = {
    "YOUR_DIRECTORY/tile_0.tif",
    "YOUR_DIRECTORY/tile_1.tif",
    "YOUR_DIRECTORY/tile_2.tif"
};
```

> **نصيحة احترافية:** احفظ القطع بترتيب لغوي (0, 1, 2…) لأن المحرك سيجمع النص المعترف به بنفس تسلسل تدفق التيارات.

---

## الخطوة 2 – تفعيل وضع البث على محرك OCR (الكلمة المفتاحية الأساسية)

الآن نقوم بإنشاء كائن `OcrEngine` ونفعل البث. هذا هو جوهر **how to ocr tiff** دون تحميل الصورة بالكامل في الذاكرة.

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Activate streaming – essential for large or tiled TIFFs
ocrEngine.getProcessingSettings().setEnableStreaming(true);

// Set the language to English; change as needed (e.g., "fr", "de")
ocrEngine.getLanguageSettings().setLanguage("en");
```

**لماذا البث؟**  
عند استدعاء `setEnableStreaming(true)`، يتعامل المحرك مع كل `ImageStream` وارد كاستمرار للتيار السابق. يبني لوحة افتراضية داخلية، يدمج القطع افتراضيًا، ويجري OCR مرة واحدة في النهاية. هذا يتجنب خطأ “OutOfMemoryError” الذي سيظهر إذا حاولت تحميل ملف TIFF متعدد الجيجابايت دفعة واحدة.

---

## الخطوة 3 – إلحاق كل قطعة كتيار إدخال (الكلمة المفتاحية الثانوية)

إليك الحلقة التي تغذي كل قطعة إلى المحرك. يضمن بلوك `try‑with‑resources` إغلاق مقبض الملف بسرعة، وهو أمر حاسم عند التعامل مع عشرات الملفات.

```java
for (String tilePath : tilePaths) {
    try (InputStream stream = new FileInputStream(tilePath)) {
        // Wrap the raw InputStream in Aspose's ImageStream wrapper
        ocrEngine.appendImage(ImageStream.fromStream(stream));
    } catch (IOException e) {
        // If a single tile fails, we log and continue – you might want to abort instead
        System.err.println("Failed to load tile: " + tilePath);
        e.printStackTrace();
    }
}
```

لاحظ أن عبارة **extract text tiles** مدمجة بطبيعية: كل تكرار *يستخرج* النص من قطعة ويضيفه إلى مجموعة النتائج المتزايدة.

---

## الخطوة 4 – تشغيل التعرف وإخراج النص المدمج (الكلمة المفتاحية الأساسية)

بعد إضافة جميع القطع إلى القائمة، يتم استدعاء واحد لتنفيذ OCR على الصورة الافتراضية. النتيجة تحتوي على النص الكامل، كما لو كان لديك ملف TIFF ضخم واحد.

```java
// Perform OCR on the combined virtual image
OcrResult ocrResult = ocrEngine.recognize();

// Print the extracted text to the console
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**الناتج المتوقع** (بافتراض أن القطع تحتوي على العبارة “Hello World” مقسمة بينها):

```
=== OCR Output ===
Hello World
```

إذا احتوت قطعك على مزيد من الأسطر، فستظهر بالترتيب نفسه الذي قدمته. يمكنك أيضًا كتابة `ocrResult.getText()` إلى ملف لمعالجة لاحقة.

---

## الخطوة 5 – مثال كامل قابل للتنفيذ (جميع الخطوات في مكان واحد)

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في `StreamingExample.java`. يتضمن جميع الاستيرادات، التعليقات، ومعالجة الأخطاء.

```java
import com.aspose.ocr.*;
import java.io.*;

public class StreamingExample {
    public static void main(String[] args) throws Exception {
        // ------------------------------------------------------------
        // Step 1: List the TIFF tile files
        // ------------------------------------------------------------
        String[] tilePaths = {
            "YOUR_DIRECTORY/tile_0.tif",
            "YOUR_DIRECTORY/tile_1.tif",
            "YOUR_DIRECTORY/tile_2.tif"
        };

        // ------------------------------------------------------------
        // Step 2: Set up the OCR engine in streaming mode
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getProcessingSettings().setEnableStreaming(true);
        ocrEngine.getLanguageSettings().setLanguage("en");

        // ------------------------------------------------------------
        // Step 3: Feed each tile as a separate stream
        // ------------------------------------------------------------
        for (String tilePath : tilePaths) {
            try (InputStream stream = new FileInputStream(tilePath)) {
                ocrEngine.appendImage(ImageStream.fromStream(stream));
            } catch (IOException e) {
                System.err.println("Unable to read tile: " + tilePath);
                e.printStackTrace();
                // Optionally: return; // abort on missing tile
            }
        }

        // ------------------------------------------------------------
        // Step 4: Recognize the combined image and display the text
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

احفظ، ثم قم بالترجمة والتنفيذ:

```bash
javac -cp "path/to/aspose-ocr.jar" StreamingExample.java
java -cp ".:path/to/aspose-ocr.jar" StreamingExample
```

يجب أن ترى النص المدمج من OCR يُطبع على وحدة التحكم.

---

## نصائح متقدمة ومشكلات شائعة (لماذا هذا يعمل)

| المشكلة | لماذا يحدث | كيفية الإصلاح / التحسين |
|-------|----------------|-----------------------|
| **أخطاء الذاكرة (Out‑of‑memory errors)** | تحميل TIFF بحجم كامل إلى `BufferedImage` يستهلك كامل الذاكرة. | استخدم وضع البث (`setEnableStreaming(true)`) – المحرك لا يُنشئ الصورة كاملة أبدًا. |
| **اختلاف ترتيب القطع** | الملفات تُرتب أبجديًا بدلاً من الترتيب الرقمي (مثال: `tile_10.tif` قبل `tile_2.tif`). | أضف أصفارًا بادئة للأرقام (`tile_00.tif`, `tile_01.tif`) أو رتب برمجيًا باستخدام `Comparator`. |
| **اللغة الخاطئة** | OCR يفرض الإنجليزية افتراضيًا؛ النص غير الإنجليزي يصبح مشوشًا. | استدعِ `ocrEngine.getLanguageSettings().setLanguage("fr")` (أو أي رمز ISO مدعوم). |
| **فشل جزئي** | قطعة واحدة تالفة توقف العملية بأكملها. | امسك `IOException` لكل قطعة، سجلها، وقرّر ما إذا كنت ستستمر أو تتوقف. |
| **عنق زجاجة الأداء** | إدخال/إخراج القرص يهيمن عند قراءة العديد من الملفات الصغيرة. | اجمع القطع في ملف ZIP وابث من الذاكرة، أو استخدم SSD سريع. |

---

## متى تستخدم البث مقابل OCR على صورة واحدة

- **البث** مثالي لـ:
  - ملفات TIFF متعددة الصفحات أو المسحات ذات الجيجابكسل.
  - الحالات التي تكون فيها الذاكرة محدودة (مثل حاويات Docker، الأجهزة المحمولة).
  - خطوط الأنابيب التي تستقبل بالفعل أجزاء الصورة (مثل تدفقات الكاميرا).

- **OCR على صورة واحدة** يناسب:
  - ملفات PNG/JPEG الصغيرة (< 5 MB).
  - عمليات المسح الفردية حيث البساطة تفوق الأداء.

---

## الخلاصة

أصبح لديك الآن فهم قوي لـ **how to ocr tiff** باستخدام إمكانيات البث في Aspose OCR، وتعرف كيف **extract text tiles** بفعالية. الحل الكامل—تهيئة المحرك، تفعيل البث، إلحاق كل قطعة، وأخيرًا التعرف على اللوحة الافتراضية—يغطي “ماذا”، “لماذا”، و“كيف” تحتاجه لكتابة كود جاهز للإنتاج.

ما الخطوة التالية؟ جرّب استبدال `"en"` بلغة أخرى، أو جرب صيغ صور مختلفة (`.png`, `.jpg`). يمكنك أيضًا تمرير نتيجة OCR مباشرة إلى فهرس بحث أو مولد PDF. النمط يبقى نفسه: بث، دمج، تعرف.

هل لديك أسئلة حول توسيع العملية لمئات القطع، أو تحتاج مساعدة في معالجة الأخطاء؟ اترك تعليقًا أدناه، وتمنياتنا لك بالبرمجة السعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}