---
category: general
date: 2026-06-22
description: دورة تعليمية للـ OCR الدفعي في بايثون تُظهر كيفية تشغيل OCR متعدد الخيوط
  على مجلد من صور PNG باستخدام Tesseract و pathlib. تعلم OCR للصور الدفعي بسرعة في
  بايثون.
draft: false
keywords:
- python batch ocr tutorial
- multithreaded OCR in Python
- tesseract OCR batch processing
- pathlib image handling
- OCR thread count optimization
language: ar
og_description: يُرشدك برنامج تعليمي لمعالجة OCR دفعة Python عبر سكريبت كامل قابل
  للتنفيذ يعالج العديد من ملفات PNG باستخدام Tesseract عبر عدة خيوط.
og_title: دليل بايثون للمعالجة الجماعية للـ OCR – OCR متعدد الخيوط سريع للصور بصيغة
  PNG
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  headline: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  type: TechArticle
- description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  name: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  steps:
  - name: '**Collects** every PNG with **pathlib image handling**.'
    text: '**Collects** every PNG with **pathlib image handling**.'
  - name: '**Spins up** a **multithreaded OCR in Python** worker pool.'
    text: '**Spins up** a **multithreaded OCR in Python** worker pool.'
  - name: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
    text: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
  - name: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
    text: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
  type: HowTo
tags:
- OCR
- Python
- Batch Processing
title: 'دليل بايثون للمعالجة الدفعية للتعرف الضوئي على الحروف: معالجة عدة ملفات PNG
  بكفاءة'
url: /ar/python-java/general/python-batch-ocr-tutorial-process-multiple-pngs-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# python batch ocr tutorial – OCR متعدد الخيوط سريع لصور PNG

هل تساءلت يومًا كيف تقوم بـ **python batch ocr tutorial** عبر مئات لقطات شاشة PNG دون أن ترى معالجك يذوب؟ لست وحدك. سواءً كنت تقوم برقمنة النماذج الممسوحة، أو استخراج النص من الإيصالات، أو بناء أرشيف قابل للبحث، فإن خط أنابيب OCR الجماعي القوي يوفر لك ساعات.

في هذا الدليل سننشئ سكريبتًا صغيرًا لكنه قوي يجمع كل ملفات `*.png` في مجلد، يمررها إلى Tesseract عبر معالج متعدد الخيوط، ويضع نتائج النص العادي في دليل إخراج منظم. لا مكتبات غامضة—فقط `pathlib`، `concurrent.futures`، و`pytesseract` الموثوق دائمًا. في النهاية ستحصل على **python batch ocr tutorial** يمكنك نسخه ولصقه في أي مشروع.

## ما ستتعلمه

- كيفية جمع ملفات الصور باستخدام **pathlib image handling**  
- إعداد مجموعة عمل **multithreaded OCR in Python**  
- ضبط **OCR thread count optimization** لمعالجاتك  
- حفظ كل نتيجة باستخدام نظام تسمية واضح للبحث لاحقًا  
- تشغيل كل ذلك كسكريبت واحد مستقل  

## المتطلبات المسبقة (ما تحتاجه أولاً)

| المتطلب | لماذا يهم |
|-------------|----------------|
| Python 3.9+ | الصياغة الحديثة (`pathlib`, f‑strings) |
| Tesseract 5.x مثبت ومتاح في `PATH` | محرك OCR وراء `pytesseract` |
| `pytesseract` (`pip install pytesseract`) | مغلف Python لـ Tesseract |
| `Pillow` (`pip install pillow`) | تحميل الصور لـ Tesseract |
| مجلد من ملفات PNG تريد معالجتها | هدف **tesseract OCR batch processing** الخاص بنا |

> **نصيحة احترافية:** إذا كنت على Windows، أضف `C:\Program Files\Tesseract-OCR` إلى `PATH` النظامي حتى يتمكن `pytesseract` من العثور على الملف التنفيذي تلقائيًا.

---

## الخطوة 1 – جمع جميع صور PNG (باستخدام pathlib)

أولًا: نحتاج إلى قائمة بكل صورة نعتزم تشغيل OCR عليها. تجعل `pathlib` ذلك سطرًا واحدًا وتبقي الكود مستقلًا عن نظام التشغيل.

```python
import pathlib

# Adjust the path to point at your source folder
source_dir = pathlib.Path("YOUR_DIRECTORY/batch_images")
image_files = list(source_dir.glob("*.png"))

print(f"Found {len(image_files)} PNG files to process.")
```

*لماذا `pathlib`؟* فهو يخفف الفروقات بين شرطات Windows وشرطات Unix، مما يسمح بتشغيل نفس السكريبت في أي مكان. هذا هو أساس **pathlib image handling** في دليلنا.

---

## الخطوة 2 – تعريف فئة معالج OCR جماعي بسيطة

فيما يلي غلاف خفيف الوزن يخفي تفاصيل الخيوط. إنه يعكس الشيفرة الزائفة التي رأيتها سابقًا ولكنه يعمل بالكامل.

```python
import concurrent.futures
import pytesseract
from PIL import Image
import os

class BatchOcrProcessor:
    """Encapsulates multithreaded OCR logic."""

    def __init__(self):
        self.thread_count = os.cpu_count() or 4  # sensible default
        self.output_folder = pathlib.Path("ocr_results")
        self.output_folder.mkdir(parents=True, exist_ok=True)

    def set_thread_count(self, count: int):
        """Adjust the number of worker threads (OCR thread count optimization)."""
        if count < 1:
            raise ValueError("Thread count must be at least 1")
        self.thread_count = count
        print(f"Thread pool size set to {self.thread_count}")

    def set_output_folder(self, folder: str):
        """Where each OCR result will be saved (tesseract OCR batch processing)."""
        self.output_folder = pathlib.Path(folder)
        self.output_folder.mkdir(parents=True, exist_ok=True)
        print(f"Output folder set to {self.output_folder}")

    def _process_single(self, image_path: pathlib.Path):
        """Run OCR on a single image and write the text file."""
        try:
            img = Image.open(image_path)
            text = pytesseract.image_to_string(img)
            out_file = self.output_folder / f"{image_path.stem}.txt"
            out_file.write_text(text, encoding="utf-8")
            return f"✅ {image_path.name} → {out_file.name}"
        except Exception as exc:
            return f"❌ {image_path.name} failed: {exc}"

    def process(self, image_paths):
        """Run OCR on the entire batch using a thread pool."""
        print("🚀 Starting batch OCR...")
        with concurrent.futures.ThreadPoolExecutor(max_workers=self.thread_count) as executor:
            results = list(executor.map(self._process_single, image_paths))
        for line in results:
            print(line)
        print("🏁 Batch OCR completed.")
```

**شرح الاختيارات الرئيسية**

- **ThreadPoolExecutor** يمنحنا تعدد خيوط حقيقي للمهام المرتبطة بـ I/O مثل قراءة الملفات واستدعاء برنامج Tesseract الخارجي.  
- طريقة `set_thread_count` هي المكان الذي يمكنك فيه تجربة **OCR thread count optimization**؛ عادةً ما تعني المزيد من الخيوط سرعات أعلى حتى تصل إلى نقطة تشبع نوى المعالج.  
- كل صورة تنتج ملف `.txt` مسمى بعد اسم PNG الأصلي—مثالي للفهرسة أو البحث لاحقًا.

---

## الخطوة 3 – ربط كل شيء معًا

الآن نقوم بإنشاء كائن المعالج، نضبط عدد الخيوط، نشير إلى مجلد الإخراج، وأخيرًا نمرره قائمة الصور.

```python
if __name__ == "__main__":
    # 1️⃣ Gather PNGs (already done above)
    # 2️⃣ Create processor instance
    ocr_processor = BatchOcrProcessor()

    # 3️⃣ Configure thread pool – feel free to change 8 → your core count
    ocr_processor.set_thread_count(8)   # multithreaded OCR in Python

    # 4️⃣ Choose where results land
    ocr_processor.set_output_folder("YOUR_DIRECTORY/ocr_results")

    # 5️⃣ Run the batch – this call blocks until everything is done
    ocr_processor.process(image_files)

    # 6️⃣ All done – a friendly console message
    print("✅ All images processed. Check the ocr_results folder.")
```

تشغيل السكريبت سينتج مخرجات مشابهة لـ:

```
Found 42 PNG files to process.
Thread pool size set to 8
Output folder set to YOUR_DIRECTORY/ocr_results
🚀 Starting batch OCR...
✅ invoice_001.png → invoice_001.txt
✅ receipt_2023-04-15.png → receipt_2023-04-15.txt
...
🏁 Batch OCR completed.
✅ All images processed. Check the ocr_results folder.
```

كل ملف `.txt` يحتوي على ناتج OCR الخام. افتح أي ملف وسترى النص المستخرج جاهزًا للفهرسة، تحليل المشاعر، أو أي شيء يأتي بعد ذلك.

---

## الخطوة 4 – المشكلات الشائعة وكيفية تجنبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| ملفات `.txt` فارغة | Tesseract لا يجد بيانات اللغة أو الصورة مظلمة جدًا | ثبت حزم اللغات (`tesseract-ocr-eng`) وقم بمعالجة الصور مسبقًا (زيادة التباين). |
| `UnicodeDecodeError` عند قراءة النتائج | الناتج يحتوي على أحرف غير UTF‑8 | اكتب الملفات باستخدام `encoding="utf-8"` (موجود بالفعل في الكود) أو استخدم `errors="ignore"` كحل سريع. |
| ارتفاع استهلاك المعالج دون تحسين السرعة | عدد الخيوط يتجاوز عدد الأنوية الفعلية | قلل `set_thread_count` إلى `os.cpu_count()` أو أقل. |
| `FileNotFoundError` عند فتح الصورة | المسار يحتوي على أحرف غير ASCII على Windows | أضف بادئة `r` للسلسلة أو استخدم كائنات `pathlib` مباشرة (كما نفعل). |

---

## الخطوة 5 – توسيع الدرس (الخطوات التالية)

- **إضافة معالجة مسبقة للصور** باستخدام OpenCV (`cv2`) لتحسين دقة OCR (مثل تصحيح الميل، العتبة).  
- **توزيع العمل عبر آلات متعددة** باستخدام `multiprocessing` أو طابور مهام بسيط مثل RabbitMQ لأحمال عمل ضخمة.  
- **دمج مع محرك بحث** (Elasticsearch) لجعل النص المستخرج قابلًا للبحث في الوقت الفعلي.  
- **استبدال Tesseract بواجهة برمجة تطبيقات OCR سحابية** (Google Vision، Azure Computer Vision) إذا كنت تحتاج إلى دقة أعلى للنصوص المكتوبة يدويًا.

كل هذه الأفكار تبنى على الأساس الذي لديك الآن: دليل **python batch ocr tutorial** نظيف يعمل مباشرةً.

---

## الخلاصة

لقد قمت الآن ببناء **python batch ocr tutorial** كامل يـ:

1. **يجمع** كل ملفات PNG باستخدام **pathlib image handling**.  
2. **ينشئ** مجموعة عمل **multithreaded OCR in Python**.  
3. **يحسن** عدد الخيوط وفقًا لمعداتك (**OCR thread count optimization**).  
4. **يكتب** كل نتيجة إلى مجلد مخصص (**tesseract OCR batch processing**).  

السكريبت جاهز للإدراج في أي خط أنابيب، سواءً كنت تعالج إيصالات، مستندات قانونية، أو جبل من لقطات الشاشة. العب بعدد الخيوط، أضف معالجة مسبقة للصور، أو اربط الناتج بقاعدة بيانات—الخيار لك.

هل لديك أسئلة؟ لا تتردد في التعليق أدناه، وبرمجة سعيدة!

![مخطط تدفق برنامج python batch ocr tutorial لمعالجة ملفات PNG متعددة بالتوازي](/images/python-batch-ocr-workflow.png){.center width=600 alt="دورة عمل python batch ocr tutorial"}

---

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [دورة Aspose OCR – التعرف الضوئي على الأحرف](/ocr/english/)
- [كيفية معالجة صور OCR دفعيًا باستخدام List في Aspose.OCR لـ .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [استخراج نص الصورة بـ C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}