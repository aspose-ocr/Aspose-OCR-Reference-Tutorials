---
category: general
date: 2026-05-31
description: OCR doğruluğunu Python ile artırmak için görüntüleri OCR öncesinde işleyin.
  Görüntü dosyalarından metin çıkarmayı, PNG’den metin tanımayı ve sonuçları iyileştirmeyi
  öğrenin.
draft: false
keywords:
- improve OCR accuracy
- preprocess image for OCR
- extract text from image
- recognize text from PNG
- image preprocessing for text
language: tr
og_description: Python'da metin için görüntü ön işleme uygulayarak OCR doğruluğunu
  artırın. Görüntü dosyalarından metin çıkarmak ve PNG'den metni zahmetsizce tanımak
  için bu rehberi izleyin.
og_title: Python'da OCR Doğruluğunu Artırma – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Improve OCR accuracy with Python by preprocessing images for OCR. Learn
    how to extract text from image files, recognize text from PNG, and boost results.
  headline: Improve OCR Accuracy in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Improve OCR accuracy with Python by preprocessing images for OCR. Learn
    how to extract text from image files, recognize text from PNG, and boost results.
  name: Improve OCR Accuracy in Python – Complete Step‑by‑Step Guide
  steps:
  - name: Loads the PNG into memory
    text: Loads the PNG into memory
  - name: Applies denoise and deskew based on our settings
    text: Applies denoise and deskew based on our settings
  - name: Runs the neural‑network or classic pattern matcher
    text: Runs the neural‑network or classic pattern matcher
  - name: Packages the output into `recognition_result`
    text: Packages the output into `recognition_result`
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python'da OCR Doğruluğunu Geliştirin – Tam Adım Adım Rehber
url: /tr/python-java/general/improve-ocr-accuracy-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da OCR Doğruluğunu Artırma – Tam Adım‑Adım Kılavuz

OCR doğruluğunu **artırmaya** çalıştığınızda çıktının karışık geldiğini hiç gördünüz mü? Tek başınıza değilsiniz. Çoğu geliştirici, ham görüntü gürültülü, eğik ya da düşük kontrast olduğunda takılı kalıyor. İyi haber? Birkaç ön‑işleme tekniği, bulanık bir ekran görüntüsünü temiz, makine‑okunur bir metne dönüştürebilir.

Bu öğreticide, **görüntüyü OCR için ön‑işleyen**, tanıma motorunu çalıştıran ve sonunda **görüntüden metin çıkaran** gerçek bir örnek üzerinden ilerleyeceğiz – özellikle bir PNG dosyası için. Sonuna kadar **PNG'den metin tanıma** işlemini daha yüksek bir başarı oranıyla nasıl yapacağınızı öğrenecek ve herhangi bir projeye ekleyebileceğiniz yeniden kullanılabilir bir kod parçacığına sahip olacaksınız.

## Neler Öğreneceksiniz

- OCR motorları için görüntü ön‑işlemenin neden önemli olduğu  
- En büyük performans artışını sağlayan ön‑işleme modları (gürültü giderme, eğik düzeltme)  
- Python’da bir `OcrEngine` örneğinin nasıl yapılandırılacağı  
- **Görüntüden metin çıkaran** tam, çalıştırılabilir betik  
- Döndürülmüş taramalar ya da düşük çözünürlüklü fotoğraflar gibi uç durumların nasıl ele alınacağı  

OCR SDK dışındaki ek kütüphanelere gerek yok, ancak Python 3.8+ ve okumak istediğiniz bir PNG görüntüsü gerekir.

---

![Diagram showing steps to improve OCR accuracy in Python](image.png "Improve OCR accuracy workflow")

*Alt metin: OCR doğruluğunu artırma iş akışını gösteren, ön‑işleme ve tanıma adımlarını açıklayan diyagram.*

## Önkoşullar

- Python 3.8 veya daha yeni bir sürümünün yüklü olması  
- `OcrEngine`, `OcrEngineSettings` ve `ImagePreprocessMode` sağlayan OCR SDK'sına erişim (aşağıdaki kod genel bir API kullanıyor; gerekirse satıcı sınıflarınızla değiştirin)  
- Bir PNG görüntüsü (`input.png`) erişebileceğiniz bir klasörde bulunmalı  

Sanal ortam kullanıyorsanız, şimdi etkinleştirin—fantezi bir şey yok, sadece `python -m venv venv && source venv/bin/activate`.

---

## Adım 1: OCR Motoru Örneğini Oluşturun – OCR Doğruluğunu Artırmaya Başlayın

İlk olarak bir OCR motor nesnesine ihtiyacınız var. Bunu, pikselleri okuyup karakterleri üretecek beyin olarak düşünün.

```python
# Step 1: Initialise the OCR engine
ocr_engine = OcrEngine()
```

Neden önemli: bir motor olmadan hiçbir ön‑işleme uygulayamazsınız ve ham görüntü doğrudan tanıyıcıya verilir—genellikle doğruluk açısından en kötü senaryo.

---

## Adım 2: Hedef PNG'yi Yükleyin – PNG'den Metin Tanıma İçin Sahneyi Hazırlayın

Şimdi motorun üzerinde çalışacağı dosyayı belirtiyoruz. PNG kayıpsızdır, bu da JPEG'e göre bize küçük bir avantaj sağlar.

```python
# Step 2: Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/input.png")
```

Görüntü başka bir yerde ise yolu sadece ayarlayın. Motor, desteklenen herhangi bir formatı kabul eder, ancak PNG genellikle keskin karakter kenarları için gereken ince detayları korur.

---

## Adım 3: Ön‑İşlemeyi Yapılandırın – OCR İçin Görüntüyü Ön‑İşleyin

İşte sihrin gerçekleştiği yer. Bir ayar nesnesi oluşturuyor, lekeleri silmek için gürültü giderme etkinleştiriyor ve eğik metni otomatik olarak düzeltmek için eğik düzeltmeyi açıyoruz.

```python
# Step 3: Prepare preprocessing settings to improve accuracy
preprocess_settings = OcrEngineSettings()
preprocess_settings.preprocess_mode = (
    ImagePreprocessMode.DENOISE | ImagePreprocessMode.DESKEW
)
```

### Neden Gürültü Giderme + Eğik Düzeltme?

- **Gürültü Giderme**: Rastgele piksel gürültüsü, desen‑eşleştirme algoritmalarını şaşırtır. Onu kaldırmak harfleri keskinleştirir.  
- **Eğik Düzeltme**: 2 derecelik bir eğim bile güven skorlarını büyük ölçüde düşürebilir. Eğik düzeltme, temel çizgiyi hizalayarak tanıyıcının fontları daha güvenilir eşleştirmesini sağlar.

Görüntüleriniz özellikle karanlıksa ek bayraklarla (ör. `ImagePreprocessMode.CONTRAST_ENHANCE`) deney yapabilirsiniz. SDK dokümantasyonu genellikle tüm kullanılabilir modları listeler.

---

## Adım 4: Ayarları Motora Uygulayın – Ön‑İşlemeyi OCR'a Bağlayın

Ayar nesnesini motora atayın, böylece bir sonraki tanıma çalışması tanımladığımız dönüşümleri kullanır.

```python
# Step 4: Apply the settings to the engine
ocr_engine.settings = preprocess_settings
```

Bu adımı atlayarsanız, motor varsayılanına (çoğu zaman “ön‑işleme yok”) geri döner ve **daha düşük OCR doğruluğu** görürsünüz.

---

## Adım 5: Tanıma Sürecini Çalıştırın – Görüntüden Metin Çıkarın

Her şey bağlandıktan sonra, motoru işini yapması için son olarak çağırıyoruz. Çağrı senkroniktir ve tanınan dizeyi içeren bir sonuç nesnesi döner.

```python
# Step 5: Run the recognition process
recognition_result = ocr_engine.recognize()
```

Arka planda motor şimdi:

1. PNG'yi belleğe yükler  
2. Ayarlarımıza göre gürültü giderme ve eğik düzeltme uygular  
3. Sinir ağı ya da klasik desen eşleştiriciyi çalıştırır  
4. Çıktıyı `recognition_result` içine paketler

---

## Adım 6: Tanınan Metni Çıktılayın – İyileşmeyi Doğrulayın

Çıkarılan dizeyi ekrana yazdıralım. Gerçek bir uygulamada bunu bir dosyaya, veritabanına ya da başka bir servise gönderebilirsiniz.

```python
# Step 6: Output the recognized text
print(recognition_result.text)
```

### Beklenen Çıktı

Görüntü “Hello, OCR World!” cümlesini içeriyorsa şu satırı görmelisiniz:

```
Hello, OCR World!
```

Metnin temiz olduğunu fark edin—gereksiz semboller ya da kırık karakterler yok. Bu, **metin için görüntü ön‑işlemenin** doğru uygulanmasının sonucudur.

---

## Pro İpuçları & Uç Durumlar

| Durum | Ne Ayarlanmalı | Neden |
|-----------|----------------|-----|
| Çok düşük çözünürlüklü PNG (≤ 72 dpi) | `ImagePreprocessMode.SUPER_RESOLUTION` mevcutsa ekleyin | Upsampling, tanıyıcıya daha fazla piksel sağlayarak doğruluğu artırabilir |
| Metin 5° den fazla döndürülmüş | Eğik düzeltme toleransını artırın veya motoru beslemeden önce `Pillow` ile manuel döndürün | Aşırı açıların otomatik eğik düzeltmeyi atlaması olasıdır |
| Yoğun arka plan desenleri | `ImagePreprocessMode.BACKGROUND_REMOVAL` etkinleştirin | Metin dışı gürültüyü kaldırarak yanlış okuma riskini azaltır |
| Çok dilli belge | `ocr_engine.language = "eng+spa"` (veya benzeri) ayarlayın | Motor doğru karakter setini seçer, genel doğruluğu artırır |

Unutmayın, **OCR doğruluğunu artırma** tek bir çözüm değildir; veri setinize göre ön‑işleme bayraklarını yinelemeniz gerekebilir.

---

## Tam Betik – Kopyala & Yapıştır İçin Hazır

Aşağıda, tartıştığımız tüm adımları içeren, çalıştırılabilir tam örnek bulunuyor. `improve_ocr_accuracy.py` olarak kaydedin ve `python improve_ocr_accuracy.py` komutuyla çalıştırın.

```python
"""
Improve OCR Accuracy in Python – Full Example
Author: Your Name (2026)
Requires: OCR SDK providing OcrEngine, OcrEngineSettings, ImagePreprocessMode
"""

# Import the necessary classes from the OCR SDK
from ocr_sdk import OcrEngine, OcrEngineSettings, ImagePreprocessMode

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the PNG you want to read
    image_path = "YOUR_DIRECTORY/input.png"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure preprocessing: denoise + deskew
    preprocess_settings = OcrEngineSettings()
    preprocess_settings.preprocess_mode = (
        ImagePreprocessMode.DENOISE | ImagePreprocessMode.DESKEW
    )

    # 4️⃣ Apply the settings
    ocr_engine.settings = preprocess_settings

    # 5️⃣ Run recognition
    recognition_result = ocr_engine.recognize()

    # 6️⃣ Print the extracted text
    print("=== Recognized Text ===")
    print(recognition_result.text)

if __name__ == "__main__":
    main()
```

Çalıştırın, konsolu izleyin ve **görüntüden metin çıkarma** sonucunu anında göreceksiniz. Çıktı beklentilerinizi karşılamazsa, “Pro İpuçları” tablosunda anlatıldığı gibi `preprocess_mode` bayraklarını ayarlayın.

---

## Sonuç

Python kullanarak **OCR doğruluğunu artırma** için pratik bir tarif üzerinden geçtik. Bir `OcrEngine` oluşturup bir PNG yükleyerek, **OCR için görüntüyü ön‑işleyip**, ardından **PNG'den metin tanıma** yaparak, kaynak mükemmel olmasa bile **görüntüden metin çıkarma** işlemini güvenilir bir şekilde gerçekleştirebilirsiniz.  

Sonraki adımlar? Bir döngüyle birden fazla görüntüyü işleyin, her sonucu bir CSV'ye kaydedin ya da kontrast artırma gibi ek ön‑işleme modlarıyla deney yapın. Aynı desen PDF'ler, taranmış makbuzlar ya da el yazısı notlar için de çalışır—sadece girdi dosyasını değiştirin ve ayarları uyarlayın.

Belirli bir görüntü türü hakkında sorularınız mı var ya da bunu bir web servisine nasıl entegre edeceğinizi merak ediyor musunuz? Yorum bırakın, birlikte bu senaryoları keşfedelim. Mutlu kodlamalar, OCR sonuçlarınız her daim kristal‑gibi berrak olsun!

## Sonraki Öğrenmeniz Gerekenler

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}