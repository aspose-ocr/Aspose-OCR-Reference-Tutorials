---
category: general
date: 2026-06-28
description: تعلم مثال Aspose OCR للغة Java لاستخراج النص من صور مشاريع Java وتحديد
  حد الذاكرة للمعالج الرسومي للحصول على نتائج أسرع.
draft: false
keywords:
- aspose ocr java example
- extract text from image java
- set gpu memory limit
- gpu accelerated OCR Java
- Aspose OCR licensing
language: ar
og_description: مثال Aspose OCR للغة Java يوضح كيفية استخراج النص من صورة باستخدام
  كود Java مع ضبط حد ذاكرة GPU لتحقيق الأداء الأمثل.
og_title: مثال Aspose OCR بلغة Java – استخراج نص سريع مع تسريع GPU
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn an Aspose OCR Java example to extract text from image Java projects
    and set GPU memory limit for faster results.
  headline: Aspose OCR Java Example – Extract Text from Image with GPU
  type: TechArticle
tags:
- Aspose OCR
- Java
- GPU
title: مثال Aspose OCR بلغة Java – استخراج النص من الصورة باستخدام وحدة معالجة الرسومات
url: /ar/java/advanced-ocr-techniques/aspose-ocr-java-example-extract-text-from-image-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# مثال Aspose OCR Java – استخراج النص من صورة باستخدام GPU

هل تساءلت يومًا كيف **استخراج النص من صورة Java** دون إبطاء المعالج إلى حد التوقف؟ لست وحدك. في العديد من السيناريوهات الواقعية—مثل مسح الفواتير، التحقق من الهوية، أو أرشفة المستندات الضخمة—العنق الزجاجي هو محرك OCR نفسه.  

خبر سار: هذا **مثال Aspose OCR Java** يوضح لك برنامجًا كاملًا جاهزًا للتنفيذ يستخدم تسريع الـ GPU، ويظهر لك أيضًا **كيفية ضبط حد ذاكرة الـ GPU** حتى يبقى الخادم سعيدًا. بنهاية هذا الدليل ستحصل على فئة Java تعمل على قراءة ملف صورة، تشغيل OCR على الـ GPU، وطباعة النص المعترف به إلى وحدة التحكم. لا مراجع غامضة، فقط كود ملموس وتفسيرات واضحة.

سنغطي كل شيء من الترخيص إلى ضبط الـ GPU، لذا سواء كنت مطور Java مخضرم أو تبدأ فقط في مجال الرؤية الحاسوبية، ستجد قيمة هنا. المتطلب الوحيد هو بيئة تطوير Java (JDK 8 أو أحدث) وإمكانية الوصول إلى GPU متوافق مع CUDA أو OpenCL.

---

## المتطلبات المسبقة

- **Java Development Kit (JDK) 8+** – يمكنك تنزيله من Oracle أو اعتماد OpenJDK.  
- **مكتبة Aspose.OCR for Java** – احصل على ملف JAR من موقع Aspose أو Maven Central.  
- **ملف ترخيص Aspose OCR صالح** (`Aspose.OCR.Java.lic`). النسخة التجريبية المجانية تعمل للاختبار، لكن الترخيص يزيل علامات التقييم.  
- **GPU يدعم CUDA أو OpenCL** – العرض التوضيحي يكتشف الوضع الأفضل تلقائيًا، لكن يجب تثبيت التعريفات.  
- **صورة للاختبار** – PNG أو JPEG واضح لفاتورة، توقيع، أو أي نص مطبوع.  

إذا كان أي من هذه غير مألوف لك، لا تقلق. الخطوات أدناه ستوجهك إلى روابط التحميل الدقيقة وتوضح أين تضع الملفات.

---

## الخطوة 1: مثال Aspose OCR Java – إعداد المشروع

أولًا، أنشئ مشروع Maven جديد (أو مجلدًا بسيطًا إذا كنت تفضل `javac` العادي). أضف تبعية Aspose OCR إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest version -->
</dependency>
```

> **نصيحة احترافية:** سيقوم Maven بجلب جميع التبعيات المتسلسلة، بما في ذلك مكتبات دعم الـ GPU، لذا لن تحتاج للبحث عن ملفات JAR إضافية.

ضع ملف `Aspose.OCR.Java.lic` في جذر المشروع (أو أي مجلد ستشير إليه لاحقًا). **مثال Aspose OCR Java** الذي نبنيه يتوقع مسار الترخيص أن يكون `"Aspose.OCR.Java.lic"`.

---

## الخطوة 2: تطبيق ترخيص Aspose OCR

خطوة الترخيص حاسمة—بدونها يعمل محرك OCR في وضع التقييم ويضيف علامة مائية إلى المخرجات. إليك الحد الأدنى من الكود الذي تحتاجه:

```java
import com.aspose.ocr.*;

public class LicenseUtil {
    public static void applyLicense() throws Exception {
        License license = new License();
        // Adjust the path if your license file lives elsewhere
        license.setLicense("Aspose.OCR.Java.lic");
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

تشغيل هذا مرة واحدة في بداية التطبيق يضمن أن **جميع استدعاءات OCR اللاحقة** مرخصة بالكامل.

---

## الخطوة 3: تكوين تسريع الـ GPU – ضبط حد ذاكرة الـ GPU

الآن يأتي الجزء الممتع: إخبار Aspose باستخدام الـ GPU وإمكانية **ضبط حد ذاكرة الـ GPU**. المكتبة توفر `GpuEngineOptions`، التي تسمح لك بتفعيل وضع الـ GPU، اختيار الجهاز، وتحديد حد الذاكرة. تحديد الحد مفيد على الخوادم المشتركة حيث لا تريد أن يستهلك عمل OCR كل ذاكرة الـ GPU.

```java
import com.aspose.ocr.gpu.*;

public class GpuConfig {
    public static GpuEngineOptions createOptions() {
        GpuEngineOptions gpuOptions = new GpuEngineOptions();
        gpuOptions.setEnableGpu(true);          // turn on GPU acceleration
        gpuOptions.setDeviceId(0);              // use the first GPU device
        gpuOptions.setMemoryLimitMb(2048);      // **set GPU memory limit** to 2 GB
        System.out.println("GPU options configured (memory limit = 2048 MB).");
        return gpuOptions;
    }
}
```

> **لماذا نضبط حد الذاكرة؟** إذا كانت مهام OCR تتعامل مع صور كبيرة جدًا أو تشغل العديد من الوظائف المتزامنة، قد ينفد الـ VRAM سريعًا، مما يسبب تعطلًا. بتحديد الحد، تحافظ على العملية داخل حدود آمنة وتسمح للعبء الآخر بالتعايش بسلام.

---

## الخطوة 4: استخراج النص من صورة Java – تحميل الصورة

بعد إكمال الترخيص وإعدادات الـ GPU، يمكننا أخيرًا **استخراج النص من صورة Java**. المقتطف التالي ينشئ `OcrEngine` باستخدام خيارات الـ GPU، يحمل ملف صورة، ويجري التعرف.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply the license
        LicenseUtil.applyLicense();

        // 2️⃣ Set up GPU options (including memory limit)
        GpuEngineOptions gpuOptions = GpuConfig.createOptions();

        // 3️⃣ Create the OCR engine with GPU acceleration
        OcrEngine ocrEngine = new OcrEngine(gpuOptions);

        // 4️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        // Replace the placeholder with your actual image path
        ocrInput.add("YOUR_DIRECTORY/receipt.png");

        // 5️⃣ Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 6️⃣ Output the recognized text
        System.out.println("Recognized Text (GPU):");
        System.out.println(ocrResult.getText());
    }
}
```

**نقاط رئيسية** في هذا **مثال Aspose OCR Java**:

- `OcrInput.add()` يمكنه قبول صور متعددة؛ سيعالج المحرك إياها بالتتابع.  
- `ocrResult.getText()` يُرجع سلسلة نصية عادية، تحافظ على فواصل الأسطر لكن لا تحتفظ بأي معلومات تخطيطية.  
- كامل الخط الأنابيب يعمل على الـ GPU، مما يمكن أن يكون **أسرع 5‑10×** من المعالجة باستخدام المعالج فقط للصور عالية الدقة.

---

## الخطوة 5: تشغيل العرض التوضيحي والتحقق من المخرجات

قم بترجمة البرنامج وتشغيله:

```bash
mvn compile exec:java -Dexec.mainClass=GpuOcrDemo
```

إذا تم توصيل كل شيء بشكل صحيح، يجب أن ترى شيئًا مشابهًا لـ:

```
Aspose OCR license applied successfully.
GPU options configured (memory limit = 2048 MB).
Recognized Text (GPU):
Item   Qty   Price
Apple   2    $1.20
Banana  5    $0.75
Total          $5.85
```

النص الدقيق يعتمد على صورتك، لكن المهم أن وحدة التحكم تطبع **النص المعترف به** دون علامة مائية “Evaluation version”. إذا واجهت خطأ `CUDA driver not found`، تأكد من تحديث تعريفات الـ GPU وأن مجموعة أدوات CUDA موجودة في مسار النظام.

---

## المشكلات الشائعة وكيفية تجنبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| `OutOfMemoryError: CUDA out of memory` | تجاوزت ذاكرة الـ GPU الحد | قلل `setMemoryLimitMb` (مثلاً 1024) أو عالج أجزاء أصغر من الصورة. |
| `LicenseException` | ملف الترخيص مفقود أو المسار غير صحيح | تأكد من أن `Aspose.OCR.Java.lic` قابل للوصول والمسار مطابق. |
| لا يتم إرجاع نص | الصورة غير واضحة أو مساحة اللون غير صحيحة | عالج الصورة مسبقًا (زيادة التباين، التحويل إلى تدرج رمادي) قبل تمريرها إلى OCR. |
| الـ GPU غير مستخدم | `setEnableGpu(false)` أو نقص في التعريف | تحقق من `gpuOptions.setEnableGpu(true)` وأعد تثبيت تعريفات الـ GPU. |

---

## توسيع المثال

الآن بعد أن لديك **مثال Aspose OCR Java** قوي، قد ترغب في:

- **معالجة دفعة من الملفات** – حلقة عبر المجلدات واحفظ النتائج في قاعدة بيانات.  
- **اكتشاف اللغة** – استخدم `ocrEngine.setLanguage(OcrLanguage.English)` أو أضف لغات متعددة.  
- **تطبيق ما بعد المعالجة** – نظف السلسلة الخام باستخدام regex أو أرسلها إلى مدقق إملائي.  

جميع هذه الإضافات تعيد استخدام نفس كود الترخيص وإعداد الـ GPU، لذا عليك فقط إضافة منطق الأعمال.

---

## الخلاصة

لقد رأيت الآن مثالًا كاملًا **Aspose OCR Java** ي **استخراج النص من صورة Java** مع **ضبط حد ذاكرة الـ GPU** لأداء موثوق. الأفكار الأساسية—الترخيص مبكرًا، تكوين الـ GPU، تحميل الصورة، قراءة النص—قابلة لإعادة الاستخدام عبر عدد لا يحصى من المشاريع، من ماسحات الفواتير إلى أنظمة إدخال النماذج الآلية.

من هنا، لا تتردد في تجربة قيم `GpuEngineOptions` مختلفة، تجربة صور أكبر، أو دمج خطوة OCR في خدمة microservice باستخدام Spring Boot. السماء هي الحد، وبفضل تسريع الـ GPU، الحد أصبح أعلى بكثير مما كان.

هل لديك أسئلة أو تحتاج مساعدة في ضبط إعدادات الذاكرة لمعداتك الخاصة؟ اترك تعليقًا أدناه، وبرمجة سعيدة!

---

![مخطط مثال Aspose OCR Java يوضح التدفق من إدخال الصورة → OCR معزز بالـ GPU → إخراج النص](https://example.com/images/aspose-ocr-java-example-diagram.png "مخطط مثال Aspose OCR Java")

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [كيفية ضبط الترخيص والتحقق من ترخيص Aspose.OCR في Java](/ocr/english/java/ocr-basics/set-license/)
- [استخراج النص من صورة Java باستخدام وضع اكتشاف المناطق في Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [تحويل الصورة إلى نص في Java باستخدام Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}