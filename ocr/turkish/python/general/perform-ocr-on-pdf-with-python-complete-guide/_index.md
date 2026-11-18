---
category: general
date: 2026-06-25
description: Python kullanarak PDF üzerinde OCR yapın—OCR için PDF'yi nasıl yükleyeceğinizi,
  PDF sayfalarından metin nasıl çıkaracağınızı ve tanınan metni verimli bir şekilde
  önizleyeceğinizi öğrenin.
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF pages
- load PDF for OCR
- how to OCR large PDF
- preview recognized text
language: tr
og_description: Python'da PDF üzerinde OCR gerçekleştirin. Bu rehber, OCR için PDF'yi
  nasıl yükleyeceğinizi, PDF sayfalarından metin çıkaracağınızı ve tanınan metni hızlıca
  önizleyeceğinizi gösterir.
og_title: Python ile PDF'de OCR Yapın – Adım Adım Eğitim
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  headline: Perform OCR on PDF with Python – Complete Guide
  type: TechArticle
- description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  name: Perform OCR on PDF with Python – Complete Guide
  steps:
  - name: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
    text: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
  - name: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
    text: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
  - name: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
    text: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
  - name: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
    text: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Python ile PDF'de OCR Yapın – Tam Rehber
url: /tr/python/general/perform-ocr-on-pdf-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF üzerinde OCR İşlemi Yapma – Python ile Tam Kılavuz

Hiç **perform OCR on PDF** dosyalarıyla çalışmanız gerekti ama nereden başlayacağınızı bilemediniz mi? Belki taranmış sözleşmelerden oluşan bir dağınız var ya da her zamanki metin‑çıkarıcıyla iş birliği yapmayan tek bir kalın el kitabınız var. Kısacası **load PDF for OCR** yapmak, metni çıkarmak ve hızlı bir ön izleme elde etmek istiyorsunuz—makinenizin belleğini zorlamadan.

Doğru yerdesiniz. Bu öğreticide **extracts text from PDF pages** yapan tam işlevsel bir Python betiğini adım adım inceleyecek, **preview recognized text** nasıl yapılır gösterecek ve **how to OCR large PDF** dosyalarını verimli bir şekilde ele almanın klasik sorununu çözeceğiz.

Sonunda çalıştırmaya hazır bir program, her yapılandırma ayarının net bir açıklaması ve yeni başlayanların sıkça takıldığı tuzaklardan kaçınmanız için birkaç ipucu elde edeceksiniz.

---

## Öğrenecekleriniz

- `aocr` kütüphanesini kullanarak **load PDF for OCR** nasıl yapılır.
- PDF sayfalarında **perform OCR on PDF** adımlarını tek tek nasıl yapacağınız.
- Bellek kullanımını kontrol altında tutarak **extract text from PDF pages** nasıl yapılır.
- Sonuçları doğrulamak için **preview recognized text** nasıl ön izlenir.
- **large PDFs**'i RAM tüketmeden nasıl işleyebileceğiniz stratejileri.

> **Tip:** Bu kılavuz, Python 3.9+ yüklü olduğunu ve sanal ortamlarla temel bir aşinalığınız olduğunu varsayar. Python'a yeniyseniz, önce bir virtualenv oluşturun—bana güvenin, ileride baş ağrısını önler.

---

## Önkoşullar

| Gereksinim | Neden Önemli |
|-------------|----------------|
| `aocr` Python paketi (veya uyumlu herhangi bir OCR motoru) | Script boyunca kullanılan `OcrEngine` sınıfını sağlar. |
| `pip` ve bir sanal ortam | Bağımlılıkların sistem Python'undan izole kalmasını sağlar. |
| Geçici görüntü çıkartmaları için yeterli disk alanı | Bazı OCR motorları sayfa görüntülerini işleme öncesi diske yazar. |
| Opsiyonel: `tqdm` ilerleme çubukları için | **how to OCR large PDF** işleriyle uğraşırken kullanıcı deneyimini iyileştirir. |

Gerekli paketleri şu şekilde kurun:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate
pip install aocr tqdm
```

PDF'niz şifre korumalıysa, şifreyi daha sonra sağlamanız gerekir—“Edge Cases” bölümüne bakın.

---

## Adım 1: PDF Üzerinde OCR Yapma – Motoru Kurma

İlk olarak bir OCR motoru örneğine ihtiyacımız var. Bunu, her sayfanın görüntüsünü okuyup düz metin üretecek beyin olarak düşünebilirsiniz.

```python
import aocr                     # The OCR library
from tqdm import tqdm           # Optional, for a nice progress bar

def create_engine():
    """
    Initialise the OcrEngine with sensible defaults.
    Returns the configured engine ready for processing.
    """
    engine = aocr.OcrEngine()
    # Limit memory usage – crucial when tackling how to OCR large PDF files
    engine.max_memory_mb = 200               # 200 MB cap, adjust if needed
    # Choose a recognition mode that matches your source material
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine
```

> **Why set `max_memory_mb`?**  
> OCR motorları genellikle sayfa görüntülerini RAM'de önbelleğe alır. Belleği sınırlayarak 500 sayfalık bir sözleşmede betiğinizin çökmesini önlersiniz.

---

## Adım 2: PDF'yi OCR İçin Yükleme ve Ayarları Yapılandırma

Şimdi gerçekten **load PDF for OCR** yapıyoruz. Yol mutlak ya da göreli olabilir; dosyanın mevcut olduğundan emin olun.

```python
def load_pdf(engine, pdf_path):
    """
    Loads the PDF into the OCR engine.
    Raises FileNotFoundError if the file does not exist.
    """
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages ready.")
    except Exception as e:
        raise RuntimeError(f"Failed to load PDF: {e}")
```

PDF şifreli ise, `engine.load_pdf` genellikle bir istisna fırlatır. Bu durumda `engine.load_pdf(pdf_path, password="secret")` çağrısı yapabilirsiniz—daha fazla detay için ilerleyen bölüme bakın.

---

## Adım 3: PDF Sayfalarından Metin Çıkarma – Çekirdek Döngü

Burada **perform OCR on PDF** sayfa sayfa gerçekleşir. İlk birkaç yüz karakteri **preview recognized text** olarak göstererek her şeyin doğru çalıştığını doğrulayabilirsiniz.

```python
def ocr_pages(engine, preview_len=200):
    """
    Iterates over each page, runs OCR, and yields the recognized text.
    Also prints a short preview for each page.
    """
    for page_index in tqdm(range(engine.page_count), desc="Processing pages"):
        # Select the current page – essential for multi‑page PDFs
        engine.select_page(page_index)

        # Perform the actual OCR
        page_text = engine.recognize()

        # Preview the first `preview_len` characters (helps with debugging)
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))

        yield page_text
```

> **Pro tip:** `tqdm` ilerleme çubuğu görsel bir ipucu verir, özellikle **how to OCR large PDF** belgeleri dakikalar süren işlemlerde çok faydalıdır.

---

## Adım 4: Hepsini Bir Araya Getirme – Hazır‑Çalıştırılabilir Script

Aşağıda tam, çalıştırılabilir örnek yer alıyor. `pdf_ocr.py` olarak kaydedin ve `python pdf_ocr.py path/to/your/file.pdf` komutuyla çalıştırın.

```python
#!/usr/bin/env python3
"""
Complete script to perform OCR on PDF, extract text from PDF pages,
and preview recognized text. Works for both small and large PDFs.
"""

import sys
import aocr
from tqdm import tqdm

def create_engine():
    engine = aocr.OcrEngine()
    engine.max_memory_mb = 200
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine

def load_pdf(engine, pdf_path):
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages.")
    except Exception as exc:
        raise RuntimeError(f"Unable to load PDF: {exc}")

def ocr_pages(engine, preview_len=200):
    for page_index in tqdm(range(engine.page_count), desc="OCR progress"):
        engine.select_page(page_index)
        page_text = engine.recognize()
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))
        yield page_text

def main(pdf_path):
    engine = create_engine()
    load_pdf(engine, pdf_path)

    all_text = []
    for txt in ocr_pages(engine):
        all_text.append(txt)

    # Optional: write the combined output to a .txt file
    out_path = pdf_path.rsplit(".", 1)[0] + "_ocr.txt"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write("\n\n".join(all_text))
    print(f"\n✅ OCR complete. Full text saved to: {out_path}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python pdf_ocr.py <path_to_pdf>")
        sys.exit(1)
    pdf_file = sys.argv[1]
    main(pdf_file)
```

### Beklenen Çıktı (alıntı)

```
✅ Loaded 'large_contract.pdf' – 342 pages.

--- Page 1 Preview ---
Contract Agreement between Party A and Party B ... 

--- Page 2 Preview ---
Recitals: Whereas, the parties desire to ...

...
✅ OCR complete. Full text saved to: large_contract_ocr.txt
```

Her sayfa için kısa bir ön izleme göreceksiniz, ardından birleştirilmiş metin dosyasının yazıldığına dair son bir onay mesajı alacaksınız.

---

## Kenar Durumları ve Pratik İpuçları

| Durum | Ne Yapmalı |
|-----------|------------|
| **Encrypted PDF** | Şifreyi geçin: `engine.load_pdf(pdf_path, password="mySecret")`. |
| **Very large PDF (> 1000 pages)** | `max_memory_mb` değerini dikkatli artırın, ya da parçalar halinde işleyin (ör. bir seferde 200 sayfa). |
| **Mixed content (printed + handwritten)** | Kütüphane destekliyorsa `engine.recognition_mode` değerini `aocr.RecognitionMode.MIXED` olarak değiştirin. |
| **Missing fonts or poor scan quality** | `recognize()` çağırmadan önce sayfaları bir görüntü iyileştirme kütüphanesi (ör. Pillow) ile ön işleme tabi tutun. |
| **Out‑of‑memory crashes** | `preview_len` değerini azaltın ya da tüm metni bir listede tutmak yerine her sayfanın metnini doğrudan diske yazın. |

---

## Büyük PDF'leri Verimli Şekilde OCR Yapma – İleri Düzey Stratejiler

**how to OCR large PDF** ile uğraşırken hız ve kararlılık kritik hâle gelir. Betiğe ekleyebileceğiniz birkaç püf noktası:

1. **Sayfa başına paralelleştirme** – OCR motoru thread‑safe ise `concurrent.futures.ThreadPoolExecutor` kullanın.
2. **Ara görüntüleri önbellekle** – Bazı motorlar rasterleştirilmiş sayfaları SSD'ye kaydetmenize izin verir, yeniden çalıştırmalarda CPU yükünü büyük ölçüde azaltır.
3. **Çıktıyı toplu olarak yaz** – Python listesine eklemek yerine çıktı dosyasını bir kez açın ve her sayfanın metnini hazır olur olmaz yazın.
4. **DPI'yi ayarla** – Rasterleştirme sırasında DPI'yi düşürmek belleği azaltır ancak doğruluğu etkileyebilir; uygun bir değer bulun (genellikle 200‑300 DPI).

Aşağıda OCR adımını paralelleştirmenin hızlı bir örneği (opsiyonel, kullanmak için yorum satırını kaldırın) yer alıyor:

```python
# from concurrent.futures import ThreadPoolExecutor

# def ocr_page(engine, idx):
#     engine.select_page(idx)
#     return engine.recognize()

# with ThreadPoolExecutor(max_workers=4) as executor:
#     results = list(tqdm(executor.map(lambda i: ocr_page(engine, i),
#                                    range(engine.page_count)),
#                     total=engine.page_count,
#                     desc="Parallel OCR"))
```

Unutmayın: paralellik CPU kullanımını artırabilir, bu yüzden uzun çalışmalarda sisteminizin sıcaklığını izleyin.

---

## Sıkça Sorulan Sorular

**Q: Bu scripti Tesseract gibi diğer OCR kütüphaneleriyle kullanabilir miyim?**  
A: Kesinlikle. `aocr` çağrılarını `pytesseract.image_to` ile değiştirin.

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Aspose.OCR ile .NET'te PDF OCR Nasıl Yapılır](/ocr/english/net/text-recognition/recognize-pdf/)
- [Aspose OCR Kullanarak Akıştan Görüntü Metni Çıkarma Nasıl Yapılır](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Java için Aspose.OCR ile URL'den Görüntü Metni Çıkarma](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}