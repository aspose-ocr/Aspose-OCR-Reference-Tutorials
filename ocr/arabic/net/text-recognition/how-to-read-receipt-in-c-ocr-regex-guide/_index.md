---
category: general
date: 2026-02-13
description: كيفية قراءة الإيصال بسرعة باستخدام Aspose OCR واستخراج المبلغ باستخدام
  التعبير النمطي. تعلم خطوة بخطوة معالجة الإيصال باستخدام OCR.
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: ar
og_description: كيفية قراءة الإيصال في C# باستخدام Aspose OCR والـ regex. يوضح هذا
  الدليل كيفية معالجة الإيصال باستخدام OCR واستخراج المبلغ الإجمالي.
og_title: كيفية قراءة الإيصال في C# – دليل شامل لتقنية OCR والـ Regex
tags:
- OCR
- C#
- Regex
- Aspose
title: كيفية قراءة الإيصال في C# – دليل OCR + Regex
url: /ar/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية قراءة الإيصال في C# – دليل OCR + Regex

هل تساءلت يومًا **كيف تقرأ الإيصال** من الصور دون كتابة كل سطر يدويًا؟ في العديد من تطبيقات الأعمال الصغيرة تحتاج إلى استخراج المبلغ الإجمالي من صورة الإيصال، والقيام بذلك يدويًا يتعارض مع هدف الأتمتة. الخبر السار؟ باستخدام Aspose OCR يمكنك ترك المحرك يقوم بالعمل الشاق، ثم تعبير عادي بسيط سيحدد الإجمالي. في هذا الدرس سنستعرض **process receipt with OCR**، استخراج المبلغ باستخدام regex، والحصول على قيمة إجمالية جاهزة للاستخدام.

سترى مثالًا كاملًا وقابلًا للتنفيذ، وتكتشف لماذا نموذج لغة الإيصال مهم، وتحصل على نصائح للتعامل مع الحالات الخاصة مثل رموز العملات المختلفة أو عدم وجود تسمية “Total”. لا تحتاج إلى مستندات خارجية—كل ما تحتاجه موجود هنا.

## ما ستتعلمه

- كيفية إعداد Aspose OCR للتعرف المتخصص على الإيصالات (نموذج لغة `Receipt` يقوم تلقائيًا بتصحيح الميل وإزالة الضوضاء من الصورة).  
- كيفية تطبيق تعبير عادي **extract amount using regex** يعمل على معظم الإيصالات بنمط الولايات المتحدة.  
- كيفية التعامل مع المتغيرات الشائعة مثل “TOTAL”، “Total:”، أو “Grand Total – $12.34”.  
- كيفية إخراج النتيجة بأمان وماذا تفعل عندما لا يتم العثور على النمط.  

**المتطلبات المسبقة**: .NET 6+ (أو .NET Framework 4.7+)، رخصة Aspose OCR صالحة أو نسخة تجريبية، وصورة لإيصال محفوظة محليًا. هذا كل شيء—لا تحتاج إلى حزم NuGet إضافية بخلاف Aspose.OCR.

---

## الخطوة 1 – تثبيت Aspose OCR وتحضير المشروع

### لماذا هذا مهم

Aspose OCR يوفر نموذجًا مخصصًا **process receipt with OCR** يعرف كيف يثبت ورقة مجعدة ويتجاهل الضوضاء الخلفية. استخدام نموذج النص العام سيؤدي إلى مزيد من الأخطاء، خاصةً في المسحات منخفضة الدقة.

### Code

```csharp
// Install the package via NuGet first:
//   dotnet add package Aspose.OCR
using Aspose.OCR;
using Aspose.OCR.Enums;
using System.Text.RegularExpressions;

// If you have a license file, load it now (optional but removes trial watermark)
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

> **نصيحة احترافية:** احتفظ بملف الترخيص خارج مجلد التحكم بالمصدر لتجنب الالتزام غير المقصود.

---

## الخطوة 2 – تكوين محرك OCR للتعرف على الإيصالات

### لماذا هذا مهم

نموذج لغة `Receipt` يتضمن تصحيح الميل وإزالة الضوضاء مدمجين، مما يحسن الدقة بشكل كبير على الإيصالات الواقعية التي غالبًا ما تكون مطوية أو مجعدة.

### Code

```csharp
// Step 2: Create and configure the OCR engine for receipt processing
var ocrEngine = new OcrEngine
{
    // Receipt model is optimized for invoices, grocery receipts, etc.
    Language = OcrLanguage.Receipt
};
```

---

## الخطوة 3 – التعرف على النص من صورة الإيصال

### لماذا هذا مهم

تحتاج إلى النص الخام قبل أن تتمكن من تطبيق أي تعبير عادي. طريقة `RecognizeImage` تُعيد كائن `OcrResult` يحتوي على السلسلة الكاملة، درجات الثقة، وأكثر إذا احتجت ذلك لاحقًا.

### Code

```csharp
// Step 3: Recognize text from the receipt image
// Replace the path with the actual location of your receipt file.
string receiptPath = @"C:\Receipts\sample-receipt.jpg";

OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

// Quick sanity check – print the whole OCR output (helps debugging)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(receiptResult.Text);
Console.WriteLine("===================\n");
```

**الناتج المتوقع من OCR (مثال)**  
```
Walmart Supercenter
123 Main St.
Anytown, USA
Date: 02/12/2026
Item A   $3.45
Item B   $7.89
Subtotal $11.34
Tax      $0.91
Total:   $12.25
Thank you!
```

---

## الخطوة 4 – بناء تعبير عادي **Extract Amount Using Regex**

### لماذا هذا مهم

تأتي الإيصالات بأشكال متعددة، لكن كلمة “Total” (أو ما شابه) متبوعة بمبلغ بالدولار تُعد مرساة موثوقة. النمط أدناه يتحمل المسافات الاختيارية، النقطتين أو الشرطتين، وعلامة الدولار الاختيارية.

### Code

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**شرح النمط**

| الجزء | المعنى |
|------|---------|
| `Total` | يبحث عن كلمة “Total” (غير حساسة لحالة الأحرف). |
| `\s*[:\-]?` | يسمح بأي مسافات بيضاء، ثم نقطتين أو شرطة اختيارية. |
| `\s*\$?` | مسافات اختيارية وعلامة الدولار الاختيارية. |
| `(\d+(\.\d{2})?)` | يلتقط رقمًا مكوّنًا من رقم أو أكثر، مع إمكانية وجود فاصلة عشرية ومئتي سنت. |

---

## الخطوة 5 – إخراج الإجمالي المستخرج أو التعامل مع البيانات المفقودة

### لماذا هذا مهم

حتى أفضل OCR قد يفوت كلمة، خاصةً في الإيصالات الضبابية. توفير طريقة احتياطية سلسة يمنع الأعطال ويمنحك نقطة لتطبيق منطق مخصص (مثل طلب تأكيد من المستخدم).

### Code

```csharp
// Step 5: Output the extracted total, or indicate it wasn't found
if (totalMatch.Success)
{
    string amount = totalMatch.Groups[1].Value;
    Console.WriteLine($"Total: ${amount}");
}
else
{
    Console.WriteLine("Total amount not found. Consider reviewing the OCR output manually.");
}
```

**مثال على إخراج وحدة التحكم**

```
Total: $12.25
```

---

## مثال كامل يعمل – جميع الخطوات في ملف واحد

فيما يلي برنامج مستقل يمكنك نسخه ولصقه في مشروع وحدة تحكم. يتضمن تعليقات، معالجة أخطاء، وتحميل الترخيص الاختياري.

```csharp
// ---------------------------------------------------------------
// How to Read Receipt in C# – OCR + Regex (Complete Example)
// ---------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 0️⃣ Optional: Load your Aspose OCR license (remove trial watermark)
        try
        {
            var license = new Aspose.OCR.License();
            license.SetLicense("Aspose.OCR.lic"); // path to .lic file
        }
        catch (Exception ex)
        {
            Console.WriteLine("License not found – running in trial mode.");
        }

        // 1️⃣ Configure the OCR engine for receipt processing
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Receipt // receipt model = de‑skew + de‑noise
        };

        // 2️⃣ Path to the receipt image (change to your file)
        string receiptPath = @"YOUR_DIRECTORY/receipt.jpg";

        // 3️⃣ Perform OCR
        OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

        // 4️⃣ Debug: show full OCR text (helps when regex fails)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(receiptResult.Text);
        Console.WriteLine("===================\n");

        // 5️⃣ Regex to **extract amount using regex** (find the total)
        string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
        Match totalMatch = Regex.Match(receiptResult.Text, pattern,
                                        RegexOptions.IgnoreCase);

        // 6️⃣ Output
        if (totalMatch.Success)
        {
            string amount = totalMatch.Groups[1].Value;
            Console.WriteLine($"Total: ${amount}");
        }
        else
        {
            Console.WriteLine("Total amount not found. You might need to adjust the regex or improve image quality.");
        }
    }
}
```

**تشغيل البرنامج**

1. أنشئ مشروع وحدة تحكم جديد (`dotnet new console -n ReceiptReader`).  
2. أضف حزمة Aspose.OCR عبر NuGet (`dotnet add package Aspose.OCR`).  
3. استبدل `YOUR_DIRECTORY/receipt.jpg` بالمسار الفعلي لصورة الإيصال.  
4. ابنِ وشغّل (`dotnet run`).  

سترى تفريغ OCR يليه `Total: $xx.xx` إذا كان كل شيء متطابقًا.

---

## التعامل مع الحالات الخاصة والمتغيرات الشائعة

### 1. رموز عملات مختلفة

إذا كنت تتعامل مع اليورو (€) أو الجنيه (£)، وسّع النمط:

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. عدم وجود تسمية “Total”

بعض الإيصالات تظهر فقط “Grand Total”. أضف بديلًا:

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. وجود عدة إجماليات (مثل “Subtotal” و “Total”)

إذا كان التعبير العادي يطابق أول ظهور، قد ترغب في الحصول على **آخر** تطابق:

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. صور منخفضة الدقة

- زد DPI عند المسح (`300 DPI` هو المستوى المثالي).  
- عالج الصورة مسبقًا بفلتر تقليل الضبابية قبل تمريرها إلى Aspose (خارج نطاق هذا الدليل، لكنه يستحق التجربة).

---

## نصائح احترافية للمشاريع الواقعية

- **خزن نتيجة OCR** إذا كنت بحاجة لاستخراج عدة حقول (الضريبة، العناصر، إلخ) – ستدفع تكلفة OCR مرة واحدة فقط.  
- **سجّل النص الخام من OCR** في قاعدة بيانات؛ يصبح سجلًا قيمًا للمراجعة في حالة النزاعات.  
- عند بناء API ويب، **شغّل OCR في عامل خلفي**؛ قد يستغرق بضع مئات من المللي ثانية، وهو مقبول بشكل غير متزامن لكنه غير مثالي للطلب المتزامن.  
- **تحقق من صحة المبلغ المستخرج** وفقًا لقواعد العمل (مثلاً، يجب أن يكون المبلغ > 0) قبل التخزين.

---

## الخلاصة

غطينا **كيفية قراءة الإيصال** في C# باستخدام Aspose OCR، ثم **استخراج المبلغ باستخدام regex** للعثور على سطر الإجمالي بثقة. باستخدام نموذج لغة `Receipt` تحصل على نص مصحح ومزيل للضوضاء، وتتعامل تعبير عادي مختصر مع معظم تعقيدات التنسيق. الشيفرة الكاملة أعلاه جاهزة للإدراج في أي مشروع .NET وحدة تحكم أو خدمة، والاقتراحات الخاصة بالحالات الخاصة تمنحك أساسًا قويًا للاستخدام في بيئات الإنتاج.

هل أنت مستعد للخطوة التالية؟ جرّب توسيع الحل لاستخراج بنود الفاتورة الفردية، حساب الضريبة تلقائيًا، أو التكامل مع API لتتبع النفقات. وإذا واجهت إيصالًا يكسر النمط، تذكّر أن **regex find total** هو مجرد نقطة انطلاق—يمكنك دائمًا تعديل النمط ليتناسب مع منطقتك.

برمجة سعيدة، ولتكن معالجة الإيصالات سريعة، دقيقة، ومؤتمتة بالكامل!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}