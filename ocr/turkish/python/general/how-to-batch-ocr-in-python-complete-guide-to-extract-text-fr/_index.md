---
category: general
date: 2026-06-28
description: Python'da toplu OCR nasıl yapılır—görüntülerden metin çıkarın ve taranmış
  sayfaları toplu OCR işleme kullanarak metne dönüştürün.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: tr
og_description: Python'da toplu OCR nasıl yapılır, görüntülerden metin nasıl çıkarılır
  ve taranmış sayfalar verimli toplu OCR işleme ile nasıl metne dönüştürülür öğrenin.
og_title: Python'da Toplu OCR Nasıl Yapılır – Adım Adım Rehber
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Python'da Toplu OCR Nasıl Yapılır – Görsellerden Metin Çıkarma İçin Tam Rehber
url: /tr/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da Toplu OCR Nasıl Yapılır – Görsellerden Metin Çıkarma Tam Kılavuzu

Python'da **toplu OCR nasıl yapılır** diye merak ediyorsanız, doğru yerdesiniz. Bu öğretici, **görsellerden metin çıkarmanın** ve **taratılmış sayfaları metne dönüştürmenin** tek bir OCR motoru örneği kullanarak hızlı bir yolunu gösterir. Artık bir dosyayı bir bir kopyalayıp yapıştırmak yok—kod ağır işi halletsin.

İhtiyacınız olan her şeyi adım adım anlatacağız: kütüphaneyi kurma, taramaların bulunduğu klasörü yükleme, toplu OCR işleme çalıştırma ve sonuçları sorunsuz bir şekilde ele alma. Sonunda, PNG veya JPEG yığınını saniyeler içinde aranabilir metin dosyalarına dönüştüren yeniden kullanılabilir bir betiğiniz olacak.

## Gereksinimler

* Python 3.9+ yüklü (kod 3.8'de de çalışır, ancak 3.9+ en yeni tip özelliklerini sağlar).
* Modern bir OCR kütüphanesi—burada **Aspose.OCR for Python via .NET** kullanıyoruz, bu kütüphane orijinal kod parçacığında gösterilen `OcrEngine` sınıfını sunar.  
  ```bash
  pip install aspose-ocr
  ```
* Taratılmış sayfaların bulunduğu bir klasör (`page1.png`, `page2.png`, …). Pillow'ın açabildiği her şey çalışır, bu yüzden PDF'ler, TIFF'ler veya BMP'ler de uygundur.
* Biraz merak—eğer daha önce görüntü‑den‑metne otomasyon yapmadıysanız, toplu OCR'un neden bir oyun değiştirici olduğunu göreceksiniz.

> **Pro ipucu:** Saf Python kütüphanesini tercih ediyorsanız, `OcrEngine` yerine `pytesseract.image_to_string` kullanın. Çevreleyen mantık aynı kalır.

## Python'da Toplu OCR Nasıl Yapılır – Adım‑Adım Kılavuz

Aşağıda tam, çalıştırılabilir betik yer alıyor. Her satır yorumlanmış, böylece sadece *ne* yaptığını değil, aynı zamanda *neden* önemli olduğunu görebileceksiniz.

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### Beklenen Çıktı

Betik, üç PNG taraması içeren bir klasörde çalıştırıldığında aşağıdakine benzer bir çıktı üretir:

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

Ön izleme, her sayfanın ilk 200 karakterini gösterir ve tam metin `ocr_output` dizininde bulunur.

## Tek Bir Motor Kullanarak Görsellerden Metin Çıkarma

Neden **tek** bir `OcrEngine` oluşturup tekrar kullanıyoruz? Motoru örneklemek maliyetli olabilir çünkü dil paketlerini ve yerel DLL'leri yükler. Aynı örneği toplu işlem boyunca paylaşarak:

* **Belleği tasarruf edin** – yalnızca bir kaynak seti RAM'de bulunur.
* **Hızı artırın** – motor ısınmış kalır, tekrar tekrar başlatma ihtiyacını ortadan kaldırır.
* **Tutarlılığı koruyun** – aynı tanıma ayarları her sayfaya uygulanır, bu da aynı düzeni paylaşan **görsellerden metin çıkarmak** istediğinizde çok önemlidir.

Tanıma ayarlarını (ör. imla kontrolü etkinleştirme veya dili değiştirme) `recognize_batch` çağrısından *önce* yapın. Sonraki tüm sayfalar bu ayarları otomatik olarak devralır.

## Taratılmış Sayfaları Verimli Şekilde Metne Dönüştürme

Problemin özü—**taratılmış sayfaları metne dönüştürme**—`engine.recognize_batch(images)` ile çözülür. Kütüphane, her görüntüyü arka plan iş parçacığı havuzunda işler, bu sayede çok çekirdekli makinelerde neredeyse doğrusal ölçeklenme elde edersiniz. Dikkat etmeniz gereken birkaç nokta:

* **Görüntü kalitesi önemlidir** – 300 dpi veya daha yüksek sonuçları en iyi hale getirir. Taramalarınız düşük çözünürlüklüyse, motorun önüne vermeden Pillow ile yükseltmeyi düşünün.
* **Renk vs. gri tonlaması** – OCR motorları genellikle 8‑bit gri tonlamada daha hızlı çalışır. Ön işleme adımı ekleyebilirsiniz:  
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **Dil desteği** – Aspose.OCR 40'tan fazla dili destekler. İngilizce dışındaki bir dil kullanıyorsanız, toplu çağrıdan önce `engine.language = "eng"` veya `"fra"` gibi bir değer atayın.

## Toplu OCR İşleme En İyi Uygulamaları

Yukarıdaki kod zaten kısa olsa da, üretim seviyesinde toplu OCR genellikle birkaç ek önlem gerektirir:

| Endişe | Önerilen Yaklaşım |
|---------|----------------------|
| **Büyük toplular ( > 500 dosya )** | Bellek kullanımını düşük tutmak için 100–200 görüntülik parçalar halinde bölün. |
| **Bozuk veya desteklenmeyen dosyalar** | `load_images` yardımcı işlevi zaten istisnaları yakalar ve bir uyarı kaydeder; ayrıca hatalı dosyaları atlamak veya taşımak için bir geri dönüş yazabilirsiniz. |
| **İlerleme izleme** | Kütüphane per‑image geri çağrıları sunuyorsa, `recognize_batch`'i her görüntüden sonra sonuç veren bir döngüye sarın. |
| **Son‑işlem** | Elde edilen dizeler üzerinde bir imla kontrolü veya regex temizliği çalıştırarak sonraki arama yeteneğini artırın. |
| **Paralellik** | Çoklu düğüm kurulumunuz varsa, klasörleri çalışanlar arasında dağıtın ve sonunda `.txt` çıktıları birleştirin. |

Bu ipuçları, **toplu OCR işleme**ni birkaç sayfadan binlerce sayfaya kadar çökmeden ölçeklendirmenize yardımcı olur.

## Sıkça Sorulan Sorular

**S: Bunu doğrudan PDF'lerle kullanabilir miyim?**  
C: Kesinlikle. Önce her PDF sayfasını bir görüntüye dönüştürün (ör. `pdf2image` kullanarak) ve elde edilen listeyi `recognize_batch`'e besleyin. İş akışının geri kalanı değişmeden kalır.

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanıza ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım‑Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Klasörlerde OCR İşlemi Kullanarak Görsellerden Metin Çıkarma](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Aspose.OCR for .NET ile ZIP Arşivlerinden Metin Çıkarma](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}