---
category: general
date: 2026-01-10
description: كيفية تشغيل OCR بسرعة واستخراج النص العربي من صورة. تعلم تحويل الصورة
  إلى نص، قراءة النص من PNG، واكتشف كيفية استخراج النص باستخدام Aspose OCR.
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: ar
og_description: كيفية تشغيل OCR في C# واستخراج النص العربي من صورة PNG. يوضح لك هذا
  الدليل كيفية تحويل الصورة إلى نص وقراءة النص من PNG خطوة بخطوة.
og_title: كيفية تشغيل OCR في C# – استخراج النص العربي من PNG
tags:
- OCR
- C#
- Aspose
title: كيفية تشغيل OCR في C# – استخراج النص العربي من PNG
url: /ar/net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تشغيل OCR في C# – استخراج النص العربي من PNG

هل تساءلت يومًا **كيفية تشغيل OCR** على صورة تحتوي على أحرف عربية؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى **استخراج النص العربي** من ملف PNG لكنهم لا يعرفون أي مكتبة ستتعامل مع النصوص من اليمين إلى اليسار دون عناء.  

في هذا الدرس سنستعرض كل ما تحتاج إلى معرفته لـ **تحويل الصورة إلى نص**، **قراءة النص من PNG**، وأخيرًا **كيفية استخراج النص** باستخدام Aspose.OCR في تطبيق C# console بسيط. في النهاية ستحصل على برنامج جاهز للتنفيذ يطبع السلسلة العربية مباشرةً في الطرفية الخاصة بك.

## ما ستتعلمه

- تثبيت وإضافة مرجع لحزمة Aspose.OCR عبر NuGet.  
- تكوين محرك OCR لدعم اللغة العربية.  
- تحميل صورة PNG وتشغيل عملية التعرف.  
- استرجاع وعرض النص المستخرج.  
- تعديل الإعدادات لتحسين الدقة ومعالجة المشكلات الشائعة.

لا يلزم وجود خبرة سابقة في OCR، فقط فهم أساسي للغة C# وبيئة تطوير .NET (Visual Studio، Rider، أو سطر أوامر `dotnet` يكفي).

---

## كيفية تشغيل OCR – إعداد Aspose OCR

### الخطوة 1: إضافة حزمة Aspose.OCR عبر NuGet

أول شيء نحتاجه هو مكتبة OCR نفسها. Aspose.OCR هو منتج تجاري، لكنه يقدم نسخة تجريبية مجانية تعمل بشكل مثالي لأغراض التعلم.

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

بدلاً من ذلك، افتح **NuGet Package Manager** في Visual Studio، ابحث عن **Aspose.OCR**، وانقر على **Install**.

> **نصيحة احترافية:** إذا كنت تخطط لاستخدام المكتبة في خط أنابيب CI، أضف العلامة `-v` لتثبيت الإصدار، مثال: `dotnet add package Aspose.OCR -v 23.10`.

### الخطوة 2: إنشاء مشروع Console جديد (إذا لم يكن لديك واحد)

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

الآن لديك ملف `Program.cs` جديد جاهز لكودنا.

---

## استخراج النص العربي – كتابة كود OCR

فيما يلي البرنامج الكامل الجاهز للتنفيذ. احفظه كملف `Program.cs` (أو استبدل الملف الذي تم إنشاؤه تلقائيًا).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### لماذا كل سطر مهم

- **`OcrEngine`**: الفئة المركزية التي تنسق تحميل الصورة، اختيار اللغة، والتمييز.  
- **`Language = OcrLanguage.Arabic`**: العربية تستخدم نصًا من اليمين إلى اليسار ورموزًا فريدة؛ ضبط اللغة يخبر المحرك باستخدام نماذج الأحرف الصحيحة.  
- **`ImageStream.FromFile`**: يدعم PNG، JPEG، BMP، والعديد من الصيغ الأخرى. إذا احتجت يومًا لقراءة من `MemoryStream` (مثلاً ملف تم رفعه)، استبدل هذا الاستدعاء وفقًا لذلك.  
- **`Recognize()`**: يقوم بالعمل الشاق—تحليل البكسل، التقسيم، وتصنيف الأحرف.  
- **`ocrEngine.Text`**: السلسلة النهائية Unicode، جاهزة لمزيد من المعالجة أو التخزين أو العرض.

### النتيجة المتوقعة

إذا كان الملف `arabic_sample.png` يحتوي على العبارة “مرحبا بالعالم” (Hello World)، فستطبع الطرفية:

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

إذا كان الناتج مشوهًا، تحقق مرة أخرى من وضوح الصورة، وضبط اللغة إلى العربية، وتطابق نسخة محرك OCR مع الوثائق.

---

## تحويل الصورة إلى نص – تحسين الدقة

بينما تعمل الإعدادات الافتراضية لمعظم المسحات النظيفة، غالبًا ما تحتاج الصور الواقعية إلى بعض التحسينات الإضافية.

| الإعداد | ما يفعله | متى يستخدم |
|---------|--------------|-------------|
| `ocrEngine.Config.Preprocess = true` | يفعل التحويل إلى ثنائي وإزالة الضوضاء تلقائيًا. | المستندات الممسوحة ضوئيًا ذات الظلال. |
| `ocrEngine.Config.Deskew = true` | يدور الصورة لتصحيح الميل الطفيف. | الصور الملتقطة بزاوية. |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | يتعامل مع الصورة بأكملها ككتلة نص واحدة. | تسميات بسيطة أو عناوين سطر واحد. |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | يقصر التعرف على الأحرف العربية فقط. | يقلل الإيجابيات الزائفة في الصفحات متعددة اللغات. |

يمكنك إضافة هذه الأسطر مباشرةً بعد إنشاء المحرك:

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## قراءة النص من PNG – التعامل مع مصادر الصور المختلفة

أحيانًا يكون ملف PNG مخزنًا في قاعدة بيانات أو يأتي من طلب ويب. إليك نسخة سريعة تقرأ من `byte[]`:

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

بقية العملية تبقى متطابقة، مما يعني أن **كيفية استخراج النص** تظل ثابتة بغض النظر عن المصدر.

---

## كيفية استخراج النص – الخيارات المتقدمة وحالات الحافة

### 1. ملفات PDF أو TIFF متعددة الصفحات

إذا كنت بحاجة إلى تنفيذ OCR على مستند متعدد الصفحات، قم بالتكرار عبر كل صفحة:

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **ملاحظة:** ستحتاج إلى حزمة `Aspose.PDF` لهذا المقتطف.

### 2. اكتشاف اللغة تلقائيًا

يوفر Aspose.OCR أيضًا اكتشافًا تلقائيًا للغة، لكنه أبطأ. إذا لم تكن متأكدًا ما إذا كانت الصورة تحتوي على العربية أو نص آخر، فعّل ذلك:

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

### 3. نصائح الأداء

- **إعادة استخدام كائن `OcrEngine`** لعدة صور؛ إنشاء نسخة جديدة في كل مرة يضيف عبئًا.  
- **التنفيذ المتوازي** فقط إذا كان لديك محركات منفصلة لكل خيط—مشاركة نسخة واحدة يسبب حالات سباق.

---

## الخلاصة

لقد غطينا **كيفية تشغيل OCR** في C# من البداية إلى النهاية، موضحين لك كيفية **استخراج النص العربي**، **تحويل الصورة إلى نص**، **قراءة النص من PNG**، والإجابة على **كيفية استخراج النص** في مجموعة متنوعة من السيناريوهات. الكود النموذجي كامل، مستقل، وجاهز لتلصقه في أي مشروع .NET console.

ما الخطوة التالية؟ جرّب استبدال `OcrLanguage.Arabic` بالكورية أو السيريلية الصربية لتستكشف قدرة المكتبة المتعددة اللغات. جرب علامات المعالجة المسبقة لتحسين الدقة في المسحات الضوضائية، أو دمج روتين OCR في واجهة برمجة تطبيقات ويب ليتمكن المستخدمون من رفع الصور والحصول على نتائج نصية فورية.

برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة كالكريستال!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}