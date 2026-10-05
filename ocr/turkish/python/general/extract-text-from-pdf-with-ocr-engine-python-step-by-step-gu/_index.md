---
category: general
date: 2026-01-12
description: OCR motoru Python kullanarak PDF'den metin çıkarma – OCR ile PDF nasıl
  okunur, OCR için görüntü nasıl yüklenir ve yapılandırılmış sonuçlar nasıl elde edilir
  öğrenin.
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load image for ocr
- use ocr engine python
language: tr
og_description: Python OCR motoru kullanarak PDF'den metin çıkarın. Bu öğreticide
  OCR ile PDF okuma, OCR için görüntü yükleme ve güvenilir sonuçlar elde etmek için
  Python OCR motorunu kullanma gösterilmektedir.
og_title: OCR Motoru Python ile PDF'den Metin Çıkarma – Tam Rehber
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Python OCR Motoru ile PDF'den Metin Çıkarma – Adım Adım Kılavuz
url: /tr/python/general/extract-text-from-pdf-with-ocr-engine-python-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Motoru Python ile PDF'den Metin Çıkarma – Tam Kılavuz

Hiç **PDF'den metin çıkarma** ihtiyacı duydunuz mu, ama dosya sadece taranmış bir görüntü mü? Yalnız değilsiniz. Gerçek dünyadaki birçok projede aldığınız PDF'de seçilebilir metin yoktur, bu yüzden tek yol **OCR ile PDF okuma**dır.  

Bu rehberde, **OCR için görüntü yükleme**, **OCR motoru Python** başlatma ve yapılandırılmış metni alıp sonraki işlem hatlarına besleme adımlarını gösteren pratik, uçtan uca bir çözümü adım adım inceleyeceğiz. Belirsiz referanslar yok, sadece bugün kopyalayıp yapıştırabileceğiniz tam, çalıştırılabilir bir örnek.

## Öğrenecekleriniz

- İhtiyacınız olan Python OCR kütüphanesini nasıl kurup içe aktaracağınızı.  
- Bir PDF dosyasından **OCR için görüntü yükleme** adımlarını tam olarak.  
- Motorun `recognize_structured()` metodunu nasıl çağırıp blok, satır ve kelimeler üzerinde nasıl döneceğinizi.  
- Düşük güvenilirlik sonuçları ve çok sayfalı PDF'lerle başa çıkma ipuçları.  

Bu öğreticinin sonunda, bir sayfa olsun ya da yüzlercesi, **PDF'den metin çıkarma** işlemini güvenilir bir şekilde yapan bir betiğe sahip olacaksınız.

---

![OCR motorunun bir PDF'i işleyip yapılandırılmış metin çıktısı vermesini gösteren diyagram.](images/ocr_flow.png "pdf'den metin çıkarma diyagramı")

*Görsel alt metni: pdf'den metin çıkarma diyagramı, OCR işleme adımlarını göstermektedir.*

## Ön Koşullar

- Python 3.9 veya daha yeni bir sürüm (kod f‑string ve tip ipuçları kullanıyor).  
- `OcrEngine` sınıfını sunan bir pip‑installable OCR paketi (örneğin, hayali bir `pyocr` kütüphanesi).  
- İşlemek istediğiniz PDF dosyası, yerel olarak kaydedilmiş (örnek: `form.pdf`).  

OCR kütüphaneniz eksikse, şu komutla kurun:

```bash
pip install pyocr   # replace with the actual package name you use
```

---

## Adım 1: PDF'den Metin Çıkarma – OCR Motorunu Kurma

**OCR ile PDF okuma** yapabilmek için önce bir motor örneği oluşturmalıyız. Motor, her pikseli inceleyip hangi karaktere karşılık geldiğine karar veren beyin gibidir.

```python
# Step 1: Import the OCR module and create an engine instance
import ocr  # or `import pyocr as ocr` depending on the package

# Create the OCR engine – this may load language models under the hood
ocr_engine = ocr.OcrEngine()
```

> **Neden önemli:** Motoru bir kez başlatmak, dil paketlerini birden çok dosya arasında yeniden yüklemeyi önleyerek zaman ve bellek tasarrufu sağlar.

---

## Adım 2: OCR için Görüntü Yükleme – PDF'nizi Hazırlama

PDF ham bir görüntü değildir, bu yüzden kütüphane genellikle ilk sayfayı (veya tüm sayfaları) OCR motorunun anlayabileceği bir görüntüye dönüştüren bir yardımcı sağlar.

```python
# Step 2: Load the PDF page(s) you want to process
# The `load_image` method accepts many formats – PDF, PNG, JPEG, etc.
pdf_path = "YOUR_DIRECTORY/form.pdf"
ocr_engine.load_image(pdf_path)
```

> **İpucu:** PDF'niz birden çok sayfa içeriyorsa, birçok OCR kütüphanesi `page=2` gibi bir parametre alır veya `engine.load_image(pdf_path, page=n)` ile döngü kurmanıza izin verir. Büyük belgeler için bellek dalgalanmalarını önlemek amacıyla sayfaları partiler halinde işlemek iyi bir yaklaşımdır.

---

## Adım 3: OCR Engine Python – Yapılandırılmış Metni Tanıma

Şimdi asıl iş burada gerçekleşir. `recognize_structured()` çağrısı, blok → satır → kelime hiyerarşisini, her birine dil, güven puanı ve sınırlayıcı kutular ekleyerek döndürür.

```python
# Step 3: Perform structured text recognition
structured_result = ocr_engine.recognize_structured()
```

> **Elde edeceğiniz:**  
> - `structured_result.blocks` – üst‑seviye kapsayıcılar (genellikle paragraflar veya sütunlar).  
> - Her blok `lines` içerir, her satır ise `words` içerir.  
> - Güven puanları, şüpheli sonuçları filtrelemenize olanak tanır.

---

## Adım 4: Sonuçlar Üzerinde Döngü – Blok, Satır ve Kelimelere Erişim

Aşağıdaki kompakt döngü, en faydalı bilgileri ekrana yazdırır. JSON, CSV üretmek ya da bir veritabanına beslemek için genişletebilirsiniz.

```python
# Step 4: Walk through the hierarchy and display key data
for block_idx, text_block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={text_block.language}, confidence={text_block.confidence:.2f}")

    # Show a sample line from the block, if any
    if text_block.lines:
        sample_line = text_block.lines[0]
        print(f"  Sample line: {sample_line.text}")

        # Show a sample word with its bounding box and confidence
        if sample_line.words:
            sample_word = sample_line.words[0]
            print(
                f"    Sample word: '{sample_word.text}' "
                f"bbox={sample_word.bounding_box} "
                f"conf={sample_word.confidence:.2f}"
            )
```

### Beklenen Çıktı

```
Block 1: language=en, confidence=0.97
  Sample line: Invoice Number: 2025-00123
    Sample word: 'Invoice' bbox=(12,34,78,90) conf=0.99
Block 2: language=en, confidence=0.94
  Sample line: Total Amount: $1,250.00
    Sample word: 'Total' bbox=(15,120,70,155) conf=0.96
...
```

> **Neden beğeneceksiniz:** Hiyerarşi, bir insanın sayfayı okuma şeklini taklit eder; bu da tabloları veya sütun düzenlerini daha sonra yeniden oluşturmayı kolaylaştırır.

---

## Adım 5: Kenar Durumlarıyla Baş Etme – Düşük Güven ve Çok Sayfalı PDF'ler

### Düşük Güvenli Kelimeler

Bir kelimenin güven puanı `0.70`'in altına düşerse, manuel inceleme için işaretlemek isteyebilirsiniz:

```python
LOW_CONF_THRESHOLD = 0.70

for block in structured_result.blocks:
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

### Tüm Sayfaları İşleme

```python
# Example: loop over every page in a multi‑page PDF
for page_number in range(ocr_engine.page_count):
    ocr_engine.load_image(pdf_path, page=page_number)
    result = ocr_engine.recognize_structured()
    # …process `result` just like we did above…
```

> **Pro ipucu:** OCR kütüphaneniz her seferinde görüntüyü yeniden oluşturuyorsa, ara görüntüleri PNG olarak önbelleğe alın – büyük partilerde saniyeler kazanabilirsiniz.

---

## Tam Çalışan Betik

Her şeyi bir araya getirdiğimizde, hemen çalıştırabileceğiniz tek bir dosya elde edersiniz:

```python
#!/usr/bin/env python3
"""
Extract text from PDF with OCR engine Python.
This script demonstrates loading a PDF, recognizing structured text,
and printing a concise summary of blocks, lines, and words.
"""

import ocr  # Replace with your actual OCR package import

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
PDF_PATH = "YOUR_DIRECTORY/form.pdf"
LOW_CONF_THRESHOLD = 0.70

# ----------------------------------------------------------------------
# Initialize OCR engine
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Load the PDF (first page by default)
# ----------------------------------------------------------------------
ocr_engine.load_image(PDF_PATH)

# ----------------------------------------------------------------------
# Recognize structured text
# ----------------------------------------------------------------------
structured_result = ocr_engine.recognize_structured()

# ----------------------------------------------------------------------
# Iterate and display results
# ----------------------------------------------------------------------
for block_idx, block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={block.language}, confidence={block.confidence:.2f}")

    if block.lines:
        line = block.lines[0]
        print(f"  Sample line: {line.text}")

        if line.words:
            word = line.words[0]
            print(
                f"    Sample word: '{word.text}' "
                f"bbox={word.bounding_box} "
                f"conf={word.confidence:.2f}"
            )

    # Flag low‑confidence words inside the block
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

Bunu `extract_pdf_ocr.py` olarak kaydedin ve çalıştırın:

```bash
python extract_pdf_ocr.py
```

Konsolda blok‑seviyesi detayları ve düşük‑güven uyarılarını göreceksiniz.

---

## Sonuç

**OCR motoru Python** kullanarak **PDF'den metin çıkarma** için eksiksiz, üretim‑hazır bir yöntemi ele aldık. Kütüphaneyi kurmaktan **OCR için görüntü yükleme** aşamasına, **OCR ile PDF okuma** ve yapılandırılmış çıktıyı döngüyle işleme adımlarına kadar, artık herhangi bir projeye uyarlayabileceğiniz yeniden kullanılabilir bir betiğiniz var.

İleride keşfedebileceğiniz adımlar:

- Hiyerarşiyi JSON'a aktararak sonraki NLP işlem hatlarına beslemek.  
- Dil algılaması ekleyerek OCR modellerini dinamik olarak değiştirmek.  
- Karmaşık düzenler içeren PDF'leri ön‑işlemek için `pdf2image` entegrasyonu.  

Çok sayfalı fatura gruplarında deneyin, güven eşiğini ayarlayın ve taranmış PDF'leri hızlıca aranabilir, düzenlenebilir metne dönüştürün. Sorun yaşarsanız, aşağıya yorum bırakın – iyi OCRlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}