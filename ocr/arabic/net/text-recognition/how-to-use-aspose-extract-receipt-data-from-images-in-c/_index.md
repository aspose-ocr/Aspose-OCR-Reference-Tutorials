---
category: general
date: 2026-04-04
description: تعلم كيفية استخدام Aspose لاستخراج بيانات الإيصال، وتحميل صورة الإيصال،
  وإجراء OCR لصورة الإيصال مع مثال كامل بلغة C#. دليل خطوة بخطوة للمطورين.
draft: false
keywords:
- how to use aspose
- extract receipt data
- how to extract receipt
- load receipt image
- ocr receipt image
language: ar
og_description: كيفية استخدام Aspose لاستخراج بيانات الإيصال من صورة إيصال ممسوحة
  ضوئياً. كود C# كامل، شروحات، ونصائح لمعالجة صور الإيصالات باستخدام OCR.
og_title: كيفية استخدام Aspose – استخراج بيانات الإيصال من الصور
tags:
- Aspose
- OCR
- C#
- Receipt Processing
title: كيفية استخدام Aspose – استخراج بيانات الإيصال من الصور بلغة C#
url: /ar/net/text-recognition/how-to-use-aspose-extract-receipt-data-from-images-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام Aspose – استخراج بيانات الإيصال من الصور في C#

هل تساءلت يومًا **كيف تستخدم Aspose** لاستخلاص معلومات منظمة من صورة إيصال؟ لست وحدك. سواء كنت تبني تطبيق تتبع نفقات أو تقوم بأتمتة إدخال الفواتير، فإن المشكلة هي نفسها: لديك ملف PNG أو JPEG، وتحتاج إلى اسم التاجر، التاريخ، والمبلغ الإجمالي دون كتابة يدوية.

الأمر بسيط—Aspose.OCR يجعل هذه العملية بأكملها سهلة للغاية. في هذا الدرس سنستعرض تحميل صورة الإيصال، تشغيل OCR، وأخيرًا استخراج بيانات الإيصال ببضع أسطر من C#. في النهاية ستحصل على برنامج كونسول قابل للتنفيذ يطبع اسم التاجر، التاريخ، والمبلغ الإجمالي مباشرةً في الكونسول.

> **فوز سريع:** إذا كنت تحتاج فقط إلى الكود، انتقل إلى قسم “مثال عملي كامل” في الأسفل وانسخه‑الصق.

## ما ستحتاجه

- **.NET 6.0 أو أحدث** (API يعمل مع .NET Core و .NET Framework)
- **Aspose.OCR for .NET** حزمة NuGet (`Install-Package Aspose.OCR`)
- صورة إيصال نموذجية (PNG, JPG, أو BMP) محفوظة محليًا
- Visual Studio 2022 أو أي محرر يدعم مشاريع C#

لا توجد مكتبات طرف ثالث أخرى مطلوبة. المتطلب الوحيد هو فهم أساسي لتطبيقات كونسول C#—إذا كتبت “Hello World”، فأنت جاهز للبدء.

## الخطوة 1 – تثبيت وإضافة مرجع Aspose.OCR

لكي **تستخدم Aspose**، تحتاج أولاً إلى المكتبة في مشروعك. افتح Package Manager Console وشغّل الأمر التالي:

```powershell
Install-Package Aspose.OCR
```

بدلاً من ذلك، استخدم واجهة NuGet UI وابحث عن “Aspose.OCR”. بعد التثبيت، أضف المساحات الاسمية المطلوبة في أعلى ملفك:

```csharp
using Aspose.OCR;
using Aspose.OCR.Structured;
```

> **نصيحة احترافية:** حافظ على تحديث حزم NuGet الخاصة بك. اعتبارًا من اليوم (أبريل 2026) أحدث نسخة مستقرة هي 23.11.0، والتي تشمل تحسينات أداء لـ OCR على الإيصالات عالية الدقة.

## الخطوة 2 – تحميل صورة الإيصال

عند **تحميل صورة الإيصال**، لديك مصدران شائعان: مسار محلي أو تدفق من طلب ويب. في هذا الدرس سنبقي الأمر بسيطًا ونقرأ من القرص:

```csharp
// Step 2: Load the receipt image to be processed
var ocrEngine = new OcrEngine
{
    Language = Language.English // set language for better accuracy
};

ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.png");
```

استبدل `YOUR_DIRECTORY/receipt.png` بالمسار الفعلي لملف الإيصال الخاص بك. إذا كنت تتعامل مع تحميلات المستخدمين، يمكنك تمرير `MemoryStream` إلى `ImageStream.FromStream`.

> **لماذا هذا مهم:** تحديد اللغة (English) يخبر محرك OCR بمجموعة الأحرف المتوقعة، مما يقلل الأخطاء في التعرف—وهذا مهم خاصةً عندما تقوم بـ **ocr receipt image** التي تحتوي على أرقام ورموز.

## الخطوة 3 – تشغيل OCR والتقاط معلومات التخطيط

خطوة OCR تفعل أكثر من مجرد إرجاع النص الخام؛ فهي تلتقط أيضًا التخطيط، وهو أمر حاسم لاستخلاص البيانات المنظمة لاحقًا.

```csharp
// Step 3: Run OCR to generate text and layout information (required for structured extraction)
ocrEngine.Recognize();
```

بعد انتهاء `Recognize()`، يحتفظ `ocrEngine` بالنص العادي وبيانات موضع كل كلمة. هذه هي الأساس للخطوة التالية حيث سنطلب من Aspose أن “**how to extract receipt**” الحقول تلقائيًا.

## الخطوة 4 – تهيئة مُعرّف التخطيط (Layout Recognizer)

توفر Aspose فئة `LayoutRecognizer` التي تعرف كيف يتم تنظيم الإيصالات عادةً (التاجر في الأعلى، سطر التاريخ، المجموع في الأسفل). ببساطة تمرر محرك OCR المُكوَّن:

```csharp
// Step 4: Initialize the layout recognizer with the OCR engine
var layoutRecognizer = new LayoutRecognizer(ocrEngine);
```

في الخلفية، يطبق المُعرّف مجموعة من الخوارزميات—مثل البحث عن رموز العملة أو أنماط التاريخ—لتحويل النص الخام إلى حقول دلالية.

## الخطوة 5 – استخراج بيانات الإيصال المنظمة

الآن يأتي الجزء الممتع: **extract receipt data**. استدعاء طريقة واحدة يقوم بالعمل الشاق:

```csharp
// Step 5: Extract structured receipt data (merchant, date, total amount)
var receiptData = layoutRecognizer.ExtractReceiptData();
```

`receiptData` هو كائن من النوع `ReceiptData` (معرف في `Aspose.OCR.Structured`). يحتوي على ثلاث خصائص رئيسية:

- `Merchant` – اسم المتجر
- `Date` – تاريخ الشراء كـ `DateTime` (إذا تم اكتشافه)
- `TotalAmount` – المبلغ الإجمالي كـ `decimal`

إذا لم يتمكن المحرك من العثور على حقل معين، ستكون الخاصية `null` أو `0`. يمكنك إضافة منطق احتياطي إذا لزم الأمر (مثلاً، طلب تأكيد من المستخدم).

## الخطوة 6 – عرض المعلومات المستخرجة

أخيرًا، اطبع النتائج إلى الكونسول. هنا ترى ثمار عملك:

```csharp
// Step 6: Display the extracted information
Console.WriteLine($"Merchant: {receiptData.Merchant}");
Console.WriteLine($"Date:     {receiptData.Date:d}");
Console.WriteLine($"Total:    {receiptData.TotalAmount:C}");
```

سلاسل التنسيق (`:d` و `:C`) تنتج تاريخًا مختصرًا وسلسلة عملة على التوالي، مما يجعل الإخراج قابلًا للقراءة البشرية.

### النتيجة المتوقعة

بافتراض أن الإيصال يخص “Coffee Corner”، بتاريخ 2025‑12‑01، وبمجموع $4.75، سيظهر الكونسول:

```
Merchant: Coffee Corner
Date:     12/1/2025
Total:    $4.75
```

إذا كان أي حقل مفقودًا، سترى سطرًا فارغًا أو قيمة افتراضية—مفيد للتصحيح.

## الحالات الخاصة والمشكلات الشائعة

### 1. صور منخفضة الدقة

إذا كانت صورة الإيصال غير واضحة أو أقل من 150 dpi، فإن دقة OCR تنخفض بشكل كبير. تكبير الصورة باستخدام مرشح ثنائي الخطوط البسيط قبل تمريرها إلى Aspose يمكن أن يحسن النتائج.

```csharp
ocrEngine.Image = ImageStream.FromFile("receipt.png")
    .Resize(2.0, InterpolationMode.Bilinear);
```

### 2. إيصالات غير إنجليزية

المثال الأساسي يستخدم `Language.English`. للإيصالات متعددة اللغات، اضبط `Language` إلى القيمة المناسبة (مثال: `Language.French`) أو استخدم `Language.AutoDetect` إذا لم تكن متأكدًا.

### 3. عدة إيصالات في صورة واحدة

يتوقع مُعرّف التخطيط في Aspose إيصالًا واحدًا لكل صورة. إذا كان لديك صورة لعدة إيصالات جنبًا إلى جنب، ستحتاج إلى معالجة مسبقة للصورة—اقتطاع كل إيصال إلى ملف منفصل قبل تشغيل OCR.

### 4. فقدان رمز العملة

أحيانًا يظهر المبلغ الإجمالي بدون رمز `$`. لا يزال المُعرّف يلتقط الأرقام، لكن قد تحتاج إلى معالجة لاحقة للسلسلة لضمان وضع الفاصلة العشرية بشكل صحيح.

```csharp
if (receiptData.TotalAmount == 0 && rawText.Contains("Total"))
{
    // fallback parsing logic here
}
```

## نصائح احترافية للإنتاج

- **Cache the OCR engine** إذا كنت تعالج العديد من الإيصالات دفعة واحدة؛ إعادة استخدام نفس المثيل يقلل من عبء التخصيص.
- **Log the raw OCR text** (`ocrEngine.Text`) لسجلات التدقيق. يكون مفيدًا عندما يفشل استخراج حقل ما.
- **Wrap the entire flow in a try/catch** وعرض رسالة خطأ ودية (مثال: “Unable to read receipt, please upload a clearer image”).

## مثال عملي كامل

فيما يلي تطبيق كونسول مستقل يمكنك تجميعه وتشغيله كما هو. فقط استبدل مسار الصورة وستكون جاهزًا للبدء.

```csharp
// ------------------------------------------------------------
// How to Use Aspose – Extract Receipt Data from Images (C#)
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Structured;

namespace ReceiptExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create and configure the OCR engine for English language
            var ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the receipt image you want to process
            // 👉 Make sure the file exists; otherwise an exception will be thrown.
            const string imagePath = "YOUR_DIRECTORY/receipt.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Run OCR – this also captures layout information
            ocrEngine.Recognize();

            // 4️⃣ Initialize the layout recognizer with the OCR engine
            var layoutRecognizer = new LayoutRecognizer(ocrEngine);

            // 5️⃣ Extract structured receipt data (merchant, date, total amount)
            var receiptData = layoutRecognizer.ExtractReceiptData();

            // 6️⃣ Display the extracted information
            Console.WriteLine($"Merchant: {receiptData.Merchant ?? "Not detected"}");
            Console.WriteLine($"Date:     {(receiptData.Date == DateTime.MinValue ? "Not detected" : receiptData.Date.ToShortDateString())}");
            Console.WriteLine($"Total:    {(receiptData.TotalAmount == 0 ? "Not detected" : receiptData.TotalAmount.ToString("C"))}");

            // Keep the console window open when debugging
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**تشغيل الكود**

1. أنشئ مشروع كونسول .NET جديد (`dotnet new console -n ReceiptExtractor`).
2. أضف حزمة Aspose.OCR (`dotnet add package Aspose.OCR`).
3. استبدل ملف `Program.cs` المُولد بالمقتطف أعلاه.
4. ضع صورة إيصال في المسار الذي حددته.
5. قم بالبناء والتشغيل (`dotnet run`).

يجب أن ترى اسم التاجر، التاريخ، والمجموع مطبوعًا تمامًا كما هو موضح سابقًا.

## الخلاصة

في هذا الدليل غطينا **how to use Aspose** لـ **load receipt image**، تشغيل **ocr receipt image**، وأخيرًا **extract receipt data** ببضع أسطر فقط. النقطة الأساسية هي أن Aspose.OCR يقوم بالعمل الشاق—بمجرد تكوين محرك OCR، يقوم `LayoutRecognizer` بتحويل النص الخام إلى كائن منظم يمكنك الاعتماد عليه.

ما الخطوات التالية؟ جرّب إدخال القيم المستخرجة إلى قاعدة بيانات، أو إنشاء ملخص إيصال PDF، أو حتى تمريرها إلى نموذج تعلم آلي لتصنيف النفقات. يمكنك أيضًا تجربة أنواع مستندات منظمة أخرى مثل الفواتير أو ملصقات الشحن—`ExtractInvoiceData` في Aspose يعمل بطريقة مشابهة جدًا.

هل لديك أسئلة حول الحالات الخاصة أو تريد معرفة كيفية التعامل مع ملفات PDF متعددة الصفحات؟ اترك تعليقًا أو راجع وثائق Aspose.OCR الرسمية للسيناريوهات المتقدمة. برمجة سعيدة، واستمتع ببساطة **how to use Aspose** لأتمتة الإيصالات!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}