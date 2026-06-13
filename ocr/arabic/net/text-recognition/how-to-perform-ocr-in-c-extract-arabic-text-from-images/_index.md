---
category: general
date: 2026-03-17
description: تعلم كيفية تنفيذ تقنية التعرف الضوئي على الحروف (OCR) في C# لاستخراج
  النص العربي، والتعرف على النص من الصورة وتحويل الصورة إلى نص مع مثال كامل للكود.
draft: false
keywords:
- how to perform OCR
- extract arabic text
- recognize text from image
- convert image to text
- extract text from image
language: ar
og_description: كيف تقوم بتنفيذ OCR في C#؟ يوضح لك هذا الدليل كيفية استخراج النص العربي،
  والتعرف على النص من الصورة، وتحويل الصورة إلى نص في بضع خطوات فقط.
og_title: كيفية تنفيذ OCR في C# – استخراج النص العربي
tags:
- OCR
- C#
- Arabic
- ImageProcessing
title: كيفية تنفيذ OCR في C# – استخراج النص العربي من الصور
url: /ar/net/text-recognition/how-to-perform-ocr-in-c-extract-arabic-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR في C# – استخراج النص العربي من الصور

هل تساءلت يومًا **كيف تقوم بتنفيذ OCR** على فاتورة عربية أو مستند ممسوح ضوئيًا؟ لست وحدك—العديد من المطورين يواجهون صعوبة عندما يحتاجون لاستخراج الأحرف العربية من صورة bitmap. الخبر السار هو أنه ببضع أسطر من C# يمكنك التعرف على النص من ملفات الصور، تحويل الصورة إلى نص، وفي النهاية **استخراج النص العربي** للمعالجة اللاحقة.

في هذا الدرس سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يوضح لك بالضبط كيفية تنفيذ OCR، لماذا كل خطوة مهمة، وما الذي يجب الانتباه إليه عند التعامل مع النصوص من اليمين إلى اليسار. بنهاية الدرس ستكون قادرًا على **استخراج النص من صورة** باللغات العربية، الأردية، الكردية، أو أي لغة يدعمها محرك OCR.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يتوافق أيضًا مع .NET Core)  
- إشارة إلى مكتبة OCR التي توفر `OcrEngine` (مثل `MyOcrSdk.dll`).  
- ملف صورة يحتوي على نص عربي، مثل `invoice_arabic.png`.  
- إلمام أساسي بتطبيقات C# console.

> **نصيحة احترافية:** إذا لم يكن لديك SDK OCR، فإن النسخة المجانية من *MyOcrSdk* مناسبة للاختبار وتدعم اللغات التي سنستخدمها.

---

## الخطوة 1 – إعداد المشروع واستيراد مساحة الأسماء الخاصة بـ OCR

قبل أن نتمكن من **التعرف على النص من الصورة** نحتاج إلى هيكل مشروع وتعليمات `using` الصحيحة.

```csharp
using System;
using MyOcrSdk;          // <-- Replace with the actual namespace of your OCR library
using MyOcrSdk.IO;       // For ImageStream helper class

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the OCR workflow will go here
        }
    }
}
```

*لماذا هذه الخطوة مهمة:* استيراد مساحات الأسماء الصحيحة يمنحك الوصول إلى `OcrEngine` و `Language` و `ImageStream`. تخطي هذه الخطوة يؤدي إلى أخطاء تجميع قد تكون محبطة للمبتدئين.

---

## الخطوة 2 – إنشاء كائن OCR Engine (الكلمة المفتاحية الأساسية مضمنة)

الآن نقوم فعليًا **بتنفيذ OCR** بإنشاء مثيل للمحرك.

```csharp
// Step 2: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

كائن `OcrEngine` هو قلب العملية؛ فهو يحمل الإعدادات، يقوم بالمعالجة الثقيلة، ويعيد كائن النتيجة الذي يحتوي على السلسلة المستخرجة. فكر فيه كـ “العقل” الذي سيقوم **تحويل الصورة إلى نص**.

---

## الخطوة 3 – اختيار اللغة للتعرف

العربية، الأردية، الكردية… كلها تشترك في نفس عائلة الخط، لذا يجب إخبار المحرك باللغة المتوقعة. هذا يحسن الدقة بشكل كبير.

```csharp
// Step 3: Choose the language for recognition (Arabic, Urdu, Kurdish, etc.)
ocrEngine.Config.Language = Language.Arabic;   // You can switch to Language.Urdu, etc.
```

*لماذا هذه الخطوة مهمة:* محركات OCR تعتمد على نماذج اللغة. اختيار النموذج الصحيح يقلل من الأخطاء في التعرف على الأحرف المتشابهة، خاصةً للخطوط من اليمين إلى اليسار.

---

## الخطوة 4 – تحميل الصورة التي تحتوي على النص

نحتاج إلى bitmap يمكن للمحرك تحليله. الدالة المساعدة `ImageStream.FromFile` تُبسط تفاصيل الإدخال/الإخراج للملف.

```csharp
// Step 4: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_arabic.png");
```

تأكد أن المسار يشير إلى **صورة صالحة**. إذا كان الملف مفقودًا أو تالفًا، سيُطلق المحرك استثناءً، ولن تتمكن من **استخراج النص من صورة** بنجاح.

---

## الخطوة 5 – تشغيل عملية OCR واسترجاع النتيجة

أخيرًا، نستدعي `Recognize()` ونعرض السلسلة المستخرجة.

```csharp
// Step 5: Perform the OCR operation
var ocrResult = ocrEngine.Recognize();

// Step 6: Display the extracted text
Console.WriteLine("=== Extracted Arabic Text ===");
Console.WriteLine(ocrResult.Text);
```

خاصية `ocrResult.Text` تحتوي على تمثيل النص العادي لكل ما تمكن المحرك من قراءته. في معظم الحالات ستظهر مزيجًا من الأحرف العربية والأرقام، وهو مثالي للمعالجة اللاحقة مثل إدخال البيانات في قاعدة أو ترجمتها.

### النتيجة المتوقعة

```
=== Extracted Arabic Text ===
فاتورة رقم: 12345
التاريخ: 2026/03/15
المبلغ: 2500.00 ريال
...
```

إذا رأيت أحرفًا مشوشة، تحقق من إعداد اللغة وتأكد من أن الصورة ذات دقة عالية (300 dpi أو أعلى هو المثالي).

---

## مثال كامل يعمل

فيما يلي **البرنامج الكامل المستقل** يمكنك نسخه ولصقه في مشروع console جديد وتشغيله فورًا.

```csharp
// Full OCR demo – extracts Arabic text from an image
using System;
using MyOcrSdk;
using MyOcrSdk.IO;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Set language – Arabic (change to Urdu or Kurdish if needed)
            ocrEngine.Config.Language = Language.Arabic;

            // 3️⃣ Load the source image
            // Replace YOUR_DIRECTORY with the folder that holds your PNG/JPG
            string imagePath = @"YOUR_DIRECTORY/invoice_arabic.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            try
            {
                // 4️⃣ Run OCR
                var result = ocrEngine.Recognize();

                // 5️⃣ Output the text
                Console.WriteLine("=== Extracted Arabic Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – useful when you need to **extract text from image** in batch jobs
                Console.Error.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

> **ملاحظة:** إذا كان SDK OCR الخاص بك يتطلب ترخيصًا، تأكد من تفعيل الترخيص قبل الخطوة 1 (مثال: `OcrEngine.SetLicense("YOUR_LICENSE_KEY");`). تم حذف هذا السطر هنا لتقليل الطول.

---

## التعامل مع الحالات الشائعة

| الحالة | لماذا يحدث ذلك | الحل السريع |
|-----------|----------------|-----------|
| **صورة غير واضحة أو منخفضة الدقة** | دقة OCR تنخفض إلى أقل من 70 % | امسح بدقة 300 dpi، أو قم بزيادة الدقة باستخدام خوارزمية bicubic قبل تمريرها للمحرك. |
| **لغات مختلطة (عربي + إنجليزي)** | قد يتوقف المحرك بعد أول مجموعة لغة | فعّل وضع متعدد اللغات: `ocrEngine.Config.Language = Language.Arabic \| Language.English;` |
| **مشكلات عرض من اليمين إلى اليسار** | وحدة التحكم تطبع الأحرف من اليسار إلى اليمين، مما يجعل العربية مقلوبة | استخدم `Console.OutputEncoding = System.Text.Encoding.UTF8;` واستخدم طرفية تدعم النصوص RTL. |
| **ملفات PDF كبيرة مقسمة إلى صفحات متعددة** | استهلاك الذاكرة يرتفع | عالج صفحة واحدة في كل مرة: حمّل كل صفحة كصورة منفصلة وكرر تدفق OCR. |
| **رموز خاصة (عملات، تواريخ)** | بعض نماذج OCR تعتبرها ضوضاء | عالج `ocrResult.Text` لاحقًا باستخدام regex لتطبيع الأنماط المعروفة. |

---

## توسيع الحل – من OCR إلى استخراج البيانات

الآن بعد أن **عرفت كيفية تنفيذ OCR**، قد تتساءل: *ماذا يمكنني أن أفعل بالنص العربي المستخرج؟* إليك بعض الأفكار التي تتبع ذلك طبيعيًا:

1. **تحليل الفواتير** – استخدم تعبيرات regex لاستخراج أرقام الفواتير، التواريخ، والمبالغ.  
2. **إرسال النص إلى API ترجمة** – أرسل السلسلة العربية إلى Azure Translator أو Google Cloud Translate.  
3. **تخزين في قاعدة بيانات** – أدخل النص المنقح في جدول SQL للتقارير.  
4. **تشغيل سير عمل** – دمج مع طابور رسائل (مثل RabbitMQ) لبدء المعالجة اللاحقة.

جميع هذه السيناريوهات تعتمد على العملية الأساسية: **تحويل الصورة إلى نص**، ثم معالجة النتيجة.

---

## الخلاصة

غطينا كل ما تحتاج معرفته حول **كيفية تنفيذ OCR** في C# لاستخراج **النص العربي** من صورة. بدءًا من إعداد المشروع، أنشأنا كائن `OcrEngine`، ضبطنا اللغة، حمّلنا bitmap، نفّذنا التعرف، وطبعنا النتيجة. كما ناقشنا العقبات الشائعة وأظهرنا كيفية توسيع التدفق الأساسي إلى خطوط أنابيب واقعية.

جرّبه—غيّر مسار الصورة، غير اللغة إلى الأردية، أو اربط الناتج بقاعدة بيانات. السماء هي الحد عندما تستطيع بثقة **التعرف على النص من صورة** و**تحويل الصورة إلى نص**.

---

### مواضيع ذات صلة قد ترغب في استكشافها

- **استخراج النص من صورة** باستخدام Tesseract OCR (بديل مفتوح المصدر)  
- **معالجة OCR دفعةً** لآلاف ملفات PDF الممسوحة  
- **تحسين دقة OCR** عبر ما قبل معالجة الصورة (تطبيق عتبة، إزالة الضوضاء)  
- **التعامل مع النصوص من اليمين إلى اليسار** في أطر .NET UI (WPF, WinForms)

لا تتردد في ترك تعليق إذا واجهت أي صعوبات، أو مشاركة كيفية تعديلك لهذا النمط في مشاريعك الخاصة. برمجة سعيدة!  

![مثال على كيفية تنفيذ OCR](images/ocr_flow.png "مثال على كيفية تنفيذ OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}