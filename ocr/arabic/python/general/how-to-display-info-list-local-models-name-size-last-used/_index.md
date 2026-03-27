---
category: general
date: 2026-01-12
description: تعلم كيفية عرض المعلومات من AsposeAI عن طريق سرد النماذج المحلية، مع
  إظهار اسم النموذج وحجمه وتاريخ ووقت الاستخدام الأخير في مثال بايثون واضح.
draft: false
keywords:
- how to display info
- list local models
- display model name
- show model size
- show last used
language: ar
og_description: 'كيفية عرض المعلومات من AsposeAI: سرد النماذج المحلية، عرض اسم النموذج،
  حجمه، وتاريخ ووقت آخر استخدام مع دليل كامل بلغة بايثون.'
og_title: كيفية عرض المعلومات – قائمة النماذج المحلية، الاسم، الحجم، آخر استخدام
tags:
- AsposeAI
- Python
- Model Management
title: كيفية عرض المعلومات – قائمة النماذج المحلية، الاسم، الحجم، آخر استخدام
url: /ar/python/general/how-to-display-info-list-local-models-name-size-last-used/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية عرض المعلومات – قائمة النماذج المحلية، الاسم، الحجم، آخر استخدام

هل تساءلت يومًا **كيف تعرض المعلومات** من تثبيت AsposeAI الخاص بك دون الحاجة للغوص في السجلات أو الواجهة؟ لست وحدك. في العديد من خطوط أنابيب علم البيانات، أول شيء تحتاجه هو نظرة سريعة على النماذج الموجودة على جهازك، ما هي أسماؤها، حجمها، ومتى تم استخدامها آخر مرة.

هذا بالضبط ما سنغطيه: مقتطف Python مختصر من البداية إلى النهاية **يسرد النماذج المحلية**، ثم **يعرض اسم النموذج**، **يظهر حجم النموذج**، و**يعرض طابع الوقت لآخر استخدام**. لا مكتبات خارجية، لا سحر مخفي—فقط عميل AsposeAI الذي لديك بالفعل.

بنهاية هذا الدرس ستتمكن من إدراج الكود في أي سكريبت، تشغيله، والحصول فورًا على جدول منظم للنماذج المخزنة محليًا. إنه مثالي للتحقق من صحة البيئات، بناء لوحات مراقبة الصحة، أو مجرد إشباع الفضول حول ما يختبئ على القرص.

## المتطلبات المسبقة

- Python 3.8 أو أحدث (المثال يستخدم f‑strings، لذا 3.6+ ضروري)
- حزمة `asposeai` مثبتة (`pip install asposeai`)
- ترخيص AsposeAI صالح أو مفتاح تجريبي (العميل سيقرأ الاعتمادات من المتغيرات البيئية أو ملف إعداد)

إذا كنت قد تحققت من هذه النقاط، عظيم—لنبدأ.

## الخطوة 1: كيفية عرض المعلومات – تهيئة عميل AsposeAI

قبل أن نتمكن من **سرد النماذج المحلية**، نحتاج إلى كائن عميل يتواصل مع بيئة تشغيل AsposeAI. هذه الخطوة هي الأساس؛ بدونها سيظهر خطأ `NameError` في باقي الكود.

```python
# Step 1: Create an instance of the AsposeAI client
# The client automatically reads credentials from the environment
aspose_ai = AsposeAI()
```

*لماذا هذا مهم*: تهيئة العميل تُنشئ جلسة مع محرك الاستدلال المحلي، وتحمل أي مكتبات أصلية ضرورية. كما تتحقق من أن ترخيصك فعال، مما يمنع الأخطاء الغامضة لاحقًا عند استعلام النماذج.

> **نصيحة احترافية**: إذا كنت تشغل هذا على خادم CI، ضع المتغير `ASPOSEAI_LICENSE` في البيئة حتى يتمكن العميل من البدء دون مطالبات تفاعلية.

## الخطوة 2: قائمة النماذج المحلية – استرجاع النماذج المتاحة

الآن بعد أن أصبح العميل جاهزًا، يمكننا **سرد النماذج المحلية**. تُعيد طريقة `list_local()` مجموعة من الكائنات، كل منها ي expose خصائص مثل `name`، `size_mb`، و `last_used`.

```python
# Step 2: Retrieve the list of locally available models
local_models = aspose_ai.list_local()
```

*ما يحدث في الخلفية*: `list_local()` تفحص الدليل الذي يخزن فيه AsposeAI ملفات النماذج (`~/.asposeai/models` افتراضيًا) وتُنشئ كائنات بيانات خفيفة. هذا سريع لأنه لا يحمل أوزان النموذج—فقط يقرأ ملف JSON صغير للبيانات الوصفية.

إذا تساءلت يومًا ما إذا كان نموذج معين مُخزنًا مسبقًا، فإن هذه الدالة هي أسرع طريقة للتأكد.

## الخطوة 3: عرض اسم النموذج، إظهار حجم النموذج، وإظهار آخر استخدام

مع النماذج في المتناول، نُظهر **المعلومات** أخيرًا عبر التكرار على المجموعة وطباعة كل سمة. هنا ن **نعرض اسم النموذج**، **نظهر حجم النموذج**، و **نظهر آخر استخدام** في سطر واحد منسق.

```python
# Step 3: Print each model's name, size (in MB), and last‑used timestamp
print("Available local models:")
print("-" * 50)
for model_info in local_models:
    # Using an f‑string to format the output cleanly
    print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
```

**الناتج المتوقع** (ستختلف طوابع الوقت لديك):

```
Available local models:
--------------------------------------------------
gpt‑tiny‑en – 120 MB – last used 2025-11-02 14:23:11
bert‑base‑fr – 420 MB – last used 2025-10-18 09:07:45
whisper‑large‑audio – 1580 MB – last used 2025-09-30 22:41:02
```

*لماذا نصّغه بهذه الطريقة*: الشرطة (`–`) تفصل الحقول لتسهيل القراءة، وسطر العنوان يجعل مخرجات الكونسول سهلة المسح. إذا احتجت تنسيقًا قابلًا للقراءة آليًا لاحقًا (CSV، JSON)، يمكنك بسهولة استبدال استدعاء `print` بـ `writer.writerow` أو `json.dump`.

### معالجة الحالات الحدية

- **لا توجد نماذج مخزنة** – `list_local()` تُعيد قائمة فارغة. سيتخطى الحلقة ببساطة، وستحصل فقط على سطر العنوان. قد ترغب في إضافة حماية:

  ```python
  if not local_models:
      print("No local models found. Use aspose_ai.download(...) to fetch one.")
  ```

- **خصائص مفقودة** – في حالات نادرة قد يكون ملف البيانات الوصفية تالفًا. الوصول إلى `model_info.last_used` قد يرفع `AttributeError`. غلف الطباعة بـ `try/except` إذا توقعت مثل هذه المشكلات.

- **دليل نماذج كبير** – إذا كان لديك مئات النماذج، فكر في تقسيم المخرجات أو الكتابة إلى ملف بدلًا من الطباعة على الكونسول.

## ملخص بصري (اختياري)

إذا كنت تفضّل إشارة بصرية سريعة، يوضح المخطط أدناه تدفق العملية من تهيئة العميل إلى العرض النهائي.  

![مخطط يوضح كيفية عرض المعلومات من عميل AsposeAI](/images/how-to-display-info.png "مخطط كيفية عرض المعلومات")

*نص بديل*: **كيفية عرض المعلومات** – مخطط يوضح تهيئة عميل AsposeAI، سرد النماذج، وعرض المعلومات.

## السكريبت الكامل العامل

بتجميع كل ما سبق، إليك السكريبت الكامل الجاهز للتنفيذ:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
How to display info from AsposeAI:
List local models and show each model's name, size, and last‑used timestamp.
"""

from asposeai import AsposeAI

def main():
    # Initialize client
    aspose_ai = AsposeAI()

    # Retrieve local models
    local_models = aspose_ai.list_local()

    # Header
    print("Available local models:")
    print("-" * 50)

    if not local_models:
        print("No local models found. Use aspose_ai.download(...) to fetch one.")
        return

    # Display each model's details
    for model_info in local_models:
        try:
            print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
        except AttributeError:
            # Fallback if any attribute is missing
            print(f"{model_info.name} – info incomplete")

if __name__ == "__main__":
    main()
```

احفظه باسم `list_models.py`، اجعله قابلًا للتنفيذ (`chmod +x list_models.py`)، ثم شغّله:

```bash
./list_models.py
```

سترى القائمة المنظمة التي تم عرضها سابقًا.

## الخلاصة

لقد استعرضنا **كيفية عرض المعلومات** من AsposeAI عبر **سرد النماذج المحلية**، ثم **عرض اسم النموذج**، **إظهار حجم النموذج**، و**إظهار طابع الوقت لآخر استخدام**. النهج خفيف الوزن، يتطلب فقط حزمة `asposeai` القياسية، ويمكن إدراجه في أي خط أنابيب أتمتة أو جلسة تصحيح.

من هنا يمكنك:

- تصدير المخرجات إلى CSV للتحليل في جداول البيانات (وحدة `csv`).
- إمداد طوابع الوقت إلى لوحة مراقبة للتنبيه عند وجود نماذج قديمة.
- دمج هذا السكريبت مع `aspose_ai.download()` لتحديث النماذج التي لم تُستخدم منذ فترة.

تذكر، الرؤية الواضحة لمخزون نماذجك توفر الوقت، تقلل من تراكم التخزين، وتُبقي خدمات الذكاء الاصطناعي تعمل بسلاسة. جرّب السكريبت، عدّل التنسيق حسب رغبتك، واجعله جزءًا أساسيًا من أدواتك.

برمجة سعيدة، ولتظل نماذجك دائمًا محدثة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}