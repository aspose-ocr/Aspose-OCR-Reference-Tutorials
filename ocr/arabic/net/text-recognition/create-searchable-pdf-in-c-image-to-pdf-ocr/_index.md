---
category: general
date: 2026-02-28
description: إنشاء ملف PDF قابل للبحث من ملف TIFF متعدد الصفحات باستخدام C#. يوضح
  هذا الدليل كيفية تحويل الصورة إلى PDF قابل للبحث مع مثال كامل لتقنية OCR بلغة C#.
draft: false
keywords:
- create searchable pdf
- image to searchable pdf
- convert tiff to pdf
- c# ocr example
- c# image to pdf
language: ar
og_description: إنشاء ملف PDF قابل للبحث من ملف TIFF باستخدام Aspose.OCR. اتبع مثال
  OCR خطوة بخطوة بلغة C# لتحويل الصور إلى ملفات PDF قابلة للبحث.
og_title: إنشاء ملف PDF قابل للبحث في C# – تحويل الصورة إلى PDF باستخدام OCR
tags:
- OCR
- PDF
- C#
- Aspose
title: إنشاء PDF قابل للبحث في C# – تحويل الصورة إلى PDF باستخدام OCR
url: /ar/net/text-recognition/create-searchable-pdf-in-c-image-to-pdf-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء ملف PDF قابل للبحث في C# – تحويل صورة إلى PDF مع OCR

هل احتجت يومًا إلى **إنشاء ملف PDF قابل للبحث** من مستند ممسوح ضوئيًا لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك. في العديد من سير عمل المكاتب، يكون ملف PDF القابل للبحث هو الفرق بين ملف غير قابل للاستخدام وأرشيف يمكن البحث فيه.

في هذا الدرس سنستعرض مثالًا كاملًا **c# ocr** يحول ملف TIFF متعدد الصفحات إلى PDF قابل للبحث، كل ذلك باستخدام Aspose.OCR. بنهاية الدرس ستعرف بالضبط كيف **تحول صورة إلى PDF قابل للبحث**، وكيف **تحول tiff إلى pdf**، وستحصل على مقطع كود جاهز يمكنك إدراجه في أي مشروع .NET.

## ما ستتعلمه

* كيفية تثبيت وإضافة مرجع Aspose.OCR في مشروع C#.  
* الخطوات الدقيقة لتحميل ملف TIFF، ضبط اللغة، واستدعاء `RecognizeToPdf`.  
* لماذا كل خطوة مهمة – من إدارة الذاكرة إلى اختيار اللغة.  
* نصائح للتعامل مع المستندات الكبيرة، حل المشكلات الشائعة في OCR، وتوسيع الحل لتشمل صيغ صور أخرى.

**المتطلبات المسبقة** – .NET SDK حديث (4.6+ أو .NET Core 3.1+)، Visual Studio (أو أي بيئة تطوير مفضلة)، ورخصة Aspose.OCR (الإصدار التجريبي المجاني يكفي للاختبار). لا توجد مكتبات خارجية أخرى مطلوبة.

---

## إنشاء PDF قابل للبحث – نظرة عامة

على مستوى عالٍ، تبدو العملية هكذا:

1. **تهيئة** `OcrEngine`.  
2. **تحميل** صورة المصدر (ملف TIFF في مثالنا).  
3. **تكوين** إعدادات اللغة للحصول على دقة أعلى.  
4. **تشغيل** OCR و **حفظ** النتيجة مباشرةً كملف PDF قابل للبحث.  

هذا كل شيء. تقوم واجهة برمجة تطبيقات Aspose بالعمل الشاق، لذا لا تحتاج إلى دمج مكتبات OCR و PDF منفصلة.

---

## الخطوة 1: تثبيت Aspose.OCR وإعداد المشروع

أولًا، أضف حزمة Aspose.OCR عبر NuGet:

```bash
dotnet add package Aspose.OCR
```

أو، إذا كنت تفضّل وحدة التحكم الخاصة بمدير الحزم في Visual Studio:

```powershell
Install-Package Aspose.OCR
```

بعد استعادة الحزمة، افتح ملف المشروع وتأكد من وجود المرجع:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
</ItemGroup>
```

> **نصيحة محترف:** استخدم أحدث نسخة مستقرة (تحقق من موقع Aspose) للحصول على تصحيحات الأخطاء وحزم اللغات الأحدث.

---

## الخطوة 2: تحويل TIFF إلى PDF – تحميل الصورة

الآن سنقوم بتحميل ملف TIFF الذي تريد جعله قابلًا للبحث. تدعم طريقة `Image.Load` في Aspose ملفات TIFF متعددة الصفحات مباشرةً.

```csharp
using Aspose.OCR;
using System.Drawing;

// Load the multi‑page TIFF. Replace the path with your actual file.
using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");
```

> **لماذا هذا مهم:** تحميل الصورة داخل كتلة `using` يضمن تحرير الموارد غير المُدارة فورًا—وهو أمر حاسم عند معالجة مستندات كبيرة.

---

## الخطوة 3: صورة إلى PDF قابل للبحث – تكوين محرك OCR

قبل تشغيل OCR، سنخبر المحرك أي لغة نتوقعها. اللغة الإنجليزية تكفي في معظم الحالات، لكن يمكنك استبدالها بأي قيمة من تعداد `OcrLanguage`.

```csharp
// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// (Optional) Specify language for better accuracy
ocrEngine.Language = OcrLanguage.English;
```

> **ملاحظة خبير:** اختيار اللغة الصحيحة يقلل بشكل كبير من الأخطاء في التعرف. إذا كان لديك لغات مختلطة، يمكنك دمجها باستخدام عامل `|`، مثل `OcrLanguage.English | OcrLanguage.French`.

---

## الخطوة 4: مثال C# OCR – التعرف والحفظ

مع جاهزية المحرك، استدعِ `RecognizeToPdf`. تقوم الطريقة بكتابة ملف PDF القابل للبحث مباشرةً إلى القرص، وتضمّن طبقة نص غير مرئية خلف الصورة الأصلية.

```csharp
// Define the output path for the searchable PDF
string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";

// Perform OCR and write the searchable PDF
ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);
```

بعد تنفيذ هذا السطر، سيحتوي `output.pdf` على صفحات TIFF الأصلية بالإضافة إلى طبقة نص مخفية يمكن لأي قارئ PDF البحث فيها.

---

## الخطوة 5: صورة C# إلى PDF – التحقق من النتيجة

لنتأكد من أن كل شيء عمل بشكل صحيح. افتح ملف PDF المُولد في Adobe Reader (أو أي عارض) وجرب البحث عن كلمة تعرف أنها موجودة في ملف TIFF الأصلي.

```csharp
Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
```

إذا عادت عملية البحث بنتائج، فقد نجحت في **إنشاء PDF قابل للبحث** من صورة. إذا لم يحدث ذلك، تحقق مرة أخرى من إعداد اللغة أو جودة ملف TIFF الأصلي.

---

## مثال كامل يعمل

بتجميع جميع الأجزاء معًا، إليك تطبيق console مستقل يمكنك تجميعه وتشغيله:

```csharp
using Aspose.OCR;
using System.Drawing;

class SearchablePdfDemo
{
    static void Main()
    {
        // Step 1: Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑page TIFF
        using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");

        // Step 3: (Optional) Set language for better accuracy
        ocrEngine.Language = OcrLanguage.English;

        // Step 4: Convert the image to a searchable PDF
        string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);

        // Step 5: Inform the user
        System.Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
    }
}
```

**الناتج المتوقع** (في وحدة التحكم):

```
Searchable PDF created at: C:\MyFolder\output.pdf
```

افتح `output.pdf` ويجب أن تكون قادرًا على كتابة أي كلمة من TIFF الأصلي في مربع البحث الخاص بالعارض ومشاهدة النتائج المظللة.

---

![Create searchable PDF example](placeholder-image.png){: .align-center alt="مثال على إنشاء PDF قابل للبحث"}

*الصورة أعلاه تُظهر ملف PDF قابل للبحث مفتوحًا في عارض مع تفعيل طبقة النص المخفي.*

---

## أسئلة شائعة وحالات خاصة

### ماذا لو كان ملف TIFF كبيرًا (مئات الصفحات)؟

يقوم Aspose.OCR ببث الصفحات واحدة تلو الأخرى، لكن قد تواجه حدود الذاكرة. فكر في معالجة TIFF على دفعات:

```csharp
for (int i = 0; i < tiffImage.PageCount; i++)
{
    using var singlePage = tiffImage.ExtractPage(i);
    ocrEngine.RecognizeToPdf(singlePage, $"page_{i}.pdf");
}
```

لاحقًا، يمكنك دمج ملفات PDF لكل صفحة باستخدام مكتبة PDF (مثل Aspose.PDF).

### هل يمكنني الإخراج إلى صيغة مختلفة، مثل DOCX قابل للبحث؟

نعم—استخدم `RecognizeToDocument` بدلاً من `RecognizeToPdf`. واجهة البرمجة مماثلة لطريقة PDF، فقط غير امتداد الملف المستهدف.

### كيف أتعامل مع لغات غير الإنجليزية؟

استبدل `OcrLanguage.English` بالعدد المناسب، على سبيل المثال `OcrLanguage.Spanish`. يمكنك أيضًا دمج لغات متعددة:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.German;
```

### ماذا عن ملفات PDF محمية بكلمة مرور؟

بعد خطوة OCR، يمكنك فتح ملف PDF المُولد باستخدام Aspose.PDF وتطبيق التشفير:

```csharp
var pdfDoc = new Aspose.Pdf.Document(outputPdfPath);
pdfDoc.Encrypt("ownerPassword", "userPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save(outputPdfPath);
```

---

## خلاصة

غطّينا كل ما تحتاجه لإنشاء ملفات **PDF قابلة للبحث** من صور TIFF باستخدام C#. بدءًا من تثبيت Aspose.OCR، تحميل الصورة، تكوين اللغة، تشغيل OCR، وأخيرًا التحقق من النتيجة القابلة للبحث، لديك الآن مثال **c# ocr** قوي يمكنك تكييفه مع صيغ أخرى.

إذا كنت مستعدًا للمتابعة، جرّب:

* **تحويل TIFF إلى PDF** للأرشفة غير القابلة للبحث (فقط تخطى خطوة OCR).  
* تجربة **صورة إلى PDF قابل للبحث**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}