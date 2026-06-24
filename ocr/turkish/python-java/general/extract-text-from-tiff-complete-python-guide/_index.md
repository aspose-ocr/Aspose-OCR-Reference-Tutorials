---
category: general
date: 2026-06-16
description: Python OCR kullanarak TIFF dosyalarından metin çıkarın. TIFF'i metne
  adım adım dönüştürmeyi öğrenin, çok sayfalı belgeleri kolaylıkla işleyin.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: tr
og_description: Python OCR ile TIFF dosyalarından metin çıkarın. Bu kılavuzu izleyerek
  TIFF'i metne dönüştürün, çok sayfalı taramaları yönetin ve temiz sonuçlar elde edin.
og_title: TIFF'ten Metin Çıkar – Tam Python Rehberi
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: TIFF'ten Metin Çıkarma – Tam Python Rehberi
url: /tr/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFF'ten Metin Çıkarma – Tam Python Rehberi

Hiç **TIFF'ten metin çıkarmak** gerektiğinde nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz—birçok geliştirici taranmış arşivler ya da eski belgelerle uğraşırken bu soruna takılıyor. İyi haber? Birkaç satır Python ile **TIFF'i metne dönüştürebilirsiniz**, dosya onlarca sayfa içeriyor olsa bile.

Bu öğreticide gerçek bir örnek üzerinden ilerleyeceğiz: çok sayfalı bir TIFF'i yüklemek, OCR dilini Fransızca olarak ayarlamak ve her sayfadan tanınan metni çekmek. Sonunda çalıştırmaya hazır bir betiğiniz olacak, her adımın neden önemli olduğunu anlayacaksınız ve diğer diller ya da görüntü formatları için nasıl uyarlayacağınızı öğreneceksiniz.

## Önkoşullar

İlerlemeye başlamadan önce şunların yüklü olduğundan emin olun:

- Python 3.8 veya daha yeni bir sürüm.
- `ocr` paketi (veya `OcrEngine` sınıfı sunan uyumlu bir OCR kütüphanesi). `pip install ocr-lib` ile kurabilirsiniz—kullandığınız gerçek paket adıyla değiştirin.
- İşlemek istediğiniz çok sayfalı TIFF dosyası (ör. `french-scans.tif`).
- Python betikleme konusunda temel bilgi.

Ağır bağımlılıklar yok, harici hizmetler yok—sadece saf Python ve bir OCR motoru.

---

## Adım 1: OCR Motorunu **TIFF'ten Metin Çıkarma** İçin Ayarlayın

İlk iş olarak bir OCR motoru örneği oluşturmalı ve hangi dili kullanacağını ona söylemeliyiz. Bizim durumumuzda kaynak materyal Fransızca, bu yüzden dili buna göre ayarlayacağız.

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**Neden önemli:**  
Dil ayarı doğruluğu büyük ölçüde artırır. “é” ya da “ç” gibi Fransızca karakterler, motor İngilizce varsayılanı ile çalışırsa genel semboller olarak okunur. Fransızcayı açıkça seçerek motorun doğru karakter haritasını kullanmasını sağlarız.

> **İpucu:** Birden fazla dilde belge işliyorsanız, her `recognize()` çağrısından önce `engine.language` değerini dinamik olarak değiştirebilirsiniz.

---

## Adım 2: **TIFF'i Metne Dönüştürmek** İçin Çok Sayfalı TIFF'i Yükleyin

Bir TIFF birden fazla çerçeve tutabilir—her çerçeve ayrı bir sayfa gibi düşünülebilir. OCR kütüphanesi bunu bizim için soyutlar, bu yüzden sadece dosyayı gösteririz.

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**Köşe durum uyarısı:**  
Dosya yolu hatalıysa ya da TIFF bozuksa, `load_from_file` metodu bir istisna fırlatır. Üretim kodunda bunu bir `try/except` bloğuna alın:

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## Adım 3: Tüm Belge Üzerinde OCR Çalıştırın – **TIFF'ten Metin Çıkarma**'nın Çekirdeği

Şimdi motorun sihrini izleyelim. `recognize()` çağrısı tüm sayfaları bir kerede işler ve zengin bir sonuç nesnesi döndürür.

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**Arka planda ne oluyor?**  
Motor her çerçeveyi sırayla dolaşır, ön işleme (eğrilik düzeltme, ikilileştirme) uygular, sinir ağını çalıştırır ve çıktıyı birleştirir. `recognize()` metodunu yalnızca bir kez çağırdığımız için kütüphane sayfalar arasında kaynakları paylaşabilir; bu, manuel döngüden daha hızlıdır.

---

## Adım 4: JSON Sonucundan Tanınan Metni Çıkarın – **TIFF'i Metne Dönüştürmek** Sayfa Sayfa

Sonuç nesnesi JSON’a serileştirilebilir. Bu JSON içinde `pages` adlı bir dizi bulunur; her öğe bir `text` alanı içerir.

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

Artık her bir sayfanın OCR çıktısını temsil eden temiz bir Python listemiz var.

---

## Adım 5: Her Sayfa İçin Metni Yazdırın veya Kaydedin – **TIFF'ten Metin Çıkarma**'nın Son Parçası

Sayfalar üzerinden döngü kurup çıkarılan metni gösterelim. İsterseniz her sayfayı ayrı bir `.txt` dosyasına da yazabilirsiniz.

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### Beklenen Çıktı (örnek)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

OCR başarılıysa, her sayfa için temiz Fransızca cümleler göreceksiniz. Karakter bozulması fark ederseniz, dil ayarını tekrar kontrol edin ya da OCR öncesinde görüntü çözünürlüğünü artırmayı düşünün.

---

## **TIFF'i Metne Dönüştürürken** Yaygın Sorunları Ele Alma

| Sorun | Neden Oluşur | Hızlı Çözüm |
|-------|----------------|-----------|
| **Boş `pages` dizisi** | TIFF doğru yüklenmemiş ya da çerçeve içermiyor. | Dosya yolunu doğrulayın ve TIFF'in tek sayfalı PNG gibi sahte bir TIFF olmadığından emin olun. |
| **Bozuk karakterler** | Dil uyumsuzluğu ya da düşük görüntü kalitesi. | Doğru `engine.language` ayarlayın ve görüntüyü ön işleyin (ör. DPI artırın). |
| **Büyük TIFF'lerde bellek patlaması** | Tüm sayfalar aynı anda yüklendiğinde RAM tüketilir. | Parçalar halinde işleyin: tek bir çerçeveyi yükleyin, tanıyın, ardından bir sonraki çerçeveye geçmeden önce serbest bırakın. |
| **Yazdırırken Unicode hataları** | Konsol kodlaması aksanlı karakterleri desteklemiyor. | `print(page["text"].encode('utf-8').decode('utf-8'))` kullanın ya da terminalinizi UTF‑8 olarak yapılandırın. |

---

## Betiği Genişletmek: **TIFF'ten Metin Çıkarma**'dan Toplu İşleme

Temel yapıyı kurduğunuza göre şu adımları düşünebilirsiniz:

1. **Toplu dönüşüm** – Akışı `def ocr_tiff(path):` fonksiyonuna sarın ve bir klasördeki TIFF dosyaları üzerinde yineleyin.
2. **Dosyalara çıktı** – Yazdırmak yerine her sayfanın metnini `page_{i}.txt` olarak kaydedin ya da tümünü tek bir belgeye birleştirin.
3. **Alternatif OCR motorları** – Daha yüksek doğruluk gerekiyorsa `ocr.OcrEngine()` yerine Tesseract (`pytesseract`) ya da Azure Cognitive Services kullanın—yalnızca “TIFF'ten metin çıkarma” mantığını aynı tutun.
4. **Son işlem** – Ham OCR çıktısını düzeltmek için imla kontrolü, dil tespiti ya da regex temizlikleri uygulayın.

---

## Tam, Çalıştırmaya Hazır Betik

Aşağıda kopyala‑yapıştır yapabileceğiniz eksiksiz kod yer alıyor. Temel hata yönetimi ve her sayfanın metnini ayrı dosyalara kaydetme seçeneği içeriyor.

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

Bu betiği çalıştırın, `tiff_file` değişkenini belgenize yönlendirin ve konsolun temiz Fransızca cümlelerle dolduğunu izleyin. `out_folder` belirttiyseniz, `page_#.txt` dosyaları da oluşturulmuş olacak ve sonraki işlemler için hazır olacaktır.

---

## Sonuç

Basit bir Python OCR akışıyla **TIFF dosyalarından metin çıkardık** ve **TIFF'i metne dönüştürmeyi** güvenilir bir şekilde nasıl yapacağınızı öğrendiniz. Motoru doğru dil ile başlatmaktan, her sayfanın JSON sonucunu döngüyle işlemeye kadar her adımın “neden”ini açıkladık; böylece bu deseni diğer dillere, görüntü formatlarına ya da daha büyük toplu işlere uyarlayabilirsiniz.

Sırada ne var? OCR arka ucunu Tesseract ile değiştirin, farklı dil paketleri deneyin ya da çıktıyı aranabilir bir veritabanına entegre edin. Tarama görüntülerini aranabilir metne dönüştürebildiğiniz sürece sınır yoktur.

Herhangi bir sorunla karşılaşırsanız ya da ek geliştirme fikirleriniz varsa yorum bırakın. Kodlamanın tadını çıkarın!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve ilgili konuları derinlemesine ele alan tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}