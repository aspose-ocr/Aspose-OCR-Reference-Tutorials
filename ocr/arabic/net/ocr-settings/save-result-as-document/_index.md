---
description: تعلم كيفية حفظ نتائج OCR باستخدام Aspose.OCR لـ .NET – تحويل الصورة إلى
  PDF، استخراج النص من PNG، وحفظ النص المعترف به إلى DOCX أو TXT أو PDF أو XLSX.
linktitle: How to Save OCR Result as Document
second_title: Aspose.OCR .NET API
title: كيفية حفظ نتيجة OCR كوثيقة
url: /ar/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حفظ نتيجة OCR كمستند

## المقدمة

في هذا الدرس ستكتشف **كيفية حفظ OCR** باستخدام Aspose.OCR لـ .NET. سنستعرض عملية التعرف على النص داخل صورة، ثم تحويل هذا النص إلى صيغ مستندات شائعة مثل DOCX، TXT، PDF، و XLSX. في النهاية، ستكون قادرًا على أتمتة استخراج البيانات من الصور وتخزينها كملفات قابلة للبحث والتحرير—مناسبة للأرشفة، وإعداد التقارير، أو المعالجة اللاحقة.

## إجابات سريعة
- **ماذا يعني “كيفية حفظ OCR”؟** يشير إلى حفظ النص المُستخرج من صورة في صيغة ملف مثل DOCX أو PDF وغيرها.  
- **ما الصيغ التي يمكنني التصدير إليها؟** DOCX، TXT، PDF، وXLSX مدعومة مباشرة.  
- **هل أحتاج إلى ترخيص؟** الإصدار التجريبي المجاني يكفي للتقييم؛ يتطلب الاستخدام الإنتاجي ترخيصًا تجاريًا.  
- **هل يمكنني تحويل الصورة إلى PDF مباشرة؟** نعم—احفظ نتيجة OCR كملف PDF للحصول على مستند PDF قابل للبحث.  
- **هل يدعم PNG؟** بالطبع؛ يمكنك **استخراج النص من صور PNG** باستخدام نفس الـ API.

## ما هو OCR ولماذا حفظ النتائج كمستندات؟

التعرف الضوئي على الأحرف (OCR) يحول النص المطبوع أو المكتوب يدويًا داخل الصور إلى سلاسل قابلة للقراءة آليًا. حفظ هذه السلاسل كمستندات يتيح لك:

* إنشاء ملفات PDF قابلة للبحث للامتثال.  
* ملء جداول البيانات (XLSX) لتحليل البيانات.  
* إنشاء تقارير قابلة للتحرير (DOCX).  
* أرشفة سجلات النص العادي (TXT) للبحث السريع.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- Aspose.OCR لـ .NET مثبت. يمكنك تنزيله **[هنا](https://releases.aspose.com/ocr/net/)**.  
- مجلد على جهازك سيحتوي على الصور المصدرية والمستندات الناتجة. حدّث المتغيّر `dataDir` في الشيفرة ليشير إلى هذا المجلد.

## استيراد مساحات الأسماء

نحتاج إلى بعض مساحات الأسماء في .NET للوصول إلى إدخال/إخراج الملفات وفئات Aspose OCR.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### الخطوة 1: تهيئة Aspose.OCR

حدد المسار إلى دليل العمل الخاص بك وأنشئ نسخة من محرك OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### الخطوة 2: التعرف على الصورة

مرّر ملف الصورة (مثل PNG) إلى أداة التعرف. هنا نقوم **بالتعرف على نص الصور** وتحويله إلى كائن `RecognitionResult`.

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### الخطوة 3: حفظ النتيجة بصيغ مختلفة

الآن نقوم بتصدير النص المُتعرف عليه. اختر الصيغة التي تناسب سير عملك—سواء كنت تحتاج إلى **تحويل الصورة إلى PDF**، **استخراج النص من PNG**، أو إنشاء جدول بيانات.

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### الخطوة 4: عرض رسالة النجاح

رسالة بسيطة في وحدة التحكم تؤكد أن العملية انتهت دون أخطاء.

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

##  ​  

## Common  



  



 



 



 



## المشكلات الشائعة والنصائح

- **مسارات الملفات:** استخدم دائمًا مسارات مطلقة أو تأكد من أن `dataDir` ينتهي بفاصل مسار (`\\` أو `/`).  
- **جودة الصورة:** الصور ذات الدقة العالية تحسن الدقة؛ فكر في المعالجة المسبقة (إزالة الميل، إزالة الضوضاء) للحصول على نتائج أفضل.  
- **وضع الترخيص:** في وضع التقييم قد يحتوي الناتج على علامة مائية؛ استخدم ترخيصًا صالحًا لإزالتها.

## الأسئلة المتكررة

**س1. هل Aspose.OCR متوافق مع صيغ صور مختلفة؟**  
نعم، Aspose.OCR يدعم مجموعة واسعة من صيغ الصور، مما يضمن مرونة في مهام OCR الخاصة بك.

**س2: هل يمكنني تخصيص إعدادات التعرف للحصول على دقة أفضل؟**  
بالطبع! Aspose.OCR يوفر `RecognitionSettings` لضبط عملية OCR بدقة وفقًا لمتطلباتك الخاصة.

**س3: هل هناك نسخة تجريبية مجانية متاحة؟**  
نعم، يمكنك البدء بنسخة تجريبية مجانية **[هنا](https://releases.aspose.com/)**.

**س4: كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.OCR؟**  
يمكن الحصول على تراخيص مؤقتة **[هنا](https://purchase.aspose.com/temporary-license/)**.

**س5: أين يمكنني طلب المساعدة أو التواصل مع المجتمع؟**  
انضم إلى مجتمع Aspose.OCR على **[منتدى Aspose](https://forum.aspose.com/c/ocr/16)** للحصول على الدعم والنقاشات.

---

**آخر تحديث:** 2026-02-12  
**تم الاختبار مع:** Aspose.OCR 24.11 لـ .NET  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}