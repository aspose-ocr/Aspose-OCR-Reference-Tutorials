---
category: general
date: 2026-03-13
description: كيفية تنفيذ OCR في C# واستخراج النص من الصورة باستخدام OcrEngine. تعلم
  تحويل الصورة إلى نص بسرعة من خلال دليل شامل خطوة بخطوة.
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- read text from picture
- how to extract text
language: ar
og_description: كيفية تنفيذ OCR في C#؟ يوضح لك هذا الدليل كيفية استخراج النص من الصورة،
  تحويل الصورة إلى نص، وقراءة النص من الصورة باستخدام OcrEngine.
og_title: كيفية تنفيذ OCR في C# – استخراج النص من الصورة
tags:
- OCR
- C#
- Image Processing
title: كيفية تنفيذ OCR في C# – استخراج النص من الصورة
url: /ar/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR في C# – استخراج النص من صورة

كيفية تنفيذ OCR في C# هو سؤال شائع للمطورين الذين يحتاجون إلى **قراءة النص من ملفات الصور**. في هذا الدليل سنرشدك إلى استخراج النص من صورة باستخدام مكتبة `OcrEngine`، وتحويل الصور إلى سلاسل قابلة للبحث ببضع أسطر من الشيفرة فقط.  

إذا سبق لك أن حدقت في فاتورة ممسوحة ضوئياً، أو ملاحظة مكتوبة بخط اليد، أو لقطة شاشة وتساءلت *“كيف أستخرج النص؟”*، فأنت في المكان الصحيح. سنتطرق أيضاً إلى تحويل الصورة إلى نص للمعالجة الدفعية، حتى تتمكن من أتمتة سير العمل بالكامل.

---

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي:

- **.NET 6.0 أو أحدث** (واجهة برمجة التطبيقات التي نستخدمها تعمل مع .NET Standard 2.0+)
- حزمة NuGet **OcrEngine** (أو أي مكتبة OCR متوافقة تُظهر الخصائص `Language`، `Image`، `Recognize`، و `Text`)
- ملف صورة تجريبي، مثال: `hindi_page.jpg`، موجود في مجلد يمكنك الإشارة إليه من الشيفرة
- فهم أساسي لصياغة C# – لا حاجة لحيل متقدمة

هذا كل شيء. لا خدمات خارجية، لا مفاتيح API، مجرد مكتبة محلية تقوم بالعمل الشاق.

---

## تنفيذ خطوة بخطوة

فيما يلي نقسم العملية إلى أجزاء منطقية. كل قسم يحتوي على عنوان واضح، مقتطف شيفرة قصير، وتفسير **لماذا** الخطوة مهمة—not مجرد **ماذا** تفعل.

### كيفية تنفيذ OCR – الخطوات الأساسية

يمكن تلخيص التدفق العام في خمس إجراءات:

1. **إنشاء** كائن محرك OCR
2. **اختيار** اللغة التي تريد التعرف عليها
3. **تحميل** الصورة التي تحتوي على النص
4. **تشغيل** خوارزمية التعرف
5. **قراءة** النص المستخرج

هذا هو الهيكل؛ الأقسام التالية تفصل كل خطوة.

---

### استخراج النص من صورة – إنشاء المحرك

أولاً، نحتاج إلى كائن يعرف كيف يتواصل مع محرك OCR.

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

*لماذا هذا مهم:* إنشاء كائن `OcrEngine` يخصص جميع المخازن الداخلية ويحمل أي ملفات DLL أصلية مطلوبة لتحليل الصورة. تخطي هذه الخطوة سيتركك بدون مُعرّف لتستدعيه لاحقاً.

> **نصيحة محترف:** إذا كنت تخطط لمعالجة العديد من الصور على التوالي، حافظ على بقاء نفس كائن `ocrEngine` فعالاً. فهو يعيد استخدام نماذج اللغة ويسرّع الاستدعاءات اللاحقة.

---

### تحويل الصورة إلى نص – اختيار اللغة

تعتمد دقة OCR بشكل كبير على نموذج اللغة الذي تزوده به. للغة الهندية أو التاميلية أو أي نص آخر، اضبط الخاصية `Language` وفقاً لذلك.

```csharp
// Step 2: Select the language of the text to recognize (e.g., Hindi)
ocrEngine.Language = Language.Hindi;   // You can also use Language.Tamil, Language.English, etc.
```

*لماذا هذا مهم:* يستخدم المحرك مجموعات أحرف ونماذج إحصائية مخصصة للغة. توفير لغة غير صحيحة غالباً ما ينتج مخرجات مشوهة، خاصةً للخطوط غير اللاتينية.

> **حالة خاصة:** إذا كنت بحاجة إلى دعم متعدد اللغات، تسمح بعض المكتبات بتعيين قائمة احتياطية، مثال: `ocrEngine.Language = Language.Multilingual;`.

---

### قراءة النص من الصورة – تحميل صورة المصدر

الآن نوجه المحرك إلى الملف الذي يحمل النص البصري.

```csharp
// Step 3: Load the image that contains the text
ocrEngine.Image = ImageStream.FromFile(@"C:\OCR\Samples\hindi_page.jpg");
```

*لماذا هذا مهم:* `ImageStream.FromFile` يحول الملف الخام إلى تنسيق bitmap يمكن لنواة OCR فهمه. توفير ملف تالف أو بتنسيق غير مدعوم (مثل SVG) سيتسبب في استثناء.

> **احذر:** الصور الكبيرة قد تستهلك الكثير من الذاكرة. إذا كنت تعالج مسحات عالية الدقة، فكر في تقليل الحجم باستخدام `Image.Resize` قبل تمريرها إلى المحرك.

---

### تحويل الصورة إلى نص – تشغيل عملية التعرف

مع جاهزية المحرك وتحميل الصورة، نستدعي أخيراً عملية OCR.

```csharp
// Step 4: Perform the OCR operation
ocrEngine.Recognize();
```

*لماذا هذا مهم:* `Recognize` يُطلق سلسلة من الخطوات الداخلية—ما قبل المعالجة، التجزئة، تصنيف الأحرف، وما بعد المعالجة. الاستدعاء محجوز، أي أن الخيط ينتظر حتى يصبح النص جاهزاً.

> **ملاحظة أداء:** على جهاز مكتبي عادي، يستغرق التعرف على صفحة بدقة 300 dpi أقل من ثانية. على الخادم، قد ترغب في تشغيل ذلك في مهمة خلفية لتجنب تجميد الواجهة.

---

### كيفية استخراج النص – استرجاع النتيجة

بعد انتهاء عملية التعرف، يخزن المحرك النص الصافي في الخاصية `Text`.

```csharp
// Step 5: Output the recognized text
Console.WriteLine(ocrEngine.Text);
```

*لماذا هذا مهم:* الخاصية `Text` تعطيك سلسلة UTF‑8 نظيفة يمكنك كتابتها إلى ملف، أو إدخالها في قاعدة بيانات، أو تمريرها إلى خطوط معالجة لغة طبيعية لاحقة.

> **الناتج المتوقع:** بالنسبة لصفحة الهندية التجريبية، قد ترى شيئاً مثل  
> `यह एक उदाहरण पाठ है जो OCR द्वारा पहचाना गया है।`  
> (الناتج الدقيق يعتمد على جودة الصورة ونموذج اللغة.)

---

## اعتبارات إضافية للمشاريع الواقعية

فيما يلي بعض السيناريوهات “ماذا لو” التي قد تواجهها عند **استخراج النص من صورة** في بيئة الإنتاج.

### معالجة عدة صور داخل حلقة

إذا كنت بحاجة إلى **تحويل الصورة إلى نص** لعدة ملفات، غلف الخطوات داخل حلقة `foreach` وأعد استخدام نفس كائن `ocrEngine`:

```csharp
string[] files = Directory.GetFiles(@"C:\OCR\Batch\", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), ocrEngine.Text);
}
```

### التعامل مع مسحات منخفضة الجودة

- **معالجة مسبقة** باستخدام التثنية (`Image.Binarize()`)، إزالة الضوضاء، أو تصحيح الميل.
- **زيادة DPI** عند المسح (300 dpi يعتبر قاعدة آمنة).
- **اختيار نموذج لغة** يدعم ربط الحروف للخط (مثلاً Devanagari للغة الهندية).

### قراءة النص من صورة على الويب

عندما تأتي الصورة من عنوان URL، قم بتحميلها إلى تدفق ذاكرة أولاً:

```csharp
using (HttpClient client = new())
{
    byte[] data = await client.GetByteArrayAsync(imageUrl);
    using var ms = new MemoryStream(data);
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
    Console.WriteLine(ocrEngine.Text);
}
```

### السلامة من الخيوط والتوازي

معظم مكتبات OCR **ليست** آمنة للاستخدام المتعدد الخيوط مباشرة. إذا كنت تخطط إلى **قراءة النص من صورة** بشكل متوازي، أنشئ كائنات `OcrEngine` منفصلة لكل خيط، أو استخدم طابور منتج‑مستهلك لتسلسل الوصول.

---

## مثال عملي كامل

بدمج كل ما سبق، إليك تطبيق console جاهز للتنفيذ يوضح **كيفية تنفيذ OCR**، **استخراج النص من صورة**، و**قراءة النص من صورة** في برنامج موحد.

```csharp
using System;
using OcrLibrary;               // Adjust to your OCR library's namespace
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Choose the language (Hindi in this case)
        ocrEngine.Language = Language.Hindi;

        // Load the image file
        string imagePath = @"C:\OCR\Samples\hindi_page.jpg";
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }

        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // Run the recognition process
        ocrEngine.Recognize();

        // Output the extracted text
        string result = ocrEngine.Text;
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(result);

        // Optional: Save to a .txt file
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, result);
        Console.WriteLine($"Text saved to {txtPath}");
    }
}
```

**ما يجب أن تراه:** سيتطبع الـ console جملة الهندية المستخرجة من `hindi_page.jpg`، متبوعةً بتأكيد إنشاء ملف النص. إذا كانت الصورة نظيفة، سيكون الناتج مطابقاً تقريباً للنص المطبوع الأصلي.

---

## الخلاصة

أنت الآن تعرف **كيفية تنفيذ OCR** في C# من البداية إلى النهاية، وكيفية **استخراج النص من صورة**، **تحويل الصورة إلى نص**، و**قراءة النص من صورة** باستخدام سير عمل `OcrEngine` بسيط. نمط الخطوات الخمس—إنشاء، تعيين اللغة، تحميل، التعرف، قراءة—يغطي معظم الحالات، والنصائح الإضافية تساعدك على التعامل مع المهام الدفعية، المسحات منخفضة الجودة، والمصادر عبر الويب.

هل أنت مستعد للتحدي التالي؟ جرّب تغيير اللغة إلى الإنجليزية، أو معالجة صفحة PDF محوّلة إلى صورة، أو ربط ناتج OCR بخط أنابيب فهرسة بحث. السماء هي الحد عندما تتقن أساسيات OCR في C#.

هل لديك أسئلة أو صورة معقدة لا تتعاون؟ اترك تعليقاً أدناه، ولنحل المشكلة معاً. برمجة سعيدة!  

![مثال على كيفية تنفيذ OCR](images/ocr-example.png "مثال على كيفية تنفيذ OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}