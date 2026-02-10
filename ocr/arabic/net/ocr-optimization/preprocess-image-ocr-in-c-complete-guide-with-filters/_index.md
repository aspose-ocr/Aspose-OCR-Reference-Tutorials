---
category: general
date: 2026-02-09
description: تعلم كيفية التحضير المسبق لتقنية OCR للصور والتعرف على نص الصورة باستخدام
  Aspose OCR. قلل ضوضاء الصورة، أضف الفلاتر، واستخرج النص العادي خلال دقائق.
draft: false
keywords:
- preprocess image OCR
- recognize text image
- extract plain text
- reduce image noise
- how to add filters
language: ar
og_description: قم بمعالجة OCR للصور بسرعة. يوضح هذا الدليل كيفية إضافة الفلاتر، وتقليل
  ضوضاء الصورة، واستخراج النص العادي من أي صورة.
og_title: معالجة مسبقة لتقنية OCR للصور في C# – دليل خطوة بخطوة
tags:
- OCR
- C#
- Image Processing
title: معالجة مسبقة لتقنية OCR للصور في C# – دليل شامل مع الفلاتر
url: /ar/net/ocr-optimization/preprocess-image-ocr-in-c-complete-guide-with-filters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# معالجة صورة OCR في C# – دليل شامل مع الفلاتر

هل واجهت صعوبة في **معالجة صورة OCR** لأن مسحاتك مائلة، أو ذات حبيبات، أو صعب قراءتها؟ لست وحدك. في العديد من المشاريع الواقعية، يمكن أن تجعل صورة إيصال مهتزّة أو نموذج ممسوح ضوضائيًّا محرك OCR ينتج نصًا غير مفهوم بدلاً من بيانات مفيدة.  

الخبر السار؟ يمكنك تنظيف تلك الصور قبل تمريرها إلى المحرك، وستحصل على دقة أعلى بشكل ملحوظ عندما **تتعرف على نص الصورة**. في هذا الدرس سنستعرض خطوة بخطوة **كيفية إضافة الفلاتر**، تقليل الضوضاء، وأخيرًا **استخراج النص العادي** باستخدام Aspose.OCR في C#.

سنغطي كل ما تحتاجه—من تثبيت المكتبة إلى تشغيل الكود والتحقق من النتيجة—حتى تتمكن من نسخ‑لصق حل يعمل فورًا.

---

## ما ستحتاجه

- **.NET 6+** (أو أي نسخة حديثة من .NET؛ API يعمل بنفس الطريقة)
- حزمة NuGet **Aspose.OCR for .NET**  
  ```bash
  dotnet add package Aspose.OCR
  ```
- صورة نموذجية تعاني من دوران، ضوضاء، أو تباين منخفض (مثال: `skewed_noisy.jpg`)
- بيئة تطوير أو محرر تفضله (Visual Studio، VS Code، Rider—اختر ما يناسبك)

هذا كل ما تحتاجه. لا مكتبات أصلية إضافية، ولا أطر معالجة صور ثقيلة. Aspose يأتي مع الفلاتر التي نحتاجها.

---

## الخطوة 1 – إنشاء كائن محرك OCR  

أول ما تقوم به هو إنشاء `OcrEngine`. فكر فيه كالعقل الذي سيقرأ الأحرف بعد أن ننظف الصورة.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;

class FilterExample
{
    static void Main()
    {
        // Initialize the OCR engine – this object will hold our filters and settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **لماذا هذا مهم:** المحرك يحتوي على **خط أنابيب المعالجة المسبقة**. إضافة الفلاتر لاحقًا سيجعلها تُطبق تلقائيًا في كل مرة تستدعي فيها `Recognize`.

---

## الخطوة 2 – إضافة فلاتر لتقليل ضوضاء الصورة وتحسين قابلية القراءة  

الآن **نضيف الفلاتر**. كل فلتر يعالج عيبًا محددًا:

| الفلتر | ما يُصلحه | القيم النموذجية المستخدمة |
|--------|-----------|---------------------------|
| `DeskewFilter` | النص المائل (الانحراف) | `MaxAngle = 12` (درجة) |
| `DenoiseFilter` | البقع العشوائية، الحبيبات | `Strength = 0.6` (0‑1) |
| `ContrastBoostFilter` | الأحرف الباهتة | `Level = 1.3` (1‑2) |
| `BinarizeAdaptiveFilter` | الإضاءة غير المتساوية | الإعدادات الافتراضية تعمل جيدًا |

```csharp
        // Step 2: Add preprocessing filters to improve image quality
        //   • Deskew to correct rotation (max 12°)
        //   • Denoise to reduce noise (strength 0.6)
        //   • Contrast boost to enhance visibility (level 1.3)
        //   • Adaptive binarization for better binarization
        ocrEngine.Preprocessing.Add(new DeskewFilter { MaxAngle = 12 });
        ocrEngine.Preprocessing.Add(new DenoiseFilter { Strength = 0.6 });
        ocrEngine.Preprocessing.Add(new ContrastBoostFilter { Level = 1.3 });
        ocrEngine.Preprocessing.Add(new BinarizeAdaptiveFilter());
```

> **نصيحة محترف:** إذا كانت صورك بالفعل مستقيمة، يمكنك تخطي خطوة تصحيح الميل. إزالة الفلاتر غير الضرورية تُسرّع المعالجة.

---

## الخطوة 3 – تحميل الصورة التي تريد معالجتها  

بعد ذلك، نخبر المحرك أي صورة يجب تنظيفها. `ImageStream.FromFile` يقرأ الملف إلى صيغة يفهمها محرك OCR.

```csharp
        // Step 3: Load the image that needs OCR processing
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **حالة خاصة:** عند العمل مع تدفقات (streams) تأتي من واجهة ويب API، استبدل `FromFile` بـ `FromStream` لتجنب الوصول إلى نظام الملفات.

---

## الخطوة 4 – تشغيل محرك OCR والتعرف على نص الصورة  

الآن يحدث السحر. المحرك يطبق كل الفلاتر التي أضفناها، ثم ينفّذ التعرف على الأحرف.

```csharp
        // Step 4: Run the OCR engine on the prepared image
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **لماذا هذا يعمل:** خط أنابيب المعالجة المسبقة يضمن أن الصورة الممرَّرة إلى المُعرّف نظيفة قدر الإمكان، مما يعزز مباشرةً دقة **التعرف على نص الصورة**.

---

## الخطوة 5 – استخراج النص العادي وعرضه  

أخيرًا، نستخرج النتيجة النصية العادية ونطبعها على وحدة التحكم. هذه هي خطوة **استخراج النص العادي** في سير العمل.

```csharp
        // Step 5: Output the recognized plain text
        Console.WriteLine(ocrResult.PlainText);
    }
}
```

### النتيجة المتوقعة

إذا كانت `skewed_noisy.jpg` تحتوي على سطر فاتورة بسيط مثل `Total: $123.45`، يجب أن ترى:

```
Total: $123.45
```

حتى وإن كانت الملف الأصلي مائلًا 10°، يحتوي على بقع، وتباينه منخفض، يجب أن تقوم الفلاتر بتنظيفه بما يكفي ليقرأه محرك OCR بشكل صحيح.

---

## نظرة بصرية عامة  

فيما يلي توضيح سريع لخط أنابيب المعالجة المسبقة. المخطط ليس ضروريًا لتشغيل الكود، لكنه يساعد على تصور التدفق.

![preprocess image OCR diagram](https://example.com/ocr-pipeline.png "preprocess image OCR pipeline")

*نص بديل: مخطط معالجة صورة OCR يُظهر خطوات تصحيح الميل، إزالة الضوضاء، تعزيز التباين، والتحويل الثنائي التكيفي.*

---

## أسئلة شائعة ومشكلات محتملة  

- **ماذا لو كانت نتيجة OCR لا تزال مشوشة؟**  
  جرّب زيادة `DenoiseFilter.Strength` إلى `0.8` أو خفض `ContrastBoostFilter.Level` إلى `1.1`. زيادة التباين بشكل مفرط قد تُنشئ هالات تُربك المُعرّف.

- **هل يمكنني إضافة فلتر مخصص خاص بي؟**  
  نعم. يتيح لك Aspose.OCR تنفيذ `IFilter` وحقنه في `ocrEngine.Preprocessing`. هذا موضوع متقدم، لكنه مفيد عندما تكون لديك احتياجات معالجة مسبقة خاصة بالمجال.

- **هل يعمل هذا مع ملفات PDF؟**  
  فقط إذا قمت أولًا بتحويل كل صفحة PDF إلى صورة (مثلاً باستخدام Aspose.PDF). بمجرد حصولك على صورة bitmap، تُطبق سلسلة الفلاتر نفسها.

- **هل المكتبة آمنة للاستخدام متعدد الخيوط؟**  
  كائن `OcrEngine` **ليس** آمنًا للاستخدام متعدد الخيوط. أنشئ محركًا منفصلًا لكل خيط أو غلف الاستدعاءات بـ lock.

---

## توسيع المثال  

الآن بعد أن لديك أساسًا ثابتًا، فكر في الخطوات التالية:

1. **المعالجة الدفعية** – كرّر عبر مجلد من الصور، طبّق نفس سلسلة الفلاتر، واكتب كل نتيجة إلى ملف `.txt`.  
2. **حزم اللغات** – إذا كنت بحاجة إلى التعرف على الفرنسية أو الألمانية، حمّل بيانات اللغة المناسبة عبر `ocrEngine.Language = "fra"` (أو `"deu"`).  
3. **منطقة الاهتمام (ROI)** – استخدم `ocrEngine.Recognize(image, new Rectangle(x, y, width, height))` للتركيز على منطقة محددة، مما قد يسرّع معالجة المسحات الكبيرة.

---

## الخلاصة  

في هذا الدليل قمنا **بمعالجة صورة OCR** بإضافة سلسلة من الفلاتر المدمجة، ثم **تعرّفنا على نص الصورة** وأخيرًا **استخراجنا النص العادي** من صورة مشوشة ومائلة. الكود الكامل القابل للتنفيذ موجود أعلاه، ويمكنك تكييفه مع أي مشروع C# يحتاج إلى نتائج OCR موثوقة.  

تذكر، المفتاح للحصول على OCR ممتاز ليس فقط محرك قوي—بل إدخال نظيف. من خلال تقليل ضوضاء الصورة ومحاذاة النص بشكل صحيح، تمنح المُعرّف أفضل فرصة للنجاح.  

لا تتردد في تجربة قيم الفلاتر، تجربة صيغ صور مختلفة، أو دمج هذا النهج مع مكتبات Aspose أخرى. إذا واجهت أي عائق، اترك تعليقًا أدناه أو راجع الوثائق الرسمية لـ Aspose لتفاصيل أعمق حول كل فئة فلتر. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}