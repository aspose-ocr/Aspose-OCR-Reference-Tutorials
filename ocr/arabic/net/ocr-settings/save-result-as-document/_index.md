---
date: 2025-12-27
description: تعلم كيفية استخدام Aspose.OCR لـ .NET لاستخراج النص من الصورة، والتعرف
  على النص في الصور، وتحويل الصورة إلى PDF .NET بتنسيقات مستندات مختلفة.
linktitle: Save Result as Document in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: تحويل الصورة إلى PDF .NET – حفظ النتيجة كوثيقة في التعرف الضوئي على الأحرف
  (OCR)
url: /ar/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل الصورة إلى PDF .NET – حفظ النتيجة كمستند في التعرف الضوئي على الأحرف (OCR)

## المقدمة

مرحبًا بك في عالم التعرف الضوئي على الأحرف (OCR) المثير مع Aspose.OCR لـ .NET! في هذا الدرس ستتعلم كيفية **تحويل الصورة إلى PDF .NET**، استخراج النص من الصورة، وحفظ مخرجات OCR في صيغ مستندات قابلة للبحث مثل PDF، DOCX، TXT، وExcel. سواء كنت بحاجة لإنشاء PDF قابل للبحث أو تصدير نتائج OCR إلى Excel، فإن الخطوات أدناه ستوجهك خلال العملية بسرعة وكفاءة.

## إجابات سريعة
- **ماذا يعني “image to pdf .net”؟** يشير إلى تحويل ملفات الصور إلى مستندات PDF باستخدام مكتبات .NET، وفي هذه الحالة Aspose.OCR.  
- **ما الصيغ التي يمكنني تصدير نتائج OCR إليها؟** تدعم الصيغ DOCX، TXT، PDF، وXLSX مباشرة.  
- **هل أحتاج إلى ترخيص للاستخدام في الإنتاج؟** نعم، يتطلب الاستخدام التجاري ترخيصًا تجاريًا؛ يتوفر إصدار تجريبي مجاني للتقييم.  
- **هل يمكنني استخراج نص قابل للبحث من PDF؟** بالتأكيد – الـ PDF المُولد هو **ocr to searchable pdf** يمكنك فهرسته.  
- **ما إصدارات .NET المدعومة؟** يعمل Aspose.OCR مع .NET Framework 4.5+، .NET Core 3.1+، و .NET 5/6+.  

## ما هو “image to pdf .net”؟
“Image to PDF .NET” هو عملية أخذ الصور النقطية (PNG، JPEG، TIFF، إلخ) وتحويلها برمجيًا إلى ملفات PDF باستخدام مكتبة .NET. لا يقتصر Aspose.OCR على تحويل الصورة فقط، بل يقوم أيضًا بعملية OCR، مما يتيح لك **التعرف على النص في الصور** وإدراج هذا النص في ملف PDF الناتج، مما يجعله قابلًا للبحث.

## لماذا نستخدم Aspose.OCR لهذه المهمة؟
- **دقة عالية** – محرك OCR متقدم يدعم لغات وخطوط متعددة.  
- **تحويل بخطوة واحدة** – يمكنك التعرف على النص وحفظه مباشرة إلى PDF، DOCX، TXT، أو Excel دون معالجة إضافية.  
- **بدون تبعيات خارجية** – مكتبة .NET صافية، لا تحتاج إلى ملفات تنفيذية أصلية.  
- **مرونة** – يمكنك بسهولة تغيير صيغة الإخراج لإنشاء مستند من OCR أو تصدير OCR إلى Excel للتحليل البياني.

## المتطلبات المسبقة

قبل الشروع في رحلة OCR، تأكد من توفر المتطلبات التالية:

- Aspose.OCR لـ .NET. تأكد من تثبيت مكتبة Aspose.OCR. يمكنك تنزيلها [هنا](https://releases.aspose.com/ocr/net/).

- دليل المستندات: احرص على وجود دليل مخصص لمستنداتك، وقم بتحديث المتغير `dataDir` في الشيفرة المقدمة وفقًا لذلك.

## استيراد المساحات الاسمية

ابدأ باستيراد المساحات الاسمية الضرورية. هذه هي اللبنات التي ستمكن شيفرتك من قدرات OCR.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

الآن، لنقسم المثال إلى عدة خطوات:

## كيفية تحويل الصورة إلى PDF .NET باستخدام Aspose.OCR

### الخطوة 1: تهيئة Aspose.OCR

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

هذه الخطوة تمهيدية لتفعيل واجهة برمجة تطبيقات Aspose.OCR.

### الخطوة 2: التعرف على الصورة

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

هنا نستخدم Aspose.OCR **للتعرف على النص داخل الصورة المحددة** (استبدل `"sample.png"` بملف الصورة الخاص بك). هذا هو المكان الذي يحدث فيه عملية **extract text from image**.

### الخطوة 3: حفظ النتيجة بصيغ مختلفة

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

خصص هذه الخطوة وفقًا لاحتياجاتك. يتيح لك Aspose.OCR **حفظ النص المعترف به بصيغ مستندات مختلفة مثل DOCX، TXT، PDF، وXLSX**، مما يحقق **إنشاء مستند من OCR** أو **تصدير OCR إلى Excel**.

### الخطوة 4: عرض رسالة النجاح

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

رسالة تأكيد بسيطة لتعلمك أن العملية انتهت بنجاح دون أي مشاكل.

باتباع هذه الخطوات، تكون قد استغللت بنجاح قوة Aspose.OCR لـ .NET في التعرف على النص داخل الصور وحفظ النتائج بصيغ مستندات مختلفة، بما في ذلك **ocr to searchable pdf**.

## المشكلات الشائعة والحلول
- **الصورة غير معترف بها** – تأكد من أن الصورة ذات دقة كافية (على الأقل 300 dpi) وبصيغة مدعومة (PNG، JPEG، TIFF).  
- **اكتشاف لغة غير صحيح** – مرّر كائن `RecognitionSettings` مع ضبط خاصية `Language` المناسبة (مثال: `Language = Language.English`).  
- **ملف الإخراج غير مُنشأ** – تحقق من أن `dataDir` يشير إلى مجلد صالح وقابل للكتابة وأن أسماء الملفات فريدة.

## الأسئلة المتكررة

**س: هل Aspose.OCR متوافق مع صيغ صور مختلفة؟**  
ج: نعم، يدعم Aspose.OCR مجموعة واسعة من صيغ الصور، مما يضمن مرونة في مهام OCR الخاصة بك.

**س: هل يمكنني تخصيص إعدادات التعرف لتحسين الدقة؟**  
ج: بالتأكيد! يوفر Aspose.OCR إعدادات التعرف لضبط عملية OCR وفقًا لمتطلباتك الخاصة.

**س: هل يتوفر إصدار تجريبي مجاني؟**  
ج: نعم، يمكنك البدء بإصدار تجريبي مجاني [هنا](https://releases.aspose.com/).

**س: كيف يمكنني الحصول على تراخيص مؤقتة لـ Aspose.OCR؟**  
ج: يمكن الحصول على تراخيص مؤقتة [هنا](https://purchase.aspose.com/temporary-license/).

**س: أين يمكنني طلب المساعدة أو التواصل مع المجتمع؟**  
ج: انضم إلى مجتمع Aspose.OCR على [منتدى Aspose](https://forum.aspose.com/c/ocr/16) للحصول على الدعم والنقاش.

## الخاتمة

ختامًا، يفتح Aspose.OCR لـ .NET آفاقًا واسعة لتحويل **image to pdf .net**، استخراج النص، وإنشاء المستندات. سواء كنت تستخرج بيانات، تنشئ PDFs قابلة للبحث، أو تصدر نتائج OCR إلى Excel، فإن Aspose.OCR يبسط العملية بواجهة برمجة تطبيقات بديهية ومجموعة ميزات قوية.

---

**آخر تحديث:** 2025-12-27  
**تم الاختبار مع:** Aspose.OCR 24.11 لـ .NET  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}