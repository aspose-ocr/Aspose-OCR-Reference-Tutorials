---
category: general
date: 2026-07-05
description: Görüntüyü hızlıca eğriltmeyi düzeltme. OCR için görüntüyü ön işleme,
  görüntü dönüşünü düzeltme ve taramayı Python ile metne dönüştürmeyi öğrenin.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- convert scan to text
- correct image rotation
language: tr
og_description: Görüntüyü eğriltme düzeltme ve OCR için ön işleme nasıl yapılır. Bu
  rehber, görüntü döndürmesini nasıl düzelteceğinizi ve Python kullanarak görüntüden
  metin nasıl çıkarılacağını gösterir.
og_title: Görüntüyü Eğrilikten Düzeltme – Adım Adım OCR Ön İşleme
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to deskew image quickly. Learn to preprocess image for OCR, correct
    image rotation, and convert scan to text with Python.
  headline: How to Deskew Image – Complete Guide for OCR Preprocessing
  type: TechArticle
tags:
- OCR
- image-processing
- Python
title: Görüntüyü Düzeltme – OCR Ön İşleme İçin Tam Rehber
url: /tr/python-java/general/how-to-deskew-image-complete-guide-for-ocr-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüyü Eğriltmeyi Düzeltme – OCR Ön İşleme İçin Tam Kılavuz

Hiç **görüntüyü eğriltmeyi düzeltme** dosyalarının eğri bir tarayıcıdan alınmış gibi göründüğünü merak ettiniz mi? Tek başınıza değilsiniz. Birçok gerçek dünya projesinde **görüntüden metin çıkarma** işlemine başlamadan önce yapmanız gereken ilk şey bu eğimi düzeltmektir.  

Bu öğreticide, **OCR için görüntüyü ön işleme** yapan, döndürmeyi düzelten ve sonunda bir Python OCR kütüphanesi kullanarak **tarama dosyasını metne dönüştüren** uygulamalı, uçtan uca bir örnek üzerinden ilerleyeceğiz. Belirsiz referanslar yok, sadece kopyalayıp‑yapıştırabileceğiniz çalışan bir betik ve yaygın hatalar üzerine ipuçları.  

## Başaracaklarınız

* Hafif eğimli herhangi bir taranmış JPEG veya PNG dosyasını yükleyin.  
* OCR doğruluğunu artırmak için bir eğriltme filtresi ve bir ikilileştirme adımı uygulayın.  
* OCR motorunu çalıştırın ve **görüntüden metin çıkarma** işlemini güvenilir bir şekilde gerçekleştirin.  
* **Doğru görüntü döndürme**'nin sonraki metin çıkarma sürecinde neden önemli olduğunu anlayın.  

### Önkoşullar

* Makinenizde Python 3.9+ yüklü olmalı.  
* Örnekte kullanılan `ocr` ad alanını taklit eden bir pip‑installable OCR paketi (örneğin, Tesseract etrafında ince bir sarmalayıcı).  
* Python fonksiyonları ve görüntü işleme kavramlarına temel aşinalık.  

Eğer bunlara sahipseniz, başlayalım.

![how to deskew image example](deskew_before_after.png){alt="görüntüyü eğriltmeyi düzeltme – düzeltme öncesi ve sonrası"}

## Adım 1: OCR Motorunu Kurun – Python Kullanarak Görüntüyü Eğriltmeyi Düzeltme

İlk olarak, belgenizin dilini anlayabilecek bir OCR motoruna ihtiyacınız var. Aşağıdaki kod parçacığı, motoru oluşturmak ve İngilizce metinle çalıştığınızı belirtmek için gerekli minimum temel kodu gösterir.

```python
import ocr  # Assume this is a wrapper around your OCR backend

# Create an OCR engine instance and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH
```

*Nasıl önemli:* Motorun dil ayarı, kullandığı karakter seti ve sözlüğü etkiler. Bu adımı atlamak, OCR'nin yaygın kelimeleri yanlış yorumlamasına neden olabilir, özellikle **görüntü döndürmeyi düzelttikten** sonra.

## Adım 2: Düzeltmek İstediğiniz Taranmış Görüntüyü Yükleyin

Şimdi dosyayı belleğe alıyoruz. `"YOUR_DIRECTORY/skewed_scan.jpg"` ifadesini kendi görüntünüzün yolu ile değiştirin.

```python
# Load the raw scanned image
raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")
```

Görüntü zaten bir NumPy dizisi ya da OpenCV `Mat` içinde ise, yükleyiciyi buna göre uyarlayabilirsiniz – önemli olan nesnenin daha sonra kullanılan `apply_filter` metodunu sunmasıdır.

## Adım 3: OCR İçin Görüntüyü Ön İşleme – Eğriltmeyi Düzeltme ve İkilileştirme

İşte sihrin gerçekleştiği yer. İki filtreyi zincirleme uyguluyoruz:

1. **Deskew** – baskın metin taban çizgisini otomatik olarak algılar ve görüntüyü yataya döndürür.  
2. **Binarize (Otsu)** – resmi saf siyah‑beyaz hâle getirir, bu da tanıma oranlarını büyük ölçüde artırır.

```python
# Preprocess: deskew then binarize
preprocessed_image = (
    raw_image
    .apply_filter(ocr.Filter.deskew())          # <-- how to deskew image
    .apply_filter(ocr.Filter.binarize_otsu())  # improves OCR reliability
)
```

*Pro ipucu:* İkilileştirmeden sonra metnin hâlâ bulanık göründüğünü fark ederseniz, kontrastı ayarlamayı veya farklı bir eşikleme yöntemi kullanmayı deneyin. `ocr.Filter` modülü genellikle zorlu durumlar için `adaptive_threshold()` içerir.

## Adım 4: OCR Çalıştır – Görüntüden Metin Çıkarma

Temiz ve düzeltilmiş bir kanvasla, görüntüyü motora veriyoruz. Sonuç nesnesi tanınan dizeyi, güven skorlarını ve gerekirse daha sonra kullanabileceğiniz sınırlama kutularını içerir.

```python
# Perform recognition on the preprocessed image
recognition_result = engine.recognize(preprocessed_image)

# Print the raw text output
print(recognition_result.text)
```

Tipik çıktı şu şekildedir:

```
Invoice #12345
Date: 2026-07-01
Total: $1,250.00
Thank you for your business!
```

Satır sonlarının mükemmel hizalandığını fark ettiniz mi? Bu, **doğru görüntü döndürme**'nin faydasıdır – OCR artık satır yönünü tahmin etmek zorunda değil.

## Adım 5: Hepsini Bir Araya Getir – Tarama Dosyasını Metne Dönüştüren Tek‑Dosya Betiği

Aşağıda, tartıştığımız tüm parçaları birleştiren tam, çalıştırılabilir betik yer alıyor. `deskew_ocr.py` olarak kaydedin ve `python deskew_ocr.py` komutuyla çalıştırın.

```python
#!/usr/bin/env python3
"""
Complete example: how to deskew image, preprocess it for OCR,
and extract text from a scanned document.
"""

import ocr  # Replace with your actual OCR library import

def main():
    # 1️⃣ Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Load the image (change path as needed)
    raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")

    # 3️⃣ Preprocess – deskew then binarize
    preprocessed = (
        raw_image
        .apply_filter(ocr.Filter.deskew())          # how to deskew image
        .apply_filter(ocr.Filter.binarize_otsu())  # preprocess image for OCR
    )

    # 4️⃣ Recognize text
    result = engine.recognize(preprocessed)

    # 5️⃣ Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

### Neden Bu Çalışıyor

* **Önce eğriltmeyi düzelt** – görüntüyü ikilileştirmeden önce döndürmek, eşikleme algoritmasının düz bir ufukta çalışmasını sağlar.  
* **Eğriltmeyi düzelttikten sonra ikilileştir** – Otsu yöntemi ikili bir histogram varsayar; eğik bir sayfa bu varsayımı bozar.  
* **İngilizce dil modeli** – OCR'ye hangi karakterlerin beklendiğini söyler, yanlış pozitifleri azaltır.  

Başka dilleri işlemek isterseniz, sadece `ocr.Language.ENGLISH` ifadesini uygun enum ile değiştirin.

## Yaygın Sorular & Kenar Durumları

| Soru | Cevap |
|----------|--------|
| *Tarama dosyası baş aşağı olursa ne olur?* | `deskew()` filtresi genellikle 180° döndürmeyi de algılar. Başarısız olursa, eğriltmeyi düzeltmeden önce `apply_filter(ocr.Filter.rotate(180))` çağırın. |
| *Belgemde renkli grafikler var – ikilileştirme onları silecek mi?* | Evet. Karışık içerik için yalnızca `ocr.Filter.deskew()` kullanmayı düşünün, ardından renkli görüntüde OCR çalıştırın. Grafikleri korurken hâlâ metin çıkarabilirsiniz. |
| *Bir dosya topluluğunu işleyebilir miyim?* | Mantığı bir döngüye sarın, her dosya yolunu bir listeden okuyun ve her `result.text` değerini ayrı bir `.txt` dosyasına kaydedin. |
| *Düşük çözünürlüklü taramalarda doğruluğu nasıl artırabilirim?* | Görüntüyü bir bikübik filtre ile **eğriltmeyi düzeltmeden** önce ölçeklendirin, ardından bir keskinleştirme filtresi uygulayın. Daha fazla piksel OCR motoruna daha iyi ipuçları sağlar. |

## Bonus: Eğriltmeyi Düzeltmenin Görsel Doğrulaması

Ön‑ve‑sonu yan yana görmek isterseniz, hızlı bir Matplotlib kod parçacığı ekleyin:

```python
import matplotlib.pyplot as plt

def show_comparison(original, processed):
    fig, axs = plt.subplots(1, 2, figsize=(10, 4))
    axs[0].imshow(original.to_numpy(), cmap='gray')
    axs[0].set_title('Original')
    axs[0].axis('off')

    axs[1].imshow(processed.to_numpy(), cmap='gray')
    axs[1].set_title('Deskewed & Binarized')
    axs[1].axis('off')
    plt.show()

show_comparison(raw_image, preprocessed)
```

## Sonuç

**görüntüyü eğriltmeyi düzeltme** dosyalarını, **OCR için görüntüyü ön işleme**'nin neden önemli olduğunu ve **görüntüden metin çıkarma** yoluyla sonunda **tarama dosyasını metne dönüştürme** konularını ele aldık. İş akışı—yükle → eğriltmeyi düzelt → ikilileştir → tanı →—OCR'nin temiz, düz bir sayfa görmesini sağlar; bu da daha yüksek doğruluk ve daha az manuel düzeltme anlamına gelir.

OCR yolculuğunuzda bir sonraki adım ne? Şunları deneyin:

* Farklı dil paketleri (`ocr.Language.FRENCH` vb.).  
* Sütun veya tablo tespiti için bir yerleşim analizi adımı eklemek.  
* OCR sonuçlarını bir PDF kütüphanesi kullanarak aranabilir PDF'lere aktarmak.  

Bir sorunla karşılaşırsanız yorum bırakmaktan çekinmeyin ya da özellikle inatçı taramaları ele almak için kendi ayarlamalarınızı paylaşın. İyi kodlamalar, ve görüntüleriniz her zaman mükemmel düz olsun!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [AspOCR Nasıl Kullanılır: .NET için Görüntü OCR Filtrelerini Ön İşleme](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Aspose.OCR Kullanarak C# ile Görüntü Metni Çıkarma ve Dil Seçimi](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Görüntüyü OCR Yapma – OCR Görüntü Tanıma’da Görüntü Üzerinde OCR Gerçekleştirme](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}