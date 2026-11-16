---
category: general
date: 2026-05-03
description: استخراج الجداول من الصورة باستخدام Aspose OCR Java. تعلم كيفية تحميل
  الصورة للتعرف الضوئي على الأحرف، استخراج الجدول من ملف PNG، تحويل نص جدول الصورة،
  والتعرف بسرعة على صورة الفاتورة.
draft: false
keywords:
- extract tables from image
- extract table from png
- load image for ocr
- convert image table text
- recognize receipt image
language: ar
og_description: استخراج الجداول من الصورة باستخدام Aspose OCR Java. يوضح هذا الدليل
  كيفية تحميل الصورة للتعرف الضوئي على الأحرف، استخراج الجدول من ملف PNG، تحويل نص
  جدول الصورة، والتعرف على صورة الإيصال.
og_title: استخراج الجداول من الصورة – دليل Aspose OCR للغة Java
tags:
- Aspose OCR
- Java
- Image Processing
title: استخراج الجداول من الصورة – دليل Aspose OCR الكامل لجافا
url: /ar/python-java/general/extract-tables-from-image-complete-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج الجداول من الصورة – دليل Aspose OCR الكامل للـ Java

هل احتجت يوماً إلى **استخراج الجداول من ملفات الصورة** لكنك واجهت صعوبة؟ ربما لديك إيصال ممسوح ضوئياً أو فاتورة مصورة وتكون البيانات الجدولية مخبأة داخل ملف PNG. في هذا الدرس ستتعرف بالضبط على كيفية *تحميل الصورة للـ OCR*، تحويل تلك الصورة إلى صفوف منظمة، و **تحويل نص جدول الصورة** إلى شيء يمكنك العمل معه في Java.  

سنستعرض كل خطوة، من ترخيص محرك Aspose OCR إلى طباعة كل خلية من الجداول المكتشفة. في النهاية ستتمكن من **التعرف على صورة إيصال** واستخراج جداولها دون عناء.

## ما ستتعلمه

- كيفية تهيئة محرك Aspose OCR وتطبيق الترخيص.
- لماذا تمكين كشف الجداول هو المفتاح لـ **استخراج الجداول من الصورة**.
- الكود الدقيق المطلوب لـ **تحميل الصورة للـ OCR** وتشغيل التعرف على ملف PNG.
- طرق التعامل مع جداول متعددة، مسحات منخفضة الدقة، والمشكلات الشائعة.
- كيفية **تحويل نص جدول الصورة** إلى صيغة قابلة للطباعة (أو جاهزة لقاعدة البيانات).

لا حاجة لأي وثائق خارجية—كل ما تحتاجه موجود هنا.

## المتطلبات المسبقة

- Java 17 أو أحدث (الكود يستخدم نظام الوحدات الحديث).
- ملف ترخيص Aspose OCR for Java (`Aspose.OCR.Java.lic`). إذا كنت تجرب فقط، فإن مفتاح التقييم المؤقت يعمل كذلك.
- صورة PNG تحتوي على جدول واضح (مثال: `receipt_with_table.png`).  
- Maven أو Gradle لجلب تبعية Aspose OCR:

```xml
<!-- Maven snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

> **نصيحة احترافية:** احفظ ملف الترخيص بجوار مجلد `src/main/resources` حتى يبقى المسار ثابتاً عبر البيئات.

---

## الخطوة 1 – تهيئة محرك OCR لـ **استخراج الجداول من الصورة**

قبل أن يتمكن المحرك من أي شيء، يحتاج إلى معرفة أنك مستخدم مرخص.

```java
import com.aspose.ocr.*;

public class TableExtractor {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Apply your Aspose OCR license – this removes evaluation watermarks
        License license = new License();
        license.setLicense("Aspose.OCR.Java.lic");
        ocrEngine.setLicense(license);
```

*لماذا هذا مهم:* بدون ترخيص صالح يعمل محرك OCR في وضع التجربة، مما قد يقتطع النتائج أو يضيف علامات مائية غير مرغوبة—مما يجعل استخراج الجداول غير موثوق.

---

## الخطوة 2 – تمكين كشف الجداول (**استخراج جدول من PNG**)

كشف الجداول غير مفعل افتراضياً؛ عليك تشغيله.

```java
        // Step 2: Turn on table detection so the engine looks for tabular structures
        ocrEngine.getConfig().setEnableTableDetection(true);
```

تفعيل هذا العلم يخبر Aspose OCR بمعاملة مجموعات النص المتراصة كصفوف وأعمدة، وهو بالضبط ما تحتاجه عندما تريد **استخراج الجداول من الصورة** التي تكون ملفات PNG.

---

## الخطوة 3 – **تحميل الصورة للـ OCR** و **التعرف على صورة إيصال**

الآن نقوم بتمرير الصورة إلى المحرك.

```java
        // Step 3: Load the PNG that contains the table
        // You can also use Image.fromStream(...) for in‑memory data
        Image inputImage = Image.fromFile("YOUR_DIRECTORY/receipt_with_table.png");

        // Run the recognition process – this returns an OcrResult object
        OcrResult ocrResult = ocrEngine.recognize(inputImage);
```

إذا كنت تتعامل مع سيناريو **التعرف على صورة إيصال**، قد ترغب في معالجة مسبقة للصورة (إزالة الميل، زيادة التباين). هذا خارج نطاق هذا الدليل السريع لكنه يستحق الاستكشاف للماسحات الضوضائية.

---

## الخطوة 4 – معالجة نتيجة OCR و **تحويل نص جدول الصورة**

قد يحتوي كائن `OcrResult` على جدول واحد أو أكثر. لنقُم بالتكرار عليه وطباعة كل خلية.

```java
        // Step 4: Iterate over every detected table
        if (ocrResult.getTables().isEmpty()) {
            System.out.println("No tables were detected. Try improving image quality.");
            return;
        }

        for (Table table : ocrResult.getTables()) {
            System.out.println("Table detected:");
            for (TableRow row : table.getRows()) {
                // Join each cell's text with a tab for easy copy‑paste
                String line = row.getCells()
                                 .stream()
                                 .map(Cell::getText)
                                 .reduce((a, b) -> a + "\t" + b)
                                 .orElse("");
                System.out.println(line);
            }
            System.out.println(); // Blank line between tables
        }
    }
}
```

**ما يفعله هذا:**  

- يتحقق ما إذا تم العثور على أي جداول؛ إذا لم يكن كذلك، يقترح تعديل الجودة.  
- لكل جدول، يطبع الصفوف مع خلايا مفصولة بعلامات تبويب، وهو تنسيق ملائم لاستيراد CSV.  
- استدعاء `Cell::getText` هو جوهر **تحويل نص جدول الصورة** – فهو يجلب النص الأصلي من كل خلية.

### النتيجة المتوقعة

بافتراض أن `receipt_with_table.png` يحتوي على جدول بسيط 3 × 2، سترى شيئاً مثل:

```
Table detected:
Item	Quantity
Apple	2
Banana	5
```

إذا كانت الصورة تحتوي على جداول متعددة، سيُفصل كل جدول بسطر فارغ.

---

## الخطوة 5 – التحقق من الجداول المستخرجة ومعالجة الحالات الخاصة

### المشكلات الشائعة

| المشكلة | لماذا يحدث | الحل السريع |
|-------|------------|------------|
| **لم يتم اكتشاف أي جداول** | الصورة غير واضحة أو ذات تباين منخفض | تطبيق التحويل الثنائي (`ImageProcessing.applyThreshold`) قبل OCR |
| **خلايا مدمجة** | خطوط الجدول ضعيفة، فيعاملها OCR ككتلة واحدة | زيادة `TableDetectionSensitivity` في `ocrEngine.getConfig()` |
| **ترتيب الأعمدة غير صحيح** | صورة مائلة تسبب عدم محاذاة | استخدم `ImageProcessing.deskew` أو قم بتدوير الصورة 90° |

### ما الخطوة التالية

- **تصدير إلى CSV** – استبدل `System.out.println(line);` بـ `FileWriter` لحفظ البيانات.  
- **إدخال إلى قاعدة بيانات** – اربط كل صف بـ POJO واستخدم JPA للحفظ.  
- **دمج مع واجهات برمجة أخرى** – لمعالجة الإيصالات يمكنك أيضاً استخراج الإجماليات باستخدام تعبيرات regex على نص OCR.

---

## مثال كامل يعمل (جاهز للنسخ واللصق)

```java
import com.aspose.ocr.*;

public class TableExtractor {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine and apply license
        OcrEngine ocrEngine = new OcrEngine();
        License license = new License();
        license.setLicense("Aspose.OCR.Java.lic");
        ocrEngine.setLicense(license);

        // Enable table detection – crucial for extracting tables from image
        ocrEngine.getConfig().setEnableTableDetection(true);

        // Load the PNG image (replace with your actual path)
        Image inputImage = Image.fromFile("YOUR_DIRECTORY/receipt_with_table.png");

        // Recognize the image – this step performs OCR on the whole picture
        OcrResult ocrResult = ocrEngine.recognize(inputImage);

        // Verify we have tables; otherwise suggest a quality fix
        if (ocrResult.getTables().isEmpty()) {
            System.out.println("No tables were detected. Try improving image quality.");
            return;
        }

        // Print each table row by row, converting image table text into tab‑separated values
        for (Table table : ocrResult.getTables()) {
            System.out.println("Table detected:");
            for (TableRow row : table.getRows()) {
                String line = row.getCells()
                                 .stream()
                                 .map(Cell::getText)
                                 .reduce((a, b) -> a + "\t" + b)
                                 .orElse("");
                System.out.println(line);
            }
            System.out.println(); // Blank line between tables
        }
    }
}
```

شغّل هذا البرنامج، ووجّهّه إلى ملف PNG يحتوي على جدول واضح، وسترى وحدة التحكم تمتلئ بصفوف منسقة بشكل أنيق.

---

## الخلاصة

أصبح لديك الآن حل شامل من البداية إلى النهاية لـ **استخراج الجداول من الصورة** باستخدام Aspose OCR للـ Java. من الترخيص إلى **تحميل الصورة للـ OCR**، تمكين **استخراج جدول من PNG**، وأخيراً **تحويل نص جدول الصورة**، كل خطوة مغطاة بشرح ونصائح عملية.  

بعد ذلك، جرّب ربط الناتج بملف CSV، أو دفع الصفوف إلى قاعدة بيانات علائقية، أو دمج خطوة OCR مع روتين استخراج إجمالي الإيصال. نفس النمط يعمل مع الفواتير، قوائم الأسعار، وأي مستند ممسوح يحتوي على بيانات مخفية خلف شبكة.

هل لديك أسئلة حول التعامل مع إيصالات منخفضة الدقة أو توسيع هذا إلى معالجة دفعات؟ اترك تعليقاً أدناه، ونتمنى لك برمجة سعيدة!  

![مثال لاستخراج الجداول من الصورة](https://example.com/assets/extract-tables-from-image.png "استخراج الجداول من الصورة – مثال النتيجة")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}