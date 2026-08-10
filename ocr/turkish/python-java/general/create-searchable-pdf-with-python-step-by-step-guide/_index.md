---
category: general
date: 2026-05-31
description: Python OCR kullanarak taranmış görüntülerden aranabilir PDF oluşturun.
  Taranmış görüntü PDF'sini nasıl dönüştüreceğinizi, TIFF'i PDF'ye nasıl dönüştüreceğinizi
  ve dakikalar içinde OCR metin katmanı eklemeyi öğrenin.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: tr
og_description: Aranabilir PDF'yi anında oluşturun. Bu kılavuz, OCR çalıştırmayı,
  taranmış görüntü PDF'sini dönüştürmeyi ve tek bir Python betiği kullanarak OCR metin
  katmanı eklemeyi gösterir.
og_title: Python ile Aranabilir PDF Oluşturma – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: Python ile Aranabilir PDF Oluşturma – Adım Adım Kılavuz
url: /tr/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python ile Aranabilir PDF Oluşturma – Adım Adım Kılavuz

Hiç bir taranmış sayfadan **aranabilir PDF** oluşturmanın, onlarca aracı bir arada kullanmadan nasıl yapılacağını merak ettiniz mi? Tek başınıza değilsiniz. Birçok ofis iş akışında taranmış bir TIFF veya JPEG ortak bir sürücüye düşer ve bir sonraki kişi metni elle kopyala‑yapıştırmak zorunda kalır—acı verici, hataya açık ve zaman kaybettirici.  

Bu öğreticide, **taranmış görüntü PDF'yi dönüştürmenizi**, **TIFF'i PDF'ye çevirmenizi** ve **OCR metin katmanı eklemenizi** tek bir adımda sağlayan temiz, programatik bir çözümü adım adım inceleyeceğiz. Sonunda OCR çalıştıran, gizli metni gömen ve indeksleyebileceğiniz, arayabileceğiniz veya güvenle paylaşabileceğiniz bir aranabilir PDF üreten, kullanıma hazır bir betiğe sahip olacaksınız.

## Gereksinimler

- Python 3.9+ (herhangi bir yeni sürüm çalışır)
- `aspose-ocr` ve `aspose-pdf` paketleri (`pip install aspose-ocr aspose-pdf` ile kurulur)
- Taranmış bir görüntü dosyası (`.tif`, `.png`, `.jpg`, hatta sadece bir görüntü içeren bir PDF sayfası)
- Orta seviyede bir RAM miktarı (OCR motoru hafiftir; bir dizüstü bilgisayar bile bunu kaldırır)

> **Pro ipucu:** Windows kullanıyorsanız, paketleri edinmenin en kolay yolu komutu yükseltilmiş bir PowerShell penceresinde çalıştırmaktır.

```bash
pip install aspose-ocr aspose-pdf
```

Gereksinimler halledildiğine göre, koda dalalım.

## Adım 1: OCR Motoru Örneği Oluşturma – *create searchable pdf*

İlk yaptığımız şey OCR motorunu başlatmaktır. Bunu, her pikseli okuyup karakterlere dönüştürecek bir beyin olarak düşünün.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **Neden önemli:** Motoru yalnızca bir kez başlatmak bellek kullanımını düşük tutar. Her sayfa için bir döngü içinde `OcrEngine()` çağırırsanız, kaynaklarınız çabucak tükenir.

## Adım 2: Taranmış Görüntüyü Yükleme – *convert tiff to pdf* & *convert scanned image pdf*

Sonra, motoru işlemek istediğiniz dosyaya yönlendirin. API herhangi bir raster görüntüyü kabul eder, bu yüzden bir TIFF JPEG kadar iyi çalışır.

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

Eğer sadece taranmış bir görüntü içeren bir PDF'niz varsa, `load_image`'i yine de kullanabilirsiniz çünkü Aspose ilk sayfayı otomatik olarak çıkarır.

## Adım 3: PDF Kaydetme Seçeneklerini Hazırlama – *add OCR text layer*

Burada son PDF'nin nasıl görünmesi gerektiğini yapılandırıyoruz. Kritik bayrak `create_searchable_pdf`; bunu `True` olarak ayarlamak, kütüphaneye görsel içeriği yansıtan görünmez bir metin katmanı eklemesini söyler.

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **Metin katmanının yaptığı şey:** Oluşturulan dosyayı Adobe Reader'da açıp metni seçmeye çalıştığınızda gizli karakterleri göreceksiniz. Arama motorları da bunları indeksleyebilir—uyumluluk veya arşivleme için mükemmel.

## Adım 4: OCR'ı Çalıştır ve Kaydet – *how to run OCR* tek bir çağrıda

Şimdi sihir gerçekleşiyor. Tek bir metod çağrısı tanıma motorunu çalıştırır ve aranabilir PDF'yi diske yazar.

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

`recognize` metodu, hataları inceleyebileceğiniz bir durum nesnesi döndürür, ancak çoğu basit senaryo için yukarıdaki basit çağrı yeterlidir.

### Beklenen Çıktı

Betik çalıştırıldığında şu çıktı verir:

```
PDF saved as searchable PDF.
```

`scanned_page_searchable.pdf` dosyasını açarsanız, metni seçebildiğinizi, kopyala‑yapıştırabildiğinizi ve hatta `Ctrl+F` araması yapabildiğinizi fark edeceksiniz. Bu, **create searchable pdf** iş akışının temel özelliğidir.

## Tam Çalışan Betik

Aşağıda eksiksiz, çalıştırmaya hazır betik yer alıyor. Yer tutucu yolları gerçek dosya konumlarınızla değiştirmeniz yeterli.

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

Bunu `create_searchable_pdf.py` olarak kaydedin ve çalıştırın:

```bash
python create_searchable_pdf.py
```

## Yaygın Sorular & Kenar Durumları

### 1️⃣ Çok sayfalı PDF'leri işleyebilir miyim?

Evet. `ocr_engine.load_image("file.pdf")` kullanın ve ardından her sayfa için `ocr_engine.recognize(pdf_save_options, page_number)` ile döngü oluşturun. Kütüphane otomatik olarak çok sayfalı bir aranabilir PDF oluşturur.

### 2️⃣ Kaynak dosyam yüksek çözünürlüklü bir TIFF (300 dpi+) ise ne olur?

Daha yüksek DPI, daha iyi OCR doğruluğu sağlar ancak aynı zamanda daha fazla bellek kullanır. `MemoryError` alırsanız, önce görüntüyü küçültün:

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ OCR dilini nasıl değiştiririm?

Görüntüyü yüklemeden önce motorun `language` özelliğini ayarlayın:

```python
ocr_engine.language = "fra"   # French
```

Desteklenen dil kodlarının tam listesi Aspose belgelerinde bulunur.

### 4️⃣ Orijinal görüntü kalitesini korumam gerekirse?

`PdfSaveOptions` sınıfının bir `compression` özelliği vardır. Raster veriyi tam olarak olduğu gibi korumak için `PdfCompression.None` olarak ayarlayın.

```python
pdf_save_options.compression = "None"
```

## Üretim‑Hazır Dağıtımlar İçin İpuçları

- **Toplu işleme:** Temel mantığı, dosya yolu listesi kabul eden bir fonksiyon içinde paketleyin. Her başarı/başarısızlığı denetim izleri için bir CSV'ye kaydedin.
- **Paralellik:** OCR'ı birden çok çekirdekte çalıştırmak için `concurrent.futures.ThreadPoolExecutor` kullanın. Her thread'in kendi `OcrEngine` örneğine ihtiyacı olduğunu unutmayın.
- **Güvenlik:** Hassas belgelerle çalışıyorsanız, betiği izole bir ortamda çalıştırın ve işleme sonrasında geçici dosyaları hemen silin.

## Sonuç

Artık kısa bir Python betiği kullanarak taranmış görüntülerden **aranabilir PDF** dosyaları oluşturmayı biliyorsunuz. Bir OCR motorunu başlatarak, bir TIFF'i (veya herhangi bir raster'ı) yükleyerek, `PdfSaveOptions`'ı **add OCR text layer** olarak yapılandırarak ve sonunda `recognize`'ı çağırarak, tüm **convert scanned image pdf** ve **convert TIFF to PDF** süreci tek bir tekrarlanabilir komut haline geliyor.

Sonraki adımlar? Bu betiği bir dosya izleyiciyle zincirleyerek, bir klasöre düşen her yeni taramanın otomatik olarak aranabilir olmasını sağlayın. Ya da çok dilli arşivleri desteklemek için farklı OCR dilleriyle deneyler yapın. OCR'ı PDF oluşturmayla birleştirdiğinizde sınır yoktur.

**how to run OCR** hakkında başka dillerde veya çerçevelerde sorularınız mı var? Aşağıya bir yorum bırakın, iyi kodlamalar! 

![Taranmış görüntü → OCR motoru → aranabilir PDF (create searchable pdf) akışını gösteren diyagram](searchable-pdf-flow.png "Aranabilir pdf akış diyagramı")


## Sonraki Öğrenmeniz Gerekenler

- [Aspose.OCR ile .NET'te PDF'yi OCR'lamak](/ocr/english/net/text-recognition/recognize-pdf/)
- [Görüntüleri PDF'ye Dönüştür C# – Çok Sayfalı OCR Sonucunu Kaydet](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Aspose.OCR Kullanarak Dil ile Görüntü Metnini OCR'lamak](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}