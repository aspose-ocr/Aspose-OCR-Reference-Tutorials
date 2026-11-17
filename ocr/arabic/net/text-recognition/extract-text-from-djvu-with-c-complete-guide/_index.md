---
category: general
date: 2026-06-25
description: استخراج النص من DjVu باستخدام C# و Aspose OCR – تعلّم كيفية تحويل DjVu
  إلى نص في بضع خطوات بسيطة.
draft: false
keywords:
- extract text from djvu
- convert djvu to text
- Aspose OCR C#
- DjVu OCR example
- .NET document processing
language: ar
og_description: استخراج النص من ملفات DjVu باستخدام C# و Aspose OCR. اتبع هذا الدليل
  خطوة بخطوة لتحويل DjVu إلى نص بسرعة وموثوقية.
og_title: استخراج النص من DjVu باستخدام C# – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from DjVu with C# using Aspose OCR – learn how to convert
    DjVu to text in a few simple steps.
  headline: Extract Text from DjVu with C# – Complete Guide
  type: TechArticle
- description: Extract text from DjVu with C# using Aspose OCR – learn how to convert
    DjVu to text in a few simple steps.
  name: Extract Text from DjVu with C# – Complete Guide
  steps:
  - name: '**Low quality scans** – DjVu can compress images heavily, which sometimes
      hurts OCR accuracy. Increase the DPI before feeding the image to Aspose: `ocrEngine.ImageProcessingOptions.Dpi
      = 300;`.'
    text: '**Low quality scans** – DjVu can compress images heavily, which sometimes
      hurts OCR accuracy. Increase the DPI before feeding the image to Aspose: `ocrEngine.ImageProcessingOptions.Dpi
      = 300;`.'
  - name: '**Non‑Latin scripts** – By default Aspose OCR assumes English. Switch the
      language pack (`ocrEngine.Language = OcrLanguage.Russian;`) to improve results
      for Cyrillic or other alphabets.'
    text: '**Non‑Latin scripts** – By default Aspose OCR assumes English. Switch the
      language pack (`ocrEngine.Language = OcrLanguage.Russian;`) to improve results
      for Cyrillic or other alphabets.'
  - name: '**Memory leaks** – `OcrImage` implements `IDisposable`. In a long‑running
      service, wrap image loading in a `using` block.'
    text: '**Memory leaks** – `OcrImage` implements `IDisposable`. In a long‑running
      service, wrap image loading in a `using` block.'
  - name: '**Unexpected null result** – If `ocrResult.Text` is empty, check `ocrResult.HasError`
      and inspect `ocrResult.ErrorMessage` for clues (e.g., unsupported file format).'
    text: '**Unexpected null result** – If `ocrResult.Text` is empty, check `ocrResult.HasError`
      and inspect `ocrResult.ErrorMessage` for clues (e.g., unsupported file format).'
  type: HowTo
tags:
- C#
- OCR
- DjVu
- Aspose
title: استخراج النص من DjVu باستخدام C# – دليل شامل
url: /ar/net/text-recognition/extract-text-from-djvu-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من ملفات DjVu باستخدام C# – دليل شامل

هل تحتاج إلى **استخراج النص من ملفات DjVu** في تطبيق .NET؟ يوضح لك هذا الدليل كيفية استخراج النص من DjVu باستخدام Aspose OCR ويغطي أيضًا كيفية **تحويل DjVu إلى نص** بكفاءة. سواءً كنت تقوم برقمنة كتيبات قديمة أو استخراج سلاسل قابلة للبحث من كتب ممسوحة ضوئيًا، فإن الشيفرة أدناه تنجز المهمة في ثوانٍ.

في الأقسام التالية سنستعرض كل سطر من البرنامج النموذجي، نشرح لماذا كل خطوة مهمة، ونشير إلى المشكلات الشائعة التي قد تواجهها. في النهاية ستحصل على تطبيق كونسول جاهز للتنفيذ يطبع نتيجة OCR مباشرةً في الكونسول – دون الحاجة إلى أدوات إضافية.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

* **.NET 6.0** (أو أي نسخة حديثة من .NET) مثبتة على جهازك.  
* حزمة **Aspose.OCR** من NuGet – يمكنك إضافتها باستخدام `dotnet add package Aspose.OCR`.  
* ملف **DjVu** تريد معالجته (المثال يستخدم `old_manual.djvu`).  
* كمية جيدة من القهوة – لأن تصحيح أخطاء OCR قد يكون غريبًا بعض الشيء.

هذا كل شيء. لا توجد تبعيات خارجية ثقيلة، ولا COM interop، فقط C# عادي.

## استخراج النص من DjVu – تنفيذ خطوة بخطوة

البرنامج الكامل القابل للتنفيذ أدناه. انسخه في مشروع كونسول جديد، استبدل مسار الملف، واضغط **F5**.

```csharp
using System;
using Aspose.OCR;

namespace DjvuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            // The OcrEngine is the heart of Aspose OCR – it holds
            // configuration like language, resolution, and
            // recognition mode. You can tweak these settings
            // later if the default output isn’t satisfactory.
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Load the DjVu file to be processed
            // -------------------------------------------------
            // OcrImage.FromFile understands many formats,
            // DjVu included. If the file can’t be found,
            // an exception will be thrown – wrap this in
            // a try/catch in production code.
            var djvuImage = OcrImage.FromFile(@"YOUR_DIRECTORY\old_manual.djvu");

            // -------------------------------------------------
            // Step 3: Perform OCR recognition on the loaded image
            // -------------------------------------------------
            // Recognize returns an OcrResult object that contains
            // the extracted text, confidence scores, and more.
            // The method is synchronous; for large batches
            // consider the async overload.
            var ocrResult = ocrEngine.Recognize(djvuImage);

            // -------------------------------------------------
            // Step 4: Output the recognized text to the console
            // -------------------------------------------------
            // The Text property holds the plain‑text result.
            // You can also write it to a file, a database,
            // or feed it into a search index.
            Console.WriteLine("=== OCR Output Start ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== OCR Output End ===");
        }
    }
}
```

### لماذا كل خطوة مهمة

| الخطوة | الغرض | نصائح وحالات خاصة |
|------|---------|-------------------|
| **Create OcrEngine** | إنشاء محرك OCR بالإعدادات الافتراضية. | إذا كنت بحاجة إلى لغة معينة (مثلاً الفرنسية)، عيّن `ocrEngine.Language = OcrLanguage.French;` قبل عملية التعرف. |
| **Load DjVu file** | قراءة حاوية DjVu واستخراج الصور النقطية للـ OCR. | يمكن أن تحتوي ملفات DjVu على عدة صفحات. Aspose OCR يعالج الصفحة الأولى تلقائيًا؛ لمعالجة ملفات متعددة الصفحات، كرّر عبر `djvuImage.Pages`. |
| **Recognize** | تشغيل خوارزمية استخراج النص الفعلية. | الملفات الكبيرة قد تستغرق بضع ثوانٍ. للوظائف الدفعة، أعد استخدام نفس كائن `OcrEngine` لتجنب تكلفة التهيئة المتكررة. |
| **Print result** | عرض النص المستخرج. | الكونسول مناسب للعرض التجريبي، لكن في التطبيقات الفعلية يمكنك كتابة النتيجة إلى ملف `.txt`: `File.WriteAllText("output.txt", ocrResult.Text);`. |

#### تحويل DjVu إلى نص على نطاق واسع

إذا كان لديك مجلد مليء بكتيبات DjVu، غلف المنطق أعلاه بحلقة بسيطة:

```csharp
string sourceDir = @"C:\DjVuDocs";
foreach (var file in Directory.GetFiles(sourceDir, "*.djvu"))
{
    var image = OcrImage.FromFile(file);
    var result = ocrEngine.Recognize(image);
    string txtPath = Path.ChangeExtension(file, ".txt");
    File.WriteAllText(txtPath, result.Text);
    Console.WriteLine($"Converted {Path.GetFileName(file)} → {Path.GetFileName(txtPath)}");
}
```

*نصيحة محترف*: احذف كائنات `OcrImage` المؤقتة بعد كل تكرار (`image.Dispose()`) لتقليل استهلاك الذاكرة عند معالجة مئات الملفات.

## التعامل مع المشكلات الشائعة

1. **مسحات منخفضة الجودة** – يمكن أن يضغط DjVu الصور بشكل كبير، مما يؤثر أحيانًا على دقة OCR. زد الـ DPI قبل تمرير الصورة إلى Aspose: `ocrEngine.ImageProcessingOptions.Dpi = 300;`.
2. **الخطوط غير اللاتينية** – افتراضيًا يفترض Aspose OCR اللغة الإنجليزية. غيّر حزمة اللغة (`ocrEngine.Language = OcrLanguage.Russian;`) لتحسين النتائج للخطوط السيريالية أو غيرها.
3. **تسرب الذاكرة** – `OcrImage` يطبق `IDisposable`. في خدمة طويلة التشغيل، احط تحميل الصورة بكتلة `using`.
4. **نتيجة فارغة غير متوقعة** – إذا كان `ocrResult.Text` فارغًا، تحقق من `ocrResult.HasError` واطلع على `ocrResult.ErrorMessage` للحصول على دلائل (مثل تنسيق ملف غير مدعوم).

## النتيجة المتوقعة

تشغيل العينة على دليل DjVu واضح باللغة الإنجليزية يجب أن ينتج شيئًا مشابهًا لـ:

```
=== OCR Output Start ===
Chapter 1 – Introduction
This manual explains how to operate the XYZ device...
...
=== OCR Output End ===
```

إذا ظهرت النتيجة مشوهة، راجع النصائح أعلاه—خاصةً إعدادات DPI واللغة.

## ملخص هيكل المشروع الكامل

```
DjvuOcrDemo/
│
├─ Program.cs          <-- contains the code shown earlier
├─ old_manual.djvu    <-- your source DjVu file
└─ DjvuOcrDemo.csproj <-- .NET project file (auto‑generated)
```

ابنِ المشروع باستخدام `dotnet build` وشغّله بـ `dotnet run`. هذا كل ما يلزم **لاستخراج النص من DjVu** و**تحويل DjVu إلى نص** باستخدام C#.

## الخطوات التالية والمواضيع ذات الصلة

* **ما بعد المعالجة** – استخدم التعبيرات النمطية لتنظيف فواصل الأسطر أو إزالة العناوين.
* **دمج البحث** – أدخل ناتج OCR إلى Elasticsearch للبحث النصي الكامل عبر أرشيف DjVu الخاص بك.
* **معالجة الصور مسبقًا** – اجمع بين Aspose OCR وAspose.Imaging لتصحيح الميل أو إزالة الضوضاء قبل التعرف.
* **مكتبات بديلة** – إذا كنت تفضّل مجموعة مفتوحة المصدر، استكشف `Tesseract` مع خطوة تحويل DjVu إلى PNG.

لا تتردد في التجربة: جرّب قيم DPI مختلفة، غيّر حزم اللغة، أو عالج دليلًا كاملاً دفعة واحدة. النمط الأساسي يبقى نفسه—أنشئ محركًا، حمّل صورة DjVu، نفّذ التعرف، وتعامل مع النتيجة.

---

*برمجة سعيدة! إذا صادفتك أي مشاكل، اترك تعليقًا أدناه وسنساعدك في حلها.*


## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}