---
category: general
date: 2026-04-01
description: كيفية تحويل مخرجات OCR إلى JSON و XML في C# – تعلم استخراج النص من الصورة
  وكتابة ملف JSON باستخدام C# و Aspose.OCR.
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: ar
og_description: كيفية تحويل نتائج OCR إلى ملفات JSON و XML منظمة باستخدام C#. دليل
  خطوة بخطوة لاستخراج النص من الصورة وكتابة ملف JSON باستخدام C#.
og_title: كيفية تحويل OCR إلى JSON و XML في C# – كتابة ملف JSON
tags:
- OCR
- C#
- Aspose
title: كيفية تحويل OCR إلى JSON و XML في C# – كتابة ملف JSON
url: /ar/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تحويل OCR إلى JSON & XML في C# – كتابة ملف JSON

**كيفية تحويل نتائج OCR** إلى شيء يمكنك فعلاً استخدامه هو سؤال يطرحه الكثير من المطورين. في هذا الدليل سنظهر لك كيفية استخراج النص من صورة، وتحويل مخرجات OCR إلى JSON و XML منسقين بشكل جميل، ثم كتابة تلك الملفات إلى القرص باستخدام C#.

إذا سبق لك أن نظرت إلى سلسلة OCR خام وفكرت، “يجب أن يكون هناك طريقة أفضل لتخزين هذا”، فأنت في المكان الصحيح. بنهاية هذا الدليل ستحصل على برنامج كامل قابل للتنفيذ لا يقتصر فقط على **استخراج النص من ملفات الصورة** بل يعرف أيضاً كيف **يكتب ملف JSON في C#** و **يكتب ملف XML في C#** دون عناء.

## ما الذي ستحتاجه

- **.NET 6.0** أو أحدث (الكود يعمل أيضاً مع .NET Framework 4.6+).  
- حزمة NuGet **Aspose.OCR** – قم بتثبيتها باستخدام `dotnet add package Aspose.OCR`.  
- صورة تحتوي على نص (مثال: `invoice.png`).  
- أي بيئة تطوير تفضلها – Visual Studio، Rider، أو VS Code ستكفي.

> **نصيحة احترافية:** احفظ ملفات الصور في مجلد مخصص (مثال: `Resources/`) لتبقى المسارات منظمة.

## الخطوة 1: إعداد محرك OCR – كيفية تحويل OCR

أولاً، نقوم بإنشاء كائن `OcrEngine` ونخبره بأي لغة يبحث عنها. في معظم الحالات تكون اللغة الإنجليزية كافية، لكن يمكنك استبدال `Language.English` بأي لغة مدعومة.

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **لماذا هذا مهم:** تهيئة المحرك باللغة الصحيحة تحسن الدقة بشكل كبير، خاصةً للخطوط غير اللاتينية.

## الخطوة 2: التعرف على النص – استخراج النص من الصورة

الآن نقوم بتمرير الصورة إلى المحرك. طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي على النص الخام بالإضافة إلى بيانات الموقع.

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

إذا لم يتم العثور على الصورة، فإن `Recognize` تُطلق استثناء `FileNotFoundException`. لتبسيط العرض سنفترض أن المسار صحيح، لكن في بيئة الإنتاج يجب تغليف ذلك بكتلة try‑catch.

## الخطوة 3: تحويل النتيجة إلى JSON – كتابة ملف JSON C#

تجعل Aspose.OCR عملية التسلسل سهلة. طريقة `ToJson` تقبل علامة `indent` لإنتاج مخرجات منسقة بشكل جميل، وهو مثالي عندما تريد فتح الملف في محرر نصوص.

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### عينة JSON المتوقعة

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **كيفية استخراج النص:** الخاصية `Text` تعطيك السلسلة النصية العادية التي يمكنك تمريرها إلى خدمات أخرى (فهارس البحث، قواعد البيانات، إلخ).

## الخطوة 4: حفظ JSON – كتابة ملف JSON C# (متابعة)

مع جاهزية سلسلة JSON، نكتبها ببساطة إلى ملف باستخدام `File.WriteAllText`. هذا يضمن الترميز UTF‑8 بشكل افتراضي.

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

الآن لديك ملف `invoice.json` بجوار صورتك، جاهز للمعالجة اللاحقة.

## الخطوة 5: تحويل النتيجة إلى XML – كتابة ملف XML C#

إذا كنت تفضل XML للأنظمة القديمة، فإن طريقة `ToXml` تقوم بالعمل الشاق. مثل `ToJson`، تدعم أيضاً التنسيق المنسق.

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### عينة XML المتوقعة

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## الخطوة 6: حفظ XML – كتابة ملف XML C# (متابعة)

حفظ XML يتم بنفس طريقة حفظ JSON؛ فقط استخدم امتداد `.xml`.

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### مثال كامل يعمل

نجمع كل ما سبق في برنامج كامل يمكنك نسخه ولصقه في تطبيق Console:

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

شغّل البرنامج، وستجد ملفين جديدين—`invoice.json` و `invoice.xml`—في المكان الذي حددته. افتحهما للتحقق من أن البنية تتطابق مع العينات أعلاه.

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| **ماذا لو احتوت الصورة على لغات متعددة؟** | أنشئ كائنات `OcrEngine` منفصلة لكل لغة أو استخدم `Language.Multi` إذا كان مدعومًا. |
| **هل يمكنني التحكم في تنسيق المخرجات (مثل استبعاد بيانات المنطقة)؟** | نعم. كل من `ToJson` و `ToXml` يقبلان معلمات اختيارية لتصفية الحقول؛ راجع وثائق Aspose.OCR لـ `ExportOptions`. |
| **كيف أتعامل مع ملفات PDF كبيرة تحتوي على صفحات متعددة؟** | عالج كل صفحة على حدة، اجمع النتائج، ثم قم بالتسلسل مرة واحدة. |
| **هل المخرجات آمنة UTF‑8؟** | بالتأكيد—Aspose.OCR يستخدم Unicode داخليًا، و`File.WriteAllText` يكتب UTF‑8 افتراضيًا. |
| **ماذا عن الأداء؟** | OCR يستهلك الكثير من وحدة المعالجة. للوظائف الدفعية فكر في التنفيذ المتوازي عبر الأنوية أو استخدام API السحابة من Aspose. |

## الخلاصة

أنت الآن تعرف **كيفية تحويل نتائج OCR** إلى كل من JSON و XML باستخدام C#. باتباع الخطوات أعلاه يمكنك **استخراج النص من الصورة**، ثم **كتابة ملف JSON في C#** و **كتابة ملف XML في C#** ببضع أسطر فقط. هذه الطريقة سريعة، موثوقة، وتعمل مع أي نوع صورة تدعمه Aspose.OCR.

هل أنت مستعد للتحدي التالي؟ جرّب إمداد الـ

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}