---
category: general
date: 2026-08-18
description: تعلم كيفية إنشاء مسجل وحدة تحكم في C# واستخدام Aspose AI لتصحيح نص OCR
  باستخدام معالج ما بعد التدقيق الإملائي.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create console logger
- correct ocr text
- spell check ocr
language: ar
lastmod: 2026-08-18
og_description: إنشاء مسجل وحدة تحكم في C# وتصحيح نص OCR باستخدام Aspose AI. اتبع
  هذا الدليل الكامل لإضافة معالج ما بعد التدقيق الإملائي إلى خط أنابيب OCR الخاص بك.
og_image_alt: Illustration of creating a console logger in C# code editor
og_title: إنشاء مسجل وحدة تحكم وتدقيق إملائي لنص OCR في C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-08-18'
  description: Learn how to create console logger in C# and use Aspose AI to correct
    OCR text with a spell‑check post‑processor.
  headline: How to create console logger and spell‑check OCR text in C#
  type: TechArticle
tags:
- C#
- OCR
- AI
- logging
title: كيفية إنشاء مسجل وحدة تحكم وتدقيق إملائي لنص OCR في C#
url: /ar/net/text-recognition/how-to-create-console-logger-and-spell-check-ocr-text-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء مسجل وحدة تحكم وتصحيح نص OCR باستخدام التدقيق الإملائي في C#

إذا كنت بحاجة إلى **إنشاء مسجل وحدة تحكم** لإخراج التشخيص أثناء معالجة المستندات الممسوحة ضوئياً، يوضح لك هذا الدليل حلاً كاملاً. بنهاية البرنامج التعليمي ستكون قادرًا على **تصحيح نص OCR** باستخدام معالج ما بعد التدقيق الإملائي المدمج عبر Aspose AI SDK.

غالبًا ما تترك نتائج OCR أخطاء إملائية تؤثر على التحليلات اللاحقة. إضافة خطوة التدقيق الإملائي تضمن أن النص نظيف وجاهز للفهرسة أو الترجمة أو استخراج البيانات. الأقسام التالية تقودك عبر كل جزء مطلوب، من إنشاء المسجل إلى التحقق النهائي.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 أو أحدث مثبت  
* Visual Studio 2022 (أو أي بيئة تطوير متكاملة تدعم C#)  
* حزمة NuGet الخاصة بـ Aspose.AI مضافة إلى مشروعك (`dotnet add package Aspose.AI`)  

لا توجد خدمات خارجية إضافية مطلوبة لأن نموذج Aspose AI يمكن تنزيله تلقائيًا.

## الخطوة 1: كيفية إنشاء مسجل وحدة تحكم للتشخيص

يقوم المسجل بالتقاط معلومات وقت التشغيل، مما يسهل استكشاف أخطاء تحميل النموذج أو تنفيذ معالج ما بعد المعالجة. تسمح واجهة `ILogger` بتبديل التنفيذات دون تعديل باقي الشيفرة.

```csharp
// Step 1: (Optional) Create a logger for diagnostic output
ILogger logger = new ConsoleLogger();   // set to null if logging is not needed
```

يكتب `ConsoleLogger` كل سجل إلى تدفق الإخراج القياسي. استخدام واجهة يبقي الشيفرة قابلة للاختبار ويسمح لك باستبدال المسجل بمسجل يعتمد على ملف أو سحابة لاحقًا.

## الخطوة 2: تكوين نموذج AI لتمكين التنزيل التلقائي

يمكن لـ Aspose AI تنزيل ملفات النموذج المطلوبة عند الحاجة. تحديد مجلد محلي يمنع حركة المرور المتكررة على الشبكة ويمنحك التحكم في التخزين.

```csharp
// Step 2: Configure the AI model – enable automatic download and specify a local folder
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,
    DirectoryModelPath = "YOUR_DIRECTORY"
};
```

`AllowAutoDownload` يضمن أن SDK يجلب النموذج في المرة الأولى التي يتم تشغيله فيها. `DirectoryModelPath` يشير إلى موقع دائم على جهازك، وهو مفيد لأنابيب CI.

## الخطوة 3: تهيئة محرك AsposeAI مع المسجل

تمرير المسجل إلى المحرك يربط إخراج التشخيص بكل عملية داخلية، بما في ذلك تحميل النموذج وتنفيذ معالج ما بعد المعالجة.

```csharp
// Step 3: Initialise the AsposeAI engine with the logger
AsposeAI ai = new AsposeAI(logger);
```

يقبل مُنشئ `AsposeAI` كائنًا من نوع `ILogger`. إذا قمت بتمرير `null` في الخطوة 1، سيعمل المحرك بصمت.

## الخطوة 4: إنشاء معالج ما بعد التدقيق الإملائي المدمج

يوفر Aspose AI مكوّن تدقيق إملائي جاهز يعمل مباشرة على نتائج OCR. إنشاءه لا يتطلب أي إعدادات.

```csharp
// Step 4: Create the built‑in spell‑check post‑processor
SpellCheckAIProcessor spellChecker = new SpellCheckAIProcessor();
```

`SpellCheckAIProcessor` يطبق واجهة `IAIProcessor`، مما يسمح بتسجيله جنبًا إلى جنب مع تكوين النموذج.

## الخطوة 5: تسجيل معالج التدقيق الإملائي مع تكوين النموذج

ربط المعالج بالمحرك يضمن أن نتائج OCR تمر عبر مرحلة التدقيق الإملائي تلقائيًا.

```csharp
// Step 5: Register the spell‑check processor together with the model configuration
ai.SetPostProcessor(spellChecker, modelConfig);
```

`SetPostProcessor` يربط `spellChecker` بـ `modelConfig`. عندما تستدعي لاحقًا `RunPostprocessor`، سيقوم المحرك بتشغيل منطق التدقيق الإملائي باستخدام النموذج الذي تم تنزيله.

## الخطوة 6: تنفيذ معالج ما بعد المعالجة على نتائج OCR التي تم الحصول عليها مسبقًا

بافتراض أن لديك مخرجات OCR مخزنة في المتغيّر `ocrResult`، استدعِ معالج ما بعد المعالجة للحصول على النص المصحح.

```csharp
// Step 6: Execute the post‑processor on previously obtained OCR results (variable `ocrResult`)
ai.RunPostprocessor(ocrResult);
```

`RunPostprocessor` يعالج كل صفحة من `ocrResult`. يحلل خوارزمية التدقيق الإملائي سلاسل التعرف، ويطبق القواميس الخاصة باللغة، وينتج نسخة مصححة.

## الخطوة 7: استرجاع وعرض النص المصحح

بعد المعالجة، يحتفظ `SpellCheckAIProcessor` بالنتائج المنقحة. يمكنك جلبها وإخراجها إلى وحدة التحكم.

```csharp
// Step 7: Retrieve and display the corrected text
Console.WriteLine("CORRECTED RESULT\n");
Console.WriteLine(spellChecker.GetResult()[0].RecognitionText);
```

العنصر الأول في `GetResult()` يتCorrespond إلى الصفحة الأولى من مستند OCR. إذا عالجت ملفًا متعدد الصفحات، كرّر عبر المجموعة لعرض النص المصحح لكل صفحة.

## الخطوة 8: تنظيف الموارد عند الانتهاء

إطلاق سراح كائن `AsposeAI` يحرر الموارد غير المُدارة ويغلق أي مقبض ملف مفتوح.

```csharp
// Clean up resources when finished
ai.Dispose();
```

استدعاء `Dispose` هو ممارسة جيدة لأي كائن يطبق `IDisposable`، خاصة عند العمل مع مكتبات أصلية.

## النتيجة المتوقعة

عند تشغيل البرنامج بنجاح، سترى مخرجات مشابهة لما يلي:

```
CORRECTED RESULT

The quick brown fox jumps over the lazy dog.
```

النص أعلاه يعكس الإدخال الأصلي لـ OCR مع تصحيح الأخطاء الإملائية بواسطة معالج ما بعد التدقيق الإملائي.

## الأسئلة الشائعة والحالات الخاصة

**ماذا لو كانت نتيجة OCR فارغة؟**  
يتعامل معالج ما بعد المعالجة بأناقة مع الصفحات الفارغة ويعيد سلسلة فارغة. لا يتم رمي استثناء.

**هل يمكنني استخدام قاموس مخصص؟**  
`SpellCheckAIProcessor` يقبل خاصية اختيارية `CustomDictionaryPath`. اضبطها قبل استدعاء `SetPostProcessor` إذا كنت تحتاج إلى مصطلحات خاصة بمجال معين.

**هل مسجل وحدة التحكم آمن للثريدات؟**  
`ConsoleLogger` يكتب إلى `Console.Out` الذي يتم مزامنته بواسطة وقت تشغيل .NET. للسيناريوهات ذات الإنتاجية العالية قد تستبدله بمسجل يجمع الرسائل في مخزن مؤقت.

**ماذا لو احتجت لمعالجة مستندات متعددة بشكل متزامن؟**  
أنشئ نسخة منفصلة من `AsposeAI` لكل خيط أو استخدم نمط مجموعة آمنة للثريدات. مشاركة نسخة واحدة قد تؤدي إلى حالات سباق لأن حالة النموذج الداخلية ليست محلية للثريد.

## الخلاصة

أنت الآن تعرف **كيفية إنشاء مسجل وحدة تحكم** في C# وتكامل **معالج تدقيق إملائي لنص OCR** لتصحيح **نص OCR**. يغطي سير العمل الكامل — من تهيئة المسجل عبر تكوين النموذج، المعالجة، والتنظيف — جميع الخطوات الأساسية لإنشاء خط أنابيب تصحيح OCR قوي.

بعد ذلك، فكر في توسيع هذا الخط بأن تضيف معالجات ما بعد أخرى مثل اكتشاف اللغة أو استخراج الكيانات. يمكنك أيضًا تجربة أطر تسجيل أخرى مثل Serilog لالتقاط بيانات تشخيصية أغنى. happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم استعراضها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Create Searchable PDF with Aspose OCR Batch Processing – C# Guide](/ocr/english/net/ocr-optimization/create-searchable-pdf-with-batch-ocr-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}