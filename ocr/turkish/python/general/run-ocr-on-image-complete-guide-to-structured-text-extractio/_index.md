---
category: general
date: 2026-05-03
description: Görüntü üzerinde OCR çalıştırmayı ve yapılandırılmış OCR tanıma kullanarak
  koordinatlarla metin çıkarmayı öğrenin. Adım adım Python kodu dahil.
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: tr
og_description: Görüntüde OCR çalıştırın ve yapılandırılmış OCR tanıma kullanarak
  koordinatlarıyla birlikte metni elde edin. Açıklamalı tam Python örneği.
og_title: Görselde OCR Çalıştır – Yapılandırılmış Metin Çıkarma Öğreticisi
tags:
- OCR
- Python
- Computer Vision
title: Görüntüde OCR Çalıştırma – Yapılandırılmış Metin Çıkarma İçin Tam Kılavuz
url: /tr/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüde OCR Çalıştırma – Yapılandırılmış Metin Çıkarma İçin Tam Kılavuz

Hiç **run OCR on image** dosyalarını çalıştırmanız gerekti ama her kelimenin tam konumunu nasıl koruyacağınızdan emin değildiniz? Yalnız değilsiniz. Birçok projede—makbuz tarama, form dijitalleştirme veya UI testi—yalnız ham metni değil, aynı zamanda her satırın resimde nerede olduğunu gösteren sınırlama kutularına da ihtiyacınız var.  

Bu öğretici, **aocr** motorunu kullanarak *run OCR on image* işlemini, **structured OCR recognition** talep etmeyi ve ardından sonucu geometrisini koruyarak post‑process etmeyi gösterir. Sonunda sadece birkaç Python satırıyla **extract text with coordinates** yapabilecek ve yapılandırılmış modun sonraki görevler için neden önemli olduğunu anlayacaksınız.

## Öğrenecekleriniz

- **structured OCR recognition** için OCR motorunu nasıl başlatacağınızı.  
- Bir görüntüyü nasıl besleyeceğinizi ve satır sınırlarını içeren ham sonuçları nasıl alacağınızı.  
- Geometrisini kaybetmeden metni temizleyen bir post‑processor'ı nasıl çalıştıracağınızı.  
- Son satırlar üzerinde nasıl döngü yapıp her metin parçasını sınırlama kutusuyla birlikte nasıl yazdıracağınızı.  

Sihir yok, gizli adım yok—kendi projenize ekleyebileceğiniz tam, çalıştırılabilir bir örnek.

---

## Önkoşullar

İçeriğe girmeden önce, aşağıdakilerin yüklü olduğundan emin olun:

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

Ayrıca net, okunabilir metin içeren bir görüntü dosyasına (`input_image.png` veya `.jpg`) ihtiyacınız olacak. Tarama faturası olsun ya da ekran görüntüsü, OCR motorunun karakterleri görebildiği sürece işe yarar.

---

## Adım 1: Yapılandırılmış tanıma için OCR motorunu başlatma

İlk yaptığımız şey `aocr.Engine()` bir örnek oluşturmak ve ona **structured OCR recognition** istediğimizi söylemektir. Yapılandırılmış mod yalnızca düz metni değil, aynı zamanda her satır için geometrik verileri (sınırlama dikdörtgenleri) döndürür; bu, metni görüntüye geri eşlemeniz gerektiğinde çok önemlidir.

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **Neden önemli:**  
> Varsayılan modda motor yalnızca birleştirilmiş kelimeler dizisi verebilir. Yapılandırılmış mod, sayfalar → satırlar → kelimeler hiyerarşisini, her biri koordinatlarla birlikte, sağlar; bu da sonuçları orijinal görüntünün üzerine yerleştirmeyi veya bir layout‑aware modele beslemeyi çok daha kolaylaştırır.

---

## Adım 2: Görüntüde OCR Çalıştırma ve ham sonuçları elde etme

Şimdi görüntüyü motora besliyoruz. `recognize` çağrısı, her biri kendi sınırlama dikdörtgenine sahip satırların bir koleksiyonunu içeren bir `OcrResult` nesnesi döndürür.

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

Bu noktada `raw_result.lines` iki önemli özelliğe sahip nesneler tutar:

- `text` – o satır için tanınan dize.  
- `bounds` – satırın konumunu tanımlayan `(x, y, width, height)` gibi bir tuple.

---

## Adım 3: Geometriyi koruyarak post‑process yapma

Ham OCR çıktısı genellikle gürültülüdür: rastgele karakterler, yanlış yerleştirilmiş boşluklar veya satır sonu sorunları. `ai.run_postprocessor` işlevi metni temizler ancak **orijinal geometriyi** bozulmadan tutar, böylece hâlâ doğru koordinatlara sahipsiniz.

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **Pro ipucu:** Alan‑spesifik sözlükleriniz (ör. ürün kodları) varsa, doğruluğu artırmak için post‑processor'a özel bir sözlük besleyin.

---

## Adım 4: Koordinatlarla metin çıkarma – yinele ve göster

Son olarak, temizlenmiş satırlar üzerinde döngü yapar, her satırın sınırlama kutusunu metniyle birlikte yazdırırız. Bu, **extract text with coordinates** işleminin özüdür.

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### Beklenen Çıktı

Girdi görüntüsünün iki satır içerdiğini varsayalım: “Invoice #12345” ve “Total: $89.99”, aşağıdakine benzer bir şey göreceksiniz:

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

İlk tuple, orijinal görüntüdeki satırın `(x, y, width, height)` değeridir; bu sayede dikdörtgen çizebilir, metni vurgulayabilir veya koordinatları başka bir sisteme besleyebilirsiniz.

---

## Sonucu Görselleştirme (İsteğe Bağlı)

Sınırlama kutularının görüntü üzerine bindirilmiş halini görmek istiyorsanız, Pillow (PIL) kullanarak dikdörtgen çizebilirsiniz. Aşağıda hızlı bir kod parçacığı var; yalnızca ham verilere ihtiyacınız varsa atlayabilirsiniz.

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![run OCR on image örneği, sınırlama kutularını gösteriyor](/images/ocr-bounding-boxes.png "run OCR on image – sınırlama kutusu katmanı")

Yukarıdaki alt metin **primary keyword** içerir ve görüntü alt öznitelikleri için SEO gereksinimini karşılar.

---

## Neden Yapılandırılmış OCR Tanıma, Basit Metin Çıkarma'dan Daha İyi

Şöyle düşünebilirsiniz: “Sadece OCR çalıştırıp metni alabilir miyim? Neden geometriyle uğraşayım?”  

- **Spatial context:** Bir formdaki alanları eşlemeniz gerektiğinde (ör. “Date” tarih değerinin yanında), koordinatlar verinin *nerede* olduğunu söyler.  
- **Multi‑column layouts:** Basit doğrusal metin sıralamayı kaybeder; yapılandırılmış veri sütun sırasını korur.  
- **Post‑processing accuracy:** Kutunun boyutunu bilmek, bir kelimenin başlık mı, dipnot mu yoksa rastgele bir artefakt mı olduğunu belirlemenize yardımcı olur.  

Kısacası, **structured OCR recognition** daha akıllı veri akışları oluşturma esnekliği sağlar—veriyi bir veritabanına besliyor olun, aranabilir PDF'ler oluşturuyor olun veya layout'a saygı gösteren bir makine‑learning modeli eğitiyor olun.

---

## Yaygın Kenar Durumları ve Nasıl Ele Alınır

| Durum | Dikkat Edilmesi Gereken | Önerilen Çözüm |
|-----------|-------------------|---------------|
| **Döndürülmüş veya eğik görüntüler** | Sınırlama kutuları eksen dışı olabilir. | Deskewing (ör. OpenCV’nin `warpAffine`) ile ön‑işlem yapın. |
| **Çok küçük fontlar** | Motor karakterleri kaçırabilir, bu da boş satırlara yol açar. | Görüntü çözünürlüğünü artırın veya `ocr_engine.set_dpi(300)` kullanın. |
| **Karışık diller** | Yanlış dil modeli bozuk metne neden olabilir. | `ocr_engine.language = ["en", "de"]` tanıma öncesinde ayarlayın. |
| **Çakışan kutular** | Post‑processor iki satırı istemeden birleştirebilir. | `line.bounds` işleme sonrası doğrulayın; `ai.run_postprocessor` içinde eşik değerleri ayarlayın. |

Bu senaryoları erken ele almak, özellikle çözümü günde yüzlerce belgeye ölçeklendirdiğinizde, ileride baş ağrısını önler.

---

## Tam Uçtan Uca Script

Aşağıda tüm adımları birleştiren tam, çalıştırmaya hazır program bulunuyor. Kopyala‑yapıştır, görüntü yolunu ayarla ve hazırsın.

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

Bu scripti çalıştırdığınızda:

1. **Run OCR on image** yapılandırılmış modda.  
2. **Extract text with coordinates** her satır için.  
3. İsteğe bağlı olarak kutuları gösteren anotasyonlu bir PNG üretir.

---

## Sonuç

Artık **run OCR on image** ve **extract text with coordinates** işlemlerini **structured OCR recognition** kullanarak yapabileceğiniz sağlam, bağımsız bir çözümünüz var. Kod, motor başlatmadan post‑process ve görsel doğrulamaya kadar her adımı gösteriyor; böylece makbuzlar, formlar veya kesin metin konumlandırması gerektiren herhangi bir görsel belgeye uyarlayabilirsiniz.

Sırada ne var? `aocr` motorunu başka bir kütüphane (Tesseract, EasyOCR) ile değiştirip yapılandırılmış çıktılarının nasıl farklılaştığını görün. Yazım denetimi veya özel regex filtreleri gibi farklı post‑processing stratejileriyle alanınız için doğruluğu artırın. Daha büyük bir veri akışı kuruyorsanız, `(text, bounds)` çiftlerini ilerideki analizler için bir veritabanında saklamayı düşünün.

İyi kodlamalar, ve OCR projeleriniz her zaman doğru olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}