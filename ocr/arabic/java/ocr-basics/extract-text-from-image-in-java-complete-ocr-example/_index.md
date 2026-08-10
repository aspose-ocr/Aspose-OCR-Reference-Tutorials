---
category: general
date: 2026-01-12
description: استخراج النص من الصورة باستخدام Aspose OCR في جافا. تعلّم كيفية استخراج
  النص من صورة فاتورة باستخدام مثال OCR بجافا واحصل على نص OCR الناتج.
draft: false
keywords:
- extract text from image
- how to extract text
- java ocr example
- process invoice image
- output ocr text
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR في Java. يوضح هذا الدليل
  كيفية استخراج النص من صورة فاتورة، ويتضمن مثالًا على OCR بجافا، ويُخرج نص OCR.
og_title: استخراج النص من الصورة في جافا – مثال كامل على OCR
tags:
- OCR
- Java
- Aspose
title: استخراج النص من صورة في جافا – مثال كامل على التعرف الضوئي على الأحرف
url: /ar/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة في جافا – مثال كامل على OCR

هل تساءلت يومًا كيف **استخراج النص من الصورة** دون أن تشعر بالإحباط؟ ربما لديك مجموعة من الفواتير الممسوحة وتحتاج إلى الأرقام بسرعة. في تجربتي، أسهل طريقة هي السماح لمكتبة OCR مخصصة بالقيام بالعمل الشاق. يوضح هذا الدليل *كيفية استخراج النص* من صورة فاتورة نموذجية باستخدام Aspose OCR for Java، ويعرض أيضًا **java ocr example** الذي ينتج نص OCR يمكنك تمريره إلى نظامك اللاحق.

سنستعرض كل ما تحتاج معرفته: من إعداد المشروع، تعريف منطقة الاهتمام (ROI) التي تركز على العنوان والمبلغ الإجمالي، إلى طباعة النص المستخرج في النهاية. بحلول النهاية، ستكون قادرًا على **process invoice image** ملفات تلقائيًا واسترجاع نص نظيف قابل للبحث.

> **ما ستحصل عليه:** برنامج Java جاهز للتشغيل، شروحات واضحة لكل خطوة، ونصائح عملية للتعامل مع الفواتير الواقعية.

---

## المتطلبات المسبقة

قبل أن نغوص في التفاصيل، تأكد من وجود ما يلي:

- Java Development Kit (JDK) 8 أو أحدث مثبت.
- Maven أو Gradle لإدارة التبعيات (مثال Maven موضح).
- رخصة Aspose OCR for Java (الإصدار التجريبي المجاني يعمل للاختبار).
- صورة فاتورة (`invoice.png`) موجودة في دليل معروف.

إذا كان أي من هذه غير مألوف، لا تقلق—معظمها يمكن تحميله بسهولة، والكود سيظل يُترجم باستخدام نسخة المجتمع.

## الخطوة 1: إعداد مشروع Maven الخاص بك

أولاً، أنشئ مشروع Maven جديد (أو أضف إلى مشروع موجود). في ملف `pom.xml` الخاص بك، أضف تبعية Aspose OCR:

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest version available -->
    </dependency>
</dependencies>
```

> **نصيحة احترافية:** حافظ على تحديث رقم الإصدار؛ الإصدارات الأحدث غالبًا ما تحسن الدقة للخطوط الصعبة الموجودة في الفواتير.

بعد حفظ الملف، شغّل `mvn clean install` لجلب المكتبة إلى المستودع المحلي الخاص بك.

## الخطوة 2: تحميل صورة الفاتورة

الآن بعد أن المكتبة جاهزة، لنكتب فئة Java صغيرة. أول شيء نفعله هو إنشاء مثال `OcrEngine` وتوجيهه إلى الصورة التي تريد قراءتها.

```java
import com.aspose.ocr.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png"); // <-- replace with your path
```

لماذا ننشئ المحرك **قبل** تحميل الصورة؟ المحرك يحتفظ بالإعدادات مثل اللغة، DPI، و ROI. ضبط الصورة مبكرًا يضمن تطبيق تلك الإعدادات على الملف المحدد الذي ستعالجه.

## الخطوة 3: تعريف مناطق الاهتمام (ROI)

غالبًا ما تحتوي الفواتير على الكثير من الضوضاء—جداول، شعارات، ونص صغير. من خلال تضييق OCR على العنوان فقط والمبلغ الإجمالي، تزيد السرعة والدقة بشكل كبير. Aspose يتيح لك وصف هذه المناطق بالمستطيلات.

```java
        // Step 3: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Apply ROI to the engine
        engine.setRegion(region);
```

الإحداثيات بوحدات البكسل (`x`, `y`, `width`, `height`). إذا كانت فواتيرك تختلف في الحجم، يمكنك حساب هذه القيم ديناميكيًا—ربما عن طريق فحص أبعاد الصورة أولاً. هذه إضافة جيدة إذا كنت تحتاج حل **process invoice image** يعمل على دفعات.

## الخطوة 4: تشغيل OCR على المناطق المحددة

مع وجود ROI، يمكن لمحرك OCR تركيز انتباهه حيث يهم أكثر. طريقة `recognize()` تُعيد كائن `OcrResult` يحتوي على النص المستخرج.

```java
        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();
```

خلف الكواليس، Aspose يقوم بعدة خطوات تمهيدية: التحويل إلى ثنائي، إزالة الضوضاء، وتقسيم الأحرف. لا تحتاج إلى استدعائها يدويًا—دع `recognize()` يقوم بعمله.

## الخطوة 5: إخراج النص المستخرج

أخيرًا، نطبع النص إلى وحدة التحكم. في تطبيق حقيقي قد تخزنه في قاعدة بيانات، أو تمرره إلى خط أنابيب تحليلي لاحق، أو حتى تولد ملف PDF قابل للبحث.

```java
        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مثل:

```
ROI text:
Acme Corp.
Invoice #12345
Date: 2025-12-31
Total Amount: $1,250.00
```

إذا كان الإخراج مشوشًا، تحقق مرة أخرى من إحداثيات المستطيل أو زد دقة الصورة. محركات OCR تحب المسحات الواضحة وعالية الـ DPI.

## مثال كامل يعمل

فيما يلي ملف Java كامل ومستقل يمكنك نسخه ولصقه في `src/main/java/RoiExample.java`. لا حاجة لمقاطع خارجية—كل ما تحتاجه موجود هنا.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.region.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png");

        // Step 2: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Step 3: Apply the ROI configuration to the engine
        engine.setRegion(region);

        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

> **ملاحظة:** استبدل `YOUR_DIRECTORY` بالمسار المطلق إلى صورة الفاتورة الخاصة بك. إذا كنت تستخدم مسارًا نسبيًا، تأكد من أن دليل العمل يتطابق مع المكان الذي تشغل فيه أمر `java`.

## أسئلة شائعة وحالات حافة

### ماذا لو تغير حجم الفاتورة؟

يمكنك حساب ROI ديناميكيًا:

```java
int imgWidth = engine.getImage().getWidth();
int imgHeight = engine.getImage().getHeight();

int headerHeight = imgHeight / 10;
int totalHeight = imgHeight / 8;

OcrRegion region = OcrRegion.builder()
        .addRectangle(0, 0, imgWidth, headerHeight)
        .addRectangle(0, imgHeight - totalHeight, imgWidth, totalHeight)
        .build();
```

### كيف أتعامل مع لغات متعددة؟

Aspose OCR يدعم حزم اللغات. فقط اضبط اللغة قبل استدعاء `recognize()`:

```java
engine.setLanguage(OcrLanguage.Spanish); // or OcrLanguage.English, etc.
```

### ماذا لو أعاد OCR سلاسل فارغة؟

الأسباب الشائعة هي:

- دقة صورة منخفضة (< 300 DPI). قم بزيادة الحجم أو اطلب مسحات ذات جودة أعلى.
- خلفيات داكنة جدًا أو فاتحة جدًا. طبق مرشح تحسين التباين البسيط قبل OCR.
- إحداثيات ROI غير صحيحة تفوت النص تمامًا.

## نصائح لـ OCR جاهز للإنتاج

1. **معالجة دفعات:** غلف المنطق في حلقة تتكرر على دليل ملفات الفواتير. سجّل كل نتيجة لأغراض التدقيق.
2. **معالجة الأخطاء:** امسك `OcrException` لتجاوز الصور التالفة بلطف دون إيقاف المهمة بالكامل.
3. **الأداء:** أعد استخدام مثال واحد من `OcrEngine` عبر صور متعددة؛ إنشاء محرك جديد لكل ملف يضيف عبئًا غير ضروري.
4. **التحقق:** بعد الاستخراج، شغّل فحص regex على المبلغ الإجمالي (`\$\d{1,3}(,\d{3})*(\.\d{2})?`) للتأكد من أن الرقم يبدو واقعيًا.

تطبيق هذه الاقتراحات يحول **java ocr example** بسيط إلى حل قوي وقابل للتوسع لأي عمل يحتاج إلى **process invoice image** ملفات ليلية.

## الخاتمة

لقد غطينا للتو كيفية **استخراج النص من الصورة** في ملفات Java باستخدام Aspose OCR، مع التركيز على سيناريو عملي لمعالجة الفواتير. من خلال تعريف منطقة الاهتمام، تشغيل محرك OCR، وطباعة **output OCR text**، لديك الآن أساس قوي لبناء خطوط أنابيب التقاط البيانات تلقائيًا.

الخطوات التالية؟ حاول توسيع ROI لتشمل جداول العناصر، جرب إعدادات لغات مختلفة، أو مرر السلاسل المستخرجة إلى مكتبة توليد PDF للوثائق القابلة للبحث. السماء هي الحد عندما تجمع OCR مع أدوات Java الحديثة.

هل لديك المزيد من الأسئلة حول **كيفية استخراج النص** من أنواع مستندات أخرى، أو تحتاج مساعدة في تعديل ROI لتصاميم غير عادية؟ اترك تعليقًا أدناه—برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}