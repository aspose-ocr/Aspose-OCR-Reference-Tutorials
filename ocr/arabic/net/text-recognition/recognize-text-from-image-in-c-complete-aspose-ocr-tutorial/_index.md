---
category: general
date: 2026-05-06
description: تعلم كيفية التعرف على النص من الصورة باستخدام Aspose OCR في C#. استخراج
  النص من الفاتورة، تحميل الصورة للتعرف الضوئي على الأحرف، ومشاهدة مثال كامل لـ Aspose
  OCR.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for OCR
- Aspose OCR example
language: ar
og_description: تعلم كيفية التعرف على النص من الصورة باستخدام Aspose OCR، واستخراج
  النص من الإيصال، وتحميل الصورة للتعرف الضوئي على الأحرف في دليل مختصر خطوة بخطوة.
og_title: التعرف على النص من الصورة في C# – دليل Aspose OCR الكامل
tags:
- C#
- OCR
- Aspose
title: التعرف على النص من صورة في C# – دليل Aspose OCR الكامل
url: /ar/net/text-recognition/recognize-text-from-image-in-c-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من صورة في C# – دليل Aspose OCR الكامل

هل احتجت يومًا إلى **التعرف على النص من صورة** لكن لم تكن متأكدًا أي مكتبة تختار؟ لست وحدك—العديد من المطورين يواجهون نفس المشكلة عندما يحاولون استخراج الأرقام من إيصال أو مسح نموذج. الخبر السار هو أن Aspose OCR يجعل العملية بأكملها سهلة للغاية، وفي هذا الدليل سنرشدك عبر **مثال Aspose OCR كامل** يتيح لك **استخراج النص من الإيصال** من الصور باستخدام بضع أسطر فقط من C#.

في الدقائق القليلة القادمة ستتعلم كيف **تحمّل صورة للـ OCR**، تحدد المنطقة الدقيقة التي تحتوي على المبلغ الإجمالي، تشغّل المحرك، وأخيرًا تعرض النتيجة. لا مراجع غامضة للوثائق الخارجية، لا أجزاء مفقودة—كل ما تحتاجه للنسخ‑اللصق والتشغيل موجود هنا. قليل من الإعداد، بضع خطوات، وستتمكن من التعرف على النص من ملفات الصور في الوقت الفعلي.

> **ما ستحصل عليه**  
> * تطبيق كونسول C# قابل للتنفيذ يتعرف على النص من ملفات الصور.  
> * فهم لماذا قد ترغب في تقييد الـ OCR إلى مستطيل محدد (السرعة والدقة).  
> * نصائح للتعامل مع الحالات الشائعة مثل الإيصالات الضبابية أو المسحات المائلة.  

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

| المتطلب | لماذا يهم |
|-------------|----------------|
| .NET 6.0 SDK (or later) | Aspose OCR يُوزَّع كمكتبة .NET Standard 2.0 / .NET 5+، لذا أي بيئة تشغيل حديثة تعمل. |
| Visual Studio 2022 (or VS Code) | بيئة تطوير مريحة تُسرّع عملية التصحيح، لكن أي محرر يستطيع تجميع C# يكفي. |
| **Aspose.OCR for .NET** NuGet package | هذه هي المكتبة الأساسية التي تقوم فعليًا بالتعرف على النص من الصورة. |
| صورة إيصال تجريبية (`receipt.jpg`) | سنستخدم هذا الملف لتوضيح **استخراج النص من الإيصال**. |

يمكنك تثبيت حزمة NuGet بالأمر التالي:

```bash
dotnet add package Aspose.OCR
```

بعد الانتهاء، ستكون جاهزًا لبدء تحميل الصورة للـ OCR.

---

## الخطوة 1: تحميل الصورة للـ OCR

أول ما تحتاج إلى فعله هو توجيه المحرك إلى الملف الذي تريد تحليله. هنا يظهر المصطلح الثانوي **load image for OCR** بشكل طبيعي.

```csharp
using Aspose.OCR;
using System.Drawing;

// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// Load the receipt image – replace the path with your own file location
ocrEngine.SetImage(@"C:\Images\receipt.jpg");
```

> **نصيحة احترافية:** إذا كانت صورتك موجودة في مجلد المشروع، يمكنك استخدام مسار نسبي مثل `ocrEngine.SetImage("receipt.jpg");`. فقط تأكد من أن الملف يُنسخ إلى دليل الإخراج (`Copy to Output Directory = PreserveNewest`).

طريقة `SetImage` تقبل أي تنسيق يمكن لـ System.Drawing فكّ تشفيره (JPEG، PNG، BMP، إلخ)، لذا لست مقيدًا بنوع ملف واحد.

---

## الخطوة 2: تحديد منطقة الاهتمام – **extract text from receipt**

مسح الصورة بالكامل يستهلك دورات المعالج وقد يُدخل ضوضاء. من خلال إخبار Aspose OCR بالضبط أين يقع المبلغ الإجمالي، تعزز كلًا من السرعة والدقة. هذا هو الجزء الذي نُجري فيه **extract text from receipt**.

```csharp
// Define a rectangle that covers the total amount on the receipt
// (x, y, width, height) – adjust these numbers for your own layout
var roi = new Rectangle(150, 500, 300, 80);
ocrEngine.SetRegionOfInterest(roi);
```

> **لماذا المستطيل؟**  
> يعمل محرك OCR على شبكة بكسلية. عندما تقصره على منطقة معينة، يتجاهل كل ما هو خارجها—لا مزيد من الأحرف العشوائية من شعار المتجر أو سطر العنوان.

إذا لم تكن متأكدًا من الإحداثيات الدقيقة، يمكنك استخدام أي عارض صور يُظهر مواضع البكسل (مثل Paint.NET) لتقدير الأرقام بالعين.

---

## الخطوة 3: تشغيل المحرك – **recognize text from image** (الكلمة الرئيسية)

الآن يحدث السحر. تخبر Aspose بقراءة البكسلات داخل المستطيل الذي حددته للتو.

```csharp
// Perform the recognition
OcrResult result = ocrEngine.Recognize();
```

`OcrResult` يحتوي على النص الخام، درجات الثقة، وحتى الصناديق المحيطة لكل كلمة. لعرض سريع سنطبع النص العادي فقط.

```csharp
Console.WriteLine("Total amount detected: " + result.Text);
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مثل:

```
Total amount detected: $23.45
```

إذا كان الإخراج مشوشًا، تحقق مرة أخرى من إحداثيات ROI أو جرّب زيادة دقة الصورة.

---

## الخطوة 4: معالجة النتيجة – تحسين **Aspose OCR example**

الحل القوي يفعل أكثر من مجرد طباعة السلسلة إلى الكونسول. أدناه مثال مساعد صغير يزيل المسافات الفارغة، يحذف فواصل الأسطر العشوائية، ويتحقق من أن القيمة المستخرجة تبدو كمبلغ نقدي.

```csharp
static string CleanAmount(string raw)
{
    // Remove any non‑numeric characters except dot and comma
    var cleaned = new string(raw
        .Where(c => char.IsDigit(c) || c == '.' || c == ',')
        .ToArray());

    // Normalize decimal separator to dot
    cleaned = cleaned.Replace(',', '.');

    // If we end up with an empty string, return a friendly message
    return string.IsNullOrWhiteSpace(cleaned) ? "N/A" : cleaned;
}

// ...

string amount = CleanAmount(result.Text);
Console.WriteLine($"Parsed amount: ${amount}");
```

المساعد يوضح مثال **Aspose OCR example** واقعي يمكنك دمجه في أي نظام فواتير أكبر.

---

## الخطوة 5: برنامج كامل قابل للتنفيذ – عرض **extract text from receipt** النهائي

جمع كل ما سبق يمنحك ملفًا واحدًا جاهزًا للنسخ‑اللصق. احفظه باسم `Program.cs` وشغّله باستخدام `dotnet run`.

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;
using System.Linq;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the image for OCR
        var ocrEngine = new OcrEngine();
        ocrEngine.SetImage(@"C:\Images\receipt.jpg");   // <-- adjust path

        // 2️⃣ Define the region that holds the total amount
        var roi = new Rectangle(150, 500, 300, 80);
        ocrEngine.SetRegionOfInterest(roi);

        // 3️⃣ Run the engine – recognize text from image
        OcrResult result = ocrEngine.Recognize();

        // 4️⃣ Clean up the output
        string amount = CleanAmount(result.Text);
        Console.WriteLine($"Total amount detected: ${amount}");
    }

    // Helper that sanitises the OCR output
    static string CleanAmount(string raw)
    {
        var cleaned = new string(raw
            .Where(c => char.IsDigit(c) || c == '.' || c == ',')
            .ToArray());

        cleaned = cleaned.Replace(',', '.');
        return string.IsNullOrWhiteSpace(cleaned) ? "N/A" : cleaned;
    }
}
```

**الإخراج المتوقع**

```
Total amount detected: $23.45
```

إذا كانت صورة الإيصال أغمق أو النص مائلًا، قد ترى شيء مثل `Total amount detected: 23,45`. طريقة `CleanAmount` تُعيد تنسيق ذلك إلى صيغة عشرية قياسية.

---

## المشكلات الشائعة عند **recognize text from image**

### 1. إحداثيات ROI غير صحيحة
إذا كان المستطيل صغيرًا جدًا، سيقطع المحرك الأحرف؛ إذا كان كبيرًا جدًا فستعيد الضوضاء. استخدم أداة بصرية لضبط الأرقام، أو اكتشف حدود الإيصال برمجيًا باستخدام مكتبة معالجة صور بسيطة (مثل OpenCV).

### 2. مسحات منخفضة الدقة
تنخفض دقة الـ OCR بشكل كبير تحت 150 dpi. إذا كنت تتحكم في عملية المسح، استهدف على الأقل 300 dpi. إذا كنت عالقًا بملف منخفض الدقة، جرّب `ocrEngine.SetResolution(300);` قبل استدعاء `Recognize()`.

### 3. إيصالات مائلة أو مدورة
يمكن لـ Aspose OCR تدوير الصورة تلقائيًا، لكن عليك تفعيل ذلك:

```csharp
ocrEngine.SetAutoRotate(true);
```

### 4. إعدادات اللغة
اللغة الافتراضية هي الإنجليزية. إذا كان الإيصال يحتوي على أبجديات أخرى، عيّن اللغة صراحةً:

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
```

---

## حالات الحافة والتنوع – توسيع **Aspose OCR example**

* **حقول متعددة:** هل تريد استخراج التاريخ ومبلغ الضريبة أيضًا؟ ببساطة كرّر خطوة ROI مع مستطيل جديد واستدعِ `Recognize()` مرة أخرى (أو أعد استخدام نفس المحرك بعد إعادة تعيين ROI).  
* **معالجة دفعات:** ضع المنطق داخل حلقة `foreach (var file in Directory.GetFiles(@"C:\Receipts"))` للتعامل مع العشرات من الملفات تلقائيًا.  
* **تنفيذ غير متزامن:** طريقة `Recognize` متزامنة، لكن يمكنك نقلها إلى خيط خلفي باستخدام `Task.Run` إذا كنت تبني تطبيق واجهة مستخدم.

---

## مرجع بصري

![مثال على التعرف على النص من صورة](/images/ocr-demo.png "لقطة شاشة تُظهر نتيجة Aspose OCR – التعرف على النص من صورة")

*تُظهر لقطة الشاشة إخراج الكونسول بعد تشغيل البرنامج الكامل.*

---

## الخلاصة

لقد قمنا الآن بـ **recognize text from image** باستخدام Aspose OCR، وتعرفنا على كيفية **load image for OCR**، وبنينا سير عمل عملي لـ **extract text from receipt** يمكنك دمجه في أي مشروع .NET. مثال **Aspose OCR** الكامل لا يتجاوز بضع أسطر، لكنه يغطي أكثر السيناريوهات شيوعًا: اختيار ROI، تنظيف النتيجة، ومعالجة المشكلات المعتادة.

ما الخطوة التالية؟ جرّب استبدال المستطيل بآلية اكتشاف ديناميكية، جرب لغات مختلفة، أو دمج النتيجة في قاعدة بيانات لتتبع النفقات تلقائيًا. السماء هي الحد، ومع الأساس الذي حصلت عليه الآن، سيكون من السهل التوسع.

هل لديك أسئلة أو إيصال صعب يرفض التعاون؟

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}