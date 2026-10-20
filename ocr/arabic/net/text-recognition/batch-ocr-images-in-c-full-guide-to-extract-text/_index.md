---
category: general
date: 2026-02-24
description: قم بمعالجة صور OCR دفعةً واحدةً بسرعة باستخدام Aspose.OCR في C#. تعلّم
  كيفية قراءة الملفات من المجلد، والتعرف على النص من الصورة، وتحويل الصورة إلى نص
  في بضع خطوات.
draft: false
keywords:
- batch OCR images
- extract text from images
- read files from directory
- recognize text from image
- convert image to text
language: ar
og_description: معالجة صور OCR دفعيًا في C# باستخدام Aspose.OCR. يوضح هذا الدرس كيفية
  قراءة الملفات من الدليل، والتعرف على النص من الصورة، وتحويل الصورة إلى نص بكفاءة.
og_title: معالجة صور OCR دفعيًا في C# – دليل خطوة بخطوة كامل
tags:
- C#
- OCR
- Aspose
title: معالجة صور OCR دفعيًا في C# – دليل كامل لاستخراج النص
url: /ar/net/text-recognition/batch-ocr-images-in-c-full-guide-to-extract-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# معالجة دفعة صور OCR في C# – دليل كامل لاستخراج النص

هل احتجت يوماً إلى **batch OCR images** لكن لم تكن متأكدًا من أين تبدأ؟ أنت لست وحدك—العديد من المطورين يواجهون نفس المشكلة عندما يحاولون لأول مرة **extract text from images** على نطاق واسع. الخبر السار هو أنه ببضع أسطر من C# و Aspose.OCR يمكنك تحويل مجلد مليء بالصور إلى ملفات `.txt` مرتبة في وقت قصير.

في هذا البرنامج التعليمي سنستعرض العملية بالكامل: قراءة الملفات من دليل، إمداد كل صورة إلى محرك OCR، وأخيرًا **convert image to text** ملفات يمكنك فهرستها، البحث فيها، أو تمريرها إلى خطوط معالجة لاحقة. في النهاية ستحصل على تطبيق console مستقل يمكنك إدراجه في أي حل .NET.

## ما ستحتاجه

- **.NET 6+** (العينة تُجمع باستخدام .NET 6، لكن أي نسخة حديثة تعمل)
- **Aspose.OCR** حزمة NuGet (`Install-Package Aspose.OCR`)
- مجلد يحتوي على ملفات الصور (`.png`, `.jpg`, إلخ) التي تريد معالجتها
- Visual Studio، Rider، أو محرّكك المفضّل

لا ملفات إعداد إضافية، ولا خدمات خارجية—فقط كود C# نقي يعمل محليًا.

## معالجة دفعة صور OCR – إعداد المشروع

أولاً، أنشئ مشروع console جديد:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

### قراءة الملفات من الدليل

نحتاج إلى إخبار تطبيقنا بمكان وجود صور المصدر وأين يجب وضع ملفات النص الناتجة. استخدام `System.IO` يجعل ذلك سهلًا.

```csharp
using System;
using System.IO;
using Aspose.OCR;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Define input and output folders
        string inputFolder  = @"C:\Images\ToProcess";   // <-- change to your source folder
        string outputFolder = @"C:\Images\OcrResults"; // <-- change to your target folder

        // 2️⃣ Ensure the output folder exists
        Directory.CreateDirectory(outputFolder);
```

> **Why this step matters:** إذا لم يكن دليل الإخراج موجودًا سيتسبب البرنامج في رمي استثناء عندما يحاول كتابة ملف `.txt`. `CreateDirectory` متعادل—لا يفعل شيئًا إذا كان المجلد موجودًا بالفعل، لذا من الآمن استدعاؤه في كل تشغيل.

### التعرف على النص من الصورة وتحويل الصورة إلى نص

الآن نقوم بتشغيل محرك OCR ونتجول عبر كل ملف وجدناه. الحلقة تستخدم `Directory.GetFiles` مع حرف البدل (`*.*`) لذا تلتقط *كل* الملفات، لكن يمكنك تضييق الفلتر إلى `*.png` أو `*.jpg` إذا رغبت.

```csharp
        // 3️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 4️⃣ Process each image file in the input folder
        foreach (var imagePath in Directory.GetFiles(inputFolder, "*.*", SearchOption.TopDirectoryOnly))
        {
            // 5️⃣ Recognise text from the current image
            var ocrResult = ocrEngine.RecognizeImage(imagePath);

            // 6️⃣ Save the recognised text to a .txt file in the output folder
            string textFilePath = Path.Combine(
                outputFolder,
                Path.GetFileNameWithoutExtension(imagePath) + ".txt");

            File.WriteAllText(textFilePath, ocrResult.Text);
        }

        Console.WriteLine("✅ All images processed. Check the output folder!");
    }
}
```

**What’s happening here?**  
- `ocrEngine.RecognizeImage(imagePath)` يقرأ الـ bitmap، يشغّل خوارزمية OCR، ويعيد كائن `OcrResult`.  
- `ocrResult.Text` يحتوي على تمثيل النص العادي لكل ما استطاع المحرك قراءته.  
- `File.WriteAllText` ينشئ ملفًا جديدًا (أو يكتب فوق ملف موجود) بالنص المستخرج.

هذه هي كامل خط أنابيب **batch OCR images** في أقل من 30 سطرًا من الكود.

## نصائح احترافية وحالات خاصة

| الحالة | التوصية |
|-----------|----------------|
| الصور كبيرة ( > 5 ميغابايت ) | قُم بتصغيرها إلى عرض ~1500 بكسل لتسريع التعرف دون فقدان الدقة. |
| تحتاج إلى دعم ملفات PDF | حوّل كل صفحة PDF إلى صورة أولاً (مثلاً باستخدام `Aspose.PDF`) ثم مرّرها إلى نفس الحلقة. |
| بعض الملفات ليست صورًا (مثلًا `.txt`) | أضف فلترًا بسيطًا: `if (!imagePath.EndsWith(".png") && !imagePath.EndsWith(".jpg")) continue;` |
| تريد دعمًا متعدد اللغات | عيّن `ocrEngine.Language = Language.English | Language.Spanish;` قبل الحلقة. |
| تحتاج إلى تقارير التقدم | اكتب `Console.WriteLine($"Processing {Path.GetFileName(imagePath)}...");` داخل حلقة foreach. |

> **Pro tip:** غلف استدعاء OCR داخل `try/catch`. أحيانًا قد تتسبب صورة تالفة في رمي `RecognizeImage` استثناء؛ معالجتها يمنع توقف الدفعة بأكملها.

## النتيجة المتوقعة

بعد انتهاء البرنامج، سيحتوي `outputFolder` على ملف `.txt` لكل صورة أصلية:

```
C:\Images\OcrResults\invoice1.txt
C:\Images\OcrResults\receipt_2024-01-15.txt
C:\Images\OcrResults\signage.png.txt   <-- note the .txt extension
```

كل ملف يحتوي على النص الخام الذي استخرجه المحرك، على سبيل المثال:

```
Invoice #12345
Date: 01/15/2024
Total: $1,250.00
Thank you for your business!
```

يمكنك الآن تمرير هذه الملفات إلى فهرس بحث، تشغيل تحليل المشاعر، أو ببساطة أرشفتها للامتثال.

## الأسئلة المتكررة

**س: هل يعمل هذا على Linux؟**  
ج: بالتأكيد. Aspose.OCR متعدد المنصات، وواجهات برمجة تطبيقات `System.IO` المستخدمة هنا لا تعتمد على نظام التشغيل. فقط عدّل مسارات المجلد (`/home/user/images`).

**س: ماذا لو احتجت إلى **read files from directory** بشكل متكرر؟**  
ج: غيّر `SearchOption.TopDirectoryOnly` إلى `SearchOption.AllDirectories`. احرص على مراعاة مشكلات الأذونات في المجلدات العميقة.

**س: ما مدى دقة OCR؟**  
ج: الدقة تعتمد على جودة الصورة، الخط، واللغة. للحصول على أفضل النتائج، استخدم مسحات عالية الدقة وخلفيات نظيفة. يمكنك أيضًا تعديل `ocrEngine.Config` لتمكين تصحيح الانحراف أو تقليل الضوضاء.

## الخلاصة

لقد تعلمت الآن كيفية **batch OCR images** في C# باستخدام Aspose.OCR، من قراءة الملفات من دليل إلى **recognize text from image** وأخيرًا **convert image to text** ملفات يمكنك تخزينها أو معالجتها لاحقًا. المثال الكامل القابل للتنفيذ أعلاه يجب أن يعمل مباشرة، وقسم النصائح يمنحك خارطة طريق لتوسيع أو تخصيص الحل.

ما الخطوات التالية؟ جرّب إضافة واجهة مستخدم بسيطة باستخدام WinForms أو WPF، دمج الناتج مع Azure Cognitive Search، أو تجربة لغات أخرى يدعمها Aspose.OCR. السماء هي الحد عندما تتقن الحلقة الأساسية.

برمجة سعيدة، ولتكن دفعات OCR خالية من الأخطاء!  

![Diagram of batch OCR images process](batch-ocr-images-diagram.png "Batch OCR images workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}