---
category: general
date: 2026-03-28
description: Görüntüde OCR gerçekleştir ve sınırlayıcı kutu koordinatlarıyla temiz
  metin al. OCR'yi nasıl çıkaracağınızı, OCR'yi nasıl temizleyeceğinizi ve sonuçları
  adım adım nasıl görüntüleyeceğinizi öğrenin.
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: tr
og_description: Görüntüde OCR yapın, çıktıyı temizleyin ve sınırlayıcı kutu koordinatlarını
  kısa bir öğreticide gösterin.
og_title: Görselde OCR Yap – Temiz Sonuçlar ve Sınır Kutuları
tags:
- OCR
- Computer Vision
- Python
title: Görüntüde OCR Gerçekleştir – Temiz Sonuçlar ve Sınırlama Kutusu Koordinatlarını
  Göster
url: /tr/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüde OCR Yap – Sonuçları Temizle ve Sınırlayıcı Kutu Koordinatlarını Göster

Görüntü dosyalarında **OCR yapma** ihtiyacı hissettiniz ama dağınık metinler alıyordunuz ve her kelimenin resimde nerede olduğunu bilemiyordunuz? Tek başınıza değilsiniz. Birçok projede—fatura dijitalleştirme, fiş tarama veya basit metin çıkarma—ham OCR çıktısını elde etmek sadece ilk engeldir. İyi haber? Bu çıktıyı temizleyebilir ve çok fazla tekrarlayan kod yazmadan her bölgenin sınırlayıcı kutu koordinatlarını anında görebilirsiniz.

Bu rehberde **OCR çıkarımını nasıl yapacağınızı**, bir **OCR temizleme** sonrası işlemcisini nasıl çalıştıracağınızı ve sonunda her temizlenmiş bölge için **sınırlayıcı kutu koordinatlarını nasıl göstereceğinizi** adım adım inceleyeceğiz. Sonunda bulanık bir fotoğrafı, sonraki işlemler için hazır, düzenli ve yapılandırılmış metne dönüştüren tek bir çalıştırılabilir betiğe sahip olacaksınız.

## Gereksinimler

- Python 3.9+ (aşağıdaki sözdizimi 3.8 ve üzeri sürümlerde çalışır)
- `recognize(..., return_structured=True)` destekleyen bir OCR motoru – örneğin, kod parçacığında kullanılan kurgusal `engine` kütüphanesi. Bunu Tesseract, EasyOCR veya bölge verisi dönen herhangi bir SDK ile değiştirin.
- Python fonksiyonları ve döngülerine temel aşinalık
- Taramak istediğiniz bir görüntü dosyası (PNG, JPG, vb.)

> **Pro ipucu:** Tesseract kullanıyorsanız, `pytesseract.image_to_data` fonksiyonu zaten sınırlayıcı kutuları verir. Sonucunu, aşağıda gösterilen `engine.recognize` API'sini taklit eden küçük bir adaptöre sarabilirsiniz.

---

![görüntüde OCR yapma örneği](image-placeholder.png "görüntüde OCR yapma örneği")

*Alt metin: görüntüde OCR yapma ve sınırlayıcı kutu koordinatlarını görselleştirme diyagramı*

## Adım 1 – Görüntüde OCR Yap ve Yapılandırılmış Bölgeleri Al

İlk olarak OCR motorundan yalnızca düz metin değil, aynı zamanda metin bölgelerinin yapılandırılmış bir listesini döndürmesini istemeniz gerekir. Bu liste ham dizeyi ve onu çevreleyen dikdörtgeni içerir.

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**Neden Önemli:**  
Sadece düz metin istediğinizde uzamsal bağlamı kaybedersiniz. Yapılandırılmış veri, daha sonra **sınırlayıcı kutu koordinatlarını görüntülemenizi**, metni tablolarla hizalamanızı veya kesin konumları sonraki bir modele beslemenizi sağlar.

## Adım 2 – OCR Çıktısını Bir Post‑İşlemciyle Nasıl Temizlersiniz

OCR motorları karakterleri tespit etmede iyidir, ancak genellikle gereksiz boşluklar, satır sonu artefaktları veya hatalı tanınan semboller bırakır. Bir post‑işlemci metni normalleştirir, yaygın OCR hatalarını düzeltir ve boşlukları temizler.

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

Kendi temizleyicinizi oluşturuyorsanız, şunları göz önünde bulundurun:

- ASCII olmayan karakterleri kaldırma (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- Birden fazla boşluğu tek bir boşluğa indirgeme
- `pyspellchecker` gibi bir yazım denetleyicisi uygulamak, belirgin yazım hatalarını düzeltmek için

**Neden Önemli:**  
Düzenli bir dize, arama, indeksleme ve sonraki NLP boru hatlarını çok daha güvenilir kılar. Başka bir deyişle, **OCR nasıl temizlenir** çoğu zaman kullanılabilir bir veri seti ile baş ağrısı arasındaki farktır.

## Adım 3 – Her Temizlenmiş Bölge İçin Sınırlayıcı Kutu Koordinatlarını Göster

Metin artık düzenli olduğuna göre, her bölgeyi döngüye alıp dikdörtgenini ve temizlenmiş dizesini yazdırıyoruz. İşte sonunda **sınırlayıcı kutu koordinatlarını gösterdiğimiz** kısım.

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**Örnek çıktı**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

Artık bu koordinatları bir çizim kütüphanesine (ör. OpenCV) besleyerek orijinal görüntü üzerine kutular çizebilir veya daha sonraki sorgular için bir veritabanında saklayabilirsiniz.

## Tam, Çalıştırmaya Hazır Betik

Aşağıda üç adımı birleştiren tam program yer alıyor. Yer tutucu `engine` çağrılarını gerçek OCR SDK'nızla değiştirin.

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### Nasıl Çalıştırılır

```bash
python perform_ocr.py sample_invoice.jpg
```

Yukarıdaki örnek çıktıya benzer şekilde, temizlenmiş metinle eşleşen sınırlayıcı kutu listesini görmelisiniz.

## Sık Sorulan Sorular & Kenar Durumları

| Soru | Cevap |
|----------|--------|
| **OCR motoru `return_structured` desteklemiyorsa ne olur?** | Motorun ham çıktısını (genellikle koordinatları olan kelimeler listesi) `text` ve `bounding_box` özniteliklerine sahip nesnelere dönüştüren ince bir sarmalayıcı yazın. |
| **Güven skorları alabilir miyim?** | Birçok SDK, bölge başına bir güven metriği sunar. Bunu yazdırma ifadesine ekleyin: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **Döndürülmüş metni nasıl ele alırsınız?** | `recognize` çağırmadan önce OpenCV'nin `cv2.minAreaRect` fonksiyonuyla görüntüyü düzleştirerek ön işleme yapın. |
| **Çıktıyı JSON formatında ihtiyacım olursa ne yapmalıyım?** | `processed_result.regions` öğesini `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)` ile serileştirin. |
| **Kutuları görselleştirmenin bir yolu var mı?** | Döngü içinde OpenCV kullanın: `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)`, ardından `cv2.imwrite("annotated.jpg", img)`. |

## Sonuç

Şimdi **görüntüde OCR nasıl yapılır**, ham çıktının nasıl temizlenir ve her bölge için **sınırlayıcı kutu koordinatlarının nasıl gösterilir** öğrendiniz. Tanıma → post‑işlem → yineleme adımlarından oluşan üç adımlı akış, güvenilir metin çıkarımı gerektiren herhangi bir Python projesine ekleyebileceğiniz yeniden kullanılabilir bir desendir.

### Sıradaki Adımlar?

- **Farklı OCR arka uçlarını keşfedin** (Tesseract, EasyOCR, Google Vision) ve doğruluklarını karşılaştırın.
- Bölge verilerini aranabilir arşivler için saklamak amacıyla **bir veritabanıyla bütünleştirin**.
- Her bölgeyi uygun yazım denetleyicisine yönlendirmek için **dil tespiti ekleyin**.
- Görsel doğrulama için **kutuları orijinal görüntünün üzerine bindirin** (yukarıdaki OpenCV kod parçacığına bakın).

Eğer tuhaflıklarla karşılaşırsanız, en büyük kazancın sağlam bir post‑işlem adımından geldiğini unutmayın; temiz bir dize, karakterlerin ham dökümünden çok daha kolay işlenir.

Kodlamaktan keyif alın, ve OCR boru hatlarınız her zaman düzenli olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}