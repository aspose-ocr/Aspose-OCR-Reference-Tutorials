---
category: general
date: 2026-06-06
description: كيفية استخدام OcrEngine في C# لتقنية OCR متعددة الصفحات بسرعة. تعلم تعيين
  OcrLanguage، تحميل ملفات TIFF/PDF، واستخراج النص بأقل قدر من الشيفرة.
draft: false
keywords:
- how to use ocrengine
- OCR engine C#
- multi‑page OCR
- recognize text from TIFF
- OcrLanguage English
language: ar
og_description: كيفية استخدام OcrEngine في C# لإجراء OCR متعدد الصفحات على ملفات TIFF
  أو PDF. كود خطوة بخطوة، شروحات، ونصائح.
og_title: كيفية استخدام OcrEngine في C# – دليل OCR الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to use OcrEngine in C# for fast multi‑page OCR. Learn to set OcrLanguage,
    load TIFF/PDF files, and extract text with minimal code.
  headline: How to Use OcrEngine in C# – Complete OCR Guide
  type: TechArticle
- description: How to use OcrEngine in C# for fast multi‑page OCR. Learn to set OcrLanguage,
    load TIFF/PDF files, and extract text with minimal code.
  name: How to Use OcrEngine in C# – Complete OCR Guide
  steps:
  - name: Expected Output
    text: 'Assuming `multipage.tif` contains three scanned pages, you’ll see something
      like:'
  - name: 1. Switching to a Different Language
    text: '```csharp engine.Language = OcrLanguage.Spanish; // just change the enum
      value ```'
  - name: 2. Processing PDFs Instead of TIFFs
    text: '```csharp engine.Image = ImageStream.FromFile("Resources/document.pdf");
      ```'
  - name: 3. Disposing Resources Properly
    text: 'If `OcrEngine` implements `IDisposable`, wrap the whole block:'
  - name: 4. Large Documents – Page‑by‑Page Streaming
    text: '```csharp int totalPages = engine.GetPageCount(); // hypothetical method
      for (int i = 0; i < totalPages; i++) { engine.Image = ImageStream.FromFile(imagePath,
      pageIndex: i); var pageResult = engine.RecognizeSinglePage(); Console.WriteLine($"---
      Page {i + 1} ---"); Console.WriteLine(pageResult.Text);'
  type: HowTo
tags:
- OCR
- C#
- ImageProcessing
title: كيفية استخدام OcrEngine في C# – دليل OCR الكامل
url: /ar/net/ocr-configuration/how-to-use-ocrengine-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OcrEngine في C# – دليل OCR كامل

هل تساءلت يومًا **how to use OcrEngine** عندما تحتاج إلى استخراج النص من ملف PDF ممسوح ضوئيًا أو TIFF متعدد الصفحات؟ لست وحدك—المطورون يواجهون صعوبة مستمرة في أتمتة رقمنة المستندات. الخبر السار هو أنه ببضع أسطر من C# يمكنك تشغيل محرك OCR، وتوجيهه إلى ملف، والحصول على نص كل صفحة في لحظة.

في هذا الدرس سنستعرض مثالًا واقعيًا يوضح **how to use OcrEngine** للتعرف الضوئي على النص متعدد الصفحات، ضبط **OcrLanguage** إلى الإنجليزية، والتكرار على نتيجة كل صفحة. في النهاية ستحصل على تطبيق كونسول جاهز للتنفيذ يطبع النص المستخرج، بالإضافة إلى مجموعة من النصائح للتعامل مع ملفات أكبر، لغات غير إنجليزية، وتنظيف الموارد بشكل صحيح.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- .NET 6.0 SDK أو أحدث (الكود يعمل على .NET Core و .NET Framework أيضًا)
- إشارة إلى مكتبة OCR تُعرِّف `OcrEngine` و `OcrLanguage` و `ImageStream` (العديد من الحزم التجارية ومفتوحة المصدر تستخدم هذه الأسماء؛ العينة تفترض أن الـ API متاح بالفعل)
- ملف صورة متعدد الصفحات (`.tif` أو `.pdf`) موجود في مجلد يمكنك الإشارة إليه من الكود
- معرفة أساسية بتطبيقات كونسول C#

لا توجد حزم NuGet إضافية مطلوبة للمنطق الأساسي، لكن ستحتاج إلى ربط ملفات DLL الخاصة بمكتبة OCR في مشروعك.

## إعداد المشروع (بدء سريع)

1. افتح بيئة التطوير المفضلة لديك (Visual Studio، VS Code، Rider…).
2. أنشئ مشروع كونسول جديد:

   ```bash
   dotnet new console -n OcrEngineDemo
   cd OcrEngineDemo
   ```

3. أضف إشارة إلى تجميع OCR (استبدل `YourOcrLib.dll` بالملف الفعلي):

   ```bash
   dotnet add reference path/to/YourOcrLib.dll
   ```

4. ضع ملف TIFF متعدد الصفحات يُدعى `multipage.tif` داخل مجلد باسم `Resources` في جذر المشروع.

هذا كل شيء—بيئتك جاهزة لشرح **how to use OcrEngine**.

## الخطوة 1: استيراد المساحات الاسمية وت初始化 المحرك

أول شيء تقوم به عندما تريد **use OcrEngine** هو جلب المساحات الاسمية المطلوبة وإنشاء نسخة. هذا الكائن هو نقطة الدخول لكل عملية OCR.

```csharp
using System;
using OcrLibrary;          // <-- hypothetical namespace containing OcrEngine
using OcrLibrary.Imaging; // <-- contains ImageStream

namespace OcrEngineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create an OCR engine instance
            var engine = new OcrEngine();

            // -----------------------------------------------------------------
            // Why this matters:
            // The engine holds configuration (language, DPI, etc.) and manages
            // native resources. Instantiating it once and re‑using it is far
            // more efficient than creating a new engine per page.
            // -----------------------------------------------------------------
```

> **نصيحة احترافية:** إذا كانت مكتبة OCR الخاصة بك تُطبق `IDisposable`، اح.wrap المحرك داخل كتلة `using` لضمان تنظيف الموارد بشكل صحيح.

## الخطوة 2: اختيار اللغة للتعرف

معظم محركات OCR تحتاج إلى معرفة نموذج اللغة الذي ستُطبق. في مثال **how to use OcrEngine** الكلاسيكي سنستخدم الإنجليزية، لكن يمكنك استبدال `OcrLanguage.English` بأي لغة مدعومة.

```csharp
            // Step 2: Choose the language for recognition
            engine.Language = OcrLanguage.English;

            // -----------------------------------------------------------------
            // Why this matters:
            // Setting the language early lets the engine preload the correct
            // character set and improves accuracy dramatically.
            // -----------------------------------------------------------------
```

إذا احتجت يومًا ما إلى التعرف على نص فرنسي، استبدل `English` بـ `French`—نفس نمط **how to use OcrEngine** سيعمل.

## الخطوة 3: تحميل صورة متعددة الصفحات (TIFF أو PDF)

الآن نوجه المحرك إلى الملف الذي نريد معالجته. `ImageStream.FromFile` يخفِّي تفاصيل التنسيق، لذا يعمل نفس الكود لكل من TIFF و PDF.

```csharp
            // Step 3: Load a multi‑page image (TIFF or PDF) from disk
            string imagePath = "Resources/multipage.tif";
            engine.Image = ImageStream.FromFile(imagePath);

            // -----------------------------------------------------------------
            // Why this matters:
            // Loading the image once allows the engine to batch‑process all pages,
            // which is faster than loading each page individually.
            // -----------------------------------------------------------------
```

**حالة حافة:** إذا كان الملف أكبر من بضع مئات من الميجابايت، فكر في بثه صفحةً بصفحة لتجنب ضغط الذاكرة. معظم المكتبات توفر طريقة `LoadPage(int index)` لهذا السيناريو.

## الخطوة 4: تنفيذ OCR على جميع الصفحات مرة واحدة

جوهر **how to use OcrEngine** هو استدعاء `RecognizeMultiPage`. يُعيد مجموعة يحتوي كل عنصر فيها نص صفحة واحدة.

```csharp
            // Step 4: Perform OCR on all pages at once
            var multiPageResult = engine.RecognizeMultiPage();

            // -----------------------------------------------------------------
            // Why this matters:
            // Batch recognition leverages internal optimizations (thread pools,
            // SIMD instructions) and often yields better throughput than
            // looping over `RecognizeSinglePage`.
            // -----------------------------------------------------------------
```

إذا كنت تحتاج فقط إلى الصفحة الأولى، استبدل الاستدعاء بـ `engine.RecognizeSinglePage()`—النمط نفسه يظل صالحًا.

## الخطوة 5: التكرار على نتيجة كل صفحة وعرض النص

أخيرًا، نمر على النتائج، ونطبع النص المستخرج لكل صفحة إلى الكونسول. هذا يعكس سيناريو الإخراج النموذجي لـ **how to use OcrEngine**.

```csharp
            // Step 5: Iterate through each page's result and display the extracted text
            for (int pageIndex = 0; pageIndex < multiPageResult.Count; pageIndex++)
            {
                Console.WriteLine($"--- Page {pageIndex + 1} ---");
                Console.WriteLine(multiPageResult[pageIndex].Text);
                Console.WriteLine(); // extra line for readability
            }

            // -----------------------------------------------------------------
            // Why this matters:
            // Separating pages with a header makes the console output easy to scan,
            // especially when dealing with long documents.
            // -----------------------------------------------------------------
        }
    }
}
```

### النتيجة المتوقعة

بافتراض أن `multipage.tif` يحتوي على ثلاث صفحات ممسوحة، ستحصل على شيء مشابه لـ:

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris.
```

إذا فشل محرك OCR في التعرف على صفحة ما، فإن الخاصية `Text` ستصبح سلسلة فارغة—احرص دائمًا على التحقق من ذلك في الكود الإنتاجي.

## التعامل مع التغييرات الشائعة وحالات الحافة

### 1. التبديل إلى لغة مختلفة

```csharp
engine.Language = OcrLanguage.Spanish; // just change the enum value
```

بقية سير العمل تبقى كما هي—هذه هي جمال نمط **how to use OcrEngine**.

### 2. معالجة ملفات PDF بدلاً من TIFF

```csharp
engine.Image = ImageStream.FromFile("Resources/document.pdf");
```

معظم المكتبات تكتشف تنسيق الحاوية تلقائيًا، لذا لا تحتاج إلى كود إضافي.

### 3. تحرير الموارد بشكل صحيح

إذا كان `OcrEngine` يُطبق `IDisposable`، اح.wrap الكتلة بأكملها:

```csharp
using var engine = new OcrEngine();
engine.Language = OcrLanguage.English;
engine.Image = ImageStream.FromFile(imagePath);
var result = engine.RecognizeMultiPage();
// ...process result...
```

هذا يضمن تحرير المقابض الأصلية، مما يمنع تسرب الذاكرة في الخدمات طويلة التشغيل.

### 4. المستندات الكبيرة – بث صفحة بصفحة

```csharp
int totalPages = engine.GetPageCount(); // hypothetical method
for (int i = 0; i < totalPages; i++)
{
    engine.Image = ImageStream.FromFile(imagePath, pageIndex: i);
    var pageResult = engine.RecognizeSinglePage();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

البث يقلل من استهلاك الذاكرة في الذروة مقابل انخفاض طفيف في الأداء—اختر ما يناسب حالتك.

## مثال كامل جاهز للتنفيذ (انسخه‑الصق)

```csharp
using System;
using OcrLibrary;
using OcrLibrary.Imaging;

namespace OcrEngineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create and configure the OCR engine
            using var engine = new OcrEngine();
            engine.Language = OcrLanguage.English;

            // Load the multi‑page image (TIFF or PDF)
            string imagePath = "Resources/multipage.tif";
            engine.Image = ImageStream.FromFile(imagePath);

            // Perform batch OCR
            var multiPageResult = engine.RecognizeMultiPage();

            // Output each page's text
            for (int pageIndex = 0; pageIndex < multiPageResult.Count; pageIndex++)
            {
                Console.WriteLine($"--- Page {pageIndex + 1} ---");
                Console.WriteLine(multiPageResult[pageIndex].Text);
                Console.WriteLine();
            }
        }
    }
}
```

احفظه كـ `Program.cs`، شغّله باستخدام `dotnet run`، وسترى النص يظهر. إذا استبدلت مسار الملف بملف PDF، سيعمل نفس الكود—فوز آخر لنمط **how to use OcrEngine**.

## الخلاصة

لقد غطينا الآن **how to use OcrEngine** من البداية حتى النهاية: تثبيت المكتبة، ضبط **OcrLanguage English**، تحميل TIFF أو PDF متعدد الصفحات، تشغيل `RecognizeMultiPage`، وطباعة نص كل صفحة. النمط قابل لإعادة الاستخدام مع لغات أخرى، أنواع ملفات أخرى، وحتى لبث المستندات الكبيرة.

الخطوات التالية التي قد تستكشفها تشمل:

- تطبيق **OCR engine C#** لإنشاء ملفات PDF قابلة للبحث (إضافة النص كطبقة غير مرئية)
- استخدام **multi‑page OCR** لإدخال البيانات إلى قاعدة بيانات أو نموذج ذكاء اصطناعي
- تجربة تحسين ما قبل المعالجة للصور (إزالة الميل، التحويل إلى ثنائي) لزيادة الدقة

هل لديك سيناريو مختلف ترغب في استكشافه—مثل التعامل مع ملاحظات مكتوبة بخط اليد أو دمج

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Extract OCR – OCR Configuration](/ocr/english/net/ocr-configuration/)
- [How to Perform OCR on Archive Images with Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}