---
category: general
date: 2026-03-26
description: Seçilen alanda OCR çalıştırmak için ROI çokgeni oluşturun. Birden fazla
  bölgeyi nasıl tanımlayacağınızı, kaydedeceğinizi ve bir Python OCR motoru ile metin
  çıkaracağınızı öğrenin.
draft: false
keywords:
- create roi polygon
- ocr on selected area
- region of interest
- ocr engine
- python ocr example
language: tr
og_description: Python motoru ile ROI çokgeni oluşturun ve seçilen alanda OCR çalıştırın.
  Tam kod, açıklamalar ve ipuçları dahil.
og_title: ROI Poligonu Oluştur – Seçili Alanda Hızlı OCR
tags:
- OCR
- Python
- Image Processing
title: ROI Poligonu Oluştur – Seçilen Alanda OCR için Adım Adım Kılavuz
url: /tr/python-java/general/create-roi-polygon-step-by-step-guide-for-ocr-on-selected-ar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ROI Polygon Oluşturma – Seçili Alan Üzerinde OCR İçin Tam Kılavuz

Hiç **ROI polygon** oluşturmanız gerekti ve sadece görüntünün önemli kısmında OCR çalıştırmak istediniz mi? Belki makbuzları tarıyorsunuz ve sadece toplamlar önemli, ya da bir formunuz var ve sadece imza alanının okunması gerekiyor. Bu durumlarda, **seçili alanda OCR** zaman kazandırır ve doğruluğu artırır.  

Bu rehberde ihtiyacınız olan her şeyi adım adım ele alacağız: iki poligon tanımlamaktan, bunları bir OCR motoruna kaydetmeye, tanınan metni tek bir temiz çağrıyla almaya kadar. Sonunda çalıştırmaya hazır bir betiğiniz ve ilgi alanlarına odaklanmanın neden önemli olduğuna dair sağlam bir anlayışınız olacak.

## Öğrenecekleriniz

- Tipik bir OCR kütüphanesi kullanarak **ROI polygon** nesneleri **nasıl oluşturulur**.
- Tek bir bölge tanımlamak ile birden fazla bölge tanımlamak arasındaki fark.
- Bu bölgeleri motorla **kayıt etmek** ve `seçili alanda OCR`un nasıl gerçekleştirileceği.
- Beklenen çıktı ve yaygın tuzakların (ör. çakışan ROI’lar, boş sonuçlar) nasıl giderileceği.

### Önkoşullar

- Python 3.8+ yüklü.
- `Polygon`, `Point` ve `add_region_of_interest` metodlarını sunan bir OCR kütüphanesi (örnek, hayali bir `ocr` modülü kullanıyor; gerçek SDK’nızla, ör. Tesseract‑Python sarmalayıcıları veya EasyOCR, değiştirin).
- Aşağıdaki koordinatlarda metin içeren bir örnek görüntü dosyası (`sample.png`).

> **Pro tip:** Gerçek bir kütüphane kullanıyorsanız, görüntünün aynı koordinat uzayında yüklendiğinden emin olun (köşe sol‑üst, X sağa, Y aşağıya artar).  

---  

## Adım 1: OCR Modülünü İçe Aktarın ve Görüntünüzü Yükleyin  

İlk olarak, OCR paketini kapsam içine alın ve işlemek istediğiniz görüntüyü okuyun.  

```python
import ocr  # Replace with your actual OCR library import
from pathlib import Path

# Load the image – adjust the path as needed
image_path = Path("sample.png")
ocr_engine = ocr.Engine(image_path)
```

*Neden önemli:* Motor, **ROI polygon** eklemeden önce görüntü verisine ihtiyaç duyar. Bazı kütüphaneler görüntüyü daha sonra da alabilir, ancak erken başlatmak iş akışını düzenli tutar.

## Adım 2: İlk ROI Polygon’u Tanımlayın  

Şimdi ilk ilgi alanını oluşturuyoruz. Bunu bir tablo başlığının etrafına bir dikdörtgen çizmek gibi düşünün.  

```python
# Step 2: Define the first ROI polygon
first_roi = ocr.Polygon([
    ocr.Point(50, 20),   # top‑left
    ocr.Point(200, 20),  # top‑right
    ocr.Point(200, 80),  # bottom‑right
    ocr.Point(50, 80)    # bottom‑left
])
```

*Açıklama:*  
- `ocr.Point(x, y)` piksel koordinatlarını kullanır.  
- Nokta listesi saat yönünde sıralanmıştır; çoğu motor bunu bekler.  
- İstediğiniz kadar nokta ekleyerek düzensiz şekiller oluşturabilirsiniz; bir dikdörtgen sadece özel bir durumdur.

## Adım 3: Ek ROI Polygon’ları Tanımlayın (İsteğe Bağlı)  

Bir taneyle sınırlı kalmanız gerekmiyor. İşte sayfanın alt kısmındaki bir imza alanını yakalayan ikinci poligon.  

```python
# Step 3: Define the second ROI polygon
second_roi = ocr.Polygon([
    ocr.Point(300, 150),
    ocr.Point(480, 150),
    ocr.Point(480, 210),
    ocr.Point(300, 210)
])
```

*Neden daha fazla ekleyelim?* Birden çok bölge için **seçili alanda OCR** çalıştırmak, farklı veri parçalarını tek bir geçişte çıkarmanızı sağlar; bu, her dilimi kırpıp ayrı ayrı işlemeye göre çok daha hızlıdır.

## Adım 4: ROI’ları OCR Motoruna Kaydedin  

Poligonlar hazır olduğunda, motorun hangi alanları inceleyeceğini söyleyin.  

```python
# Step 4: Register the ROIs
ocr_engine.add_region_of_interest(first_roi)
ocr_engine.add_region_of_interest(second_roi)
```

*Önemli not:* Bazı SDK’lar, aynı motoru başka bir görüntüde yeniden kullanıyorsanız yeni bölgeler eklemeden önce `clear_regions()` metodunu çağırmanızı ister.

## Adım 5: OCR’u Çalıştırın ve Metni Alın  

Son olarak tanıma işlemini başlatın. Motor, az önce eklediğimiz poligonların içindeki alanlara bakacak.  

```python
# Step 5: Perform OCR on the defined regions
recognized_text = ocr_engine.recognize().get_text()
print("=== Recognized Text ===")
print(recognized_text)
```

**Beklenen çıktı** (örnek: `sample.png` içinde ilk ROI’da “Invoice Total: $123.45”, ikinci ROI’da “Signature: John Doe” metinleri varsa):

```
=== Recognized Text ===
Invoice Total: $123.45
Signature: John Doe
```

Çıktı boş ise, koordinatların gerçekten metinle kesiştiğini ve görüntü çözünürlüğünün koordinat sistemine uygun olduğunu tekrar kontrol edin.

## Kenar Durumları ve Yaygın Tuzaklar  

| Durum                                   | Dikkat Edilmesi Gerekenler                     | Çözüm / Çalışma Yöntemi                         |
|----------------------------------------|------------------------------------------------|-------------------------------------------------|
| **Çakışan ROI’lar**                     | Metin iki kez dönebilir.                       | Poligonları ayrık tutun veya çıktıyı tekilleştirin. |
| **ROI görüntü sınırları dışında**      | Motor hata verebilir veya hiçbir şey döndürmez. | Koordinatları `0 ≤ x < width`, `0 ≤ y < height` aralığına sınırlayın. |
| **Çok küçük ROI**                       | Yetersiz piksel nedeniyle OCR doğruluğu düşer. | Poligonu birkaç piksel genişletin veya önce görüntüyü yükseltin. |
| **Dikdörtgen olmayan şekil**            | Bazı motorlar sadece konveks poligonları destekler. | Karmaşık şekilleri birden çok konveks ROI’ya bölün. |
| **Görüntü boyutu değişiyor**            | Sabit kodlanmış koordinatlar geçersiz olur.   | ROI koordinatlarını görüntü boyutuna göre (ör. yüzde) hesaplayın. |

## Tam Çalışan Örnek  

Aşağıda, kopyalayıp yapıştırıp çalıştırabileceğiniz tam betik (gerçek kütüphanenizle `ocr` yerine geçin).  

```python
import ocr                      # <- your OCR library
from pathlib import Path

# -------------------------------------------------
# Configuration
# -------------------------------------------------
IMAGE_PATH = Path("sample.png")

# -------------------------------------------------
# Initialize OCR engine with the image
# -------------------------------------------------
engine = ocr.Engine(IMAGE_PATH)

# -------------------------------------------------
# Define ROI polygons
# -------------------------------------------------
first_roi = ocr.Polygon([
    ocr.Point(50, 20), ocr.Point(200, 20),
    ocr.Point(200, 80), ocr.Point(50, 80)
])

second_roi = ocr.Polygon([
    ocr.Point(300, 150), ocr.Point(480, 150),
    ocr.Point(480, 210), ocr.Point(300, 210)
])

# -------------------------------------------------
# Register ROIs
# -------------------------------------------------
engine.add_region_of_interest(first_roi)
engine.add_region_of_interest(second_roi)

# -------------------------------------------------
# Run OCR on the selected areas
# -------------------------------------------------
result = engine.recognize().get_text()

print("=== Recognized Text ===")
print(result)
```

`python ocr_roi_example.py` ile çalıştırın; iki tanımlı bölgeden çıkarılan metinleri görmelisiniz.

## Sonraki Adımlar  

- **Dinamik ROI üretimi:** Koordinatları sabit kodlamak yerine, görüntü işleme (ör. OpenCV kontur tespiti) kullanarak tabloları veya alanları otomatik olarak bulun.  
- **Son işlem:** Boşlukları temizleyin, regex uygulayın veya sayıları uygun veri tiplerine dönüştürün.  
- **Toplu işleme:** Görüntü klasörünü döngüye alın, düzen tutarlıysa aynı ROI tanımlarını yeniden kullanın.  

Daha karmaşık belgeler için **seçili alanda OCR** hakkında merakınız varsa—çok sayfalı PDF’ler veya taranmış formlar gibi—sayfa bazlı ROI kaydını destekleyen kütüphanelere bakın.  

---  

### Görsel Genel Bakış  

![Diagram showing two ROI polygons on a sample image](roi_diagram.png){alt="iki seçili alanı gösteren ROI poligon örneği"}

Diagram, iki dikdörtgenin (mavi ve yeşil) temel görüntü üzerine nasıl yerleştirildiğini ve OCR motorunun tam olarak neyi okuyacağını gösterir.

---  

## Sonuç  

Şimdi **ROI polygon** nesneleri oluşturduk, bunları bir OCR motoruna kaydettik ve temiz, tekrarlanabilir bir betikle `seçili alanda OCR` gerçekleştirdik. Motoru sadece ihtiyacınız olan bölgelere sınırlayarak işlem süresini kısar, doğruluğu artırır ve sonraki veri işleme adımlarını çok daha basit hâle getirirsiniz.  

Kendi görüntülerinizle deneyin—koordinatları ayarlayın, daha fazla poligon ekleyin veya çıktıyı bir veritabanına bağlayın. Bölge‑tabanlı OCR’u kavradığınızda sınırlar yoktur.  

Sorularınız mı var ya da ilginç bir kullanım senaryosu paylaşmak ister misiniz? Aşağıya yorum bırakın, mutlu kodlamalar!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}