---
category: general
date: 2026-01-02
description: استخراج النص من الصورة باستخدام Aspose OCR في Java – تعلم كيفية استخراج
  رقم VIN، واكتشاف رقم تعريف المركبة، وقراءة VIN من الصورة بسرعة.
draft: false
keywords:
- extract text from image
- how to extract vin
- detect vehicle identification number
- recognize text region
- read vin from photo
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR في Java. يوضح هذا الدليل
  كيفية استخراج رقم VIN، واكتشاف رقم تعريف المركبة، وقراءة VIN من الصورة.
og_title: استخراج النص من الصورة باستخدام جافا – قراءة رقم VIN من الصورة
tags:
- OCR
- Java
- Aspose
- Vehicle Identification Number
title: استخراج النص من الصورة باستخدام جافا – قراءة رقم VIN من الصورة
url: /ar/java/advanced-ocr-techniques/extract-text-from-image-with-java-read-vin-from-photo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من صورة باستخدام Java – قراءة رقم VIN من الصورة

هل احتجت يومًا إلى **استخراج النص من صورة** لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك. سواء كنت تبني نظامًا لإدارة الأسطول أو تريد فقط مسح رقم VIN لسيارة لمشروع هواية، فإن استخراج رقم تعريف المركبة من صورة يُعد نقطة ألم شائعة. في هذا الدرس سنُظهر لك **كيفية استخراج VIN** باستخدام Aspose OCR للغة Java، وسنغطي أيضًا **كيفية اكتشاف رقم تعريف المركبة** في منطقة محددة من الصورة.

فكر في الأمر هكذا: الصورة هي حشد صاخب، والـ VIN هو الصديق الذي تحاول العثور عليه. من خلال إخبار محرك OCR بالضبط أين يبحث — باستخدام **منطقة التعرف على النص** — ستحقق تحسينًا كبيرًا في الدقة والسرعة. جاهز؟ لنبدأ.

## ما الذي ستحتاجه

قبل أن نغوص في التفاصيل، تأكد من توفر ما يلي:

- **Java Development Kit (JDK) 8+** – أي نسخة حديثة تعمل.
- مكتبة **Aspose OCR for Java** (أحدث نسخة حتى 2026‑01‑02، مثل `aspose-ocr-23.8.jar`).
- ملف صورة يحتوي على VIN واضح (مثال: `car_photo.jpg`).
- بيئة تطوير مفضلة أو محرر نص بسيط وواجهة طرفية.

هذا كل شيء — لا أطر عمل ثقيلة، ولا مفاتيح سحابة. مجرد Java عادي وملف JAR واحد.

## الخطوة 1 – إعداد المشروع واستيراد Aspose OCR

أولًا، نحتاج إلى جعل فئات OCR متاحة في الكود. إذا كنت تستخدم Maven، أضف الاعتماد التالي:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.8</version>
</dependency>
```

إذا كنت تفضل الطريقة اليدوية، ضع `aspose-ocr-23.8.jar` في مجلد `libs` الخاص بالمشروع وأضفه إلى مسار الفئات (classpath).

> **نصيحة احترافية:** احتفظ بالملف JAR بجوار مجلد `src`؛ فهذا يجنبك مشاكل مسار الفئات لاحقًا.

## الخطوة 2 – تعريف منطقة الاهتمام (ROI) التي تحتوي على VIN

معظم صور السيارات يكون فيها VIN مطبوعًا في موضع متوقع — عادةً قرب الزجاج الأمامي أو باب جانب السائق. بإخبار محرك OCR *بالضبط* أين يبحث، نقلل من الإيجابيات الزائفة. في Java، تُعبّر ROI باستخدام `java.awt.Rectangle`.

```java
// Step 2: Define the ROI where the VIN lives (x, y, width, height) in pixels
Rectangle vinRegion = new Rectangle(120, 450, 400, 80);
```

لماذا هذه الأرقام؟ إنها مجرد مثال؛ سيتعين عليك تعديلها بناءً على دقة صورتك. الفكرة الأساسية هي **منطقة التعرف على النص** التي تحيط بالـ VIN بإحكام، ولا شيء أكثر.

## الخطوة 3 – تهيئة محرك Aspose OCR

الآن نقوم بتشغيل المحرك. فئة `AsposeOCR` خفيفة ولا تتطلب ترخيصًا للتقييم، لكن للإنتاج ستحتاج إلى ملف ترخيص صالح.

```java
// Step 3: Create an Aspose OCR engine instance
AsposeOCR ocrEngine = new AsposeOCR();
```

إذا كان لديك ملف ترخيص (`Aspose.OCR.lic`)، حمّله مباشرة بعد إنشاء الكائن:

```java
ocrEngine.setLicense("Aspose.OCR.lic");
```

يقوم هذا بإزالة العلامة المائية التي تظهر في وضع التجربة.

## الخطوة 4 – تشغيل OCR على الـ ROI المحددة

هذا هو جوهر الحل. نستدعي `recognizeImage` مع ثلاثة معاملات: مسار الصورة، اللغة، وROI التي عرّفناها مسبقًا.

```java
// Step 4: Recognize text within the ROI
OcrResult ocrResult = ocrEngine.recognizeImage(
        "YOUR_DIRECTORY/car_photo.jpg",
        RecognitionLanguage.ENGLISH,
        vinRegion); // overload that accepts ROI
```

ملاحظة سريعة: `RecognitionLanguage.ENGLISH` يعمل لمعظم أرقام VIN لأنها تتكون من أحرف كبيرة وأرقام. إذا احتجت لدعم أحرف غير لاتينية (مثل اللوحات السيريلية)، غيّر الـ enum وفقًا لذلك.

## الخطوة 5 – استخراج VIN وتنظيفه والتحقق منه

قد يحتوي ناتج OCR على مسافات أو فواصل سطرية غير مرغوبة. لنقُم بقطع النتيجة وإجراء تحقق بسيط: VIN يتكون بالضبط من 17 حرفًا ويحتوي فقط على أحرف (باستثناء I, O, Q) وأرقام.

```java
// Step 5: Clean up the OCR output
String rawVin = ocrResult.getText().trim().replaceAll("\\s+", "");

// Simple validation (optional but recommended)
boolean isValidVin = rawVin.matches("[A-HJ-NPR-Z0-9]{17}");

if (isValidVin) {
    System.out.println("Detected VIN: " + rawVin);
} else {
    System.err.println("Failed to extract a valid VIN. Raw output: " + rawVin);
}
```

لماذا هذا التعبير النمطي (regex)؟ لأنه يستبعد الأحرف الغامضة I, O, Q التي يمنعها معيار VIN. هذا الفحص الإضافي يساعدك على **اكتشاف رقم تعريف المركبة** بثقة، خاصةً عندما لا تكون جودة الصورة مثالية.

## مثال كامل يعمل

بدمج كل ما سبق، إليك فئة Java كاملة جاهزة للتنفيذ. يمكنك نسخها ولصقها في `RoiExample.java` ثم تشغيلها.

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

public class RoiExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize OCR engine (add license if you have one)
        AsposeOCR ocrEngine = new AsposeOCR();
        // ocrEngine.setLicense("Aspose.OCR.lic"); // uncomment for licensed version

        // Step 2: Define ROI containing the VIN (adjust values for your image)
        Rectangle vinRegion = new Rectangle(120, 450, 400, 80);

        // Step 3: Run OCR on the image within the ROI
        OcrResult ocrResult = ocrEngine.recognizeImage(
                "YOUR_DIRECTORY/car_photo.jpg",
                RecognitionLanguage.ENGLISH,
                vinRegion);

        // Step 4: Clean and validate the extracted text
        String rawVin = ocrResult.getText().trim().replaceAll("\\s+", "");
        boolean isValidVin = rawVin.matches("[A-HJ-NPR-Z0-9]{17}");

        // Step 5: Output result
        if (isValidVin) {
            System.out.println("Detected VIN: " + rawVin);
        } else {
            System.err.println("Failed to extract a valid VIN. Raw output: " + rawVin);
        }
    }
}
```

### النتيجة المتوقعة

إذا احتوت الصورة على VIN واضح مثل `1HGCM82633A004352`، سترى:

```
Detected VIN: 1HGCM82633A004352
```

إذا عانى OCR (مثلاً أحرف غير واضحة)، سيظهر في الطرفية النص الخام مع تحذير، مما يدفعك لتعديل الـ ROI أو تحسين جودة الصورة.

## نصائح لتحسين الدقة

- **زيادة التباين** قبل تمرير الصورة إلى OCR. تعديل التوزيع الترددي (histogram equalization) يمكن أن يحدث فرقًا كبيرًا.
- **تغيير حجم الصورة** بحيث يشغل VIN ارتفاعًا لا يقل عن 150 بكسل؛ محركات OCR تفضّل الخطوط الكبيرة.
- **جرب أشكال ROI مختلفة** — أحيانًا مستطيل أطول قليلًا يلتقط الظلال الخفيفة التي تساعد المحرك.
- **استخدم `RecognitionLanguage.AUTODETECT`** إذا كنت تشك أن VIN قد يحتوي على أحرف غير إنجليزية (نادرًا، لكنه ممكن في بعض الأسواق).

## كيفية استخراج VIN من عدة صور (معالجة دفعات)

إذا كان لديك مجلد مليء بصور السيارات، غلف المنطق السابق داخل حلقة:

```java
File folder = new File("YOUR_DIRECTORY");
for (File imgFile : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".jpg"))) {
    OcrResult result = ocrEngine.recognizeImage(
            imgFile.getAbsolutePath(),
            RecognitionLanguage.ENGLISH,
            vinRegion);
    // ... same cleaning/validation code ...
}
```

تتيح لك هذه القطعة **قراءة VIN من الصور** على نطاق واسع — مثالية لتدقيق المخزون.

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | لماذا يحدث | الحل |
|---------|------------|------|
| *حروف غير مفهومة* | ROI كبير جدًا، يشمل ضوضاء الخلفية | قلّص إحداثيات `Rectangle` |
| *VIN جزئي* | دقة الصورة منخفضة | قم بزيادة دقة الصورة أو التقط صورة أفضل |
| *حروف خاطئة (I/O/Q)* | OCR يخطئ في تفسير الأشكال المتشابهة | عالج النتيجة باستخدام regex للتحقق |
| *علامة مائية للترخيص* | تشغيل في وضع التجربة | استخدم ترخيص Aspose OCR صالح |

معالجة هذه القضايا مبكرًا سيوفر لك ساعات من التصحيح لاحقًا.

## الخلاصة

في هذا الدليل أظهرنا كيفية **استخراج النص من صورة** باستخدام Aspose OCR في Java، مع التركيز على المشكلة العملية لـ **كيفية استخراج VIN** و**اكتشاف رقم تعريف المركبة**. من خلال تعريف **منطقة التعرف على النص**، تهيئة المحرك، والتحقق من النتيجة، يمكنك قراءة VIN من صورة ببضع أسطر من الكود فقط.

ما الخطوة التالية؟ جرّب دمج هذه الشيفرة في خدمة microservice باستخدام Spring Boot، أو أرسل الـ VIN إلى API تاريخ مركبة من طرف ثالث. يمكنك أيضًا تجربة مكتبات OCR أخرى (Tesseract، Google Vision) ومقارنة الدقة — معرفة دائمًا مفيدة في عالم معالجة الصور المتطور.

برمجة سعيدة، ولتكن OCR دائمًا واضحة كالكريستال!

![مثال استخراج النص من صورة](https://example.com/ocr-demo.png "مثال استخراج النص من صورة")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}