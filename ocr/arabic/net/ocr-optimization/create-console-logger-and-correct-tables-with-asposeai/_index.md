---
category: general
date: 2025-12-27
description: إنشاء مسجل وحدة تحكم في C# وتمكين التحميل التلقائي إلى الجداول المصححة
  باستخدام AsposeAI. تعلم كيفية عرض مخرجات الجدول المصحح في بضع خطوات فقط.
draft: false
keywords:
- create console logger
- enable auto download
- how to correct tables
- setup console logger
- display corrected table
language: ar
og_description: إنشاء مسجل وحدة تحكم في C# وتمكين التحميل التلقائي إلى الجداول الصحيحة
  باستخدام AsposeAI. اتبع هذا الدليل لعرض ناتج الجدول المصحح بسرعة.
og_title: إنشاء مسجل وحدة التحكم وتصحيح الجداول باستخدام AsposeAI
tags:
- AsposeAI
- C#
- OCR
- Table processing
title: إنشاء مسجل وحدة التحكم وتصحيح الجداول باستخدام AsposeAI
url: /ar/net/ocr-optimization/create-console-logger-and-correct-tables-with-asposeai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مسجل وحدة التحكم وتصحيح الجداول باستخدام AsposeAI

هل احتجت يومًا إلى **إنشاء مسجل وحدة التحكم** لسلسلة معالجة AI بلغة C# لكن لم تكن متأكدًا من أين تبدأ؟ في هذا الدليل سنستعرض العملية بالكامل — كيفية إنشاء مسجل وحدة التحكم، تمكين التحميل التلقائي لملفات النماذج، وأخيرًا **كيفية تصحيح الجداول** التي خرجت من OCR. في النهاية ستتمكن من **عرض النتائج المصححة للجداول** في وحدة التحكم الخاصة بك باستخدام بضع أسطر من الشيفرة فقط.

سنغطي كل شيء من إعداد المسجل الأولي حتى التنظيف النهائي، لذا لن تحتاج إلى البحث عبر مستندات متفرقة. لا يلزم أي خبرة سابقة مع AsposeAI؛ ففهم أساسي لـ C# و .NET يكفي. على طول الطريق سنضيف نصائح حول **إعداد مسجل وحدة التحكم** وأفضل الممارسات، نتحدث عن الحالات الحدية، ونظهر لك كيف يجب أن يبدو المخرجات.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من توفر ما يلي:

- .NET 6.0 أو أحدث (الكود يستخدم ميزات لغة حديثة)
- Visual Studio 2022 أو أي بيئة تطوير تدعم مشاريع C#
- **Aspose.AI** حزمة NuGet مثبتة (`Install-Package Aspose.AI`)
- **Aspose.OCR** حزمة NuGet مثبتة (`Install-Package Aspose.OCR`)
- كائن نتيجة OCR تجريبي (`ocrResult`) من استدعاء Aspose.OCR سابق

إذا كان أيٌّ من هذه مفقودًا، توقف الآن واحصل عليه—ستشكر نفسك لاحقًا.

---

## الخطوة 1: إنشاء مسجل وحدة التحكم وتهيئة AsposeAI

الأول الذي نحتاجه هو مسجل يكتب مباشرةً إلى وحدة التحكم. هذا يجعل عملية تصحيح الأخطاء سهلة ويعطينا تغذية راجعة مباشرةً أثناء تشغيل محرك AI.

```csharp
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

// Step 1: Create a logger that writes to the console
ILogger consoleLogger = new ConsoleLogger();

// Step 2: Initialise the AsposeAI engine with the logger
AsposeAI asposeAI = new AsposeAI(consoleLogger);
```

**لماذا هذا مهم:**  
`ConsoleLogger` يطبق واجهة `ILogger`، لذا أي رسائل داخلية من AsposeAI (تحميل النموذج، حالة المعالج اللاحق، الأخطاء) تظهر فورًا في الطرفية الخاصة بك. إنها أبسط طريقة لـ **إعداد مسجل وحدة التحكم** دون الحاجة إلى أطر تسجيل خارجية.

> **نصيحة احترافية:** إذا احتجت لاحقًا إلى تسجيل إلى ملف، ما عليك سوى استبدال `ConsoleLogger` بمسجل مخصص يطبق `ILogger`—يبقى باقي الكود دون تعديل.

---

## الخطوة 2: تمكين التحميل التلقائي لنماذج AI

يمكن لـ AsposeAI جلب ملفات النموذج المطلوبة عند الحاجة. تشغيل هذا الخيار يوفر عليك تحميل ملفات ثنائية ضخمة يدويًا.

```csharp
// Step 3: (Optional) Configure automatic model download and set the model directory
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,               // <‑‑ enable auto download
    DirectoryModelPath = "YOUR_DIRECTORY"   // change to a writable folder
};
```

**ما الذي قد يخطئ؟**  
إذا كان `DirectoryModelPath` يشير إلى موقع للقراءة فقط، سيفشل التحميل التلقائي وستظهر استثناء في وحدة التحكم. تأكد من وجود المجلد وأن تطبيقك يملك صلاحيات الكتابة.

---

## الخطوة 3: إنشاء معالج ما بعد الجدول (كيفية تصحيح الجداول)

الجداول المستخرجة من OCR غالبًا ما تكون فوضوية—خلايا مدمجة، حدود مفقودة، أو نص غير محاذٍ. يمكن لـ `TableAIProcessor` من AsposeAI تنظيفها تلقائيًا.

```csharp
// Step 4: Create a table post‑processor that lets the engine decide when to run correction
TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);
```

**لماذا وضع AUTO؟**  
`AITableDetectionMode.AUTO` يسمح للمحرك بفحص مخرجات OCR وتحديد ما إذا كان التصحيح مطلوبًا. إذا كنت تفضّل التحكم اليدوي، يمكنك استخدام `MANUAL` واستدعاء `RunCorrection()` بنفسك.

---

## الخطوة 4: ربط المعالج وإعداده

الآن نجمع كل شيء معًا—المسجل، إعداد النموذج، ومعالج الجداول.

```csharp
// Step 5: Attach the post‑processor and its configuration to the AI engine
asposeAI.SetPostProcessor(tableProcessor, modelConfig);
```

في هذه المرحلة يعرف محرك AI *أين* يخزن النماذج، *كيف* يسجل، و*ما* هو المعالجة اللاحقة التي يجب تطبيقها. هذا فصل واضح للمهام يجعل التغييرات المستقبلية سهلة وغير مؤلمة.

---

## الخطوة 5: تشغيل المعالج على نتيجة OCR الخاصة بك

بافتراض أن لديك بالفعل `ocrResult` من Aspose.OCR، ما عليك سوى تمريره إلى المحرك.

```csharp
// Step 6: Run the post‑processor on the OCR result returned by Aspose.OCR
asposeAI.RunPostprocessor(ocrResult);
```

**تنبيه حالة حدية:**  
إذا كان `ocrResult` لا يحتوي على جداول، سيتخطى المعالج التصحيح بصمت. يمكنك التحقق من `tableProcessor.GetResult().Count` بعد ذلك للتأكد من أن شيئًا ما قد تم معالجته فعليًا.

---

## الخطوة 6: استرجاع و**عرض الجدول المصحح** في وحدة التحكم

أخيرًا، لنستخرج نص الجدول المنقح ونطبعه في وحدة التحكم.

```csharp
// Step 7: Retrieve and display the corrected table text
Console.WriteLine("Corrected table output:");
Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
```

سيظهر المخرجات شيئًا مثل هذا (حسب صورة المصدر):

```
Corrected table output:
| Item   | Quantity | Price |
|--------|----------|-------|
| Apple  | 10       | $1.20 |
| Banana | 5        | $0.80 |
```

إذا رأيت سلسلة فارغة، تحقق من أن OCR فعلاً اكتشف جدولًا وأن `AllowAutoDownload` نجح.

---

## الخطوة 7: تنظيف الموارد

المسؤولية الجيدة تعني تحرير الكائنات الثقيلة عند الانتهاء.

```csharp
// Step 8: Release resources used by the AI engine
asposeAI.Dispose();
```

تجاوز هذه الخطوة قد يترك مقبض ملفات مفتوحًا، خاصةً على Windows حيث تبقى ملفات النموذج مقفلة.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع وحدة تحكم جديد. استبدل `"YOUR_DIRECTORY"` بمسار حقيقي وتأكد من أن `ocrResult` مُعبأ قبل استدعاء `RunPostprocessor`.

```csharp
using System;
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

namespace AsposeAITableCorrection
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a console logger
            ILogger consoleLogger = new ConsoleLogger();

            // 2️⃣ Initialise AsposeAI with the logger
            AsposeAI asposeAI = new AsposeAI(consoleLogger);

            // 3️⃣ Configure auto‑download (optional but recommended)
            AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
            {
                AllowAutoDownload = true,
                DirectoryModelPath = @"C:\AsposeModels" // <-- change this
            };

            // 4️⃣ Create the table processor (auto‑detect mode)
            TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);

            // 5️⃣ Attach processor and config
            asposeAI.SetPostProcessor(tableProcessor, modelConfig);

            // 6️⃣ Obtain OCR result (replace with your own OCR call)
            // Example placeholder – you should have this from Aspose.OCR already
            OcrResult ocrResult = GetOcrResultSomehow();

            // 7️⃣ Run post‑processor on the OCR output
            asposeAI.RunPostprocessor(ocrResult);

            // 8️⃣ Display corrected table
            Console.WriteLine("Corrected table output:");
            if (tableProcessor.GetResult().Count > 0)
            {
                Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
            }
            else
            {
                Console.WriteLine("No tables were detected or corrected.");
            }

            // 9️⃣ Clean up
            asposeAI.Dispose();
        }

        // Dummy method – replace with your actual OCR logic
        static OcrResult GetOcrResultSomehow()
        {
            // For illustration only
            OcrEngine engine = new OcrEngine();
            engine.Image = ImageStream.FromFile("sample-table.png");
            return engine.Recognize();
        }
    }
}
```

**المخرجات المتوقعة في وحدة التحكم** (باستخدام صورة جدول بسيطة):

```
Corrected table output:
| Name   | Age | City      |
|--------|-----|-----------|
| Alice  | 30  | New York  |
| Bob    | 25  | Seattle   |
```

---

## أسئلة شائعة وإجابات

- **هل أحتاج إلى اتصال إنترنت للتحميل التلقائي؟**  
  نعم. في المرة الأولى التي يُطلب فيها النموذج، يتواصل AsposeAI مع CDN الخاص به. بعد أن يُحفظ الملف في `DirectoryModelPath`، تصبح التشغيلات اللاحقة دون اتصال.

- **ماذا لو كان جدولي يحتوي على خلايا مدمجة؟**  
  يحاول نموذج AI تقسيم الخلايا المدمجة بناءً على الإشارات البصرية. إذا بدت النتيجة غير صحيحة، فكر في معالجة الصورة مسبقًا (زيادة التباين، تصحيح الدوران) قبل OCR.

- **هل يمكنني معالجة جداول متعددة في آن واحد؟**  
  بالتأكيد. `tableProcessor.GetResult()` يُعيد قائمة؛ يمكنك التكرار عليها لطباعة كل جدول.

- **هل `ConsoleLogger` آمن للاستخدام في بيئات متعددة الخيوط؟**  
  يكتب مباشرةً إلى `System.Console`، وهو آمن للكتابات البسيطة المتعددة الخيوط. في سيناريوهات متعددة الخيوط الثقيلة، قد يكون من الأفضل مسجل مخصص مع مزامنة.

---

## الخطوات التالية والمواضيع ذات الصلة

الآن بعد أن عرفت **كيفية تصحيح الجداول**، قد ترغب في:

- **تمكين التحميل التلقائي** لنماذج AsposeAI أخرى (مثل ترجمة اللغة).
- **إعداد مسجل وحدة التحكم** بمستويات سجل مختلفة (Info, Warning, Error) للتحكم الدقيق.
- استكشاف **عرض الجدول المصحح** في واجهة GUI (WinForms أو WPF) بدلاً من وحدة التحكم.
- دمج تصحيح الجداول مع **استخراج البيانات** لإدخالها مباشرةً إلى قاعدة بيانات.

كل هذه تبني على الأساس الذي وضعناه، لذا لا تتردد في التجربة.

---

## الخلاصة

لقد استعرضنا دورة الحياة الكاملة لـ **إنشاء مسجل وحدة التحكم**، تمكين التحميل التلقائي، و**تصحيح الجداول** باستخدام AsposeAI، وانتهينا بطريقة نظيفة ل**عرض الجداول المصححة**.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}