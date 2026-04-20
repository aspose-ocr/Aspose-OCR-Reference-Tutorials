---
category: general
date: 2026-02-16
description: تعلم كيفية تنفيذ OCR في C# باستخدام Aspose.OCR – التعرف على النص من الصورة،
  قراءة النص من المسح الضوئي، واستخراج النص من الإيصال بدقة عالية.
draft: false
keywords:
- how to perform OCR
- recognize text from photo
- read text from scan
- extract text from receipt
- improve OCR accuracy
language: ar
og_description: تعلم كيفية تنفيذ OCR في C# باستخدام Aspose.OCR. يوضح لك هذا الدليل
  كيفية التعرف على النص من الصورة، قراءة النص من المسح الضوئي، واستخراج النص من الإيصال.
og_title: كيفية تنفيذ OCR في C# – دليل Aspose الكامل
tags:
- C#
- Aspose.OCR
- Image Processing
title: كيفية تنفيذ OCR في C# – دليل Aspose الكامل
url: /ar/net/text-recognition/how-to-perform-ocr-in-c-complete-aspose-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR في C# – دليل Aspose الكامل

هل تساءلت يومًا **كيف تقوم بتنفيذ OCR** على إيصال غير واضح أو صورة عشوائية التقطتها بهاتفك؟ لست وحدك. في العديد من التطبيقات الواقعية نحتاج إلى **التعرف على النص من صورة**، **قراءة النص من مسح** المستندات، أو **استخراج النص من صورة إيصال** دون إرسال البيانات إلى خدمة سحابية.  

في هذا الدرس سنستعرض مثالًا مستقلًا يوضح لك **كيف تقوم بتنفيذ OCR** باستخدام Aspose.OCR، وسنضيف نصائح حول **تحسين دقة OCR** على طول الطريق. في النهاية ستحصل على برنامج C# Console جاهز للتشغيل يستخرج النص العادي من أي صورة توجهه إليها.

> **ما ستحتاجه**  
> * .NET 6 SDK (أو أي نسخة حديثة من .NET)  
> * حزمة Aspose.OCR NuGet (`Install-Package Aspose.OCR`)  
> * صورة نموذجية – على سبيل المثال صورة لإيصال باسم `photo_receipt.jpg`  

إذا كان ذلك مألوفًا لك، رائع – لنبدأ.

![مثال على كيفية تنفيذ OCR](image.png){alt="كيفية تنفيذ OCR"}

## كيفية تنفيذ OCR باستخدام Aspose.OCR في C#

الخطوة الأولى هي إعداد محرك OCR وتحميل نموذج لغة إنجليزي. هذا هو جوهر **كيف تقوم بتنفيذ OCR** باستخدام Aspose؛ بدون نموذج لغة لن يعرف المحرك أي أحرف يبحث عنها.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the English language model – change this if you need another language
ocrEngine.LoadLanguage(LanguageModel.English);
```

*لماذا هذا مهم*: تحميل نموذج اللغة الصحيح يؤثر مباشرة على سرعة ودقة التعرف. الإنجليزية هي الحالة الأكثر شيوعًا، لكن Aspose يقدم العشرات من النماذج الأخرى إذا احتجت يومًا إلى **قراءة النص من مسح** المستندات بالفرنسية أو الألمانية، إلخ.

## التعرف على النص من صورة

الصور الملتقطة بالهاتف غالبًا ما تعاني من الدوران أو الضوضاء أو انخفاض التباين. قبل أن نطلب من المحرك **التعرف على النص من صورة**، نقوم بتكوين بعض خيارات ما قبل المعالجة التي تنظف الصورة.

```csharp
// Configure preprocessing to boost OCR results
PreprocessingOptions preprocessingOptions = new PreprocessingOptions
{
    Deskew = true,                     // Auto‑correct rotation (helps with tilted receipts)
    Denoise = DenoiseLevel.Medium,    // Reduce graininess
    Binarize = BinarizeMethod.Otsu,   // Convert to black‑and‑white for sharper edges
    ContrastEnhancement = true        // Boost contrast for faint characters
};

// Apply the preprocessing configuration
ocrEngine.Preprocessing = preprocessingOptions;
```

*نصيحة احترافية*: إذا لاحظت أحرفًا مفقودة، جرّب تغيير `DenoiseLevel` إلى `High` أو استخدام `BinarizeMethod.Sauvola`. هذه التعديلات هي جزء من استراتيجيات **تحسين دقة OCR**.

## قراءة النص من مسح

الآن بعد أن تم تجهيز المحرك، نقوم بتحميل الصورة. سواء كانت صفحة PDF ممسوحة ضُمت كملف JPEG أو صورة لنموذج مطبوع، يبقى الكود كما هو.

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/photo_receipt.jpg");
```

إذا كان لديك `Stream` بدلاً من مسار ملف، استبدل ببساطة `FromFile` بـ `FromStream`. هذه المرونة مفيدة عندما **تقرا النص من مسح** للصور التي تأتي من رفع ويب.

## استخراج النص من إيصال

مع إعداد كل شيء، استدعاء OCR الفعلي هو سطر واحد. تُعيد الطريقة سلسلة النص المستخرج، والتي يمكننا بعد ذلك عرضها أو تخزينها أو تمريرها إلى نظام آخر.

```csharp
// Perform OCR and capture the result
string extractedText = ocrEngine.Recognize();

// Output the text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(extractedText);
```

**الناتج المتوقع** (مثال لإيصال بسيط):

```
=== OCR RESULT ===
Store: CoffeeShop
Date: 2024-02-15
Item      Qty   Price
Latte      2    4.50
Bagel      1    2.75
Total            7.25
```

إذا كان الناتج مشوشًا، أعد زيارة قسم ما قبل المعالجة – فهو المكان الأكثر شيوعًا **لتحسين دقة OCR**.

## تحسين دقة OCR – تعديلات متقدمة

بينما تعمل الإعدادات الافتراضية للعديد من الحالات، غالبًا ما تحتاج خطوط الإنتاج إلى عناية إضافية:

| الحالة | التعديل | السبب |
|-----------|------------|--------|
| خلفية داكنة جدًا | `ContrastEnhancement = true` + `Binarize = BinarizeMethod.Sauvola` | يزيد الفصل بين النص والخلفية |
| ملاحظات مكتوبة بخط اليد | `ocrEngine.LoadLanguage(LanguageModel.EnglishHandwritten)` | نموذج متخصص للخطوط المتصلة |
| مسحات متعددة الصفحات | Loop over each page image and call `Recognize()` per iteration | يحافظ على استهلاك الذاكرة منخفضًا |
| صور كبيرة (> 2000 px) | Resize before feeding to OCR (`Image.Resize(width, height)`) | معالجة أسرع، استهلاك ذاكرة أقل |

تذكر أن **كيفية تنفيذ OCR** ليست وصفة واحدة تناسب الجميع – غالبًا ما ستجرب هذه الإعدادات حتى يطابق الناتج مستوى الجودة المطلوب.

## مثال كامل يعمل

فيما يلي البرنامج الكامل، جاهز للنسخ واللصق. يتضمن جميع الأجزاء التي ناقشناها، بالإضافة إلى أداة مساعدة صغيرة تتحقق مما إذا كان الملف موجودًا قبل محاولة قراءته.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine and load language
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.LoadLanguage(LanguageModel.English);

        // 2️⃣ Set up preprocessing to improve OCR accuracy
        ocrEngine.Preprocessing = new PreprocessingOptions
        {
            Deskew = true,
            Denoise = DenoiseLevel.Medium,
            Binarize = BinarizeMethod.Otsu,
            ContrastEnhancement = true
        };

        // 3️⃣ Path to the image – change this to your own file
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo_receipt.jpg");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"⚠️  Image not found: {imagePath}");
            return;
        }

        // 4️⃣ Load the image (recognize text from photo / read text from scan)
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // 5️⃣ Perform OCR – this is the core of how to perform OCR
        string extractedText = ocrEngine.Recognize();

        // 6️⃣ Show the result – you can now extract text from receipt, invoice, etc.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(extractedText);
    }
}
```

شغّل البرنامج باستخدام `dotnet run`. إذا تم إعداد كل شيء بشكل صحيح، سترى النص المستخرج يُطبع على وحدة التحكم.

## أسئلة شائعة وحالات خاصة

**س: ماذا لو كانت الصورة PDF؟**  
ج: حوّل كل صفحة PDF إلى صورة أولاً (مثلاً باستخدام `Aspose.Pdf` أو `PdfSharp`) ثم مرّر الصورة الناتجة إلى `ocrEngine.Image`.

**س: هل يمكنني معالجة الصور بشكل متوازي؟**  
ج: نعم، لكن أنشئ `OcrEngine` منفصل لكل خيط. المحرك غير آمن للاستخدام المتعدد الخيوط، لذا مشاركة نسخة واحدة قد تتسبب في ظروف سباق.

**س: هل يعمل هذا على لينكس؟**  
ج: بالتأكيد. Aspose.OCR متعدد المنصات؛ فقط تأكد من تثبيت الاعتمادات الأصلية (`libgdiplus` لـ .NET Core على لينكس).

**س: كيف أتعامل مع إيصالات متعددة اللغات؟**  
ج: حمّل نماذج لغات متعددة قبل التعرف:  
```csharp
ocrEngine.LoadLanguage(LanguageModel.English);
ocrEngine.LoadLanguage(LanguageModel.Spanish);
```  
سوف يحاول المحرك كل نموذج بالترتيب.

## الخلاصة

أصبح لديك الآن إجابة شاملة من البداية إلى النهاية على **كيفية تنفيذ OCR** في C# باستخدام Aspose.OCR. غطى الدرس كل شيء من تهيئة المحرك، **التعرف على النص من صورة**، **قراءة النص من مسح**، إلى **استخراج النص من إيصال**، وقد زودك بطرق عملية **لتحسين دقة OCR**.  

ما الخطوات التالية؟ جرّب استبدال نموذج الإنجليزية بنموذج مكتوب بخط اليد، جرب قيمًا مختلفة لـ `BinarizeMethod`، أو دمج استدعاء OCR في واجهة API لـ ASP.NET التي تعالج التحميلات مباشرة. الاحتمالات واسعة بقدر الصور التي تغذيها.  

هل لديك المزيد من الأسئلة حول OCR أو ما قبل معالجة الصور أو مكتبات Aspose؟ اترك تعليقًا أو استكشف الوثائق الرسمية لـ Aspose.OCR لمزيد من التفاصيل. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}