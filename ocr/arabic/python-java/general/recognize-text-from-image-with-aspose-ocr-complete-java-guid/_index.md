---
category: general
date: 2026-05-03
description: تعلم كيفية التعرف على النص من الصورة وتحويل الصورة إلى نص باستخدام Aspose
  OCR للـ Java. يتضمن نصائح لتحسين دقة OCR وتشغيل OCR على ملفات PNG.
draft: false
keywords:
- recognize text from image
- convert image to text
- improve ocr accuracy
- load image for ocr
- run ocr on png
language: ar
og_description: دليل خطوة بخطوة للتعرف على النص من الصورة باستخدام Aspose OCR للغة
  Java. تعلم كيفية تحويل الصورة إلى نص، تحسين دقة OCR وتشغيل OCR على ملفات PNG.
og_title: التعرف على النص من الصورة باستخدام Aspose OCR – دليل جافا
tags:
- OCR
- Java
- Aspose
- Image Processing
title: التعرف على النص من الصورة باستخدام Aspose OCR – دليل Java الكامل
url: /ar/python-java/general/recognize-text-from-image-with-aspose-ocr-complete-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة باستخدام Aspose OCR – دليل Java الكامل

هل احتجت يومًا إلى **التعرف على النص من الصورة** لكنك لم تكن متأكدًا أي مكتبة ستعطيك نتائج موثوقة؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما يحاولون استخراج البيانات من ملفات PDF الممسوحة، الإيصالات، أو تقارير المختبر. الخبر السار هو أن Aspose OCR for Java يجعل العملية بأكملها سهلة للغاية، ويمكنك حتى **تحويل الصورة إلى نص** ببضع أسطر فقط.

في هذا البرنامج التعليمي سنستعرض كل ما تحتاج إلى معرفته: من تحميل صورة للتعرف الضوئي على الأحرف (OCR)، تعديل الإعدادات لـ **تحسين دقة OCR**، إلى أخيرًا **تشغيل OCR على ملفات PNG** وطباعة النص المستخرج. لا إطالة، مجرد مثال عملي قابل للتنفيذ يمكنك إدراجه في مشروعك اليوم.

---

## ما ستحتاجه

| المتطلب المسبق | السبب |
|--------------|--------|
| Java 17 (or newer) | Aspose OCR يستهدف Java 8+، لكن أحدث JDK يمنحك أداءً أفضل. |
| Aspose OCR for Java library (`aspose-ocr.jar`) | المحرك الأساسي الذي يقوم بالمعالجة الثقيلة. |
| A valid Aspose OCR license file (`Aspose.OCR.Java.lic`) | يفعل مجموعة الميزات الكاملة؛ وإلا ستحصل على علامة مائية تجريبية. |
| An image file (PNG, JPEG, TIFF, etc.) containing clear text | سنستخدم `lab_report.png` كمثال عملي. |
| A custom dictionary (optional) | يحسن التعرف على المصطلحات المتخصصة مثل “hemoglobin”. |

إذا كان أي من هذه غير مألوف بالنسبة لك، لا تقلق—تثبيت ملف JAR وإنشاء ملف نصي بسيط هي مهام بسيطة سنغطيها لاحقًا.

## الخطوة 1 – إعداد المشروع واستيراد الاعتمادات

أولاً، أنشئ مشروع Maven (أو Gradle) جديد وأضف اعتماد Aspose OCR. يمكن لمستخدمي Maven لصق هذا المقتطف في ملف `pom.xml` الخاص بهم:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check the latest version on Maven Central -->
</dependency>
```

إذا كنت تفضل Gradle، فإن المكافئ هو:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **نصيحة احترافية:** راقب رقم الإصدار؛ الإصدارات الأحدث غالبًا ما تحتوي على إصلاحات أخطاء تؤثر مباشرة على **تحسين دقة OCR**.

الآن، أنشئ فئة Java باسم `OcrDemo.java`. في أعلى الملف، استورد الفئات المطلوبة:

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.License;
import com.aspose.ocr.Image;
import com.aspose.ocr.OcrResult;
```

## الخطوة 2 – تهيئة محرك OCR وتطبيق الترخيص الخاص بك

لا يمكنك **تشغيل OCR على ملفات PNG** دون إبلاغ المحرك أولاً بأنه مرخص. إليك الطريقة:

```java
public class OcrDemo {
    public static void main(String[] args) {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Apply your license – replace the path with your actual license location
        License lic = new License();
        lic.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
        ocrEngine.setLicense(lic);
```

لماذا كائن `License` الإضافي؟ تقوم Aspose بفصل معالجة الترخيص عن المحرك لتتمكن من تبديل الترخيص في أي وقت، وهو ما يمكن أن يكون مفيدًا في سيناريوهات SaaS متعددة المستأجرين.

## الخطوة 3 – تحميل قاموس مخصص (اختياري لكن قوي)

إذا كنت تتعامل مع مصطلحات طبية، صيغ كيميائية، أو أسماء علامات تجارية، يمكن للقاموس المخصص أن **يحسن دقة OCR** بشكل كبير. القاموس هو ملف نصي عادي يحتوي على كلمة واحدة في كل سطر:

```java
        // Optional: improve accuracy with a custom dictionary
        // Create a file named custom_dictionary.txt in YOUR_DIRECTORY
        ocrEngine.getConfig().setCustomDictionary("YOUR_DIRECTORY/custom_dictionary.txt");
```

> **لماذا يعمل:** يستخدم محرك OCR القاموس لتوجيه نموذج اللغة نحو الكلمات التي تهتم بها، مما يقلل من الأخطاء مثل “hemo­globin” → “hemoglobin”.

إذا لم يكن لديك قاموس، فقط تخط هذه السطر—ما زالت Aspose تعمل جيدًا مع حزم اللغات المدمجة.

## الخطوة 4 – تحميل الصورة التي تريد معالجتها

الآن نقوم فعليًا **بتحميل الصورة للتعرف الضوئي على الأحرف (OCR)**. تدعم Aspose العديد من الصيغ، لكن PNG يعتبر خاليًا من الفقدان، مما يجعله خيارًا آمنًا للمستندات الممسوحة.

```java
        // Load the PNG image containing the text you want to extract
        Image inputImage = Image.fromFile("YOUR_DIRECTORY/lab_report.png");
```

> **حالة خاصة:** إذا كانت صورتك ضخمة (أكثر من 5 ميغابايت)، فكر في تقليل حجمها أولاً لتسريع المعالجة. توفر فئة `Image` طريقة `resize` يمكنك استدعاؤها قبل التعرف.

## الخطوة 5 – تشغيل عملية OCR واسترجاع النص

مع إعداد كل شيء، شغّل محرك OCR. تُعيد طريقة `recognize` كائن `OcrResult` الذي يحتوي على السلسلة المستخرجة، درجات الثقة، وحتى الصناديق المحيطة إذا كنت تحتاج إلى معلومات التخطيط.

```java
        // Perform OCR on the loaded image
        OcrResult result = ocrEngine.recognize(inputImage);

        // Print the extracted text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مشابهًا لـ:

```
=== Extracted Text ===
Patient Name: John Doe
Hemoglobin: 13.5 g/dL
...
```

هذا كل شيء—لقد نجحت في **التعرف على النص من الصورة** و**تحويل الصورة إلى نص** باستخدام Aspose OCR.

## الخطوة 6 – المشكلات الشائعة وكيفية إصلاحها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| إخراج فارغ | الترخيص غير مُطبق أو منتهي | تحقق من مسار `Aspose.OCR.Java.lic` وتأكد من أنه يتطابق مع الإصدار. |
| حروف مشوشة | الصورة منخفضة الدقة أو مضغوطة بشدة | استخدم مصدرًا بدقة أعلى أو قم بمعالجة مسبقة للصورة (تثنائي، تصحيح الميل). |
| كلمات متخصصة مفقودة | لا يوجد قاموس مخصص | أضف ملف قاموس يحتوي على المصطلحات المفقودة، كلمة واحدة في كل سطر. |
| معالجة بطيئة على دفعات كبيرة | لا توجد معالجة متعددة الخيوط | أنشئ مجموعة من كائنات `OcrEngine` (هي آمنة للخيوط) وعالج الصور بشكل متوازي. |

## الخطوة 7 – توسيع المثال: حفظ النتائج إلى ملف

إذا كنت بحاجة إلى الاحتفاظ بالنص المستخرج للتحليل لاحقًا، ببساطة اكتبها إلى ملف:

```java
import java.nio.file.Files;
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;

// ...

        // Save the text to a .txt file
        Files.write(Paths.get("output.txt"),
                    result.getText().getBytes(StandardCharsets.UTF_8));
        System.out.println("Text saved to output.txt");
```

الآن لديك خط أنابيب قابل لإعادة الاستخدام يقوم **بتحميل الصورة للتعرف الضوئي على الأحرف (OCR)**، يستخرج المحتوى، ويحفظه أينما تريد.

## إضافي: تشغيل OCR على ملفات PNG متعددة في مجلد

غالبًا ما تحتاج المشاريع الواقعية إلى معالجة عشرات المسحات. إليك حلقة سريعة تلتقط كل ملف `.png` في دليل:

```java
import java.io.File;

// ...

        File folder = new File("YOUR_DIRECTORY/scans");
        File[] pngFiles = folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".png"));

        for (File png : pngFiles) {
            Image img = Image.fromFile(png.getAbsolutePath());
            OcrResult res = ocrEngine.recognize(img);
            System.out.println("---- " + png.getName() + " ----");
            System.out.println(res.getText());
        }
```

تذكر إعادة استخدام نفس كائن `ocrEngine`—إنشاء كائن جديد لكل ملف يضيف عبئًا غير ضروري.

## الخاتمة

الآن لديك حل كامل من البداية إلى النهاية يتيح لك **التعرف على النص من الصورة** باستخدام Aspose OCR for Java. من تحميل الصورة، وإثراء المحرك اختياريًا بقاموس مخصص لـ **تحسين دقة OCR**، وحتى **تشغيل OCR على ملفات PNG** وحفظ الناتج، الكود جاهز للإدراج في أي مشروع Java.

ما الخطوة التالية؟ جرّب إمداد النص المستخرج إلى خط أنابيب معالجة اللغة الطبيعية، أو جرب OCR على الملاحظات المكتوبة يدويًا (تقدم Aspose أيضًا وضعًا للخط اليدوي). الاحتمالات لا حصر لها، وقد فتحت الآن الخطوة الأولى.

برمجة سعيدة! إذا واجهت أي مشاكل، لا تتردد في ترك تعليق أدناه—دعنا نحل المشكلات معًا.

![لقطة شاشة لنتيجة OCR في وحدة التحكم – التعرف على النص من الصورة](/images/ocr_console_result.png "مثال على التعرف على النص من الصورة")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}