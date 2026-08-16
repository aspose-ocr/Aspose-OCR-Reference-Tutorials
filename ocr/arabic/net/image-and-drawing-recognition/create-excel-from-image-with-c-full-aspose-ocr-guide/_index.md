---
category: general
date: 2026-03-29
description: إنشاء ملف إكسل من صورة باستخدام C# و Aspose OCR. تعلم كيفية تحويل الصورة
  إلى إكسل، استخراج الجدول من الصورة، ومعالجة لغة OCR الإنجليزية.
draft: false
keywords:
- create excel from image
- convert image to excel
- extract table from image
- ocr image to excel
- ocr english language
language: ar
og_description: إنشاء ملف إكسل من صورة بسرعة. يوضح هذا الدليل كيفية تحويل الصورة إلى
  إكسل، استخراج الجدول من الصورة، واستخدام تقنية OCR للغة الإنجليزية في C#.
og_title: إنشاء إكسل من صورة باستخدام C# – دليل Aspose OCR الكامل
tags:
- C#
- OCR
- Aspose
- Excel
title: إنشاء ملف Excel من صورة باستخدام C# – دليل Aspose OCR الكامل
url: /ar/net/image-and-drawing-recognition/create-excel-from-image-with-c-full-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء ملف Excel من صورة باستخدام C# – دليل Aspose OCR الكامل

هل احتجت يوماً إلى **إنشاء Excel من صورة** لكن لم تعرف من أين تبدأ؟ لست وحدك؛ كثير من المطورين يواجهون هذه العقبة عند التعامل مع الفواتير الممسوحة ضوئياً، الإيصالات، أو الجداول المستخرجة من ملفات PDF. الخبر السار هو أنه باستخدام Aspose.OCR يمكنك **تحويل الصورة إلى Excel** ببضع أسطر من C# فقط—دون الحاجة إلى النسخ واللصق اليدوي.

في هذا الدليل سنستعرض العملية بالكامل: من تثبيت مكتبة Aspose OCR، ضبط محرك OCR للغة الإنجليزية، التعرف على صورة جدول، وأخيراً تصدير ذلك الجدول مباشرة إلى ملف Excel. في النهاية ستتمكن من **استخراج جدول من صورة** تلقائيًا، وسترى أيضًا كيفية التعامل مع المشكلات الشائعة مثل المسحات منخفضة الدقة. هيا نبدأ.

## ما ستحتاجه

- **.NET 6.0** أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+)
- **Visual Studio 2022** (أو أي بيئة تطوير تفضلها)
- حزمة **Aspose.OCR for .NET** عبر NuGet
- صورة تحتوي على جدول واضح على شكل شبكة (PNG أو JPEG هو الأفضل)

لا تحتاج إلى محركات OCR إضافية، ولا مفاتيح API مدفوعة—Aspose.OCR يأتي مع كل ما تحتاجه لدعم **لغة OCR الإنجليزية**.

## الخطوة 1: تثبيت Aspose.OCR وإعداد المشروع

أولاً، أضف حزمة Aspose.OCR إلى مشروع C# الخاص بك. افتح وحدة تحكم مدير الحزم واكتب:

```powershell
Install-Package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت تستخدم .NET CLI، فإن الأمر المكافئ هو `dotnet add package Aspose.OCR`.

بعد تثبيت الحزمة، أنشئ تطبيقًا سطر أوامر جديدًا (أو دمج الكود في تطبيق موجود). يجب أن يبدأ ملف `Program.cs` بتوجيهات `using` الضرورية:

```csharp
using System;
using Aspose.OCR;   // <-- Aspose OCR namespace
```

هذه الخطوة الصغيرة تمهّد كل ما سيأتي لاحقًا. بدون الإشارة الصحيحة، سيشتكي المترجم من عدم وجود `OcrEngine`.

## الخطوة 2: تهيئة محرك OCR للغة الإنجليزية

لماذا اللغة مهمة؟ تستخدم محركات OCR نماذج لغوية لتحسين التعرف على الأحرف. بما أن جدولنا يحتوي على نص إنجليزي، سنضبط المحرك صراحةً على **لغة OCR الإنجليزية**. هذا يضمن تفسير الأرقام والحروف والرموز الشائعة بشكل صحيح.

```csharp
// Step 2: Create an OCR engine and set the recognition language to English
OcrEngine ocrEngine = new OcrEngine
{
    // Language enumeration comes from Aspose.OCR.Language
    Language = Language.English
};
```

لاحظ مُهيئ الكائن—مختصر، سهل القراءة، ويتجنب سطر كود إضافي. إذا احتجت لتغيير اللغة إلى أخرى (مثلاً الفرنسية)، استبدل `Language.English` بـ `Language.French`.

## الخطوة 3: التعرف على صورة الجدول

الآن نمرّر للمحرك صورة تحتوي على جدول. تُعيد طريقة `RecognizeImage` كائن `OcrResult` يحمل كل النص المكتشف، معلومات التخطيط،—والأهم بالنسبة لنا—بُنى الجداول.

```csharp
// Step 3: Recognise the table image and obtain the result
// Replace "YOUR_DIRECTORY/table_image.png" with the actual path to your image file
OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/table_image.png");
```

> **ماذا لو كانت الصورة غير واضحة؟**  
> يقوم Aspose.OCR بمعالجة تمهيدية أساسية تلقائيًا، لكن يمكنك تحسين الدقة بتوفير مصدر عالي الدقة (300 dpi أو أكثر). إذا ما زال الناتج غير دقيق، فكر في استخدام فئة `ImagePreprocessOptions` لتعزيز التباين قبل التعرف.

## الخطوة 4: تصدير الجدول المكتشف إلى Excel

هذه هي اللحظة التي انتظرتها—تحويل الجدول الملتقط إلى ملف Excel فعلي. تكتب طريقة `SaveAsExcel` ملف `.xlsx` يعكس تخطيط الجدول الأصلي، مكتملًا بالصفوف والأعمدة.

```csharp
// Step 4: Export the detected table data to an Excel workbook
// The output file will be created at the specified location
ocrResult.SaveAsExcel("YOUR_DIRECTORY/table_output.xlsx");
```

إذا فتحت `table_output.xlsx` في Excel، ستظهر لك ورقة عمل نظيفة يمكنك تنسيقها، تصفيتها، أو تمريرها إلى عمليات لاحقة. هذا السطر الواحد يحقق الهدف الأساسي لـ **إنشاء Excel من صورة**.

## الخطوة 5: التحقق من النتيجة ومعالجة الحالات الخاصة

بعد انتهاء التصدير، من الجيد التأكد من وجود الملف واحتوائه على بيانات. فحص سريع بـ `File.Exists` مع رسالة في وحدة التحكم يكفي:

```csharp
// Step 5: Verify that the Excel file was created successfully
if (System.IO.File.Exists("YOUR_DIRECTORY/table_output.xlsx"))
{
    Console.WriteLine("Excel file created successfully.");
}
else
{
    Console.WriteLine("Something went wrong – the Excel file was not found.");
}
```

### الحالات الخاصة الشائعة

| الحالة                                 | الإصلاح المقترح |
|----------------------------------------|-----------------|
| **Empty cells appear as `?`**          | زيادة DPI للصورة أو تمكين `ocrEngine.ImagePreprocessOptions` لتحسين وضوح الصورة. |
| **Merged cells are not detected**      | استخدام `ocrEngine.RecognizeImage(..., RecognizeMode.Table)` لإجبار اكتشاف الجدول. |
| **Non‑English characters are garbled** | تغيير `Language` إلى اللغة المناسبة (مثال: `Language.Spanish`). |
| **Large tables cause memory spikes**   | معالجة الصورة على أجزاء باستخدام `OcrEngine.RecognizeRegion`. |

معالجة هذه السيناريوهات مبكرًا يوفر عليك ساعات من التصحيح لاحقًا.

## مثال عملي كامل

بدمج كل ما سبق، إليك برنامج جاهز للتنفيذ يحقق **إنشاء Excel من صورة** من البداية إلى النهاية:

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise OCR engine with English language
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // 2️⃣ Recognise the table image located on disk
        // Make sure the path points to a real PNG/JPEG file containing a table
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/table_image.png");

        // 3️⃣ Export the recognised table to an Excel workbook
        ocrResult.SaveAsExcel("YOUR_DIRECTORY/table_output.xlsx");

        // 4️⃣ Confirm the file was created
        if (System.IO.File.Exists("YOUR_DIRECTORY/table_output.xlsx"))
        {
            Console.WriteLine("Excel file created.");
        }
        else
        {
            Console.WriteLine("Failed to create Excel file.");
        }
    }
}
```

**المخرجات المتوقعة:**  
عند تشغيل البرنامج، ستظهر رسالة في وحدة التحكم تقول “Excel file created.” وسيظهر ملف `table_output.xlsx` في المجلد المستهدف، يحتوي على نفس الصفوف والأعمدة الموجودة في `table_image.png`.

## إضافي: تحويل صورة إلى Excel دون تخطيط جدول

أحيانًا تكون لديك صورة عادية بنص متفرق، دون جدول منظم. يتيح لك Aspose.OCR أيضًا **تحويل الصورة إلى Excel** عن طريق تصدير النص الخام إلى ورقة عمود واحد:

```csharp
// Export raw text to a single‑column Excel file
ocrResult.SaveAsExcel("YOUR_DIRECTORY/raw_text.xlsx", ExcelExportOptions.SingleColumn);
```

هذا الأسلوب مفيد للإيصالات أو النماذج التي ستُعالج بياناتها لاحقًا.

## الأسئلة المتكررة

**س: هل يعمل هذا على macOS؟**  
ج: بالتأكيد. Aspose.OCR متعدد المنصات؛ فقط قم بتثبيت حزمة NuGet وشغّل نفس الكود تحت .NET 6 على macOS.

**س: هل يمكنني بث الصورة بدلاً من استخدام مسار ملف؟**  
ج: نعم—`RecognizeImage(Stream imageStream)` تقبل أي `Stream`، لذا يمكنك جلب الصور من طلب ويب أو من BLOB في قاعدة البيانات.

**س: ماذا عن ملفات Excel المحمية بكلمة مرور؟**  
ج: بعد إنشاء المصنف، يمكنك فتحه باستخدام `Microsoft.Office.Interop.Excel` وتطبيق كلمة مرور إذا لزم الأمر. Aspose.OCR نفسه لا يتعامل مع تشفير المصنفات.

## الخلاصة

لقد استعرضنا معًا سير عمل عملي لـ **إنشاء Excel من صورة** باستخدام Aspose.OCR في C#. من تثبيت المكتبة، ضبط محرك OCR لـ **لغة OCR الإنجليزية**، التعرف على صورة جدول، إلى تصدير البيانات كورقة Excel نظيفة—تم تغطية كل خطوة بالكود، الشروحات، والنصائح للحالات الخاصة.

الآن يمكنك **تحويل الصورة إلى Excel**، **استخراج جدول من صورة**، وحتى معالجة النصوص الخام بأقل جهد. الخطوة التالية قد تكون ربط هذا الروتين بخدمة مراقبة ملفات بحيث يتحول أي فاتورة ممسوحة تُسقط في مجلد تلقائيًا إلى جدول بيانات. أو استكشف Aspose.Cells لتنسيق المصنف الناتج برمجيًا.

هل لديك أسئلة إضافية حول OCR، أتمتة Excel، أو أي شيء آخر؟ اترك تعليقًا أدناه، وبرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}