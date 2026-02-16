---
category: general
date: 2026-02-16
description: إنشاء ملف PDF قابل للبحث من صورة TIFF باستخدام Aspose OCR. تعلّم كيفية
  تحويل TIFF إلى PDF، واستخدام OCR لتحويل الصورة إلى PDF، والتعرف على النص من الصورة
  في C#.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- ocr image to pdf
- recognize text from image
- convert scanned image pdf
language: ar
og_description: إنشاء PDF قابل للبحث بسرعة. يوضح هذا الدرس كيفية تحويل TIFF إلى PDF،
  واستخدام OCR لتحويل الصورة إلى PDF والتعرف على النص من الصورة باستخدام Aspose OCR.
og_title: إنشاء ملف PDF قابل للبحث من TIFF – دليل Aspose OCR
tags:
- Aspose OCR
- C#
- PDF/A
- Document Processing
title: إنشاء PDF قابل للبحث من TIFF – دليل Aspose OCR خطوة بخطوة
url: /ar/net/text-recognition/create-searchable-pdf-from-tiff-aspose-ocr-step-by-step-guid/
---

Now output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث من TIFF – دليل Aspose OCR خطوة بخطوة

هل احتجت يومًا إلى **create searchable PDF** من ملف TIFF ممسوح ضوئيًا لكنك لم تكن متأكدًا أي مكتبة ستقوم بالعمل الشاق؟ لست وحدك. في العديد من مشاريع أتمتة المكاتب ننتهي بمجموعة من ملفات TIFF التي تبدو كصور، ليست نصًا. الخبر السار؟ مع Aspose OCR يمكنك **convert tiff to pdf**، تشغيل OCR على الصورة، والحصول على PDF/A‑2b قابل للبحث بالكامل.

في هذا الدرس سنستعرض مثالًا كاملًا وقابلًا للتنفيذ بلغة C# يوضح بالضبط كيفية **create searchable PDF**، ولماذا كل خطوة مهمة، وما هي الأخطاء التي يجب الانتباه إليها. في النهاية ستكون قادرًا على **recognize text from image**، **OCR image to pdf**، وحتى **convert scanned image pdf** للوثائق التي تلتزم بمعايير الأرشفة.

## ما ستتعلمه

- كيفية تثبيت وإضافة مرجع حزمة Aspose OCR NuGet.  
- الكود الدقيق المطلوب **create searchable PDF** من ملف TIFF.  
- لماذا تحميل نموذج اللغة الصحيح أمر حاسم للحصول على OCR دقيق.  
- نصائح للتعامل مع المسحات الكبيرة، ملفات TIFF متعددة الصفحات، والامتثال لـ PDF/A.  
- أين تجد الملف الناتج وكيف تتحقق من أن النص قابل للبحث.  

### المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| .NET 6.0 أو أحدث (أي بيئة تشغيل .NET الحديثة) | Aspose OCR توفر ملفات ثنائية لـ .NET Standard 2.0+، والتي تعمل في كل مكان من .NET Core إلى .NET Framework. |
| Visual Studio 2022 (أو VS Code مع امتداد C#) | يوفر لك IntelliSense وإدارة NuGet سهلة. |
| رخصة Aspose OCR سارية (أو مفتاح تقييم مجاني) | الإصدار التجريبي المجاني يحد من عدد الصفحات؛ الرخصة تزيل العلامة المائية وتمكن من إخراج PDF/A‑2b. |
| ملف TIFF تريد معالجته (مثال: `input.tif`) | هذه هي الصورة المصدر التي سنحولها إلى **searchable PDF**. |

> **نصيحة احترافية:** إذا كنت تتعامل مع ملفات TIFF متعددة الصفحات، سيعامل Aspose OCR كل صفحة كصورة منفصلة تلقائيًا—بدون الحاجة إلى أي كود إضافي.

---

## الخطوة 1: تثبيت حزمة Aspose OCR NuGet

أولاً، أضف المكتبة إلى مشروعك. افتح Package Manager Console وشغل الأمر التالي:

```powershell
Install-Package Aspose.OCR
```

أو، إذا كنت تفضل الواجهة الرسومية، ابحث عن “Aspose.OCR” في **NuGet Package Manager** وانقر **Install**. سيقوم ذلك بجلب جميع ملفات DLL المطلوبة، بما في ذلك نماذج اللغة التي سنحتاجها لاحقًا.

> **لماذا هذه الخطوة؟** بدون الحزمة لا وجود لفئة `OcrEngine`، وستواجه أخطاء تجميع. نهج NuGet يضمن أن لديك الإصدار الصحيح (حاليًا 23.12) ويجلب أي تبعيات متداخلة تلقائيًا.

---

## الخطوة 2: تهيئة محرك OCR

إنشاء نسخة من المحرك هو أول سطر كود حقيقي ستكتبه. فكر في `OcrEngine` كالعقل الذي يقوم بكل العمل الشاق.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine – this object will manage the entire pipeline
OcrEngine ocrEngine = new OcrEngine();
```

> **ما الذي يحدث؟** يقوم المُنشئ بإعداد المخازن الداخلية وتحضير المحرك لتحميل نموذج اللغة. إذا تخطيت هذه الخطوة، ستؤدي الاستدعاءات اللاحقة مثل `LoadLanguage` إلى رمي `NullReferenceException`.

---

## الخطوة 3: تحميل نموذج اللغة الإنجليزية (أو أي نموذج آخر)

تعتمد دقة OCR على نموذج اللغة الذي تقوم بتحميله. بالنسبة لمعظم المستندات الغربية، الإنجليزية كافية، لكن Aspose يدعم عشرات اللغات.

```csharp
// Load English language data – essential for recognizing Latin characters
ocrEngine.LoadLanguage(LanguageModel.English);
```

> **لماذا تحميل نموذج؟** يحتاج المحرك إلى تمثيل إحصائي لأشكال الحروف. بدون ذلك ستحصل على نص غير مفهوم أو نتيجة فارغة. إذا كنت بحاجة إلى **recognize text from image** بالفرنسية، استبدل `LanguageModel.English` بـ `LanguageModel.French`.

---

## الخطوة 4: توفير صورة TIFF وإنشاء PDF/A‑2b

الآن نوجه المحرك إلى ملف المصدر. المساعد `ImageStream.FromFile` يقرأ ملف TIFF (صفحة واحدة أو متعددة) إلى الذاكرة.

```csharp
// Step 4: Assign the TIFF image to the engine
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.tif");

// Run OCR and produce a PDF/A‑2b document – this is the searchable PDF we want
PdfAResult searchablePdf = ocrEngine.RecognizePdfA(PdfAStandard.PdfA2b);
```

> **ما الذي يفعله هذا؟** `RecognizePdfA` يقوم بثلاث عمليات في الخلفية:  
> 1️⃣ يقوم بتشغيل OCR على كل صفحة من TIFF.  
> 2️⃣ يضمّن النص المعترف به كطبقة غير مرئية.  
> 3️⃣ يضع كل ذلك في حاوية PDF/A‑2b، وهي المعيار ISO للحفظ طويل الأمد.  

إذا كنت تحتاج فقط إلى PDF عادي (بدون امتثال أرشيفي)، يمكنك استدعاء `ocrEngine.RecognizePdf()` بدلاً من ذلك. لكن في معظم سيناريوهات الشركات، PDF/A‑2b هو الخيار الأكثر أمانًا.

---

## الخطوة 5: حفظ PDF القابل للبحث على القرص

أخيرًا، احفظ النتيجة إلى ملف. طريقة `Save` تأخذ مسارًا وتتعامل مع جميع عمليات الإدخال/الإخراج.

```csharp
// Save the generated searchable PDF to your output folder
searchablePdf.Save("YOUR_DIRECTORY/output.pdf");
```

عند فتح `output.pdf` في Adobe Reader، يجب أن تكون قادرًا على كتابة كلمة في مربع البحث وإيجادها فورًا—على الرغم من أن الملف الأصلي كان مجرد صورة. هذه هي سحر عمليات **create searchable PDF**.

---

## تحويل TIFF إلى PDF – ملخص سريع

فيما يلي البرنامج الكامل القابل للتنفيذ الذي يجمع كل شيء معًا. لا تتردد في نسخه ولصقه في تطبيق Console واضغط **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the desired language model (English in this case)
        ocrEngine.LoadLanguage(LanguageModel.English);

        // 3️⃣ Point the engine at the TIFF you want to convert
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.tif");

        // 4️⃣ Recognize the image and produce a PDF/A‑2b (searchable PDF)
        PdfAResult searchablePdf = ocrEngine.RecognizePdfA(PdfAStandard.PdfA2b);

        // 5️⃣ Persist the result to disk
        searchablePdf.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("✅ Searchable PDF created successfully!");
    }
}
```

**النتيجة المتوقعة:** يظهر `output.pdf` في `YOUR_DIRECTORY`. افتحه، اختر أداة النص، وسترى نصًا قابلًا للتحديد والبحث مغطى على الصورة النقطية الأصلية.

---

## OCR Image to PDF – معالجة الحالات الخاصة

### ملفات TIFF متعددة الصفحات

إذا كان ملف المصدر يحتوي على أكثر من صفحة، سيقوم Aspose OCR تلقائيًا بمعالجة كل صفحة وإضافة صفحة مقابلة في PDF. لا حاجة لأي حلقة إضافية.

### ملفات كبيرة وإدارة الذاكرة

للمسحات بحجم الجيجابايت، فكر في تمكين **streaming mode**:

```csharp
ocrEngine.Image = ImageStream.FromFile("large.tif", useMemoryCache: false);
```

هذا يخبر المحرك بقراءة أجزاء من القرص بدلاً من تحميل الصورة بالكامل إلى الذاكرة—مفيد للمهام الدُفعية على الخادم.

### صيغ إخراج مختلفة

أحيانًا لا تحتاج إلى PDF/A‑2b بل إلى PDF عادي. غيّر الاستدعاء إلى:

```csharp
PdfResult plainPdf = ocrEngine.RecognizePdf();
plainPdf.Save("plain.pdf");
```

أو، إذا كنت تريد النص الخام فقط (بدون PDF)، استخدم:

```csharp
string extractedText = ocrEngine.RecognizeText();
System.IO.File.WriteAllText("text.txt", extractedText);
```

هذه الاختلافات تعالج سيناريو **convert scanned image pdf** حيث تقبل الأنظمة اللاحقة فقط ملفات PDF عادية.

---

## نصائح احترافية للحصول على OCR موثوق

- **DPI matters:** المسحات بدقة 300 DPI أو أعلى تعطي أفضل معدلات التعرف. أقل من 200 DPI ستلاحظ انخفاضًا في الدقة.  
- **Pre‑processing:** إذا كان TIFF يحتوي على ضوضاء، نفّذ `ocrEngine.Image = ImageProcessor.Deskew(...).Apply(ocrEngine.Image);` قبل التعرف.  
- **Licensing:** تذكر ضبط الرخصة مبكرًا في التطبيق (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`). بدونها سيحتوي الإخراج على علامة مائية “Evaluation”.  
- **Batch processing:** غلف المنطق الأساسي داخل حلقة `foreach` على مجلد يحتوي على ملفات TIFF لتقوم بـ **convert tiff to pdf** بالجملة.

---

## الأسئلة المتكررة

**س: هل يعمل هذا على Linux؟**  
ج: بالتأكيد. Aspose OCR يستهدف .NET Standard، لذا يمكنك تشغيل نفس الملف الثنائي على Windows أو Linux أو macOS باستخدام بيئة تشغيل .NET 6.

**س: ماذا لو احتجت إلى التعرف على لغة غير الإنجليزية؟**  
ج: ما عليك سوى استبدال `LanguageModel.English` بالعدد المناسب، مثل `LanguageModel.Spanish`. يمكنك أيضًا تحميل عدة لغات في آن واحد للمستندات متعددة اللغات.

**س: هل يمكنني تضمين خط مخصص في PDF/A؟**  
ج: نعم. استخدم `ocrEngine.Options.PdfOptions.Font = PdfFont.CreateFont("path/to/font.ttf");` قبل استدعاء `RecognizePdfA`.

---

## الخلاصة

لقد غطينا كل ما تحتاجه لإنشاء ملفات **create searchable PDF** من صور TIFF باستخدام Aspose OCR. من تثبيت حزمة NuGet، تحميل نموذج اللغة المناسب، إلى توليد PDF/A‑

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}