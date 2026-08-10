---
category: general
date: 2026-06-06
description: Aspose OCR Cloud kullanarak PDF'yi OCR'lamak nasıl yapılır. PDF'den metin
  çıkarmayı, PDF sayfasını PNG'ye dönüştürmeyi ve Python'da PDF sayfa görüntülerini
  kaydetmeyi öğrenin.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf page png
- extract plain text pdf
- save pdf page images
language: tr
og_description: Aspose OCR Cloud ile PDF'yi OCR'lamak nasıl yapılır. Bu kılavuz, düz
  metin PDF'sini çıkarmayı, PDF sayfasını PNG'ye dönüştürmeyi ve PDF sayfa görüntülerini
  kaydetmeyi gösterir.
og_title: Aspose OCR Cloud ile PDF'yi OCR'lamak – Adım Adım
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Aspose OCR Cloud. Learn to extract text from PDF,
    convert PDF page PNG, and save PDF page images in Python.
  headline: How to OCR PDF with Aspose OCR Cloud – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Aspose OCR Cloud ile PDF'yi OCR'lamak – Tam Rehber
url: /tr/python-java/general/how-to-ocr-pdf-with-aspose-ocr-cloud-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Cloud ile PDF OCR Nasıl Yapılır – Tam Kılavuz

Ağır masaüstü araçlarıyla uğraşmadan **PDF OCR nasıl yapılır** dosyalarını merak ettiniz mi? Tek başınıza değilsiniz—birçok geliştirici, taranmış belgelerden metin çıkarmak için hızlı ve programatik bir yol gerektiğinde bu engelle karşılaşıyor. İyi haber? Aspose OCR Cloud ile **PDF'den metin çıkarabilir**, her sayfayı PNG'ye dönüştürebilir ve hatta **PDF sayfa görüntülerini** daha sonra kullanmak üzere kaydedebilirsiniz, hepsi düzenli bir Python betiğinden.

Bu öğreticide, bilmeniz gereken her şeyi adım adım göstereceğiz: SDK'yı kurmaktan, motoru lisanslamaya ve çok sayfalı PDF'leri tanımaya, düz metin çıkarmaya, sayfaları PNG'ye dönüştürmeye ve bu görüntüleri diske kalıcı olarak kaydetmeye kadar. Sonunda, **PDF OCR nasıl yapılır** yeteneklerine ihtiyaç duyan herhangi bir projeye ekleyebileceğiniz yeniden kullanılabilir bir kod parçacığına sahip olacaksınız.

## Gereksinimler

- **Python 3.8+** (kod 3.10 ve üzeri sürümlerde de çalışır)  
- Bir Aspose OCR Cloud hesabı – ücretsiz deneme lisans dosyasını (`Aspose.OCR.lic`) alacaksınız  
- `asposeocrcloud` paketi (`pip install asposeocrcloud`)  
- İşlemek istediğiniz taranmış, çok sayfalı bir PDF  

Hepsi bu. Ekstra ikili dosyalar, yerel bağımlılıklar yok, sadece saf Python.

## PDF OCR Nasıl Yapılır – Kurulum ve Lisans

Herhangi bir OCR metodunu çağırmadan önce SDK'ya kim olduğunuzu bildirmeniz gerekir. Aspose, betiğinizin erişebileceği bir yere koymanız gereken hafif bir lisans dosyası kullanır.

```python
# Step 1: Import the OCR package and apply your license (optional but recommended)
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply the license – replace the path with your actual .lic file location
License().set_license("Aspose.OCR.lic")
```

*Pro ipucu:* Lisans adımını atlayarsanız, SDK yine çalışır ancak çıktı görüntülerine küçük bir filigran ekler. Üretim ortamı için ideal değildir.

## Adım 2: Aspose OCR Cloud Python SDK'sını Kurun

Bir terminal açın ve şu komutu çalıştırın:

```bash
pip install asposeocrcloud
```

Paket, gerekli tüm bağımlılıkları (requests, pillow vb.) otomatik olarak çeker, böylece başka bir şey aramanıza gerek kalmaz.

## Adım 3: Bir OCR Motoru Oluşturun ve Dil Seçin

Motor, işlemin kalbidir. Aspose tarafından desteklenen herhangi bir dili belirtebilirsiniz; İngilizce çoğu durumda işe yarar.

```python
# Step 3: Create an OCR engine and set the recognition language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)
```

Neden dili ayarlamalısınız? Çünkü OCR motoru, doğruluğu artırmak için dile özgü sözlükler kullanır. Fransızca PDF'ler işliyorsanız, sadece `ENGLISH` yerine `FRENCH` yazın.

## Adım 4: Çok Sayfalı PDF'inize İşaret Edin

Motora işlemek istediğiniz dosyanın tam yolunu verin. Göreceli yollar, betiğin çalışma dizininden çözüldükleri sürece uygundur.

```python
# Step 4: Specify the path to the multi‑page PDF you want to process
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"
```

Dosyanın okunabilir olduğundan emin olun; aksi takdirde `FileNotFoundError` alırsınız.

## Adım 5: OCR'ı Çalıştırın – Sonuçların Listesini Alırsınız

`recognize_pdf` çağrısı, her bir öğesi kaynak PDF'in bir sayfasına karşılık gelen bir liste döndürür.

```python
# Step 5: Run OCR on the PDF – a list of OcrResult objects is returned (one per page)
results = engine.recognize_pdf(pdf_path)
```

Her `OcrResult` iki kullanışlı özelliğe sahiptir:

* `text` – sayfanın düz metin temsili (**extract plain text pdf** için harika)  
* `image` – işlenen sayfanın Pillow `Image` nesnesi (**convert pdf page png** için mükemmel)

## Adım 6: PDF'den Metin Çıkarın ve Sayfaları PNG'ye Dönüştürün

Şimdi sonuçlar üzerinde döngü kuruyor, çıkarılan metni yazdırıyor ve her sayfanın PNG sürümünü kaydediyoruz.

```python
# Step 6: Iterate through each page, output the extracted text and optionally save the page image
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    # Extract plain text for this page
    print(res.text)                     # <-- this is the "extract plain text pdf" part
    # Convert the page to PNG and save it
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # <-- this does the "convert pdf page png"
```

### Beklenen Konsol Çıktısı

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

`page_1.png`, `page_2.png`, … dosyalarını `YOUR_DIRECTORY` içinde bulacaksınız. Bunlar, sonraki görüntü işleme boru hatlarına besleyebileceğiniz rasterleştirilmiş sayfa görüntüleridir.

## Adım 7: PDF Sayfa Görüntülerini Kaydedin (İsteğe Bağlı Son İşlem)

Sadece görüntülere ihtiyacınız varsa ve metne gerek yoksa, `print(res.text)` satırını atlayabilirsiniz. Aksine, metni ayrı `.txt` dosyalarına kaydetmek isterseniz, sadece küçük bir yazma işlemi ekleyin:

```python
# Optional: Save each page's text to a .txt file
for i, res in enumerate(results, start=1):
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)
```

Bu küçük ekleme, **PDF sayfa görüntülerini kaydetmenin** ne kadar kolay olduğunu ve aynı zamanda çıkarılan içeriği kalıcı hale getirdiğini gösterir.

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, `ocr_pdf.py` dosyasına kopyalayıp yapıştırabileceğiniz tam betiği aşağıda bulabilirsiniz:

```python
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply your license – optional but removes watermarks
License().set_license("Aspose.OCR.lic")

# Initialize the OCR engine and set language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)

# Path to the source PDF
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"

# Run OCR – get a list of results (one per page)
results = engine.recognize_pdf(pdf_path)

# Process each page
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(res.text)  # extract plain text PDF
    # Save the rendered page as PNG
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # convert PDF page PNG
    # Optional: also save the text to a .txt file
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)  # save PDF page images + text
```

Şu komutla çalıştırın:

```bash
python ocr_pdf.py
```

Her sayfanın metninin konsola döküldüğünü ve bir dizi PNG dosyası oluşturulduğunu görmelisiniz

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanıza ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.OCR ile .NET'te PDF OCR Nasıl Yapılır](/ocr/english/net/text-recognition/recognize-pdf/)
- [PDF Metni Tanıma – Java için Aspose.OCR ile OCR İşlemleri](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Görüntüleri PDF'ye Dönüştür C# – Çok Sayfalı OCR Sonucunu Kaydet](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}