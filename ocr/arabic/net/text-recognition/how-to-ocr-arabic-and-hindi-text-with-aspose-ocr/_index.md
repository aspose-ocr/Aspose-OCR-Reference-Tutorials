---
category: general
date: 2026-01-15
description: تعلم كيفية التعرف الضوئي على النص العربي وتحديد النص الهندي باستخدام
  Aspose OCR. يوضح لك هذا الدليل خطوة بخطوة كيفية استخراج النص من الصورة وتحويل الصورة
  إلى نص بكفاءة.
draft: false
keywords:
- how to ocr arabic
- recognize arabic text
- extract text from image
- convert image to text
- recognize hindi text
language: ar
og_description: كيفية التعرف الضوئي على النص العربي وتعرف النص الهندي في برنامج C#
  واحد. اتبع هذا الدليل الكامل لاستخراج النص من الصورة وتحويل الصورة إلى نص.
og_title: كيفية التعرف الضوئي على النص العربي والهندي باستخدام Aspose OCR
tags:
- Aspose OCR
- C#
- Multilingual OCR
title: كيفية التعرف الضوئي على النص العربي والهندي باستخدام Aspose OCR
url: /ar/net/text-recognition/how-to-ocr-arabic-and-hindi-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف الضوئي على النص العربي والهندي باستخدام Aspose OCR

هل تساءلت يومًا **كيفية التعرف الضوئي على النص العربي** الذي يتدفق من اليمين إلى اليسار، مع استخراج الحروف الهندية من إيصال؟ لست وحدك. يواجه العديد من المطورين نفس المشكلة عندما يحتاجون إلى **التعرف على النص العربي** و**التعرف على النص الهندي** في نفس سير العمل.  

في هذا الدرس سنستعرض مثالًا كاملاً وقابلاً للتنفيذ بلغة C# يوضح لك كيفية **استخراج النص من الصورة**، **تحويل الصورة إلى نص**، ومعالجة كل من النص العربي والهندي باستخدام Aspose OCR. لا مراجع غامضة—فقط الكود الذي يمكنك نسخه‑لصقه، بالإضافة إلى شرح كل سطر.

> **نصيحة احترافية:** إذا لم تستخدم Aspose OCR من قبل، قم أولاً بتثبيت حزمة NuGet `Aspose.OCR`. إنها عملية بنقرة واحدة في Visual Studio، وتقوم بجلب جميع الملفات الثنائية الأصلية التي تحتاجها للتعرف القائم على وحدة المعالجة المركزية.

---

![how to ocr arabic example](/images/arabic-ocr-sample.png "كيفية التعرف الضوئي على النص العربي – مثال على لافتة عربية")

*نص بديل للصورة:* **مثال على كيفية التعرف الضوئي على النص العربي**  

---

## كيفية التعرف الضوئي على النص العربي – إعداد البيئة

قبل الغوص في الكود، دعنا نتأكد من أن بيئة التطوير جاهزة.

1. **الإطار المستهدف** – .NET 6.0 أو أحدث. الإصدارات الأقدم لا تزال تُترجم، لكنك ستفقد أحدث ميزات اللغة.  
2. **الحزمة** – نفّذ `dotnet add package Aspose.OCR` في الطرفية، أو استخدم واجهة مدير الحزم NuGet.  
3. **الصور** – ضع صورتين مثاليتين في مجلد يمكنك الإشارة إليه، مثل `C:\OCRSamples\arabic_sign.jpg` و `C:\OCRSamples\hindi_receipt.png`. يجب أن تحتوي الصورة العربية على أحرف عربية واضحة وعالية التباين؛ ويمكن أن تكون الصورة الهندية إيصالًا ممسوحًا ضوئيًا أو صورة لافتة.  

هذا كل شيء—لا ملفات إعداد إضافية، لا برامج تشغيل GPU، مجرد محرك OCR يعتمد على وحدة المعالجة المركزية.

---

## التعرف على النص العربي – التحميل والمعالجة

الآن سنقوم فعليًا **بالتعرف على النص العربي**. المفتاح هو إخبار المحرك باللغة المتوقعة؛ وإلا سيفترض المحرك أن النص لاتيني وستحصل على مخرجات مشوشة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class MultiLangDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine (CPU‑based by default)
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load an image that contains Arabic script
        var arabicImage = OcrImage.FromFile(@"C:\OCRSamples\arabic_sign.jpg");

        // 3️⃣ Recognize the Arabic text – note the Language.Arabic enum
        var arabicResult = ocrEngine.Recognize(arabicImage, Language.Arabic);

        // 4️⃣ Print the result to the console
        System.Console.WriteLine("Arabic: " + arabicResult.Text);
```

**لماذا يعمل هذا:**  
* `OcrEngine` يتعامل مع جميع الأعمال الثقيلة—المعالجة المسبقة، التجزئة، وتصنيف الأحرف.  
* بتمرير `Language.Arabic`، نقوم بتنشيط محرك التخطيط من اليمين إلى اليسار ومجموعة الأحرف العربية. بدون ذلك، سيعامل المحرك الصورة كنص لاتيني من اليسار إلى اليمين، مما يؤدي إلى فقدان العلامات وتقطّع الكلمات.  

**الناتج المتوقع** (النص الفعلي سيختلف بناءً على الصورة):

```
Arabic: مرحبا بكم في متجرنا
```

إذا رأيت سلاسل فارغة، تحقق مرة أخرى من أن الصورة ليست مظلمة جدًا وأن مسار الملف صحيح.  

---

## استخراج النص من الصورة – معالجة النصوص من اليمين إلى اليسار

العربية ليست النص الوحيد الذي يحتاج إلى معالجة خاصة. اللغات التي تُكتب من اليمين إلى اليسار تتطلب من محرك OCR عكس الترتيب البصري بعد التعرف. يقوم Aspose بذلك تلقائيًا عندما تحدد `Language.Arabic`، لكن يجدر الإشارة إلى ذلك لتوسعات مستقبلية (مثل العبرية).

*نصيحة:* عند عرض نتيجة OCR في واجهة المستخدم لاحقًا، تأكد من أن التحكم يدعم العرض من اليمين إلى اليسار؛ وإلا سيظهر النص مشوشًا.

---

## تحويل الصورة إلى نص – العمل مع اللغة الهندية

ننتقل الآن إلى **تحويل الصورة إلى نص** لإيصال هندي. العملية مشابهة لتدفق العربية، لكننا نستخدم `Language.Hindi` بدلاً من ذلك.

```csharp
        // 5️⃣ Load the Hindi (Devanagari) image
        var hindiImage = OcrImage.FromFile(@"C:\OCRSamples\hindi_receipt.png");

        // 6️⃣ Recognize Hindi text – Language.Hindi tells the engine to use Devanagari models
        var hindiResult = ocrEngine.Recognize(hindiImage, Language.Hindi);

        // 7️⃣ Output the Hindi OCR result
        System.Console.WriteLine("Hindi: " + hindiResult.Text);
    }
}
```

**لماذا نعيد استخدام نفس كائن `ocrEngine`:**  
إن إنشاء محرك جديد لكل لغة سيهدر الذاكرة ووقت التهيئة. محرك Aspose آمن للاستخدام المتسلسل عبر الخيوط، لذا فإن إعادة استخدامه فعال ونظيف.

**نموذج مخرجات وحدة التحكم** (مرة أخرى، يعتمد على صورتك):

```
Hindi: कुल राशि: ₹ 1,250.00
```

إذا ظهر النص الهندي كحروف لاتينية مشوشة، فربما نسيت تحديد تعداد اللغة أو أن دقة الصورة منخفضة (<300 dpi). تكبير الصورة أو تطبيق مرشح ثنائي بسيط يمكن أن يحسّن الدقة بشكل كبير.

---

## التعرف على النص الهندي – المشكلات الشائعة والحالات الخاصة

حتى مع تعيين لغة صحيحة، قد تواجه بعض العقبات:

| المشكلة | العَرَض | الحل |
|-------|---------|-----|
| انخفاض التباين | العديد من الأحرف تصبح “؟” أو تُحذف | معالجة مسبقة باستخدام `OcrImage.AdjustContrast(1.5)` |
| الصورة مائلة | النص يظهر مدوّرًا، ويعيد OCR سلسلة فارغة | استدعاء `ocrEngine.PreprocessImage(arabicImage, ImageProcessingOptions.Rotate)` |
| لغات مختلطة | سطر عربي يليه أرقام إنجليزية | تشغيل تمريرين: أولاً بـ `Language.Arabic`، ثم بـ `Language.English` على نفس الصورة ودمج النتائج |
| حجم ملف كبير | التعرف بطيء أو أخطاء نفاد الذاكرة | تقليل الحجم إلى أقصى عرض 2000 بكسل باستخدام `OcrImage.Resize(2000, 0)` |

هذه النصائح تساعدك على **استخراج النص من الصورة** التي لا تكون ممسوحة ضوئيًا بشكل مثالي، وهو أمر شائع في المشاريع الواقعية.

---

## تجميع كل شيء معًا – مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه مباشرةً إلى مشروع وحدة تحكم جديد. لا تبعيات مخفية، لا إعدادات إضافية—فقط C# صافي.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class MultiLangDemo
{
    static void Main()
    {
        // Initialize the OCR engine (CPU‑based)
        var ocrEngine = new OcrEngine();

        // -------------------- Arabic --------------------
        var arabicPath = @"C:\OCRSamples\arabic_sign.jpg";
        var arabicImage = OcrImage.FromFile(arabicPath);
        var arabicResult = ocrEngine.Recognize(arabicImage, Language.Arabic);
        System.Console.WriteLine("Arabic: " + arabicResult.Text);

        // -------------------- Hindi --------------------
        var hindiPath = @"C:\OCRSamples\hindi_receipt.png";
        var hindiImage = OcrImage.FromFile(hindiPath);
        var hindiResult = ocrEngine.Recognize(hindiImage, Language.Hindi);
        System.Console.WriteLine("Hindi: " + hindiResult.Text);
    }
}
```

**تشغيل البرنامج** سيطبع كلًا من السلاسل العربية والهندية إلى وحدة التحكم، مؤكدًا أنك نجحت في **التعرف على النص العربي** و**التعرف على النص الهندي** في تشغيل واحد.  

---

## الخلاصة

أصبح لديك الآن حل شامل من البداية إلى النهاية لسؤال **كيفية التعرف الضوئي على النص العربي** مع معالجة الهندية. من خلال إنشاء `OcrEngine` واحد، تحميل كل صورة، وتمرير تعداد `Language` المناسب، يمكنك **استخراج النص من الصورة**، **تحويل الصورة إلى نص**، و**التعرف على النص العربي** وكذلك **التعرف على النص الهندي** دون أي مكتبات إضافية.  

من هنا قد ترغب في استكشاف:

* **معالجة دفعات** – التكرار عبر مجلد من الصور وتخزين النتائج في قاعدة بيانات.  
* **معالجة لاحقة** – استخدام تعبيرات نمطية لتنظيف رموز العملة في إيصالات اللغة الهندية.  
* **اكتشاف لغة هجين** – تمرير الصورة الخام إلى نموذج تحديد اللغة قبل اختيار الـ enum.  

جرّبه، عدّل خطوات المعالجة المسبقة، وستلاحظ تحسنًا سريعًا في دقة OCR. إذا واجهت أي مشاكل، أرسل  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}