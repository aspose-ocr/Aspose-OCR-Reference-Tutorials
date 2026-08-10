---
category: general
date: 2026-06-25
description: Python aocr kütüphanesiyle görüntülerden metin çıkarın – toplu OCR öğrenin,
  tanıma modunu basılı olarak ayarlayın ve bir AI sonrası işleyici ekleyin.
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: tr
og_description: Python aocr kütüphanesini kullanarak görüntülerden metin çıkarın.
  Bu öğreticide toplu OCR, basılı tanıma modu ve isteğe bağlı AI post‑işlemci gösterilmektedir.
og_title: Python'da Görüntülerden Metin Çıkarma – Tam aocr Batch Kılavuzu
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: Python ile aocr OCR Batch kullanarak Görsellerden Metin Çıkar
url: /tr/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntülerden Metin Çıkarma Python ile aocr OCR Batch Kullanarak

Hiç **görüntülerden metin çıkarma** ihtiyacı duydunuz mu, ama onlarca küçük adım karşısında bunalmış hissettiniz mi? Tek başınıza değilsiniz. Tarama formlarını dijitalleştiriyor, makbuzlardan veri çekiyor ya da aranabilir bir arşiv oluşturuyorsanız, ölçekli ve güvenilir OCR sonuçları elde etmek dik bir tepeyi tırmanmak gibi görünebilir.

İyi haber? **aocr kütüphanesi** sayesinde sadece birkaç satır kodla tam bir **Python OCR batch** oluşturabilirsiniz. Bu rehberde bir OCR batch’i nasıl oluşturacağınızı, bir klasörden desteklenen tüm görüntüleri nasıl yükleyeceğinizi, doğru **recognition mode printed** seçimini ve hatta doğruluğu artırmak için bir **AI postprocessor** eklemeyi adım adım göstereceğiz. Sonunda, görüntülerden metin çıkaran ve dosya başına ne kadar metin yakalandığını gösteren çalıştırmaya hazır bir betiğiniz olacak.

## Öğrenecekleriniz

- `aocr` paketinin nasıl kurulup içe aktarılacağını.
- Binlerce dosyayı otomatik olarak işlemek için bir `OcrBatch` nasıl ayarlanır.
- Basılı belgeler için optimal tanıma modunun nasıl seçileceği.
- (İsteğe bağlı) Gürültülü sonuçları temizlemek için bir AI post‑processor nasıl bağlanır.
- Her dosya yolunu çıkarılan metnin uzunluğu ile birlikte nasıl gösterilir.
- Desteklenmeyen formatlar veya boş sayfalar gibi kenar durumlarını ele almak için ipuçları.

### Önkoşullar

- Makinenizde yüklü Python 3.8 veya daha yeni bir sürüm.  
- Python betikleme (döngüler, içe aktarmalar vb.) konusunda temel bilgi.  
- Tarama görüntülerinin bulunduğu bir klasöre erişim (PNG, JPG, TIFF vb.).  

Eğer bunlara sahipseniz, dış hizmetlere ihtiyaç duymadan hemen başlayalım.

## Adım 1: aocr Kütüphanesini Kurun

İlk iş olarak. `aocr` paketi standart kütüphanenin bir parçası değildir, bu yüzden PyPI’dan çekmeniz gerekir.

```bash
pip install aocr
```

> **Pro ipucu:** Bağımlılıkları izole tutmak için bir sanal ortam (`python -m venv .venv`) kullanın.  

Kurulum tamamlandıktan sonra çekirdek sınıfları içe aktarabilirsiniz.

```python
# core imports
import aocr
```

## Adım 2: Bir OCR Batch Örneği Oluşturun

`OcrBatch`, dizininizi tarayan ve her görüntü dosyasını izleyen iş gücüdür. Bunu, resimleri OCR motoruna besleyen bir taşıma bandı gibi düşünün.

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

Bu noktada batch boş, ancak bir sonraki adımda dolduracağız.

## Adım 3: Bir Klasörden (Özyinelemeli) Tüm Desteklenen Görüntüleri Ekleyin

Muhtemelen iç içe klasör yapınız vardır—belki her müşteri ya da her ay için bir alt klasör. `add_folder` metodu, ağaçta dolaşarak okuyabildiği her görüntüyü sizin için çeker.

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

`"YOUR_DIRECTORY/scanned_forms/"` ifadesini sisteminizdeki gerçek yol ile değiştirin. Bu çağrıdan sonra `ocr_batch.file_paths` mutlak dosya adlarının bir listesini tutar ve batch kaç öğe işleyeceğini bilir.

## Adım 4: Basılı Metin İçin Tanıma Modunu Seçin

`aocr` motoru birkaç mod destekler (el yazısı, basılı, karışık). Temiz, basılı formlarla çalıştığımız için modu buna göre ayarlayın. Bu küçük bayrak, motorun el yazısı için gereken ağır sezgisel kontrolleri atlaması sayesinde doğruluğu büyük ölçüde artırabilir.

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **Neden Önemli:** Basılı metin tutarlı alt çizgiler ve karakter şekilleri içerir, bu da OCR modelinin daha sıkı karakter sözlükleri uygulamasına izin verir. Modu “auto” bırakırsanız düşük çözünürlüklü taramalarda ekstra gürültü alabilirsiniz.

## Adım 5: (İsteğe Bağlı) Bir AI Post‑Processor Ekleyin

Taramalarınız bulanık, düşük kontrastlı ya da alışılmadık fontlarda ise, bir AI post‑processor ham OCR çıktısını temizleyerek sonraki sistemlere daha iyi bir veri sunabilir. `set_ai_postprocessor` metodu, `process(text: str) -> str` arayüzünü uygulayan bir nesne bekler.

Aşağıda hayali bir `SimpleCleaner` sınıfı kullanan minimal bir örnek var. Gerçekte bir HuggingFace transformer, özel bir dil modeli ya da kural‑tabanlı bir yazım denetleyicisi bağlayabilirsiniz.

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

Bu adımı atlayarsanız, batch sadece ham OCR stringlerini döndürür.

## Adım 6: Tüm Batch Üzerinde OCR Çalıştırın ve Sonuçları Toplayın

Şimdi asıl iş başlıyor. `run` metodu her dosya üzerinde döner, OCR motorunu çalıştırır, isteğe bağlı AI post‑processor’dan geçirir ve bir dizi string döndürür—her görüntü için bir tane.

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

Metod bir düz Python listesi döndürdüğü için, onu başka bir koleksiyon gibi kullanabilirsiniz—saklayabilir, CSV’ye yazabilir ya da bir veritabanına aktarabilirsiniz.

## Adım 7: Her Dosya Yolunu Çıkarılan Metnin Uzunluğu ile Görüntüleyin

Hızlı bir doğrulama için her dosyadan kaç karakter çıkarıldığını yazdırın. Bir sayfa boşsa ya da OCR başarısız olduysa, uzunluk `0` olur.

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

Tipik çıktı şöyle görünür:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

`0` gördüğünüzde, hangi dosyaların ikinci bir gözden geçirme gerektirdiğini anında anlayabilirsiniz (belki bozuk ya da görüntü olmayan dosyalar).

## Yaygın Kenar Durumlarını Ele Alma

### 1. Desteklenmeyen Dosya Türleri

`aocr` çözemediği dosyaları sessizce atlar. PDF ya da BMP gibi dosyalarınız olduğunu düşünüyorsanız, önceden filtreleyin:

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. Büyük Batch’ler ve Bellek Kullanımı

Binlerce yüksek çözünürlüklü tarama belleği şişirebilir. Bunu parçalar halinde işleyerek hafifletin:

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. Boş ya da Düşük Kontrastlı Sayfalar

Bir sayfada 10 karakterden az çıkıyorsa, manuel inceleme için işaretlemek isteyebilirsiniz:

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## Tam Çalışan Örnek

Hepsini bir araya getirdiğimizde, hemen kopyalayıp çalıştırabileceğiniz bir betik elde edersiniz. `batch_ocr.py` olarak kaydedin.

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**Beklenen çıktı** (kısaltılmış):

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

Şu komutla çalıştırın:

```bash
python batch_ocr.py
```

Her şey doğru ayarlandıysa, her görüntü için karakter sayısını raporlayan bir satır göreceksiniz.

## Sık Sorulan Sorular

**S: Bu PDF’lerde çalışır mı?**  
C: Kutudan çıkınca değil. `aocr` yalnızca raster görüntüleri işler. PDF’leri önce PNG/TIFF’e dönüştürün (ör. `pdf2image` kullanarak).

**S: Tanıma modunu el yazısına değiştirebilir miyim?**  
C: Tabii—`aocr.RecognitionMode.PRINTED` yerine `aocr.RecognitionMode.HANDWRITTEN` kullanın. Çalışma süresi yavaşlayabilir ama el yazısı notlarda daha iyi sonuç alırsınız.

**S: Çok dilli desteğe ihtiyacım olursa?**  
C: Kütüphane dil paketleriyle gelir. İstediğiniz dil modülünü kurun (`pip install aocr-lang-fr` Fransızca için vb.) ve çalıştırmadan önce `ocr_batch.language = "fr"` ayarlayın.

## Sonraki Adımlar ve İlgili Konular

- **Paralel işleme:** Batch yürütmesini bir `concurrent.futures.ThreadPoolExecutor` içinde sararak birden fazla CPU çekirdeği kullanın.  
- **Sonuçları saklama:** `ocr_results`ı bir CSV ya da SQLite veritabanına yazarak sonraki analizlere hazırlayın.  
- **Bulut AI entegrasyonu:** `SimpleCleaner`ı HuggingFace’den bir transformer modeliyle değiştirerek en güncel yazım düzeltmesini elde edin.  
- **aocr’u ince ayar:** Özel bir font setiniz varsa, `aocr.Trainer`ı keşfederek basılı‑mod doğruluğunu artırın.

---

Bu kadar—artık sağlam bir temele sahipsiniz


## Bir Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımları keşfetmeniz için adım adım açıklamalar ve tam çalışan kod örnekleri içerir.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}