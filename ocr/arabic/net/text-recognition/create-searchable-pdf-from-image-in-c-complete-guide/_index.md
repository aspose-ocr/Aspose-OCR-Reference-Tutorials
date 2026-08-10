---
category: general
date: 2026-02-19
description: إنشاء ملف PDF قابل للبحث من صورة باستخدام C# و Aspose OCR. تعلّم كيفية
  استخراج النص من الصورة وتحويلها إلى PDF قابل للبحث.
draft: false
keywords:
- create searchable pdf
- extract text from image
- image to searchable pdf
- ocr image c#
- searchable pdf from image
language: ar
og_description: إنشاء ملف PDF قابل للبحث من صورة باستخدام C# و Aspose OCR. يوضح هذا
  الدليل خطوة بخطوة كيفية استخراج النص من الصورة وإنتاج ملف PDF قابل للبحث.
og_title: إنشاء ملف PDF قابل للبحث من صورة باستخدام C# – دليل كامل
tags:
- C#
- OCR
- PDF
title: إنشاء ملف PDF قابل للبحث من صورة في C# – دليل كامل
url: /ar/net/text-recognition/create-searchable-pdf-from-image-in-c-complete-guide/
---

encryption features to". We keep as is? It ends incomplete. Keep same.

Then closing shortcodes.

Make sure to keep all shortcodes unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء ملف PDF قابل للبحث من صورة باستخدام C# – دليل كامل

هل احتجت يومًا إلى **إنشاء ملف PDF قابل للبحث** من عقد ممسوح ضوئيًا لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك؛ العديد من المطورين يواجهون هذه المشكلة عندما يتعاملون لأول مرة مع سير عمل يعتمد على OCR. الخبر السار هو أنه ببضع أسطر من C# و Aspose OCR يمكنك تحويل أي صورة نقطية (TIFF، JPEG، PNG…) إلى ملف PDF قابل للبحث في ثوانٍ.  

في هذا الدرس سنستعرض العملية بالكامل — من تثبيت المكتبة، استخراج النص من الصورة، إلى كتابة ملف **الصورة إلى PDF قابل للبحث** النهائي. على طول الطريق سنتطرق أيضًا إلى كيفية **استخراج النص من الصورة** لسيناريوهات أخرى، ولماذا طبقة النص المخفي مهمة لمحركات البحث اللاحقة.

> **ملاحظة سريعة:** جميع الشيفرات أدناه جاهزة للتنفيذ؛ لا تحتاج للبحث عن مقتطفات إضافية أو وثائق خارجية.

## ما ستحتاجه

قبل أن نغوص، تأكد من توفر المتطلبات التالية:

| المتطلبات المسبقة | لماذا يهم |
|------------------|-----------|
| .NET 6 SDK (أو أحدث) | ميزات اللغة الحديثة وأداء أفضل |
| Visual Studio 2022 (أو VS Code) | IDE مع IntelliSense يجعل الحياة أسهل |
| حزمة Aspose.OCR NuGet | توفر محرك OCR وكاتب PDF |
| صورة نموذجية (`input.tif`) | المصدر الذي ستحوله إلى PDF قابل للبحث |

إذا كان لديك مشروع .NET بالفعل، يمكنك تخطي خطوة “إنشاء مشروع جديد” والانتقال مباشرة إلى تثبيت NuGet.

## الخطوة 1: تثبيت حزمة Aspose OCR NuGet

أولاً، أضف المكتبة التي تقوم بالعمل الشاق.

```bash
dotnet add package Aspose.OCR
```

هذا السطر الواحد يجلب محرك OCR الأساسي، كاتب PDF، وجميع الاعتمادات الأصلية. في Visual Studio يمكنك أيضًا النقر بزر الماوس الأيمن على المشروع → **Manage NuGet Packages** → البحث عن *Aspose.OCR* والنقر على **Install**.

> **نصيحة احترافية:** حافظ على تحديث الحزمة. حتى تاريخ اليوم (فبراير 2026) الإصدار 23.9 هو الأحدث ويشمل تحسينات أداء للملفات TIFF عالية الدقة.

## الخطوة 2: إعداد هيكل المشروع

أنشئ تطبيق console بسيط إذا لم يكن لديك واحد:

```bash
dotnet new console -n PdfDemo
cd PdfDemo
```

افتح `Program.cs` (أو `PdfDemo.cs` إذا تفضّل فئة مسماة) واحذف الشيفرة الافتراضية “Hello World”. سنستبدلها بمثال كامل قابل للتنفيذ **ينشئ PDF قابل للبحث** من صورة.

## الخطوة 3: تهيئة محرك OCR – “استخراج النص من الصورة”

يحتاج محرك OCR إلى معرفة اللغة التي تقوم بمسحها. لمعظم العقود الإنجليزية ستستخدم `Language.English`. إذا كان لديك مستندات متعددة اللغات، يدعم Aspose حزم لغات يمكنك تحميلها لاحقًا.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;

class PdfDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine and set the language to English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // 2️⃣ Perform OCR on the input image – this is where we **extract text from image**
        OcrResult ocrResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/input.tif");

        // 3️⃣ Write the OCR result to a searchable PDF (image + hidden text layer)
        PdfResultWriter.Write(ocrResult, @"YOUR_DIRECTORY/contract_searchable.pdf");

        // 4️⃣ Notify that the PDF has been created
        Console.WriteLine("Searchable PDF created.");
    }
}
```

### لماذا نهيئ المحرك بهذه الطريقة

* **اختيار اللغة** يخبر المعرّف بمجموعة الأحرف المتوقعة، مما يحسّن الدقة بشكل كبير.  
* **`RecognizeImage`** يُعيد كائن `OcrResult` يحتوي على كل من الصورة الأصلية والنص Unicode المستخرج. هذا التمثيل المزدوج هو ما يتيح تحويل **الصورة إلى PDF قابل للبحث** لاحقًا.

## الخطوة 4: كتابة طبقة النص المخفي – توليد **صورة إلى PDF قابل للبحث**

يأخذ `PdfResultWriter` كائن `OcrResult` وينشئ PDF حيث تُظهر كل صفحة الصورة النقطية الأصلية **بالإضافة إلى** طبقة نص غير مرئية. يمكن لمحركات البحث (ومشغّلات PDF) فهرسة هذا النص المخفي، مما يجعل المستند قابلًا للبحث.

```csharp
// Inside Main, after OCR succeeds
PdfResultWriter.Write(ocrResult, @"YOUR_DIRECTORY/contract_searchable.pdf");
```

خلف الكواليس، يدمج Aspose النص باستخدام خاصية *ActualText* في PDF. إذا فتحت الملف الناتج في Adobe Acrobat وقمت بتحديد نص، ستلاحظ أنه يمكنك نسخ الكلمات الأساسية رغم أنها مُرسومة كجزء من الصورة.

## الخطوة 5: التحقق من النتيجة

شغّل البرنامج:

```bash
dotnet run
```

يجب أن ترى:

```
Searchable PDF created.
```

انتقل إلى `YOUR_DIRECTORY` وافتح `contract_searchable.pdf`. جرّب تحديد كلمة — إذا أظهر التحديد النص غير المرئي، فقد نجحت في **إنشاء PDF قابل للبحث** من صورتك الأصلية.

### فحص سريع للتأكد

*افتح PDF في أداة استخراج نص (مثلاً Adobe Reader → Edit → Copy). إذا استطعت لصق نص مقروء، فإن الطبقة المخفية تعمل.* إذا حصلت على أحرف مشوشة، تحقق من أن الصورة المصدرية ذات دقة كافية (300 dpi يعتبر قاعدة جيدة).

## الخطوة 6: معالجة الحالات الشائعة

### مسحات منخفضة الدقة

إذا كان ملف TIFF أقل من 200 dpi، قد تتأثر دقة OCR. تكبير الصورة قبل التعرف (باستخدام `System.Drawing` أو `ImageSharp`) غالبًا ما يعطي نتائج أفضل.

```csharp
using System.Drawing;

// Load, upscale, then feed to OCR
Bitmap lowRes = new Bitmap(@"YOUR_DIRECTORY/input.tif");
Bitmap highRes = new Bitmap(lowRes, new Size(lowRes.Width * 2, lowRes.Height * 2));
highRes.Save(@"YOUR_DIRECTORY/upscaled.tif");
```

### مستندات متعددة الصفحات

عند التعامل مع ملفات TIFF متعددة الصفحات، قم بالتكرار عبر كل إطار:

```csharp
using System.Drawing.Imaging;

// Assume input.tif contains multiple frames
using (Image multiPage = Image.FromFile(@"YOUR_DIRECTORY/input.tif"))
{
    int pageCount = multiPage.GetFrameCount(FrameDimension.Page);
    for (int i = 0; i < pageCount; i++)
    {
        multiPage.SelectActiveFrame(FrameDimension.Page, i);
        string tempPath = $@"YOUR_DIRECTORY/page_{i}.tif";
        multiPage.Save(tempPath, ImageFormat.Tiff);

        OcrResult pageResult = ocrEngine.RecognizeImage(tempPath);
        PdfResultWriter.Write(pageResult, $@"YOUR_DIRECTORY/page_{i}_searchable.pdf");
    }
}
```

يمكنك بعد ذلك دمج ملفات PDF الفردية باستخدام Aspose.PDF أو أي مكتبة PDF أخرى.

## مثال كامل يعمل (جميع الخطوات في ملف واحد)

فيما يلي البرنامج الكامل المستقل الذي يمكنك نسخه‑لصقه في `Program.cs`. يغطي التثبيت، OCR، توليد PDF، وملف تغليف بسيط لمعالجة الأخطاء.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;

class PdfDemo
{
    static void Main()
    {
        // Path to the source image – adjust to your environment
        const string inputPath = @"YOUR_DIRECTORY/input.tif";
        const string outputPath = @"YOUR_DIRECTORY/contract_searchable.pdf";

        try
        {
            // 👉 Step 1: Initialize OCR engine (English language)
            OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

            // 👉 Step 2: Run OCR – this **extracts text from image**
            Console.WriteLine("Running OCR on image...");
            OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

            // 👉 Step 3: Convert OCR result to a searchable PDF
            Console.WriteLine("Creating searchable PDF...");
            PdfResultWriter.Write(ocrResult, outputPath);

            Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

### النتيجة المتوقعة

* يظهر ملف باسم `contract_searchable.pdf` في دليلك.  
* فتحه في أي عارض PDF يُظهر المسح الأصلي، لكن تحديد النص ينسخ الكلمات الفعلية.  
* البحث داخل المستند (Ctrl + F) يجد المصطلحات المستخرجة فورًا.

## الأسئلة المتكررة

**س: هل يعمل هذا مع لغات أخرى؟**  
ج: بالطبع. استبدل `Language.English` بـ `Language.French`، `Language.German`، إلخ، أو حمّل حزمة لغة مخصصة من Aspose.

**س: ماذا لو احتجت إلى PDF يحتوي على نص فقط؟**  
ج: بعد OCR يمكنك تخطي الصورة واستخدام `PdfResultWriter.WriteTextOnly(ocrResult, path)` (متاح في إصدارات Aspose الأحدث).

**س: هل يمكنني تضمين الخطوط لتحسين العرض؟**  
ج: نعم. كاتب PDF يضم تلقائيًا مجموعة خطوط قياسية، لكن يمكنك توفير كائن `PdfSaveOptions` مخصص إذا كنت تحتاج إلى خطوط الشركة.

## الخلاصة

لقد **أنشأنا PDF قابل للبحث** من صورة باستخدام C# و Aspose OCR، مع تغطية كل شيء من **استخراج النص من الصورة** إلى ملف **الصورة إلى PDF قابل للبحث** النهائي. المقتطف جاهز للإنتاج، والآن لديك أساس قوي لمعالجة دفعات أكبر، لغات مختلفة، أو حتى دمج العملية في واجهة برمجة تطبيقات ويب.

### ما التالي؟

* جرّب تحويل مجلد كامل من المسحات إلى PDF قابل للبحث موحد.  
* جرب ميزات تشفير Aspose PDF لت

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}