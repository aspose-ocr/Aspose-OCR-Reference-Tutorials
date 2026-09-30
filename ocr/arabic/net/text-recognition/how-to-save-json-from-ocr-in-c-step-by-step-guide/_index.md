---
category: general
date: 2026-02-19
description: كيفية حفظ JSON من مخرجات OCR في C# – تعلم استخراج النص من الصورة، كتابة
  ملف JSON في C#، وتحويل الصورة إلى JSON باستخدام Aspose OCR.
draft: false
keywords:
- how to save json
- extract text from image
- write json file c#
- convert image to json
- c# ocr tutorial
language: ar
og_description: كيفية حفظ JSON من نتائج OCR في C# سهل. اتبع هذا الدرس لاستخراج النص
  من الصورة وكتابة ملف JSON بأسلوب C#.
og_title: كيفية حفظ JSON من OCR في C# – دليل شامل
tags:
- C#
- OCR
- JSON
title: كيفية حفظ JSON من OCR في C# – دليل خطوة بخطوة
url: /ar/net/text-recognition/how-to-save-json-from-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حفظ JSON من OCR في C# – دليل كامل

كيفية حفظ json من نتائج OCR في C# هي حاجة شائعة عندما تقوم بتحويل المستندات الممسوحة ضوئياً إلى بيانات منظمة. في هذا الدليل ستتعرف بالضبط على كيفية استخراج النص من الصورة، تحويله إلى json، وأخيراً كتابة ملف json بأسلوب C# — بدون إطالة، مجرد حل عملي.

هل حاولت قراءة إيصال باستخدام الماسح الضوئي، فقط لتجد صورة غير واضحة لا يمكنك البحث فيها؟ هذه هي المشكلة التي يواجهها العديد من المطورين عندما يحتاجون لاستخراج البيانات من الصور. بنهاية هذه المقالة ستحصل على تطبيق console صغير يقرأ صورة، يستخرج النص باستخدام Aspose OCR، ويحفظ ملف json نظيف يمكنك إرساله إلى أي خدمة لاحقة.

سنغطي كل شيء: حزمة NuGet التي تحتاجها، الكود الدقيق (كامل، قابل للتنفيذ، ومُعلق بشكل مكثف)، المشكلات الشائعة، وطريقة سريعة للتحقق من النتيجة. لا تحتاج إلى خبرة سابقة في OCR — فقط فهم أساسي لـ C# و .NET.

## المتطلبات المسبقة

- .NET 6 SDK أو أحدث (الكود يستهدف .NET 6 لكنه يعمل على .NET 5+)
- Visual Studio 2022، VS Code، أو أي محرر تفضله
- ملف صورة (`input.png`) تريد معالجته
- اتصال بالإنترنت لجلب حزمة **Aspose.OCR** NuGet

إذا كان أي منها مفقودًا، احصل عليه الآن؛ وإلا ستضيع وقتًا لاحقًا.  

> **نصيحة احترافية:** Aspose OCR يقدم مفتاح تجربة مجانية — مثالي للتجربة دون الحاجة إلى ترخيص.

## الخطوة 1: تثبيت حزمة Aspose OCR NuGet

أولاً، أضف المكتبة التي تقوم بالعمل الشاق. افتح طرفية في مجلد مشروعك وشغّل:

```bash
dotnet add package Aspose.OCR
```

هذا الأمر الواحد يقوم بتحميل أحدث ملفات Aspose OCR الثنائية ويضيف إشارة إلى ملف `.csproj` الخاص بك.  

> **لماذا هذه الخطوة مهمة:** بدون الحزمة، لا توجد فئة `OcrEngine`، وستواجه أخطاء تجميع.  

الآن بعد أن تم تثبيت الحزمة، لننشئ هيكل تطبيق console الخاص بنا.

## الخطوة 2: إعداد بنية المشروع

أنشئ مشروع console جديد إذا لم تقم بذلك بالفعل:

```bash
dotnet new console -n JsonExportOcr
cd JsonExportOcr
```

داخل `Program.cs` استبدل المحتوى الافتراضي بالمثال الكامل أدناه. سنستعرض كل سطر لاحقًا، لكن وجود الملف جاهز يساعدك على النسخ واللصق دون فقدان أي قوس.

## الخطوة 3: تهيئة محرك OCR (استخراج النص من الصورة)

السطر الحقيقي الأول من الكود ينشئ محرك OCR ويخبره بالبحث عن الأحرف الإنجليزية. يمكنك التبديل إلى `Language.Spanish` أو أي لغة مدعومة أخرى، لكن الإنجليزية هي الحالة الأكثر شيوعًا.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;
using System.IO;

class JsonExport
{
    static void Main()
    {
        // Step 3.1: Create an OCR engine and set the language to English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // Step 3.2: Recognize text from the input image
        // Replace the path with where your image actually lives
        string inputPath = @"YOUR_DIRECTORY/input.png";
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);
```

**ماذا يحدث؟**  
- `OcrEngine` هو نقطة الدخول لـ Aspose OCR.  
- تعيين `Language` يحسن الدقة لأن المحرك يمكنه تطبيق خوارزميات خاصة باللغة.  
- `RecognizeImage` تُعيد كائن `OcrResult` الذي يحتوي على جميع الكلمات المعترف بها، درجات الثقة، ومربعات الإحاطة.

إذا كانت الصورة مفقودة أو تالفة، فإن شرط الحماية يطبع رسالة ودية ويتوقف — هذا الفحص الصغير يحفظك من مرجع null محير لاحقًا.

## الخطوة 4: تحويل نتيجة OCR إلى JSON (تحويل الصورة إلى JSON)

Aspose OCR يأتي بمساعد يُدعى `JsonResultWriter`. يقوم بتسلسل `OcrResult` إلى سلسلة JSON نظيفة تعكس البنية التي تتوقعها من واجهة REST API.

```csharp
        // Step 4: Convert the OCR result to a JSON string
        string jsonResult = JsonResultWriter.Write(ocrResult);
```

**لماذا نستخدم `JsonResultWriter`؟**  
- يتعامل تلقائيًا مع الكائنات المعقدة (مثل مجموعات `Word` المتداخلة).  
- تتجنب كتابة محولك الخاص، الذي قد يغفل حقول دقيقة مثل نسب الثقة.

في هذه المرحلة `jsonResult` يبدو تقريبًا هكذا (منسق للقراءة):

```json
{
  "PageCount": 1,
  "Pages": [
    {
      "PageNumber": 1,
      "Words": [
        {
          "Text": "Hello",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 50, "Height": 15 }
        },
        // … more words …
      ]
    }
  ]
}
```

يمكنك نسخ هذا المقتطف إلى عارض JSON لاستكشاف البنية.  

> **حالة حافة:** إذا كانت صورتك تحتوي على صفحات متعددة، سيشمل JSON مصفوفة `Pages` — تأكد من أن المستهلكين اللاحقين يمكنهم التعامل معها.

## الخطوة 5: كتابة JSON إلى القرص (كيفية حفظ JSON)

الآن يأتي جوهر الدرس: **كيفية حفظ json** إلى ملف على القرص. فئة .NET `File` تجعل ذلك سطرًا واحدًا، لكننا سنضيف قليلًا من معالجة الأخطاء للمتانة.

```csharp
        // Step 5: Write the JSON string to an output file
        string outputPath = @"YOUR_DIRECTORY/output.json";
        try
        {
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"JSON saved to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to write JSON: {ex.Message}");
        }
```

هذه هي اللحظة التي تجيب فيها أخيرًا على سؤال *كيفية حفظ json* — يتم إنشاء الملف، أو استبداله إذا كان موجودًا مسبقًا، وستحصل على رسالة واضحة في console تؤكد النجاح.

## الخطوة 6: التحقق من النتيجة

بعد انتهاء البرنامج، افتح `output.json` في أي محرر (VS Code، Notepad++، أو حتى متصفح). يجب أن ترى تمثيل JSON منسق جيدًا لمخرجات OCR. إذا لاحظت مصفوفات `"Words": []` فارغة، تحقق مرة أخرى من جودة الصورة — OCR يواجه صعوبة مع التباين المنخفض أو الضوضاء الكبيرة.

يمكنك أيضًا تشغيل فحص سريع من سطر الأوامر:

```bash
dotnet run
```

يجب أن ترى:

```
JSON saved to YOUR_DIRECTORY/output.json
```

إذا حصلت على خطأ، سيخبرك console ما إذا كان ملف الإدخال مفقودًا أو فشلت عملية الكتابة.

## مثال كامل يعمل

فيما يلي البرنامج **الكامل** الذي يمكنك نسخه‑ولصقه في `Program.cs`. استبدل `YOUR_DIRECTORY` بالمجلد الذي يحتوي على `input.png`. لا تحتاج إلى ملفات أخرى.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;
using System.IO;

class JsonExport
{
    static void Main()
    {
        // Step 3: Initialize OCR engine (extract text from image)
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // Define file paths
        string inputPath = @"YOUR_DIRECTORY/input.png";
        string outputPath = @"YOUR_DIRECTORY/output.json";

        // Validate input image exists
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        // Recognize text
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Convert OCR result to JSON (convert image to json)
        string jsonResult = JsonResultWriter.Write(ocrResult);

        // Write JSON to disk (how to save json)
        try
        {
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"JSON saved to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to write JSON: {ex.Message}");
        }
    }
}
```

شغّل البرنامج، افتح الملف المُنشأ، وقد أتممت بنجاح **دروس OCR في C#** التي توضح **كيفية حفظ json** من صورة.

## المشكلات الشائعة والنصائح (كتابة ملف JSON في C#)

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **مصفوفة `Words` فارغة** | الصورة مظلمة جدًا أو بدقة منخفضة | معالجة مسبقة للصورة (زيادة التباين، استخدام DPI أعلى) |
| `File.WriteAllText` يطرح UnauthorizedAccessException | محاولة الكتابة إلى مجلد للقراءة فقط | اختر مجلدًا قابلًا للكتابة (مثلاً `%TEMP%` أو مجلد مشروعك) |
| حزمة NuGet مفقودة | نسيان `dotnet add package Aspose.OCR` | أعد تشغيل الأمر وأعد البناء |
| JSON في سطر واحد | `WriteAllText` يكتب السلسلة الخام بدون تنسيق | استخدم `JsonResultWriter.Write(ocrResult, true)` إذا كان هناك تحميل زائد، أو مرّر الناتج عبر `JsonSerializer` مع `WriteIndented = true` |

هذه الفحوصات السريعة تحافظ على سلاسة سير عمل **كتابة ملف json في C#** وتمنع لحظات “لم يحدث شيء” المخيفة.

## الخطوات التالية (استخراج النص من الصورة والمزيد)

الآن بعد أن عرفت **كيفية حفظ json**، قد ترغب في:

- **احفظ الـ

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}