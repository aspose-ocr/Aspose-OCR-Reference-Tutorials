---
category: general
date: 2026-04-04
description: إنشاء ملف PDF قابل للبحث من صورة TIF باستخدام C# – تعلم كيفية تحويل الصورة
  إلى PDF، إضافة بيانات تعريف PDF، وإنشاء مستند قابل للبحث باستخدام Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- add metadata to pdf
- add pdf metadata
- create pdf from tif
language: ar
og_description: إنشاء ملف PDF قابل للبحث من ملف TIF باستخدام C#. تحويل الصورة إلى
  PDF، إضافة بيانات تعريف PDF، وإنتاج مستند قابل للبحث باستخدام Aspose.OCR.
og_title: إنشاء ملف PDF قابل للبحث من TIF – دليل خطوة بخطوة
tags:
- Aspose.OCR
- C#
- PDF generation
title: إنشاء ملف PDF قابل للبحث من TIF – تحويل الصورة إلى PDF، إضافة بيانات تعريف
  PDF
url: /ar/net/text-recognition/create-searchable-pdf-from-tif-convert-image-to-pdf-add-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث من TIF – دليل C# كامل

هل احتجت يومًا إلى **إنشاء PDF قابل للبحث** من فاتورة ممسوحة ضوئيًا لكنك لم تكن متأكدًا من كيفية الحفاظ على النص قابل للبحث وتنظيم بيانات الملف التعريفية؟ لست وحدك. في العديد من مشاريع الأتمتة يجب أن يكون الـ PDF قابلًا للقراءة آليًا ومُعَلَّم بشكل صحيح بمعلومات مثل العنوان، المؤلف، وع thresholds الثقة.

في هذا الدليل سنستعرض حلًا كاملاً **يحوِّل صورة إلى PDF**، يضيف **بيانات تعريفية للـ PDF**، ويُفلتر نتائج OCR ذات الثقة المنخفضة — كل ذلك باستخدام مكتبة Aspose.OCR. في النهاية ستحصل على مقتطف جاهز للاستخدام يمكنك إدراجه في أي مشروع .NET، بالإضافة إلى مجموعة من النصائح للتعامل مع الحالات الخاصة.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.6+)
- حزمة NuGet الخاصة بـ Aspose.OCR (`Install-Package Aspose.OCR`)
- صورة TIF تريد تحويلها إلى PDF قابل للبحث (مثال: `input.tif`)
- معرفة أساسية بـ C# و Visual Studio (أو أي بيئة تطوير تفضّلها)

لا توجد خدمات خارجية أخرى مطلوبة — العملية كلها تُنفَّذ محليًا.

## الخطوة 1 – إعداد محرك OCR (إنشاء نواة PDF قابل للبحث)

أول شيء نحتاجه هو مثيل `OcrEngine` يعرف أي لغة يجب التعرف عليها. في معظم السيناريوهات التجارية تكون اللغة الإنجليزية كافية، لكن يمكنك استبدال `Language.English` بأي لغة مدعومة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑related extensions

// Initialize OCR engine with English language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**لماذا هذا مهم:** محرك OCR هو المسؤول عن تحويل البكسلات النقطية إلى نص Unicode. ضبط اللغة بشكل صحيح يحسّن الدقة ويقلل عدد الكلمات ذات الثقة المنخفضة التي تُفلتر لاحقًا.

> **نصيحة احترافية:** إذا كنت تتعامل مع مستندات متعددة اللغات، يمكنك إنشاء محركات متعددة أو استخدام `Language.Multilingual` لتمكين Aspose من اكتشاف اللغة تلقائيًا.

## الخطوة 2 – تحميل صورة TIF (إنشاء PDF من TIF)

الآن نُشير بالمحرك إلى ملف المصدر. المساعد `ImageStream.FromFile` يقرأ الصورة إلى تدفق يمكن لمحرك OCR استهلاكه.

```csharp
// Load the TIF image you want to make searchable
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.tif");
```

قد تتساءل، *“هل يمكنني إمداد JPEG أو PNG بدلاً من ذلك؟”* بالتأكيد — Aspose.OCR يدعم معظم صيغ الصور النقطية. فقط غيّر امتداد الملف وستكون جاهزًا.

## الخطوة 3 – تكوين خيارات PDF (إضافة بيانات تعريفية للـ PDF)

قبل التحويل، نُعرّف كائن `PdfOptions`. هنا نضيف **بيانات تعريفية للـ PDF** مثل العنوان والمؤلف، ونخبر المحرك بحذف الكلمات التي تقل ثقتها عن حد معين.

```csharp
PdfOptions searchablePdfOptions = new PdfOptions
{
    Title = "Invoice #12345",
    Author = "MyCompany",
    // Hide words with confidence lower than 0.8 (80%)
    MinConfidence = 0.8f
};
```

**ما الذي يحدث هنا؟**  
- `Title` و `Author` يصبحان جزءًا من قاموس معلومات وثيقة الـ PDF، مما يسهل فهرسة الملف في أنظمة إدارة المستندات.  
- `MinConfidence` هو حاجز أمان: OCR غالبًا ما يخطئ في قراءة الأحرف الخفيفة؛ فلترة هذه الأخطاء تُنظّف الطبقة القابلة للبحث وتحسّن استخراج النص لاحقًا.

إذا كنت بحاجة إلى بيانات تعريفية مخصصة (مثل `Subject`، `Keywords`)، يمكنك تعيينها عبر `PdfOptions.CustomProperties`.

## الخطوة 4 – تحويل الصورة إلى PDF قابل للبحث (Convert Image to PDF)

بعد تهيئة المحرك وتحديد الخيارات، يُجرى الاستدعاء النهائي للتحويل. يتم كتابة PDF قابل للبحث إلى القرص، مع تضمين طبقة نص OCR تحت الصورة الأصلية.

```csharp
ocrEngine.ConvertToSearchablePdf(
    outputPath: @"YOUR_DIRECTORY/output.pdf",
    pdfOptions: searchablePdfOptions);
```

بعد تنفيذ هذا السطر، يحتوي `output.pdf` على:
- صورة TIF الأصلية كخلفية بصرية  
- طبقة نص غير مرئية يمكن لمحركات البحث وعمليات النسخ‑اللصق قراءتها  
- البيانات التعريفية التي عرّفناها مسبقًا (العنوان، المؤلف، إلخ)

### النتيجة المتوقعة

افتح الـ PDF المُولَّد في Adobe Reader أو أي عارض PDF وحاول تحديد النص. يجب أن تكون قادرًا على نسخ الجمل التي تطابق المسح الأصلي. سيظهر حوار **Properties** العنوان “Invoice #12345” والمؤلف “MyCompany”.

## الخطوة 5 – التحقق من فلترة الثقة (لماذا يساعد MinConfidence)

من المفيد التأكد من أن الكلمات ذات الثقة المنخفضة قد أُزيلت فعلاً. يمكنك فحص النص المخفي في الـ PDF باستخدام أداة مثل `pdftotext`:

```bash
pdftotext output.pdf - | grep -i "unlikelyword"
```

إذا لم يظهر الكلمة، فإن فلتر `MinConfidence` عمل كما هو متوقع. عدّل العتبة (مثال: `0.7f`) إذا احتجت إلى فلترة أكثر صرامة أو تساهلًا.

## الخطوة 6 – معالجة صفحات متعددة (Create Searchable PDF from Multi‑Page TIF)

العديد من الفواتير تأتي كملفات TIFF متعددة الصفحات. Aspose.OCR يتعامل مع كل إطار كصفحة منفصلة تلقائيًا. ما عليك سوى توجيه المحرك إلى الملف متعدد الصفحات؛ استدعاء `ConvertToSearchablePdf` نفسه سيولد PDF قابل للبحث متعدد الصفحات.

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
ocrEngine.ConvertToSearchablePdf(@"YOUR_DIRECTORY/multi_output.pdf", searchablePdfOptions);
```

**حالة خاصة:** إذا كانت الصفحة فارغة، قد يولد OCR طبقة نصية فارغة، وهذا لا يسبب ضررًا. مع ذلك، يمكنك تخطي الصفحات الفارغة بفحص `ocrEngine.HasText` قبل التحويل.

## الخطوة 7 – تجميع المثال الكامل (All Steps Together)

فيما يلي برنامج واحد جاهز للتنفيذ يربط كل الخطوات معًا. استبدل `YOUR_DIRECTORY` بمسار المجلد الفعلي على جهازك.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load the TIF image (create pdf from tif)
        string inputPath = @"YOUR_DIRECTORY/input.tif";
        ocrEngine.Image = ImageStream.FromFile(inputPath);

        // 3️⃣ Set PDF metadata and confidence filter
        PdfOptions pdfOptions = new PdfOptions
        {
            Title = "Invoice #12345",
            Author = "MyCompany",
            MinConfidence = 0.8f
        };

        // 4️⃣ Convert to searchable PDF (convert image to pdf)
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ConvertToSearchablePdf(outputPath, pdfOptions);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

شغّل البرنامج (`dotnet run` أو اضغط **F5** في Visual Studio) وسترى رسالة التأكيد. سيُحفظ الـ PDF المُولَّد بجوار صورة المصدر، جاهزًا للفهرسة أو الأرشفة.

## أسئلة شائعة ومشكلات محتملة

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني إضافة خط مخصص إلى الطبقة القابلة للبحث؟** | طبقة OCR تستخدم Unicode؛ المظهر البصري يُستمد من الصورة الأصلية، لذا لا يلزم تضمين خطوط إضافية. |
| **ماذا لو كان ملف TIF ملونًا؟** | Aspose.OCR يحول الصور الملونة إلى تدرج رمادي تلقائيًا للـ OCR، لكن يمكنك الحفاظ على الألوان الأصلية في الـ PDF بتعيين `PdfOptions.PreserveColor = true`. |
| **هل المكتبة آمنة للاستخدام المتعدد الخيوط؟** | يجب استخدام كل مثيل `OcrEngine` في خيط واحد فقط. للمعالجة المتوازية، أنشئ محركًا منفصلًا لكل خيط. |
| **كيف يمكنني تشفير الـ PDF؟** | استخدم `PdfOptions.Security` لتعيين كلمة مرور وأذونات بعد تحويل OCR. |

## الخطوات التالية (توسيع مجموعة أدوات PDF الخاصة بك)

- **المعالجة الدفعية:** كرّر العملية على مجلد من ملفات TIFF لإنشاء PDF قابل للبحث لكل منها.  
- **ما بعد المعالجة:** استخدم Aspose.PDF لدمج ملفات PDF المُولَّدة في مستند رئيسي واحد.  
- **بيانات تعريفية متقدمة:** عَبِّئ حقول XMP مخصصة لتكامل أفضل مع SharePoint أو أنظمة ECM.

جميع هذه الإضافات تبني على النمط الأساسي الذي غطيناه للتو: **إنشاء PDF قابل للبحث**، **تحويل الصورة إلى PDF**، و **إضافة بيانات تعريفية للـ PDF**.

---

*برمجة سعيدة! إذا واجهت أي صعوبات، اترك تعليقًا أدناه أو راجع توثيق Aspose.OCR للحصول على أحدث تحديثات الـ API.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}