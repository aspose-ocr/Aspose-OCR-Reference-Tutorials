---
category: general
date: 2026-03-29
description: كيفية استخدام OCR مع Aspose لاستخراج النص من ملفات PNG وتحويل الصور إلى
  نص. تعلم OCR غير المتزامن خطوة بخطوة في C#.
draft: false
keywords:
- how to use OCR
- extract text from png
- convert images to text
- extract text from images
language: ar
og_description: كيفية استخدام OCR مع Aspose في C# لاستخراج النص من ملفات PNG. يوضح
  هذا الدليل OCR غير المتزامن، والكود، والنصائح.
og_title: كيفية استخدام OCR في C# – استخراج النص من صور PNG
tags:
- OCR
- C#
- Aspose
title: كيفية استخدام OCR في C# – استخراج النص من صور PNG بسرعة
url: /ar/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-png-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في C# – استخراج النص من صور PNG بسرعة

هل تساءلت يوماً **كيف تستخدم OCR** لاستخراج النص من مجموعة من لقطات شاشة PNG؟ ربما لديك إيصالات ممسوحة ضوئياً، فواتير، أو نماذج واجهة مستخدم وتحتاج إلى تحويل النص إلى صيغة قابلة للبحث. الخبر السار؟ باستخدام Aspose.OCR يمكنك تحويل الصور إلى نص ببضع أسطر من كود C# غير متزامن.

في هذا الدرس سنوضح لك بالضبط كيفية استخراج النص من ملفات PNG، نشرح لماذا كل خطوة مهمة، ونزودك ببرنامج جاهز للتنفيذ يطبع النص المعترف به لكل صفحة. بنهاية الدرس ستكون قادراً على **استخراج النص من الصور** دون الحاجة للبحث في الوثائق.

## ما ستتعلمه

- تثبيت وإضافة مرجع حزمة Aspose.OCR عبر NuGet.  
- تهيئة محرك OCR وتحديد اللغة (الإنجليزية في هذا المثال).  
- تمرير مصفوفة من ملفات PNG إلى `RecognizeImagesAsync` للمعالجة السريعة غير المتزامنة.  
- التكرار عبر كائنات `OcrResult` وعرض السلاسل المستخرجة.  

لا خدمات خارجية، لا ردود نداء معقدة—فقط C# نظيف غير متزامن يعمل على .NET 6+.

---

## المتطلبات المسبقة

| المتطلب | السبب |
|-------------|--------|
| .NET 6 SDK (أو أحدث) | ميزات اللغة الحديثة مثل `async Main`. |
| Visual Studio 2022 أو VS Code | بيئة تطوير لتجميع وتشغيل الكود. |
| حزمة Aspose.OCR NuGet (`Aspose.OCR`) | توفر الفئة `OcrEngine` المستخدمة في المثال. |
| بعض صور PNG (`page1.png`, `page2.png`, …) | ملفات الإدخال لعملية OCR. |

إذا كان لديك مشروع .NET بالفعل، فقط نفّذ `dotnet add package Aspose.OCR`. وإلا أنشئ تطبيق console جديد بالأمر `dotnet new console -n OcrDemo`.

---

## الخطوة 1: تثبيت Aspose.OCR وإعداد المشروع

أولاً، أضف مكتبة OCR إلى مشروعك:

```bash
dotnet add package Aspose.OCR
```

لماذا هذا مهم: Aspose.OCR يجمع محرك OCR الأصلي، حزم اللغات، وواجهة برمجة تطبيقات بسيطة. بإضافتها عبر NuGet تضمن توافق الإصدارات والتحديثات التلقائية.

---

## الخطوة 2: تهيئة محرك OCR واختيار اللغة

المحرك يحتاج إلى معرفة اللغة التي يجب البحث عنها. الإنجليزية هي الأكثر شيوعاً، لكن يمكنك استبدالها بـ `Language.Spanish`، `Language.French`، إلخ.

```csharp
using Aspose.OCR;

// ...

// Step 2: Create the engine and set the language to English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // Change this if you need a different language
};
```

> **نصيحة احترافية:** احرص دائماً على تعيين اللغة صراحةً؛ تركها على الإعداد الافتراضي قد يقلل الدقة ويزيد زمن المعالجة.

---

## الخطوة 3: إعداد قائمة ملفات PNG

يمكنك تمرير ملف واحد أو مصفوفة. تمرير مصفوفة يسمح للمحرك بمعالجة الملفات دفعةً بشكل غير متزامن، وهو مثالي لعدد قليل من الصفحات.

```csharp
// Step 3: Define the image files you want to process
string[] imagePaths = { "page1.png", "page2.png", "page3.png" };
```

إذا كانت صورك موجودة في مجلد فرعي، ما عليك سوى إضافة المسار النسبي (`"images/page1.png"`). سيُظهر المحرك استثناء واضح `FileNotFoundException` إذا كان المسار خاطئاً—لذا تحقق من أسماء الملفات مرة أخرى.

---

## الخطوة 4: تشغيل OCR غير المتزامن على جميع الصور

طريقة `RecognizeImagesAsync` تُعيد مصفوفة من `OcrResult`. وبما أنها غير متزامنة، يبقى واجهتك (أو وحدة التحكم) مستجيبة بينما يعمل OCR في الخلفية.

```csharp
// Step 4: Perform async OCR on every image
OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);
```

**لماذا غير متزامن؟**  
إذا كنت تدمج OCR في واجهة ويب أو تطبيق سطح مكتب، لا تريد أن يتوقف الخيط أثناء فحص المحرك لكل بكسل. `await` يُعيد الخيط إلى مجموعة الخيوط، مما يحسّن القابلية للتوسع.

---

## الخطوة 5: عرض النص المستخرج لكل صفحة

الآن بعد أن حصلنا على النتائج، نمرّ عليها ونطبع النص المعترف به. الخاصية `Text` تحتوي على النص العادي، جاهز للمعالجة الإضافية (مثلاً حفظه في قاعدة بيانات).

```csharp
// Step 5: Output the recognized text for every page
for (int i = 0; i < ocrResults.Length; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

### النتيجة المتوقعة

افترض أن `page1.png` يحتوي على “Invoice #12345” و`page2.png` يحتوي على “Total: $89.99”، ستحصل على شيء مشابه لـ:

```
--- Page 1 ---
Invoice #12345
Date: 03/28/2026
--- Page 2 ---
Total: $89.99
Paid by: Credit Card
```

إذا فشل OCR في العثور على أي نص، ستكون الخاصية `Text` سلسلة فارغة—عالج هذه الحالة في الكود الإنتاجي بالتحقق من `string.IsNullOrWhiteSpace`.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل يمكنك نسخه‑ولصقه في `Program.cs`. يتضمن جميع توجيهات `using`، الدالة `Main` غير المتزامنة، وتعليقات توضح كل خطوة.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    // Async Main is supported from C# 7.1 onward
    static async Task Main()
    {
        // Step 1: Initialize the OCR engine and set the language to English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Step 2: Define the image files to be processed
        string[] imagePaths = { "page1.png", "page2.png", "page3.png" };

        // Step 3: Perform asynchronous OCR on all images
        OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);

        // Step 4: Output the recognized text for each page
        for (int i = 0; i < ocrResults.Length; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].Text);
        }
    }
}
```

احفظ الملف، ضع ملفات PNG بجوار الملف التنفيذي (أو عدّل المسارات)، ثم شغّله:

```bash
dotnet run
```

يجب أن ترى النص المستخرج يُطبع في وحدة التحكم، مؤكدًا أنك نجحت في **تحويل الصور إلى نص**.

---

## التعامل مع الحالات الشائعة

| الحالة | ما الذي يجب فعله |
|-----------|------------|
| **PNG منخفض الدقة** | زيادة `ocrEngine.ImageProcessingOptions.Dpi` قبل التعرف. |
| **لغات متعددة** | تعيين `ocrEngine.Language = Language.English | Language.Spanish;` (عملية OR بتية). |
| **دفعة كبيرة (مئات الملفات)** | المعالجة على دفعات (مثلاً 20 ملفًا لكل استدعاء `RecognizeImagesAsync`) لتجنب ارتفاع استهلاك الذاكرة. |
| **الحاجة إلى درجة الثقة** | استخدم `ocrResults[i].Confidence` (قيمة عائمة بين 0 و 1) لتصفية النتائج منخفضة الجودة. |

هذه التعديلات تجعل خط أنابيب OCR الخاص بك قويًا، خاصةً عندما تنتقل من نموذج تجريبي إلى بيئة إنتاج.

---

## مكافأة: حفظ النتائج في ملف نصي

إذا كنت تفضّل نسخة دائمة بدلاً من الإخراج على الشاشة، أضف أداة مساعدة صغيرة:

```csharp
using System.IO;

// After the for‑loop:
File.WriteAllLines("OcrOutput.txt", ocrResults.Select(r => r.Text));
Console.WriteLine("All pages saved to OcrOutput.txt");
```

الآن لديك ملف واحد **يستخرج النص من الصور** للمعالجة اللاحقة—مثالي للفهرسة، البحث، أو إمداده إلى نموذج لغة.

---

## الخلاصة

استعرضنا **كيفية استخدام OCR** في C# مع Aspose **لاستخراج النص من ملفات PNG** و**تحويل الصور إلى نص** بكفاءة. النهج غير المتزامن يضمن بقاء تطبيقك مستجيبًا، بينما تبقى الواجهة البرمجية بسيطة وسهلة الصيانة.

جرّبه مع مستنداتك الخاصة، جرّب لغات مختلفة، وربما ربط الناتج بفهرس بحث أو خدمة تلخيص. السماء هي الحد عندما يمكنك تحويل الصور إلى سلاسل قابلة للبحث بثقة.

---

### الخطوات التالية والمواضيع ذات الصلة

- **استخراج النص من الصور** بصيغ أخرى (JPEG, TIFF) – فقط غيّر امتداد الملف.  
- **معالجة دفعات باستخدام Parallel.ForEach** لأحمال عمل ضخمة.  
- **تنظيف ما بعد OCR** باستخدام تعبيرات نمطية لتوحيد التواريخ، المبالغ، أو المعرفات.  
- **دمج مع Azure Cognitive Services** إذا احتجت OCR سحابي بميزات إضافية.  

لا تتردد في ترك تعليق إذا واجهت أي صعوبة، أو مشاركة كيفية توسيعك لهذا التدفق الأساسي. برمجة سعيدة!   ![OCR result screenshot showing extracted text](/images/ocr-result.png){.align-center alt="نتيجة مثال استخدام OCR"} 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}