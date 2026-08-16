---
category: general
date: 2026-04-03
description: التعرف على النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية تحميل
  الصورة للتعرف الضوئي على الأحرف، استخراج النص من الصورة، كتابة ملف JSON في C#، وإجراء
  التعرف الضوئي على الأحرف لملف PNG.
draft: false
keywords:
- recognize text from image
- write json file c#
- load image for ocr
- extract text from image
- perform ocr on png
language: ar
og_description: التعرف على النص من الصورة باستخدام Aspose OCR في C#. دليل خطوة بخطوة
  لتحميل الصورة للتعرف الضوئي على الأحرف، استخراج النص من الصورة، كتابة ملف JSON في
  C#، وإجراء التعرف الضوئي على الأحرف لملف PNG.
og_title: التعرف على النص من الصورة في C# – دليل Aspose OCR الكامل
tags:
- OCR
- C#
- Aspose
title: التعرف على النص من الصورة في C# – دليل Aspose OCR الكامل
url: /ar/net/text-recognition/recognize-text-from-image-in-c-full-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من صورة في C# – دليل Aspose OCR الكامل

هل احتجت يوماً إلى **التعرف على النص من صورة** لكنك لم تكن متأكدًا أي مكتبة تختار؟ ربما لديك مجموعة من الإيصالات الممسوحة ضوئيًا، أو لقطة شاشة بصيغة PNG، أو ملاحظة مكتوبة بخط اليد تريد تحويلها إلى بيانات قابلة للبحث. الخبر السار: باستخدام Aspose.OCR يمكنك القيام بذلك ببضع أسطر من كود C#، وستحصل حتى على ملف JSON منظم يمكنك إمداده إلى أنظمة أخرى.

في هذا الدرس سنستعرض تحميل صورة للـ OCR، استخراج النص من الصورة، تسلسل النتيجة إلى ملف JSON، وأخيرًا التعامل مع ملفات PNG دون عناء. بنهاية الدرس ستحصل على تطبيق console جاهز للتنفيذ **يتعرف على النص من صورة** ويكتب النتيجة إلى *output.json*.

## ما الذي ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework)
- حزمة NuGet الخاصة بـ Aspose.OCR (`Install-Package Aspose.OCR`)
- صورة PNG (أو أي صيغة مدعومة) تريد معالجتها
- Visual Studio، VS Code، أو أي محرر C# تفضله

لا توجد مكتبات طرف ثالث إضافية مطلوبة—فقط محرك Aspose OCR ومُسلسل `System.Text.Json` المدمج.

## الخطوة 1: التعرف على النص من صورة باستخدام Aspose OCR

الخطوة الأولى هي إنشاء مثيل `OcrEngine`. هذا الكائن يقوم بالعمل الشاق خلف الكواليس.

```csharp
using Aspose.OCR;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this is where the magic starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image for OCR – replace the path with your own file.
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/input.png");

        // Perform OCR on the loaded image and get a structured result.
        OcrResult ocrResult = ocrEngine.RecognizeToResult(sourceImage);

        // Serialize the result into a nicely indented JSON string.
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // Write JSON file C# – this will create output.json next to your exe.
        File.WriteAllText(@"YOUR_DIRECTORY/output.json", json);
    }
}
```

**لماذا هذا مهم:** إنشاء `OcrEngine` مرة واحدة وإعادة استخدامها أكثر كفاءة من إنشاء محرك جديد لكل ملف. استدعاء `RecognizeToResult` يُعيد كائن `OcrResult` يحتوي بالفعل على النص المستخرج، درجات الثقة، ومربعات الإحاطة—مثالي للمعالجة اللاحقة.

## الخطوة 2: تحميل الصورة للـ OCR – التعامل مع صيغ مختلفة

يمكن لـ Aspose OCR قراءة PNG، JPEG، BMP، والعديد من الصيغ الأخرى. إذا كنت تتعامل مع PNG يحتوي على شفافية، قد ترغب في تسطيحه أولاً لتجنب الفراغات غير المتوقعة.

```csharp
// Optional: flatten PNG with transparency to a white background.
if (sourceImage.RawFormat.Equals(System.Drawing.Imaging.ImageFormat.Png))
{
    Bitmap flat = new Bitmap(sourceImage.Width, sourceImage.Height);
    using (Graphics g = Graphics.FromImage(flat))
    {
        g.Clear(Color.White);
        g.DrawImage(sourceImage, 0, 0);
    }
    sourceImage = flat;
}
```

**نصيحة احترافية:** تأكد دائمًا من أن أبعاد الصورة معقولة (مثلاً، العرض > 50 px). الصور الصغيرة جدًا قد تجعل محرك OCR يفوت الأحرف، مما يؤدي إلى انخفاض درجات الثقة.

## الخطوة 3: كتابة ملف JSON في C# – جعل المخرجات قابلة للاستخدام

مُسلسل `System.Text.Json` سريع ومدمج، لكن يمكنك استبداله بـ `Newtonsoft.Json` إذا احتجت محولات مخصصة. المثال أعلاه يستخدم بالفعل `WriteIndented = true` بحيث يكون الملف الناتج قابلًا للقراءة البشرية.

```csharp
// Expected output (truncated):
{
  "Text": "Hello World",
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello World",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 120, "Height": 30 }
        }
      ]
    }
  ]
}
```

وجود بيانات OCR بصيغة JSON يتيح لك استيرادها بسهولة إلى قواعد البيانات، إرسالها عبر HTTP، أو إمدادها إلى خطوط أنابيب التعلم الآلي.

## الخطوة 4: التحقق من النتيجة – فحص سريع للمنطقية

بعد تشغيل البرنامج، افتح `output.json` وابحث عن الحقل `"Text"`. إذا كان يحتوي على السلسلة المتوقعة، فقد نجحت في **استخراج النص من صورة**. إذا كانت درجة الثقة منخفضة، فكر في معالجة مسبقة للصورة (مثل زيادة التباين أو تطبيق عتبة ثنائية).

```csharp
Console.WriteLine($"Extracted text: {ocrResult.Text}");
Console.WriteLine($"Overall confidence: {ocrResult.Confidence:P2}");
```

سيطبع الكونصول شيئًا مشابهًا لـ:

```
Extracted text: Hello World
Overall confidence: 98.00%
```

هذا مؤشر قوي على أن الـ OCR عمل كما هو متوقع.

## المشكلات الشائعة والحالات الخاصة

| المشكلة | السبب | الحل |
|-------|----------------|------------|
| **إخراج فارغ** | الصورة مظلمة جدًا أو تحتوي على مساحة ألوان غير مدعومة | تحويلها إلى تدرج الرمادي، زيادة السطوع، أو تسطيح PNG (انظر الخطوة 2) |
| **حروف غير مفهومة** | DPI منخفض (< 72) أو ضوضاء شديدة | تكبير الصورة أو تطبيق مرشح إزالة الضوضاء قبل تمريرها إلى `RecognizeToResult` |
| **ملفات كبيرة تسبب ضغطًا على الذاكرة** | تحميل PNG متعدد الميجابكسل إلى `Bitmap` يستهلك RAM | معالجة الصور على دفعات أو تقليل حجمها مع الحفاظ على قابلية القراءة |
| **خطأ في تسلسل JSON** | `OcrResult` يحتوي على مراجع دائرية (نادر) | استخدم `JsonSerializerOptions { ReferenceHandler = ReferenceHandler.IgnoreCycles }` |

## إضافي: تنفيذ OCR على PNG في حلقة دفعة

إذا كان لديك مجلد مليء بملفات PNG، يمكنك توسيع المثال لتكرار العملية على كل ملف:

```csharp
string[] pngFiles = Directory.GetFiles(@"YOUR_DIRECTORY", "*.png");
foreach (var file in pngFiles)
{
    Image img = Image.FromFile(file);
    OcrResult res = ocrEngine.RecognizeToResult(img);
    string outPath = Path.ChangeExtension(file, ".json");
    File.WriteAllText(outPath, JsonSerializer.Serialize(res, new JsonSerializerOptions { WriteIndented = true }));
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(outPath)}");
}
```

الآن البرنامج **ينفذ OCR على ملفات PNG** جماعيًا، ويكتب ملف JSON مطابق لكل صورة.

## الخلاصة

لقد تعلمت الآن كيف **تتعرف على النص من صورة** في C# باستخدام Aspose OCR، **تحمل صورة للـ OCR**، **استخراج النص من صورة**، و**كتابة ملف JSON في C#** لتخزين النتائج. المثال الكامل القابل للتنفيذ يغطي الخطوات الأساسية، يوضح لماذا كل جزء مهم، ويظهر أيضًا كيفية التعامل مع خصوصيات PNG.

ما الخطوة التالية؟ جرّب إمداد JSON إلى فهرس بحث، دمجه مع كشف اللغة، أو دمجه في واجهة ويب API تعالج التحميلات مباشرة. يمكنك أيضًا استكشاف دعم Aspose للتعرف على الخط اليدوي إذا كان ذلك يناسب حالتك.

هل لديك أسئلة حول الحالات الخاصة أو تحسين الأداء؟ اترك تعليقًا أدناه—برمجة سعيدة! 

![recognize text from image demo](/images/ocr-demo.png "Diagram showing how Aspose OCR recognizes text from image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}