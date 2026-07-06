---
category: general
date: 2026-02-19
description: استخراج النص من الصورة باستخدام Java OCR. تعلم مثال Java OCR يقوم بتحميل
  صورة للـ OCR ويستخرج النص من ملفات الفواتير في بضع خطوات فقط.
draft: false
keywords:
- extract text from image
- java ocr example
- load image for ocr
- extract text from invoice
language: ar
og_description: استخراج النص من الصورة باستخدام Java OCR. يوضح هذا الدليل كيفية تحميل
  الصورة للتعرف الضوئي على الأحرف واستخراج النص من الفواتير باستخدام مثال بسيط لـ
  Java OCR.
og_title: استخراج النص من صورة في جافا – مثال كامل على OCR
tags:
- OCR
- Java
- Aspose
- Image Processing
title: استخراج النص من الصورة في جافا – مثال كامل على التعرف الضوئي على الأحرف (OCR)
url: /ar/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

craft.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من صورة في جافا – مثال كامل على OCR

هل احتجت يومًا إلى **استخراج النص من صورة** لكن لم تكن متأكدًا أي مكتبة تختار؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عند أتمتة معالجة الفواتير أو بناء أرشيفات قابلة للبحث. الخبر السار؟ ببضع أسطر من جافا يمكنك تحميل صورة للـ OCR، تعريف منطقة اهتمام، واستخراج النص الدقيق الذي تحتاجه.  

في هذا الدرس سنستعرض **مثال java ocr** يوضح بالضبط كيف **نحمّل صورة للـ OCR**، نحدد ROI، و**نستخرج النص من ملفات الفواتير** باستخدام Aspose.OCR. في النهاية ستحصل على برنامج قابل للتنفيذ يمكنك إدراجه في أي مشروع جافا.

## ما ستتعلمه

- كيفية إنشاء كائن `OcrEngine` ولماذا هو مهم.
- الطريقة الصحيحة **لتحميل صورة للـ OCR** باستخدام `ImageStream` من Aspose.
- ضبط **منطقة الاهتمام (ROI)** بحيث تعالج فقط الجزء من الصورة الذي يحتوي على مبلغ الفاتورة.
- استخراج النص المعترف به وطباعة النتيجة إلى وحدة التحكم.
- الأخطاء الشائعة (مثل إحداثيات المستطيل الخاطئة) والحلول السريعة.

**المتطلبات المسبقة**

- جافا 8 أو أحدث مثبتة.
- Maven أو Gradle لجلب مكتبة Aspose.OCR (`com.aspose:aspose-ocr`).
- صورة فاتورة نموذجية (`invoice.png`) موجودة في دليل معروف.

هل لديك كل ذلك؟ رائع—لنبدأ.

![استخراج النص من صورة باستخدام Java OCR](/images/extract-text-from-image-java.png "مثال استخراج النص من صورة")

## استخراج النص من صورة – مثال Java OCR خطوة بخطوة

فيما يلي الشيفرة الكاملة. يمكنك نسخها ولصقها في `RoiOcrExample.java` وتشغيلها مباشرة.

```java
import com.aspose.ocr.*;

public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance.
        // The engine holds all configuration and performs the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image.
        // You can point to any PNG, JPG, or TIFF file. Here we use a sample invoice.
        String imagePath = "YOUR_DIRECTORY/invoice.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Define the region of interest (ROI) you want to recognize.
        // x = 120, y = 340, width = 500, height = 120 – tweak these values for your own layout.
        Rectangle regionOfInterest = new Rectangle(120, 340, 500, 120);
        ocrEngine.setRegionOfInterest(regionOfInterest);

        // Step 4: Perform OCR on the specified ROI and retrieve the text.
        // recognize() returns an OcrResult object; getText() extracts the plain string.
        String extractedText = ocrEngine.recognize().getText();

        // Step 5: Output the recognized text.
        System.out.println("ROI text: " + extractedText);
    }
}
```

### لماذا كل خطوة مهمة

1. **إنشاء محرك OCR** – بدون محرك لا يوجد سياق لمعالجة الصورة. الكائن يتيح لك أيضًا تعديل حزم اللغات لاحقًا إذا احتجت دعمًا متعدد اللغات.  
2. **تحميل الصورة** – `ImageStream.fromFile` يخفف عنك التعامل مع تنسيقات الملفات، مما يضمن أن المحرك يقرأ البايتات بشكل صحيح. إذا تخطيت هذه الخطوة ستحصل على `NullPointerException`.  
3. **تحديد ROI** – معالجة الصفحة بأكملها قد تكون مضيعة للموارد. بتضييق المستطيل إلى منطقة إجمالي الفاتورة، تسرّع التعرف وتقلل الضوضاء.  
4. **استدعاء `recognize()`** – هنا يحدث السحر. الطريقة تنفّذ خوارزمية OCR على الـ ROI وتنتج كائن نتيجة.  
5. **طباعة النتيجة** – في المشاريع الفعلية ربما تخزن النص في قاعدة بيانات، لكن `System.out.println` مثالي للعرض السريع.

## تحميل صورة للـ OCR

إذا كنت تتساءل ما إذا كان المسار يجب أن يكون مطلقًا أم نسبيًا، الجواب هو أن كلاهما يعمل—فقط تأكد أن عملية جافا يمكنها قراءة الملف. على نظام Windows، يجب هروب الشرطات العكسية (`C:\\images\\invoice.png`) أو يمكنك استخدام الشرطات المائلة (`C:/images/invoice.png`).  

**نصيحة محترف:** إذا كنت تعالج العديد من الفواتير داخل حلقة، أعد استخدام نفس كائن `OcrEngine`؛ فهو يخزن الموارد الداخلية ويحسّن الإنتاجية.

## تعريف منطقة الاهتمام (ROI)

اختيار المستطيل المناسب قد يتطلب بعض التجربة. طريقة مفيدة للحصول على الإحداثيات هي فتح الصورة في أي محرر رسومات (مثل GIMP أو Paint.NET) وتحريك المؤشر فوق المنطقة—ستظهر قيم X/Y في شريط الحالة.  

حالة خاصة: بعض الفواتير لها تخطيطات متغيرة. في هذه الحالة يمكنك إجراء مسح سريع مسبق على الصورة بأكملها، البحث عن كلمات مفتاحية مثل “Total:” باستخدام تعبير نمطي، ثم تعديل الـ ROI ديناميكيًا.

## تنفيذ OCR والحصول على النص

استدعاء `recognize()` متزامن—يتوقف الخيط حتى ينتهي المحرك. للدفعات الكبيرة قد ترغب في إنشاء مجموعة خيوط ومعالجة الصور بالتوازي. تذكر أن كل خيط يحتاج إلى كائن `OcrEngine` خاص به؛ فهي غير آمنة للاستخدام المتعدد الخيوط.

## تشغيل البرنامج والتحقق من النتيجة

قم بالترجمة والتنفيذ:

```bash
javac -cp "path/to/aspose-ocr.jar" RoiOcrExample.java
java -cp ".:path/to/aspose-ocr.jar" RoiOcrExample
```

يجب أن ترى شيئًا مشابهًا لـ:

```
ROI text: $1,254.00
```

إذا ظهرت النتيجة مشوشة، تحقق مرة أخرى من إحداثيات الـ ROI وتأكد من جودة الصورة (300 dpi أو أكثر هو الأفضل).  

### الأخطاء الشائعة وكيفية إصلاحها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| سلسلة فارغة | ROI خارج حدود الصورة | تحقق من قيم المستطيل مقارنة بأبعاد الصورة |
| كلمات مكتوبة خطأ | دقة منخفضة | استخدم مصدر بدقة أعلى أو طبّق معالجة مسبقة للصورة (مثل التحويل إلى ثنائي) |
| `java.lang.NoClassDefFoundError` | عدم وجود ملف JAR الخاص بـ Aspose في مسار الفئة | أضف `aspose-ocr.jar` إلى `-cp` أو استخدم إدارة الاعتمادات عبر Maven/Gradle |

## الخلاصة

الآن تعرف كيف **استخراج النص من صورة** في جافا باستخدام **مثال java ocr** مختصر. بتحميل الصورة بشكل صحيح، تعريف ROI مركّز، واستدعاء `recognize()`، يمكنك بثقة **استخراج النص من ملفات الفواتير** وإرسال البيانات إلى الأنظمة اللاحقة.

ما الخطوة التالية؟ جرّب تغيير الـ ROI لحقول مختلفة (التاريخ، اسم المورد)، جرب حزم اللغات للفواتير متعددة اللغات، أو دمج خطوة OCR في خدمة ميكروية مبنية على Spring Boot. النمط نفسه يعمل مع الإيصالات، جوازات السفر، أو أي مستند تحتاج فيه إلى استخراج نص دقيق.

إذا كان لديك أسئلة حول توسيع هذا الحل أو التعامل مع المسحات الضوضائية، اترك تعليقًا أدناه—برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}