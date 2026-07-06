---
category: general
date: 2026-02-22
description: إنشاء ملف PDF قابل للبحث واستخراج النص من الصورة باستخدام Aspose OCR.
  تعلّم كيفية تحويل الصورة إلى PDF وإنتاج النص العادي في دليل واحد.
draft: false
keywords:
- generate searchable pdf
- extract text from image
- convert image to pdf
- output plain text
- convert scanned image pdf
language: ar
og_description: إنشاء ملف PDF قابل للبحث من الصور الممسوحة ضوئياً باستخدام Aspose
  OCR. يوضح هذا الدليل كيفية استخراج النص من الصورة، وإخراج النص العادي، وتحويل الصورة
  إلى PDF.
og_title: إنشاء PDF قابل للبحث من الصور – دليل C# الكامل
tags:
- C#
- OCR
- PDF generation
- Aspose
title: إنشاء ملف PDF قابل للبحث من الصور في C# – دليل خطوة بخطوة
url: /ar/net/text-recognition/generate-searchable-pdf-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث من الصور في C# – دليل كامل

هل احتجت يومًا إلى **إنشاء PDF قابل للبحث** من صورة ممسوحة ضوئيًا لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك—معظم المطورين يواجهون هذه المشكلة عندما يلتقون بـ OCR لأول مرة. الخبر السار؟ مع Aspose OCR يمكنك **استخراج النص من الصورة**، **إخراج نص عادي**، و**تحويل الصورة إلى PDF** ببضع أسطر من C#.

في هذا الدليل سنستعرض العملية بالكامل، من تحميل ملف PNG إلى حفظ PDF قابل للبحث وملف نص عادي. في النهاية ستحصل على مقتطف قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع .NET. لا إطالة، فقط ما ينجز المهمة.

## ما ستتعلمه

- كيفية إعداد **Aspose.OCR** في تطبيق .NET Console.  
- الفرق بين وضع **إخراج نص عادي** ووضع **PDF قابل للبحث**.  
- كيفية **استخراج النص من الصورة** وكتابته إلى ملف `.txt`.  
- كيفية **تحويل الصورة إلى PDF** مع الحفاظ على الصورة الأصلية وإضافة طبقة نص مخفية.  
- نصائح للتعامل مع دفعات كبيرة، الأخطاء الشائعة، وأين يمكنك تعديل الإعدادات للحصول على دقة أفضل.

> **المتطلبات المسبقة** – تحتاج إلى .NET 6+ (أو .NET Framework 4.7+)، Visual Studio 2022 (أو أي محرر)، ورخصة Aspose OCR (أو نسخة تجريبية مجانية). لا توجد مكتبات طرف ثالث أخرى مطلوبة.

![مثال على PDF قابل للبحث تم إنشاؤه](image-placeholder.png "مثال على PDF قابل للبحث تم إنشاؤه")

## الخطوة 1: تثبيت Aspose OCR وإنشاء المحرك

أولاً وقبل كل شيء—أضف حزمة NuGet إلى مشروعك:

```bash
dotnet add package Aspose.OCR
```

الآن يمكننا تشغيل محرك OCR وإخبارها باللغة التي نتعامل معها. الإنجليزية هي الافتراضية، لكن يمكنك التبديل إلى الفرنسية أو الإسبانية، إلخ، عن طريق تغيير تعداد `Language`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine for English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };
```

**لماذا هذا مهم:** المحرك يحتفظ بجميع الإعدادات—اللغة، صيغة الإخراج، وعلامات ما قبل المعالجة الاختيارية. ضبطه مرة واحدة وإعادة استخدامه يجنبك تكلفة إنشاء نسخة جديدة لكل ملف.

## الخطوة 2: استخراج النص وحفظه كنص عادي

إذا كنت تحتاج فقط إلى الأحرف الخام، غيّر المحرك إلى `OutputFormat.Text`. هذا يخبر Aspose OCR بتجاوز إنشاء PDF تمامًا وإعطائك سلسلة نصية.

```csharp
        // Tell the engine to return plain text
        ocrEngine.OutputFormat = OutputFormat.Text;

        // Path to your source image (PNG, JPEG, BMP, etc.)
        string inputImagePath = @"YOUR_DIRECTORY/input.png";

        // Perform recognition – the result contains the extracted string
        OcrResult plainTextResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Write the text to a .txt file
        string textOutputPath = @"YOUR_DIRECTORY/output.txt";
        File.WriteAllText(textOutputPath, plainTextResult.Text);
```

**نصيحة احترافية:** `plainTextResult.Text` يزيل بالفعل فواصل الأسطر التي تنتمي إلى تخطيط OCR. إذا كنت تحتاج إلى الحفاظ على المسافات الأصلية، فافحص `plainTextResult.TextBlocks` بدلاً من ذلك.

### النتيجة المتوقعة

افتح `output.txt` وسترى شيئًا مشابهًا لـ:

```
Hello, world!
This is a sample scanned document.
```

هذا هو جزء **إخراج النص العادي** من الدرس—سريع، خفيف، ومثالي للمعالجة اللاحقة (مثل الفهرسة).

## الخطوة 3: التبديل إلى وضع PDF قابل للبحث

الآن لننشئ **PDF قابل للبحث**. سيقوم المحرك بدمج الصورة الأصلية وإضافة طبقة النص التي تم توليدها بواسطة OCR تحتها، مما يجعل المستند قابلًا للبحث في أي عارض PDF.

```csharp
        // Change the output format to searchable PDF
        ocrEngine.OutputFormat = OutputFormat.SearchablePdf;

        // Recognize the same image again – this time we get PDF bytes
        OcrResult pdfResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Save the PDF bytes to a file
        string pdfOutputPath = @"YOUR_DIRECTORY/output.pdf";
        File.WriteAllBytes(pdfOutputPath, pdfResult.RawData);
    }
}
```

**لماذا نعيد التعرف:** محرك OCR يخزن آخر صورة في الذاكرة، لكن صيغة الإخراج تحدد البيانات التي يتم إرجاعها. تغيير الصيغة يجبر المحرك على إجراء تمريرة جديدة تشمل طبقة النص المخفية.

### شكل الـ PDF

افتح `output.pdf` في Adobe Reader أو أي عارض وحاول تحديد النص. ستلاحظ أنه يمكنك النسخ، البحث، وتظليل المحتوى—على الرغم من أن المظهر البصري لا يزال الصورة الأصلية. هذا هو ما يميز **تحويل صورة ممسوحة إلى PDF**.

## الخطوة 4: معالجة ملفات متعددة (اختياري)

في المشاريع الواقعية نادراً ما نتعامل مع صورة واحدة. أدناه حلقة سريعة تعالج كل ملفات PNG في مجلد، وتنتج ملفات `.txt` و`.pdf` مطابقة.

```csharp
        string folder = @"YOUR_DIRECTORY";
        foreach (var file in Directory.GetFiles(folder, "*.png"))
        {
            // Plain‑text extraction
            ocrEngine.OutputFormat = OutputFormat.Text;
            var txtResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllText(Path.ChangeExtension(file, ".txt"), txtResult.Text);

            // Searchable PDF generation
            ocrEngine.OutputFormat = OutputFormat.SearchablePdf;
            var pdfResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllBytes(Path.ChangeExtension(file, ".pdf"), pdfResult.RawData);
        }
```

**ملاحظة حالة حافة:** الصور الكبيرة قد تستنفد الذاكرة. إذا واجهت `OutOfMemoryException`، فكر في تقليل الحجم باستخدام `Image.Resize` قبل التعرف، أو عالج الملفات على دفعات أصغر.

## الخطوة 5: تحسين دقة OCR

توفر Aspose OCR بعض الخيارات التي يمكنك تعديلها:

| الإعداد | ما يفعله | متى يُستخدم |
|---------|----------|-------------|
| `ocrEngine.PageSegmentationMode` | يتحكم في طريقة تقسيم المحرك للصورة إلى كتل نصية. | مفيد لتخطيطات متعددة الأعمدة. |
| `ocrEngine.Deskew` | يدور الصفحات المائلة قليلاً تلقائيًا. | المستندات الممسوحة التي ليست محاذية تمامًا. |
| `ocrEngine.RemoveNoise` | يحاول تنظيف البقع والضوضاء الخلفية. | مسوحات منخفضة الجودة أو صفحات فاكس. |

مثال:

```csharp
ocrEngine.Deskew = true;
ocrEngine.RemoveNoise = true;
```

تفعيل هذه الخيارات قد يزيد من زمن المعالجة، لكن التحسين في جودة **استخراج النص من الصورة** غالبًا ما يكون مجديًا.

## الخطوة 6: التحقق من النتيجة برمجيًا

أحيانًا تحتاج إلى التأكد من أن الـ PDF يحتوي فعليًا على نص قابل للبحث (مثلًا في الاختبارات الآلية). أبسط فحص هو التحقق من أن مصفوفة بايتات الـ PDF غير فارغة وأن طول `RawData` يتجاوز حجم الصورة.

```csharp
if (pdfResult.RawData.Length > Image.Load(inputImagePath).Data.Length)
{
    Console.WriteLine("Searchable PDF generated successfully!");
}
else
{
    Console.WriteLine("Warning: PDF may not contain hidden text.");
}
```

لتحقق أعمق يمكنك استخدام مكتبة PDF (مثل iTextSharp) لاستخراج تدفق النص ومقارنته بـ `plainTextResult.Text`.

## الأخطاء الشائعة وكيفية تجنبها

- **غياب الرخصة** – بدون رخصة Aspose صالحة تعمل المكتبة في وضع التقييم، وتضيف علامة مائية إلى ملفات PDF. سجّل رخصتك مبكرًا (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`).  
- **مسار غير صحيح** – كتابة المسارات المطلقة صلبة تعمل على جهازك لكن تفشل في بيئات أخرى. استخدم `Path.Combine` مع `AppDomain.CurrentDomain.BaseDirectory` للقدرة على النقل.  
- **تنسيقات صور غير مدعومة** – ملفات GIF وTIFF ذات الإطارات المتعددة تحتاج معالجة خاصة (`Image.LoadMultiPage`). حوّلها إلى PNG/JPEG أولًا إذا كنت تحتاج الإطار الأول فقط.  
- **اختناقات الأداء** – إعادة إنشاء `OcrEngine` داخل حلقة مكلفة. احتفظ بنسخة واحدة فقط وغيّر `OutputFormat` كما هو موضح.

## ملخص

غطينا سير العمل بالكامل لـ **إنشاء PDF قابل للبحث** من صورة ممسوحة باستخدام Aspose OCR:

1. تثبيت حزمة NuGet وإنشاء `OcrEngine`.  
2. ضبط `OutputFormat.Text` لـ **إخراج نص عادي** وكتابته إلى ملف `.txt`.  
3. التبديل إلى `OutputFormat.SearchablePdf` لـ **تحويل الصورة إلى PDF** مع طبقة نص غير مرئية.  
4. حفظ بايتات الـ PDF واختياريًا تنفيذ حلقة على دليل لمعالجة دفعات.  
5. تحسين الدقة باستخدام Deskew، إزالة الضوضاء، وخيارات تقسيم الصفحات.  

كل ذلك يندمج في برنامج صغير مستقل يمكنك نسخه ولصقه في Visual Studio.

## ماذا تجرب بعد ذلك؟

- **معالجة دفعات** بواجهة مستخدم (WinForms أو WPF) بحيث يمكن للمستخدمين سحب وإفلات الملفات.  
- **اكتشاف اللغة** – Aspose OCR يمكنه اكتشاف اللغة تلقائيًا؛ جرّب `ocrEngine.Language = Language.AutoDetect`.  
- **معالجة لاحقة** – أدخل النص المستخرج في فهرس بحث (ElasticSearch، Azure Cognitive Search) لاسترجاع المستندات فورًا.  
- **مخرجات بديلة** – استخدم `OutputFormat.Hocr` للحصول على نتائج OCR بصيغة HTML، مفيدة للمعاينات على الويب.

لا تتردد في تجربة دقات صورة مختلفة، أوضاع ألوان، وإعدادات OCR. كلما لعبت أكثر، كلما فهمت أفضل التوازن بين السرعة والدقة.

---

**برمجة سعيدة!** إذا صادفت أي مشاكل، اترك تعليقًا أدناه أو راجع وثائق Aspose OCR لمزيد من التفاصيل. مشروعك التالي—سواء كان فواتير، أرشفة، أو بناء قاعدة معرفة قابلة للبحث—أصبح أسهل بكثير.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}