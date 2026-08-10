---
category: general
date: 2026-02-13
description: تعلم كيفية إجراء التعرف الضوئي على الأحرف (OCR) على الصور العربية واستخراج
  النص العربي من ملف JPG. يوضح لك هذا الدليل خطوة بخطوة كيفية قراءة نص الصورة وتحويل
  الصورة إلى نص باستخدام C#.
draft: false
keywords:
- how to perform OCR
- extract arabic text
- read image text
- extract text jpg
- convert image to text
language: ar
og_description: كيفية تنفيذ تقنية التعرف الضوئي على الأحرف (OCR) على الصور العربية
  واستخراج النص العربي. اتبع هذا الدليل الكامل لقراءة نص الصورة من ملفات JPG وتحويل
  الصورة إلى نص في C#.
og_title: كيفية تنفيذ التعرف الضوئي على الحروف في الصور العربية – استخراج النص في
  C#
tags:
- OCR
- C#
- Image Processing
title: كيفية إجراء OCR على الصور العربية – استخراج النص في C#
url: /ar/net/text-recognition/how-to-perform-ocr-on-arabic-images-extract-text-in-c/
---

CODE_BLOCK_0}} etc.

Also ensure we keep markdown formatting: headings, lists, bold, etc.

Now produce final output with translated content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR على الصور العربية – استخراج النص في C#

هل تساءلت يومًا **كيف تقوم بتنفيذ OCR** على الصور العربية دون أن تشد شعرك؟ لست الوحيد—المطورون يواجهون دائمًا صعوبة عندما يحتاجون إلى قراءة نص الصورة المكتوب من اليمين إلى اليسار.  

في هذا الدرس سترى حلاً كاملاً وقابلاً للتنفيذ يقوم **باستخراج النص العربي** من ملف JPEG، ويظهر لك كيف **تقرأ نص الصورة**، وأخيرًا **تحول الصورة إلى نص** يمكنك استخدامه في تطبيقك. لا مراجع غامضة، فقط كود ملموس والمنطق وراء كل سطر.

> **نصيحة احترافية:** إذا كنت تعمل مع إيصالات ممسوحة، أو لافتات الشوارع، أو وثائق تاريخية، فإن الخطوات أدناه ستوفر لك ساعات من التجربة والخطأ.

## ما ستحتاجه  

- .NET 6 أو أحدث (المثال يستخدم تطبيق console).  
- مكتبة OCR تدعم العربية. للتوضيح سنستخدم حزمة NuGet الخيالية `SimpleOcr`، لكن النمط يعمل مع Tesseract أو IronOCR أو Microsoft Computer Vision.  
- ملف صورة باسم `arabic_sign.jpg` موجود في مجلد يمكنك الإشارة إليه (مثلاً `./Images/`).  

هذا كل شيء. لا حزم SDK ثقيلة، ولا مفاتيح سحابية، فقط بضع أسطر من C#.

![كيفية تنفيذ OCR على لافتة عربية](/images/arabic_sign.jpg)

*نص بديل للصورة: كيفية تنفيذ OCR على لافتة عربية*

## كيفية تنفيذ OCR على الصور العربية  

فيما يلي نقسم العملية إلى ثلاث خطوات منطقية. كل خطوة تشرح **ماذا** نفعل، **لماذا** يهم، و**كيف** يتماشى الكود.

### الخطوة 1: تثبيت وتهيئة محرك OCR  

أولاً، أضف حزمة OCR إلى مشروعك:

```bash
dotnet add package SimpleOcr
```

الآن أنشئ مثيلًا للمحرك وأخبره باستخدام نموذج اللغة العربية. ضبط اللغة مبكرًا أمر حاسم؛ وإلا سيتعامل المحرك مع الأحرف العربية كرموز غير معروفة.

```csharp
using System;
using SimpleOcr;   // <-- fictional namespace for illustration

// Step 1: Create an OCR engine configured for Arabic
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Arabic   // Enables right‑to‑left processing
};
```

**لماذا هذا مهم:** العربية تستخدم اتجاه كتابة مختلف ولها أشكال أحرف تعتمد على السياق. باختيار `OcrLanguage.Arabic` صراحةً، يطبق المحرك قواعد تشكيل صحيحة ويحسن الدقة بشكل كبير.

### الخطوة 2: تحميل ملف JPEG وتشغيل التعرف  

بعد ذلك نقوم بتمرير الصورة إلى المحرك. طريقة `RecognizeImage` تُعيد كائن `OcrResult` يحتوي على النص الخام، درجات الثقة، ومربعات الإحاطة الاختيارية.

```csharp
// Step 2: Recognize text from the input image
string imagePath = @"./Images/arabic_sign.jpg";

OcrResult ocrResult;
try
{
    ocrResult = ocrEngine.RecognizeImage(imagePath);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to process '{imagePath}': {ex.Message}");
    return;
}
```

**ملاحظة حالة الحافة:** إذا لم يُعثر على الملف أو لم يكن التنسيق مدعومًا، سيعطيك كتلة `catch` خطأ واضحًا بدلاً من تعطل صامت. هذا مفيد بشكل خاص عند **استخراج النص من ملفات JPG** في وظائف الدُفعات.

### الخطوة 3: استخراج النص واستخدامه  

أخيرًا، نستخرج السلسلة المعترف بها من `ocrResult` ونعرضها. يمكنك أيضًا كتابة النص إلى ملف، إرساله عبر API، أو تمريره إلى خطوط معالجة اللغة الطبيعية اللاحقة.

```csharp
// Step 3: Display the extracted Arabic text
Console.WriteLine("=== Extracted Arabic Text ===");
Console.WriteLine(ocrResult.Text);

// Optional: Save to a .txt file for later processing
System.IO.File.WriteAllText("./output/extracted_text.txt", ocrResult.Text);
```

**الناتج المتوقع:**  
إذا كان ملف `arabic_sign.jpg` يحتوي على العبارة “مكتبة المدينة” (City Library)، سيطبع الطرفية شيء مشابه:

```
=== Extracted Arabic Text ===
مكتبة المدينة
```

قد يتضمن الناتج مسافات زائدة؛ يمكنك تنظيفها باستخدام `String.Trim()` أو التعبيرات النمطية إذا لزم الأمر.

## تنوعات شائعة ونصائح  

### قراءة نص الصورة من صيغ مختلفة  

الكود نفسه يعمل مع PNG أو BMP أو حتى صفحات PDF (إذا كانت المكتبة تدعمها). فقط غيّر امتداد الملف في `imagePath`. تذكر الحفاظ على **الكلمة المفتاحية الأساسية** في ذهنك: في كل مرة تغير فيها الصيغ، ما زلت *تنفذ OCR* على مصدر جديد.

### تحسين الدقة عند **استخراج النص العربي**  

- **معالجة مسبقة للصورة**: زيادة التباين، تصحيح الميل، أو تطبيق عتبة ثنائية.  
- **ضبط DPI أعلى**: العديد من محركات OCR تتوقع على الأقل 300 dpi للحصول على أحرف واضحة.  
- **استخدام حزم اللغة**: بعض المكتبات تسمح بتحميل قاموس عربي مخصص لكلمات المجال المحدد.

### معالجة دفعات كبيرة (استخراج نص JPG في حلقات)  

إذا كان لديك مجلد مليء بملفات JPEG، غلف خطوة التعرف داخل حلقة `foreach`:

```csharp
foreach (var file in Directory.GetFiles("./Images", "*.jpg"))
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text}");
}
```

هذا النمط يتيح لك **تحويل الصورة إلى نص** على نطاق واسع دون إعادة كتابة الكود.

### عندما يُرجع المحرك نتائج فارغة  

- تحقق من أن الصورة ليست مظلمة جدًا أو غير واضحة.  
- تأكد من تحميل نموذج اللغة العربية بشكل صحيح (بعض الحزم تتطلب تنزيلًا منفصلًا).  
- جرّب مزود OCR مختلف؛ على سبيل المثال، Tesseract غالبًا ما يتعامل مع الصور منخفضة الدقة بشكل أفضل.

## مثال كامل وجاهز للتنفيذ  

انسخ المقتطف أدناه إلى مشروع console جديد (`dotnet new console -n ArabicOcrDemo`). يتضمن جميع بيانات `using` الضرورية، معالجة الأخطاء، ورأس تعليق مختصر.

```csharp
// ArabicOcrDemo.csproj
// <Project Sdk="Microsoft.NET.Sdk">
//   <PropertyGroup>
//     <OutputType>Exe</OutputType>
//     <TargetFramework>net6.0</TargetFramework>
//   </PropertyGroup>
//   <ItemGroup>
//     <PackageReference Include="SimpleOcr" Version="1.2.3" />
//   </ItemGroup>
// </Project>

using System;
using SimpleOcr;   // Replace with your actual OCR library namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine for Arabic
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Arabic
        };

        // 2️⃣ Path to the JPEG containing Arabic text
        string imagePath = @"./Images/arabic_sign.jpg";

        // 3️⃣ Run recognition with graceful error handling
        OcrResult result;
        try
        {
            result = ocrEngine.RecognizeImage(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error processing image: {ex.Message}");
            return;
        }

        // 4️⃣ Output the extracted text
        Console.WriteLine("=== Extracted Arabic Text ===");
        Console.WriteLine(result.Text);

        // 5️⃣ Optional: persist the text for later use
        System.IO.Directory.CreateDirectory("./output");
        System.IO.File.WriteAllText("./output/extracted_text.txt", result.Text);
    }
}
```

شغّله باستخدام:

```bash
dotnet run --project ArabicOcrDemo.csproj
```

سترى العبارة العربية مطبوعة في الطرفية ومحفوظة تحت `./output/extracted_text.txt`.

## الخلاصة  

أنت الآن تعرف **كيف تقوم بتنفيذ OCR** على الصور العربية، وكيف **استخراج النص العربي**، وكيف **قراءة نص الصورة** من ملف JPEG و**تحويل الصورة إلى نص** في تطبيق console C# نظيف وجاهز للإنتاج. تدفق الخطوات الثلاث — إعداد المحرك، التعرف على الصورة، ومعالجة النتيجة — يغطي جوهر كل مهمة OCR، بغض النظر عن اللغة أو نوع الملف.

هل أنت مستعد للتحدي التالي؟ جرّب تغيير اللغة إلى الإنجليزية، أو معالجة ملف PDF، أو دمج الناتج مع API للترجمة. يمكنك أيضًا استكشاف **استخراج نص jpg** في وضعية متوازية باستخدام `Parallel.ForEach` لمجموعات بيانات ضخمة.

هل لديك أسئلة حول حالات الحافة، تحسين الأداء، أو مكتبات بديلة؟ اترك تعليقًا أدناه—برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}