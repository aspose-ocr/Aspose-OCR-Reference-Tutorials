---
category: general
date: 2026-03-26
description: OCR kullanarak PDF metnini nasıl çıkarılır. PDF'yi görüntü olarak yüklemeyi,
  PDF metnini tanımayı ve basit bir Python örneğiyle PDF'den metin çıkarmayı öğrenin.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: tr
og_description: OCR kullanarak PDF metnini nasıl çıkarabilirsiniz. Bu rehber, PDF'yi
  görüntü olarak nasıl yükleyeceğinizi, PDF metnini nasıl tanıyacağınızı ve Python'da
  PDF'den metni nasıl çıkaracağınızı gösterir.
og_title: OCR ile PDF Metni Nasıl Çıkarılır – Tam Kılavuz
tags:
- OCR
- Python
- PDF processing
title: OCR ile PDF Metnini Nasıl Çıkarılır – Tam Adım Adım Rehber
url: /tr/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR ile PDF Metni Nasıl Çıkarılır – Tam Adım‑Adım Kılavuz

Hiç **PDF nasıl çıkarılır** sorusunu, aslında sadece taranmış görüntülerden oluşan dosyalar için sormuş muydunuz? Yalnız değilsiniz—birçok geliştirici, aranabilir içerik ihtiyacı duyduğunda ama sadece görüntü‑PDF’leri olduğunda bu engelle karşılaşıyor. İyi haber? Birkaç satır kod ve sağlam bir OCR kütüphanesi, bu resim‑PDF’leri anında düz metne dönüştürebilir.  

Bu öğreticide **OCR nasıl kullanılır** konusunu adım adım ele alacağız; PDF’yi bir görüntü olarak yükleme, PDF metnini tanıma ve sonunda **PDF’den metin çıkarma** işlemini her uzunluktaki belge için gerçekleştireceğiz. Sonunda çalıştırılabilir bir betiğiniz, her adımın net açıklaması ve yaygın tuzaklardan kaçınmak için birkaç ipucu olacak.

## Gereksinimler

- Python 3.9 veya daha yeni (kod 3.10+’da da çalışır)  
- `ocr` Python paketi (veya `OcrEngine`, `OcrEngineMode` ve `Imaging.Image` sınıflarını sunan uyumlu bir OCR kütüphanesi)  
- İşlemek istediğiniz çok sayfalı PDF (örnek olarak `multi_page.pdf` olarak adlandıralım)  
- Sanal ortamlar hakkında temel bilgi (isteğe bağlı ama önerilir)

> **Pro ipucu:** Windows kullanıyorsanız Anaconda Prompt’u tercih edin; macOS/Linux’ta basit bir `python -m venv venv && source venv/bin/activate` işinizi görür.

## Adım 1: OCR Kütüphanesini Kurun

İlk olarak OCR paketini PyPI’dan indirin. Aşağıdaki örnek, kod parçacığında gösterilen API’ye denk gelen hayali bir `ocr` paketini kullanıyor, ancak gerçek dünyada çoğu kütüphane (ör. `pytesseract` + `pdf2image`) aynı desen izler.

```bash
pip install ocr
```

Farklı bir motor kullanıyorsanız `ocr` yerine uygun ismi koyun (ör. `pip install pytesseract pdf2image`).

## Adım 2: OCR Motorunu Başlatın

Bir motor örneği oluşturmak, **PDF nasıl çıkarılır** sorusunun temelidir. Motor, her PDF sayfasındaki pikselleri yorumlayacak beyin gibidir.

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **Neden önemli:** `set_engine_mode` sayesinde hız ile doğruluk arasında denge kurabilirsiniz. `DEFAULT` dengeli bir seçimdir; daha yüksek hassasiyet gerekiyorsa (kütüphane destekliyorsa) `HIGH_ACCURACY`’ye geçin.

## Adım 3: PDF’yi Görüntü Nesnesi Olarak Yükleyin

OCR, PDF konteynerleri üzerinde değil, görüntüler üzerinde çalışır; bu yüzden PDF’yi önce bir görüntü temsiline dönüştürmeliyiz. `Imaging.Image.load` metodu çok‑sayfalı PDF’leri otomatik olarak işler.

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **Köşe durumu:** Bazı kütüphaneler yalnızca tek‑sayfalı görüntü kabul eder. Böyle bir durumda `pdf2image.convert_from_path` ile her sayfayı döngüye almanız gerekir. Bizim `load` çağrımız bu ayrıntıyı soyutlayarak **pdf nasıl yüklenir görüntü olarak** sorusunu tek satırda çözer.

## Adım 4: Tüm Sayfalarda Metni Tanıyın

Şimdi **PDF metni nasıl tanınır** sorusunun özü devreye giriyor. Motor her sayfayı tarar ve sayfa başına bir sonuç nesnesi listesi döndürür.

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

Her `page_result` nesnesi `get_text()` (düz metin) ve `get_confidence()` (isteğe bağlı kalite ölçütü) gibi metodlar içerir.  

> **İpucu:** Sadece ilk sayfaya ihtiyacınız varsa, çok‑sayfalı yardımcı yerine `recognize(pdf_image[0])` çağırın.

## Adım 5: Sonuçları Döngüye Alın ve Çıkarılan Metni Yazdırın

Son olarak, sonuçlar üzerinden döngü kurup her sayfanın metnini ekrana basıyoruz. Bu, **PDF’den metin çıkarma** iş akışını tamamlar.

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### Beklenen Çıktı

`multi_page.pdf` üç sayfa içeriyorsa ve bu sayfalarda sırasıyla “Hello”, “World” ve “Python” kelimeleri varsa, aşağıdaki gibi bir çıktı görürsünüz:

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

Bu kadar—PDF’niz artık tamamen aranabilir ve metin, sonraki işlemler (indeksleme, duygu analizi vb.) için hazır.

## Adım 6: Yaygın Tuzaklarla Baş Etme

| Sorun | Neden Oluşur | Hızlı Çözüm |
|-------|----------------|-----------|
| **Boş çıktı** | PDF sayfaları düşük DPI’da taranmış, karakterler ayırt edilemiyor. | OCR’dan önce görüntüyü büyütün: `pdf_image = pdf_image.resize(300)` (300 DPI ideal bir nokta). |
| **Garip karakterler** | Latin dışı alfabeler dil paketlerine ihtiyaç duyar. | Uygun dil modelini yükleyin: `ocr_engine.load_language('spa')` İspanyolca için vb. |
| **Büyük PDF’lerde bellek patlaması** | Tüm sayfaları bir anda yüklemek RAM tüketir. | Sayfaları parçalar halinde işleyin: `for img in pdf_image.split(batch=10): …` (pseudo‑code). |
| **Yavaş performans** | `DEFAULT` modunu büyük bir belgede kullanmak yavaş olabilir. | `FAST` moda geçin veya `concurrent.futures` ile paralel OCR çalıştırın. |

## Bonus: Çıkarılan Metni Bir Dosyaya Kaydetme

Gerçek dünyadaki çoğu pipeline metni kalıcı hale getirmeyi ister. İşte her şeyi `output.txt` dosyasına yazan küçük bir yardımcı.

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

Artık `output.txt` dosyasını bir arama motoruna, veritabanına ya da herhangi bir NLP modeline besleyebilirsiniz.

## Hepsini Bir Araya Getirme – Tam Betik

Aşağıda, çalıştırmaya hazır tam program yer alıyor. Kopyalayıp yapıştırın, dosya yollarını ayarlayın, hazırsınız.

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

Çalıştırın:

```bash
python extract_pdf_ocr.py
```

Her sayfanın içeriği konsola basılacak ve `extracted_text.txt` dosyasının oluşturulduğuna dair bir onay göreceksiniz.

## Sonuç

**PDF nasıl çıkarılır** sorusunu, görüntü‑only belgelerden OCR motoru kullanarak, kütüphane kurulumundan çok‑sayfalı sonuçların işlenmesine ve çıktının kaydedilmesine kadar ele aldık. Artık **OCR nasıl kullanılır**, **PDF nasıl yüklenir görüntü olarak** ve **PDF metni nasıl tanınır** konularında güvenilir bir bilgiye sahipsiniz.  

Sonraki adımlar? Varsayılan motor modunu yüksek‑doğruluk ayarına geçirin, çok‑dilli PDF’ler için dil paketleriyle deney yapın veya çıkarılan metni Elasticsearch gibi bir tam‑metin arama indeksine yönlendirin. Temel PDF metni çıkarma becerilerini kazandıktan sonra sınır yoktur.

---

![how to extract pdf example](images/ocr_flowchart.png){alt="PDF nasıl çıkarılır iş akışı diyagramı"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}