---
category: general
date: 2026-04-01
description: تعلم كيفية تحويل صورة إيصال إلى نص باستخدام Aspose OCR. يوضح هذا الدليل
  كيفية استخراج النص السيريلي، تحميل الصورة للتعرف الضوئي على الأحرف، والتعرف على
  الأحرف السيريليّة بكفاءة.
draft: false
keywords:
- receipt image to text
- extract cyrillic text
- load image for ocr
- recognize cyrillic characters
- create OCR engine
language: ar
og_description: حوّل صورة إيصال إلى نص باستخدام Aspose OCR. تعلم استخراج النص السيريلي،
  تحميل الصورة للتعرف الضوئي على الأحرف، والتعرف على الأحرف السيريالية في C#.
og_title: تحويل صورة الإيصال إلى نص – التعرف الضوئي على الحروف السيريالية مع Aspose
tags:
- OCR
- C#
- Aspose
- Cyrillic
title: تحويل صورة الإيصال إلى نص – التعرف الضوئي على الحروف السيريالية باستخدام Aspose
url: /ar/net/text-recognition/receipt-image-to-text-cyrillic-ocr-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل صورة الإيصال إلى نص – OCR سيريالي باستخدام Aspose

هل احتجت يوماً إلى تحويل **صورة إيصال إلى نص** لكن جميع الأحرف سيريالية؟ لست الوحيد الذي يحاول حل هذه المشكلة. في العديد من تطبيقات التجزئة أو المحاسبة، تأتي الإيصالات باللغات الروسية أو البلغارية أو الصربية، وما زلت تريد نصًا نظيفًا وقابلًا للبحث.  

في هذا الدرس سنوضح لك بالضبط كيف **استخراج النص السيريالي** من صورة إيصال، **تحميل الصورة لـ OCR**، و**التعرف على الأحرف السيريالية** باستخدام مكتبة Aspose OCR. في النهاية ستحصل على برنامج C# جاهز للتنفيذ يكتب نتيجة OCR إلى ملف `.txt`.

## ما ستحتاجه

- **.NET 6** (أو أي إصدار حديث من .NET) – الكود يعمل أيضاً على .NET Framework 4.7+ .  
- حزمة **Aspose.OCR for .NET** عبر NuGet – `Install-Package Aspose.OCR`.  
- صورة إيصال نموذجية تحتوي على نص سيريالي (مثال: `cyrillic_receipt.jpg`).  
- بيئة تطوير – Visual Studio أو VS Code أو Rider ستفي بالغرض.  

لا توجد تبعيات أصلية إضافية مطلوبة؛ فـ Aspose يضم نماذج اللغة ويتولى المعالجة الداخلية.

## تحويل صورة الإيصال إلى نص – إعداد محرك OCR

أول شيء علينا فعله هو **إنشاء مثيل محرك OCR** وتحديد اللغة التي نهتم بها. Aspose يجعل ذلك بسيطًا:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;   // language and resource handling
using System.Drawing;      // Image class
using System.IO;

class CyrillicDemo
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Tell Aspose we want Cyrillic support
        ocrEngine.Language = Language.Cyrillic;

        // Optional: Pre‑load the model if you’ll run offline later
        // ResourceManager.Preload(Language.Cyrillic);
```

> **نصيحة احترافية:** تحميل النموذج مسبقًا يتجنب استدعاء الشبكة في المرة الأولى التي تشغّل فيها البرنامج، وهو مفيد لسيناريوهات سطح المكتب أو الأجهزة المدمجة.

## كيفية استخراج النص السيريالي – تحميل صورة الإيصال

الآن بعد أن أصبح المحرك جاهزًا، نحتاج إلى **تحميل الصورة لـ OCR**. فئة `System.Drawing.Image` تعمل بشكل مثالي لمعظم صيغ البت ماب.

```csharp
        // Step 3: Point to your receipt image
        string imagePath = @"YOUR_DIRECTORY\cyrillic_receipt.jpg";

        // Step 4: Load the image inside a using block (ensures disposal)
        using (var image = Image.FromFile(imagePath))
        {
            // Step 5: Run the OCR process
            var recognitionResult = ocrEngine.Recognize(image);
```

إذا لم يُعثر على الملف، فإن `Image.FromFile` يرمي استثناء `FileNotFoundException`. قد ترغب في تغليف الكود بالكامل بكتلة `try…catch` للبيئات الإنتاجية.

## التعرف على الأحرف السيريالية – استخراج النص

كائن `recognitionResult` يحتوي على النص الخام، درجات الثقة، وحتى حدود الصناديق إذا احتجت إليها لاحقًا. لتحويل بسيط من **صورة إيصال إلى نص** نكتب خاصية `Text` إلى ملف:

```csharp
            // Step 6: Write the extracted text to a .txt file
            string outputPath = @"YOUR_DIRECTORY\cyrillic.txt";
            File.WriteAllText(outputPath, recognitionResult.Text);

            // Quick verification: print to console
            Console.WriteLine("OCR completed. Extracted text:");
            Console.WriteLine(recognitionResult.Text);
        }
    }
}
```

عند تشغيل البرنامج، يجب أن ترى شيئًا مشابهًا لـ:

```
OCR completed. Extracted text:
СЧЕТ № 12345
Дата: 01/04/2026
Товар      Кол-во   Цена
Хлеб       2        30,00
Молоко     1        45,00
Итого:               105,00
```

هذا هو نتيجة **تحويل صورة الإيصال إلى نص** التي كنت تبحث عنها.

![مثال على تحويل صورة إيصال إلى نص](receipt-ocr-example.png "مثال على تحويل صورة إيصال إلى نص")

*نص بديل للصورة: تحويل صورة إيصال إلى نص يُظهر الأحرف السيريالية المستخرجة بواسطة Aspose OCR.*

## حالات الحافة والأسئلة الشائعة

### ماذا لو لم يتم تنزيل نموذج اللغة بعد؟

يقوم Aspose بتنزيل النموذج المطلوب تلقائيًا في المرة الأولى التي تحدد فيها `ocrEngine.Language = Language.Cyrillic;`. إذا لم يتوفر اتصال بالإنترنت، سيفشل خطوة التحميل الاختيارية. في هذه الحالة، إما أن تزود النموذج يدويًا (انظر توثيق Aspose) أو تتأكد من أن الجهاز يستطيع الوصول إلى `download.aspose.com`.

### كيف أتعامل مع عدة لغات في نفس الإيصال؟

يمكنك تمرير قائمة مفصولة بفواصل:

```csharp
ocrEngine.Language = Language.Cyrillic | Language.English;
```

سيحاول Aspose التعرف على الأحرف من كلا المجموعتين.

### إيصالتي غير واضحة – هل يمكن تحسين الدقة؟

يوفر Aspose OCR معالجة مسبقة أساسية للصور:

```csharp
ocrEngine.ImagePreprocessor = new ImagePreprocessor
{
    Sharpen = true,
    Binarize = true,
    Denoise = true
};
```

طبق هذا قبل استدعاء `Recognize`.

### ماذا عن المعالجة الدفعية الكبيرة؟

غلف حلقة التعرف داخل `Parallel.ForEach` وأعد استخدام نفس مثيل `OcrEngine` (يصبح آمنًا للمتعدد الخيوط بعد تحميل النموذج). فقط تذكّر قفل المحرك إذا واجهت مشاكل في سلامة الخيوط.

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي البرنامج الكامل جاهز للنسخ واللصق، يتضمن التحميل المسبق الاختياري ومعالجة الأخطاء الأساسية:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Drawing;
using System.IO;

class CyrillicDemo
{
    static void Main()
    {
        try
        {
            // Create OCR engine and select Cyrillic language
            var ocrEngine = new OcrEngine();
            ocrEngine.Language = Language.Cyrillic;

            // Optional: preload model for offline use
            // ResourceManager.Preload(Language.Cyrillic);

            // Path to the receipt image
            string imagePath = @"YOUR_DIRECTORY\cyrillic_receipt.jpg";

            // Verify the file exists
            if (!File.Exists(imagePath))
                throw new FileNotFoundException("Receipt image not found.", imagePath);

            using (var image = Image.FromFile(imagePath))
            {
                // Perform OCR
                var result = ocrEngine.Recognize(image);

                // Output path for extracted text
                string outputPath = @"YOUR_DIRECTORY\cyrillic.txt";
                File.WriteAllText(outputPath, result.Text);

                Console.WriteLine("✅ receipt image to text conversion succeeded.");
                Console.WriteLine("Extracted text saved to: " + outputPath);
                Console.WriteLine("\n--- Extracted Text ---\n");
                Console.WriteLine(result.Text);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine("❌ An error occurred: " + ex.Message);
        }
    }
}
```

شغّل البرنامج (`dotnet run` من مجلد المشروع) وستحصل على ملف `.txt` يحتوي على ناتج **تحويل صورة الإيصال إلى نص**.

## الخلاصة

الآن لديك حل شامل من البداية إلى النهاية لتحويل **صورة إيصال إلى نص**—وبشكل خاص للخطوط السيريالية—باستخدام Aspose OCR. غطّينا كيفية **إنشاء محرك OCR**، **تحميل الصورة لـ OCR**، **استخراج النص السيريالي**، و**التعرف على الأحرف السيريالية** ببضع أسطر من C#.  

الخطوات التالية؟ جرّب معالجة مجلد من الإيصالات، جرب `ImagePreprocessor` لتحسين الدقة، أو دمج ناتج OCR مع قاعدة بيانات لأتمتة المحاسبة. إذا احتجت إلى التعامل مع أبجديات أخرى، استبدل `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}