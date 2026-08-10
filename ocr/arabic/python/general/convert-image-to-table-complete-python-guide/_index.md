---
category: general
date: 2026-03-26
description: تحويل الصورة إلى جدول باستخدام بايثون و OCR والذكاء الاصطناعي. تعلم كيفية
  استخراج الجدول من الصورة، تحسين دقة OCR، والحصول على نتائج منظمة بسرعة.
draft: false
keywords:
- convert image to table
- extract table from image
- extract tabular data image
- enhance OCR accuracy
language: ar
og_description: تحويل الصورة إلى جدول في بايثون. يوضح هذا الدليل كيفية استخراج الجدول
  من الصورة، تحسين دقة OCR، والعمل مع البيانات المنظمة.
og_title: تحويل الصورة إلى جدول – دليل بايثون خطوة بخطوة
tags:
- OCR
- Python
- AI post‑processing
title: تحويل الصورة إلى جدول – دليل بايثون الكامل
url: /ar/python/general/convert-image-to-table-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل الصورة إلى جدول – دليل بايثون الكامل

هل احتجت يوماً إلى **تحويل الصورة إلى جدول** لكنك شعرت بالعجز أمام لقطة شاشة غير واضحة؟ لست وحدك. في العديد من المشاريع القائمة على البيانات، أسرع طريقة للحصول على الأرقام في إطار بيانات هي التقاط صورة لجدول مطبوع وترك سكريبت يقوم بالمعالجة. الخبر السار؟ باستخدام محرك OCR حديث مع معالج AI صغير بعد المعالجة، يمكنك استخراج جدول نظيف ومنظم من أي صورة تقريباً.

في هذا الدرس سنستعرض **مثالاً عملياً لاستخراج بيانات جدول من صورة**، ننظفه، ونطبع كل صف كنص عادي. في النهاية ستفهم كيف **تحسن دقة OCR**، تتعامل مع المشكلات الشائعة، وتكيف الكود مع خطوط عملك الخاصة. لا سحر، فقط بايثون، بعض المكتبات، وقليل من التفكير.

> **ما ستحتاجه**  
> * Python 3.9+  
> * مكتبة OCR تدعم `OutputFormat.Structured` (مثلًا `myocr`)  
> * معالج AI اختياري بعد المعالجة (يمكن أن يكون محولًا خفيفًا أو دالة قائمة على القواعد)  
> * ملف صورة تجريبي (`table.png`) يحتوي على جدول بسيط

---

## الخطوة 1: تحويل الصورة إلى جدول – التعرف على الصورة بإخراج منظم

أول ما نقوم به هو تمرير الصورة إلى محرك OCR وطلب نتيجة **منظمة**. الإخراج المنظم يعني أن المحرك يحاول استنتاج الصفوف والأعمدة وحدود الخلايا بدلاً من إرجاع سلسلة نصية مسطحة.

```python
import myocr as ocr          # Hypothetical OCR package
import myengine as engine    # Wrapper around the OCR engine
import myai as ai            # Simple AI post‑processor

def recognize_image(path: str):
    """
    Sends the image to the OCR engine and asks for a tabular
    (structured) representation.
    """
    # Step 1: Recognize the image and request a structured (tabular) result
    structured_result = engine.recognize_image(
        path,
        output_format=ocr.OutputFormat.Structured
    )
    return structured_result
```

**لماذا هذا مهم:**  
إذا طلبت من OCR نصًا عاديًا ستحصل على مجموعة من الأحرف المتشابكة دون مفهوم للصفوف أو الأعمدة. بطلب تنسيق منظم، يقوم المحرك بعمل الكشف عن الخطوط، محاذاة الأعمدة، وحتى دمج الخلايا الأساسية. هذا يقلل بشكل كبير من كمية التحليل اليدوي التي ستحتاجها لاحقًا.

> **نصيحة احترافية:** تأكد من أن الصورة ذات تباين جيد وانحراف قليل. عادةً ما يعطي مسح بدقة 300 dpi أفضل النتائج.

---

## الخطوة 2: تحسين دقة OCR – ما بعد معالجة البنية الخام

OCR ليس مثاليًا—خاصةً عندما تحتوي الصورة المصدر على خطوط باهتة أو خطوط غير مألوفة. هنا يأتي دور AI خفيف (أو حتى سكريبت قائم على القواعد) لتنظيف المخرجات، تصحيح الأخطاء الشائعة، وإضافة السياق المفقود.

```python
def enhance_structure(structured_result):
    """
    Runs a post‑processor that fixes typical OCR errors
    (e.g., 'O' vs '0', merged cells) and adds semantic context.
    """
    # Step 2: Enhance the raw OCR structure with AI (adds context, corrects errors)
    enhanced_structure = ai.run_postprocessor(structured_result)
    return enhanced_structure
```

**لماذا هذا مهم:**  
قد يصنف جدول OCR الخام عنوانًا كـ “Q1 2022” لكنه يخطئ في قراءة “1” كـ “l”. يمكن لطبقة AI تعلم هذه الأنماط من مجموعة تدريب صغيرة وإخراج جدول أنظف. حتى خوارزمية بسيطة (استبدال “l” المنعزلة بـ “1” عندما تكون محاطة بأرقام) يمكنها رفع **تحسين دقة OCR** بشكل كبير.

> **حالة حافة شائعة:** إذا كان الجدول يحتوي على خلايا مدمجة، قد يكرر OCR المحتوى عبر الأعمدة. يجب على ما بعد المعالجة اكتشاف الخلايا المتطابقة المتجاورة ودمجها.

---

## الخطوة 3: استخراج بيانات جدول من صورة – التكرار على الصفوف وعرض نص الخلايا

الآن بعد أن أصبح لدينا هيكل منظم، يصبح استخراج البيانات أمرًا بسيطًا. سنقوم بالتكرار على أول جدول تم اكتشافه ونطبع كل صف كقائمة من قيم الخلايا.

```python
def print_table(enhanced_structure):
    """
    Prints each row of the first detected table.
    """
    # Step 3: Iterate over the rows of the first detected table and display cell text
    for row in enhanced_structure.tables[0].rows:
        print([cell.text for cell in row.cells])

if __name__ == "__main__":
    # Path to your image file
    image_path = "YOUR_DIRECTORY/table.png"

    # Run the pipeline
    raw = recognize_image(image_path)
    cleaned = enhance_structure(raw)
    print_table(cleaned)
```

**ما ستراه:**  
باستخدام `table.png` الذي يحتوي على شبكة بسيطة 3 × 2، قد يكون الخرج كالتالي:

```
['Product', 'Price']
['Apple', '$1.20']
['Banana', '$0.80']
```

إذا فشل OCR في التعرف على عنوان، من المحتمل أن يقوم معالج AI بإدخاله بناءً على السياق المحيط، وبالتالي يصبح الجدول النهائي جاهزًا لـ pandas أو أي تحليل لاحق.

> **احذر من:** الصفوف الفارغة في نهاية الجدول. بعض محركات OCR تضيف صفًا فارغًا عندما تواجه مسافات بيضاء. يمكن تصفية ذلك باستخدام شرط `if any(cell.text for cell in row.cells):`.

---

## إضافة: ما بعد ذلك – حفظ الجدول كملف CSV أو DataFrame

معظم سير العمل الواقعي يحتاج البيانات في ملف CSV أو DataFrame من pandas. إليك مقتطفًا صغيرًا يحول الصفوف المطبوعة إلى CSV دون مغادرة عملية بايثون.

```python
import csv
import pandas as pd

def save_to_csv(enhanced_structure, output_path="output.csv"):
    rows = [
        [cell.text for cell in row.cells]
        for row in enhanced_structure.tables[0].rows
        if any(cell.text for cell in row.cells)  # Skip empty rows
    ]
    # Write CSV
    with open(output_path, "w", newline="", encoding="utf-8") as f:
        writer = csv.writer(f)
        writer.writerows(rows)

    # Also return a DataFrame for immediate use
    return pd.DataFrame(rows[1:], columns=rows[0])  # Assume first row is header

# Example usage:
df = save_to_csv(cleaned, "my_table.csv")
print(df.head())
```

الآن لديك DataFrame جاهز للاستخدام، مثالي للتحليل، التصور، أو إمداده إلى نموذج تعلم آلي.

---

## الأسئلة المتكررة (FAQ)

**س: هل يعمل هذا مع ملفات PDF التي تحتوي على جداول ممسوحة ضوئيًا؟**  
ج: بالتأكيد—ما عليك سوى تحويل كل صفحة PDF إلى صورة (مثلاً باستخدام `pdf2image`) وإدخال ملفات PNG الناتجة في نفس الخطوات.

**س: جدولي يحتوي على خلايا رأس مدمجة؛ هل سيصلحها AI؟**  
ج: معالج ما بعد المعالجة المدرب جيدًا يمكنه اكتشاف الخلايا المدمجة عبر فحص امتدادات الخلايا. إذا كنت تستخدم نهجًا قائمًا على القواعد، ابحث عن نص متطابق عبر الخلايا المتجاورة ودمجها.

**س: ماذا لو أعاد OCR عدة جداول؟**  
ج: `enhanced_structure.tables` هي قائمة. يمكنك التكرار عليها، أو اختيار الجدول الذي يحتوي على أكبر عدد من الصفوف/الأعمدة—حسب ما يتناسب مع توقعاتك.

**س: هل يمكنني استبدال معالج AI بتنظيف بسيط باستخدام regex؟**  
ج: نعم. للعديد من المشاريع يكفي عدد قليل من استبدالات regex (مثل تحويل “O” → “0”). المفتاح هو تشغيل *شيء* بعد OCR لتحسين **تحسين دقة OCR**.

---

## الخاتمة

لقد أظهرنا للتو كيفية **تحويل الصورة إلى جدول** باستخدام بايثون، من التعرف الأولي عبر OCR إلى بنية محسنة بالذكاء الاصطناعي وجاهزة للاستخدام. خط الأنابيب المكوّن من ثلاث خطوات—التعرف، التحسين، الاستخراج—يغطي التحديات الأساسية لـ **استخراج جدول من صورة** ويظهر طرقًا عملية لـ **تحسين دقة OCR**.

احصل على لقطة شاشة لأي جدول، وجه السكريبت إليها، وستحصل على CSV أو DataFrame في ثوانٍ. من هنا يمكنك استكشاف حيل أكثر تقدمًا: ملفات PDF متعددة الصفحات، جداول مكتوبة يدويًا، أو حتى تدفقات كاميرا في الوقت الحقيقي.

هل أنت مستعد للتحدي التالي؟ جرّب تغذية الأنابيب بإطارات فيديو مباشرة، أو جرب معالجات ما بعد المعالجة القائمة على نماذج اللغة التي يمكنها استنتاج أسماء الأعمدة المفقودة. السماء هي الحد، والآن لديك أساس قوي للبناء عليه.

برمجة سعيدة! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}