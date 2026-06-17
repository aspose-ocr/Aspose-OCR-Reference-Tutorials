---
category: general
date: 2026-03-15
description: كيفية استخدام Aspose OCR لاستخراج النص من الصور وتحويل الصورة إلى JSON
  في C#. تعلم كيفية التعرف على النص من PNG والحصول على مخرجات منظمة بسرعة.
draft: false
keywords:
- how to use aspose
- convert image to json
- extract text from image
- recognize text from png
- how to extract ocr
language: ar
og_description: كيفية استخدام Aspose OCR لاستخراج النص من الصور وتحويل الصورة إلى
  JSON في C#. يوضح هذا الدليل كيفية التعرف على النص من ملفات PNG والحصول على مخرجات
  منظمة.
og_title: كيفية استخدام Aspose OCR لتحويل الصورة إلى JSON
tags:
- Aspose
- OCR
- C#
- JSON
title: كيفية استخدام Aspose OCR لتحويل الصورة إلى JSON
url: /ar/net/text-recognition/how-to-use-aspose-ocr-to-convert-image-to-json/
---

sure we didn't translate any code placeholders.

Now produce final content with translations.

Let's assemble.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام Aspose OCR لتحويل الصورة إلى JSON

كيفية استخدام Aspose OCR هو سؤال شائع عندما يحتاج المطورون إلى استخراج النص من الصور. إذا كنت تبحث عن **convert image to JSON** أو **recognize text from PNG**، فإن هذا الدليل يغطيك—بدون إطالة، مجرد حل عملي من البداية إلى النهاية.

في الدقائق القليلة القادمة سنستعرض كل ما تحتاجه: تثبيت المكتبة، تكوين المحرك لإخراج JSON، تحميل صورة إيصال بصيغة PNG، تشغيل OCR، وأخيرًا كتابة النتيجة إلى ملف `.json`. في النهاية ستكون قادرًا على **extract text from image** باستخدام استدعاء طريقة واحد، وستفهم لماذا كل خطوة مهمة.

> **نصيحة احترافية:** Aspose OCR يعمل مع مجموعة واسعة من صيغ الصور (PNG, JPEG, BMP, TIFF). الكود نفسه أدناه سيتعامل مع جميعها، لذا لا تحتاج إلى كتابة منطق خاص بكل صيغة.

## ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل على .NET Framework 4.6+ أيضًا)  
- حزمة Aspose.OCR NuGet صالحة (تجربة مجانية أو مرخصة)  
- ملف صورة تريد معالجته (مثال، `receipt.png`)  
- Visual Studio، VS Code، أو أي محرر C# تفضله  

هذا كل شيء—بدون تبعيات إضافية، بدون خدمات خارجية. جاهز؟ لنبدأ.

![كيفية استخدام محرك Aspose OCR](image-placeholder.png "كيفية استخدام محرك Aspose OCR")

## كيفية استخدام Aspose OCR – تكوين إخراج JSON

أول شيء عليك القيام به عندما **how to use aspose** للـ OCR هو إنشاء مثيل `OcrEngine` وإبلاغه بإصدار JSON. هذا التبديل الصغير في الإعداد يوفر عليك الحاجة إلى تسلسل النتيجة يدويًا لاحقًا.

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that does the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose to give us JSON instead of plain text.
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Load the image you want to recognize.
        var inputImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // 4️⃣ Run the OCR process.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Save the JSON payload to disk.
        File.WriteAllText(@"YOUR_DIRECTORY/receipt.json", ocrResult.Text);

        // 6️⃣ Let the developer know we’re done.
        Console.WriteLine("JSON saved.");
    }
}
```

**لماذا هذا مهم:** ضبط `OutputFormat` إلى `Json` يعني أن محرك OCR ينظم النص بالفعل في هيكلية من الصفحات، السطور، والكلمات. لا تحتاج إلى تحليل السلاسل الخام لاحقًا، مما يجعل المعالجة اللاحقة—مثل إدخال البيانات إلى قاعدة بيانات—أنظف بكثير.

## تحويل الصورة إلى JSON باستخدام Aspose OCR

الآن بعد أن تم تكوين المحرك، دعنا نتحدث عن جزء **convert image to JSON** بمزيد من التفصيل.

1. **Load the image** – `Image.FromFile` يعمل مع أي صيغة مدعومة. إذا كنت تتعامل مع تدفق (مثال، ملف تم تحميله)، يمكنك استخدام `Image.FromStream` بدلاً من ذلك.  
2. **Run `Recognize`** – هذه الطريقة تُعيد كائن `OcrResult`. لأننا ضبطنا الإخراج إلى JSON، فإن `ocrResult.Text` يحتوي بالفعل على سلسلة JSON.  
3. **Write the file** – `File.WriteAllText` هي أبسط طريقة لحفظ JSON. إذا كنت بحاجة لتخزينه في سلة سحابية، فقط استبدل هذا السطر بالنداء المناسب لـ SDK.  

### النتيجة المتوقعة لـ JSON

حزمة JSON النموذجية تبدو هكذا (مقتصرة للوضوح):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Words": [
            { "Text": "Total", "Confidence": 0.99 },
            { "Text": "$12.34", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

يمكنك الآن تمرير هذا الهيكل إلى أي نظام لاحق—سواء كان أداة تقارير، نموذج تعلم آلي، أو ملف سجل بسيط.

## استخراج النص من الصورة باستخدام Aspose OCR

إذا كنت تحتاج فقط إلى السلسلة الخام (أي لا تهتم بـ JSON)، ببساطة غيّر تنسيق الإخراج إلى نص عادي:

```csharp
ocrEngine.Configuration.OutputFormat = OutputFormat.PlainText;
var plainResult = ocrEngine.Recognize(inputImage);
Console.WriteLine(plainResult.Text);
```

**متى تختار النص العادي؟**  
- تصحيح سريع أو إخراج إلى وحدة التحكم.  
- سيناريوهات ستطبق فيها معالجة مخصصة بعدية (مثال، استخراج باستخدام regex).  

ولكن تذكر، **extract text from image** باستخدام JSON يمنحك بيانات موضعية—مفيدة لتسليط الضوء على النص في واجهة المستخدم أو محاذاة مع حقول النموذج.

## التعرف على النص من ملفات PNG

PNG هو صيغة غير مضغوطة، والتي غالبًا ما تعطي دقة OCR أفضل مقارنةً بـ JPEGs المضغوطة بشدة. إليك قائمة سريعة لضمان الحصول على أفضل النتائج عندما **recognize text from PNG**:

| عنصر القائمة | لماذا يساعد |
|----------------|--------------|
| استخدم DPI 300+ | الدقة الأعلى تعطي المحرك المزيد من البكسلات للعمل معها. |
| حافظ على الصورة بالدرجات الرمادية | يقلل الضوضاء؛ Aspose OCR يحول تلقائيًا، لكن المعالجة المسبقة يمكن أن تسرّع العملية. |
| أزل الفوضى الخلفية | الخلفيات النظيفة تحسن درجات الثقة. |

إذا واجهت درجات ثقة منخفضة، حاول زيادة DPI أو تطبيق مرشح عتبة بسيط قبل تمرير الصورة إلى Aspose.

## كيفية استخراج نتائج OCR برمجيًا

بخلاف حفظ JSON فقط، قد ترغب في قراءة حقول محددة برمجيًا—مثلاً، المبلغ الإجمالي على إيصال. لأن JSON يحتوي على هيكلية، يمكنك تحويله إلى كائن C# عبر عملية فك التسلسل:

```csharp
using System.Text.Json;

// Assuming ocrResult.Text contains the JSON string
var ocrData = JsonSerializer.Deserialize<OcrResponse>(ocrResult.Text);

// Example class definitions (simplified)
public class OcrResponse
{
    public Page[] Pages { get; set; }
}
public class Page
{
    public int PageNumber { get; set; }
    public Line[] Lines { get; set; }
}
public class Line
{
    public Word[] Words { get; set; }
}
public class Word
{
    public string Text { get; set; }
    public double Confidence { get; set; }
}
```

الآن يمكنك استعلام `ocrData` باستخدام LINQ:

```csharp
var totalLine = ocrData.Pages
    .SelectMany(p => p.Lines)
    .FirstOrDefault(l => l.Words.Any(w => w.Text.Equals("Total", StringComparison.OrdinalIgnoreCase)));

if (totalLine != null)
{
    var amount = totalLine.Words
        .FirstOrDefault(w => w.Text.StartsWith("$"))
        ?.Text;
    Console.WriteLine($"Extracted amount: {amount}");
}
```

**لماذا هذا يعمل:** JSON يخبرك بالفعل بمكان وجود كل كلمة على الصفحة، لذا يمكنك تحديد المواقع بدقة حتى إذا تغير التخطيط قليلًا.

## الحالات الحدية والمشكلات الشائعة

- **Null Result:** إذا أعاد `ocrEngine.Recognize` قيمة `null`، قد تكون الصورة غير مدعومة أو تالفة. احرص دائمًا على الحماية ضد ذلك:

  ```csharp
  var ocrResult = ocrEngine.Recognize(inputImage);
  if (ocrResult == null) throw new InvalidOperationException("OCR failed – check the image path.");
  ```

- **Large Files:** بالنسبة للصور متعددة الميجابايت، فكر في بث الصورة أو تغيير حجمها قبل OCR لتجنب استهلاك الذاكرة الزائد.

- **License Issues:** نسخة التجربة تضيف علامة مائية إلى الإخراج. تأكد من تحميل الترخيص مبكرًا في البرنامج:

  ```csharp
  Aspose.OCR.License license = new Aspose.OCR.License();
  license.SetLicense("Aspose.OCR.lic");
  ```

- **Non‑Latin Scripts:** Aspose OCR يدعم العديد من اللغات، لكن يجب ضبط خاصية `Language` وفقًا لذلك (مثال، `ocrEngine.Configuration.Language = Language.English;`).

## مثال كامل يعمل (جاهز للنسخ واللصق)

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Load your Aspose license (optional for trial)
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set output to JSON – this is the key step for convert image to JSON
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Optional: improve accuracy for PNG files
        ocrEngine.Configuration.Dpi = 300; // higher DPI = better results

        // 4️⃣ Load the image you want to process
        var inputImagePath = @"YOUR_DIRECTORY/receipt.png";
        if (!File.Exists(inputImagePath))
            throw new FileNotFoundException($"Image not found: {inputImagePath}");

        var inputImage = Image.FromFile(inputImagePath);

        // 5️⃣ Run OCR – this is where we actually extract text from image
        var ocrResult = ocrEngine.Recognize(inputImage);
        if (ocrResult == null)
            throw new InvalidOperationException("OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}