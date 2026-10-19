---
category: general
date: 2026-06-28
description: Python ile OCR için görüntüyü ön işleme tabi tutarak doğruluğu artırın.
  Tam bir görüntü ön işleme hattını öğrenin, OCR sonuçlarını iyileştirin ve Kiril
  alfabesindeki görüntülerden metin çıkarın.
draft: false
keywords:
- preprocess image for OCR
- how to improve OCR accuracy
- python OCR with preprocessing
- image preprocessing pipeline python
- extract text from Cyrillic image
language: tr
og_description: Python’da OCR için görüntüyü ön işleme ve OCR doğruluğunu nasıl artıracağınızı
  öğrenin. Bu rehber, tam bir ön işleme hattı ve Kiril alfabesindeki görüntülerden
  metin çıkarma sürecini adım adım size gösterir.
og_title: OCR için Görüntü Ön İşleme – Tam Python Eğitimi
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Preprocess image for OCR with Python to boost accuracy. Learn a full
    image preprocessing pipeline, improve OCR results, and extract text from Cyrillic
    images.
  headline: Preprocess Image for OCR – Complete Python Guide
  type: TechArticle
- description: Preprocess image for OCR with Python to boost accuracy. Learn a full
    image preprocessing pipeline, improve OCR results, and extract text from Cyrillic
    images.
  name: Preprocess Image for OCR – Complete Python Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the code works on 3.10+ as well). - Basic familiarity
      with Python packages and virtual environments. - An OCR library that provides
      `OcrEngine`, `Language`, and `ImagePreprocessor` classes (e.g., a wrapper around
      Tesseract or a commercial SDK). - A sample Cyrillic image (`cyri'
  - name: Why These Three Steps?
    text: 1. **Deskew** – OCR engines assume left‑to‑right (or top‑to‑bottom) alignment.
      A few degrees of rotation can drop accuracy by 30 % or more. 2. **Binarize**
      – Converting to a binary image reduces the data the OCR engine must analyze,
      sharpening character edges. 3. **Denoise** – Small specks or compre
  - name: How This Improves OCR Accuracy
    text: '- By feeding a **clean, deskewed, binarized** image, the engine can focus
      on character shapes rather than fighting noise. - Specifying `Language.Cyrillic`
      activates the correct character set and language model, which is a key factor
      in **how to improve OCR accuracy** for non‑Latin scripts.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR için Görüntü Ön İşleme – Tam Python Rehberi
url: /tr/python-java/general/preprocess-image-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR için Görüntü Ön İşleme – Tam Python Rehberi

OCR için **görüntü ön işleme** nasıl yapılır, metnin kristal gibi net çıkmasını merak ettiniz mi? Tek başınıza değilsiniz—birçok geliştirici, özellikle eğik veya gürültülü Kiril alıntılarında OCR motoru bozuk karakterler ürettiğinde bir duvara çarpar. İyi haber? İyi tasarlanmış bir görüntü ön işleme hattı tanıma oranlarını büyük ölçüde artırabilir.

Bu öğreticide, deskewing, binarization ve denoising işlemlerini ele alan bir **Python OCR with preprocessing** çözümüne doğrudan dalacağız ve ardından **Cyrillic image** dosyalarından **metin çıkarma** yöntemini göstereceğiz. Sonunda yeniden kullanılabilir bir betiğe sahip olacak, **OCR doğruluğunu nasıl artıracağınızı** anlayacak ve hattı herhangi bir dil veya görüntü kaynağı için uyarlamaya hazır olacaksınız.

## Öğrenecekleriniz

- Her bir ön işleme adımının mantığını ve OCR için neden önemli olduğunu.
- **image preprocessing pipeline python**'ı nasıl birleştirip projeler arasında yeniden kullanılabilir hale getireceğinizi.
- OCR motoru oluşturup bir Kiril görüntüsünü ön işleyip tanınan metni yazdıran eksiksiz, çalıştırılabilir bir örnek.
- Aşırı eğim, düşük kontrast veya çok‑dilli belgeler gibi uç durumları ele almak için ipuçları.
- Toplu işleme, özel dil paketleri ve bulut OCR hizmetleriyle entegrasyon gibi sonraki adım fikirleri.

### Ön Koşullar

- Python 3.8 ve üzeri (kod 3.10+’da da çalışır).
- Python paketleri ve sanal ortamlarla temel aşinalık.
- `OcrEngine`, `Language` ve `ImagePreprocessor` sınıflarını sağlayan bir OCR kütüphanesi (ör. Tesseract sarmalayıcısı veya ticari bir SDK).  
- Kontrol ettiğiniz bir klasöre yerleştirilmiş örnek bir Kiril görüntüsü (`cyrillic_skewed.jpg`).

> **Pro tip:** Hazır bir OCR sarmalayıcınız yoksa, açık kaynak `pytesseract` paketine göz atın ve `opencv-python` ile eşleştirin. Bu rehberdeki kavramlar doğrudan uygulanabilir.

---

## Adım 1: Gerekli Paketleri Kurun ve İçe Aktarın

İlk olarak, bağımlılıkları halledelim. Motor ve ön işleme yardımcılarını bir araya getiren varsayımsal bir `ocr_lib` kullanacağız. `pytesseract` + OpenCV kullanıyorsanız, içe aktarmaları buna göre değiştirin.

```python
# Install the (fictional) OCR library – replace with your actual package manager command
# pip install ocr-lib

from ocr_lib import OcrEngine, Language, ImagePreprocessor
import os
```

> **Neden önemli:** Doğru sınıfları içe aktarmak, OCR motoru (tanıma) ile görüntü ön işleyicisi (iyileştirme) arasında temiz bir ayrım sağlar. Bunları karıştırmak, hata ayıklaması zor karışık bir koda yol açabilir.

---

## Adım 2: **Preprocess Image for OCR** Boru Hattı Oluşturun

Şimdi öğreticinin kalbini oluşturacağız: giriş görüntüsünü deskew, binarize ve denoise yapan bir boru hattı. Her dönüşüm, OCR motorlarındaki belirli bir zayıflığı hedefler.

```python
# Step 2: Initialise the pre‑processing chain
preprocessor = ImagePreprocessor()

# Deskew – correct rotation so text lines are horizontal
preprocessor = preprocessor.deskew()

# Binarize – convert to pure black‑and‑white using a threshold (180 works well for most scans)
preprocessor = preprocessor.binarize(threshold=180)

# Remove noise – apply a mild median filter (strength=2) to smooth speckles
preprocessor = preprocessor.removeNoise(strength=2)
```

### Neden Bu Üç Adım?

1. **Deskew** – OCR motorları sol‑sağ (veya üst‑alt) hizalama varsayar. Birkaç derece dönüş, doğruluğu %30 ve üzeri düşürebilir.
2. **Binarize** – Görüntüyü ikili (binary) forma dönüştürmek, OCR motorunun analiz etmesi gereken veriyi azaltır, karakter kenarlarını keskinleştirir.
3. **Denoise** – Küçük lekeler veya sıkıştırma artefaktları, özellikle birçok harfin benzer şekle sahip olduğu Kiril alfabesinde, noktalama işaretleri veya diakritik işaretler olarak yanlış algılanabilir.

> **Uç durum notu:** Kaynak görüntüleriniz zaten temizse, `removeNoise` adımını atlayabilir veya `strength` parametresini düşürebilirsiniz. Çok agresif denoise, diakritik noktalar gibi ince detayları silebilir.

---

## Adım 3: Görüntüyü Yükleyin ve Boru Hattını Uygulayın

Boru hattı hazır olduğunda, ona bir dosya yolu veririz. `apply` metodu, OCR motorunun doğrudan tüketebileceği işlenmiş bir görüntü nesnesi döndürür.

```python
# Path to the original Cyrillic image (adjust as needed)
image_path = os.path.join("YOUR_DIRECTORY", "cyrillic_skewed.jpg")

# Run the preprocessing pipeline
processed_image = preprocessor.apply(image_path)
```

Sonucu ön izlemek isterseniz, diske kaydedebilirsiniz:

```python
# Optional: save the preprocessed image for visual verification
processed_image.save("preprocessed_cyrillic.jpg")
print("Preprocessed image saved – check the file to confirm deskewing and binarization.")
```

> **Neden ön izleme?** Dönüştürülmüş görüntüyü görmek, eşik değerlerini ince ayar yapmanıza yardımcı olur. Bazen 180 eşik değeri çok sert olabilir; 150’ye düşürmek hafif çizgileri koruyabilir.

---

## Adım 4: OCR Motorunu Kurun ve Metni Tanıyın

Şimdi gerçek OCR kısmına geçiyoruz. Motoru, **Cyrillic image** dosyalarından **metin çıkarmak** için gerekli olan Kiril dil paketini kullanacak şekilde yapılandıracağız.

```python
# Initialise the OCR engine
engine = OcrEngine()

# Tell the engine we’re working with Cyrillic text
engine.setLanguage(Language.Cyrillic)

# Perform recognition on the preprocessed image
ocr_result = engine.recognizeImage(processed_image)

# Extract plain text from the OCR result object
recognized_text = ocr_result.getText()
print("=== Recognized Text ===")
print(recognized_text)
```

### Bu OCR Doğruluğunu Nasıl İyileştirir

- **Temiz, deskewed, binarized** bir görüntü besleyerek, motor gürültüyle mücadele etmek yerine karakter şekillerine odaklanabilir.
- `Language.Cyrillic` belirtmek, doğru karakter seti ve dil modelini etkinleştirir; bu, Latin dışı betikler için **OCR doğruluğunu nasıl artıracağınız** konusunda kilit bir faktördür.

---

## Adım 5: Her Şeyi Yeniden Kullanılabilir Bir Fonksiyona Sarın (İsteğe Bağlı)

Birçok dosyayı işlemeyi planlıyorsanız, mantığı kapsüllemek kodunuzu daha temiz ve bakımını kolaylaştırır.

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Preprocess an image and extract Cyrillic text using the OCR engine.

    Parameters
    ----------
    image_path : str
        Full path to the source image.

    Returns
    -------
    str
        Recognized Cyrillic text.
    """
    # Build the preprocessing pipeline (could be cached for performance)
    preprocessor = (ImagePreprocessor()
                    .deskew()
                    .binarize(threshold=180)
                    .removeNoise(strength=2))

    processed = preprocessor.apply(image_path)

    engine = OcrEngine()
    engine.setLanguage(Language.Cyrillic)

    result = engine.recognizeImage(processed)
    return result.getText()


# Example usage
if __name__ == "__main__":
    sample_path = os.path.join("YOUR_DIRECTORY", "cyrillic_skewed.jpg")
    text = extract_cyrillic_text(sample_path)
    print("Extracted Cyrillic text:")
    print(text)
```

> **Neden fonksiyon?** Ön işleme mantığını izole eder, böylece tüm betiği yeniden yazmadan farklı bir dil eklemek veya parametreleri ayarlamak kolaylaşır.

---

## Yaygın Tuzaklar ve Nasıl Çözülür

| Sorun | Belirti | Çözüm |
|-------|----------|-----|
| **Aşırı eğim (>15°)** | Metin bozuk ya da eksik görünür | `deskew()` fonksiyonunun dayanıklılığını artırın veya OpenCV'nin `getRotationMatrix2D` ile manuel olarak ön‑döndürün. |
| **Düşük kontrast** | Binarizasyon her şeyi beyaz yapar | `threshold` değerini düşürün veya `binarize()` öncesinde kontrast‑germe adımı uygulayın. |
| **Küçük font boyutu** | Binarizasyondan sonra karakterler birleşir | Daha yüksek çözünürlüklü bir kaynak görüntüsü kullanın veya eşikleme öncesinde hafif bir Gaussian bulanıklığı uygulayın. |
| **Birden fazla dil** | Kiril harfleri okunamaz hale gelir | Kütüphane çok‑dilli modu destekliyorsa `engine.setLanguage([Language.Cyrillic, Language.English])` ayarlayın. |
| **Desteklenmeyen görüntü formatı** | `apply()` bir hata fırlatır | Pillow (`Image.open().convert('RGB')`) kullanarak görüntüyü önceden PNG veya JPEG’e dönüştürün. |

---

## **Image Preprocessing Pipeline Python** Yaklaşımını Genişletmek

1. **Batch Processing** – Görüntü dizininde döngü oluşturup her sonucu bir CSV dosyasına kaydedin.
2. **Parallel Execution** – Büyük iş yüklerini hızlandırmak için `concurrent.futures.ThreadPoolExecutor` kullanın.
3. **Custom Filters** – Basılı formlar için morfolojik işlemler (`erode`, `dilate`) ekleyin.
4. **Cloud OCR Integration** – Aynı ön işleme adımlarını korurken `OcrEngine`i bir API istemcisi (Google Vision, Azure Computer Vision) ile değiştirin.

```python
# Example of batch processing with ThreadPoolExecutor
from concurrent.futures import ThreadPoolExecutor, as_completed

def batch_extract(folder: str):
    files = [os.path.join(folder, f) for f in os.listdir(folder) if f.lower().endswith('.jpg')]
    results = {}

    with ThreadPoolExecutor(max_workers=4) as executor:
        future_to_file = {executor.submit(extract_cyrillic_text, f): f for f in files}
        for future in as_completed(future_to_file):
            file_path = future_to_file[future]
            try:
                results[file_path] = future.result()
            except Exception as exc:
                results[file_path] = f"Error: {exc}"
    return results
```

---

## Görsel Özet

![OCR için görüntü ön işleme örneği](/images/ocr_preprocess_example.png "OCR için görüntü ön işleme boru hattını gösteren diyagram: deskew → binarize → denoise → OCR engine")

*Diyagram, ham taramadan son metin çıktısına kadar **preprocess image for OCR** iş akışının her aşamasını gösterir.*

---

## Sonuç

Python’da eksiksiz bir **preprocess image for OCR** çözümünü adım adım inceledik; doğru paketlerin kurulmasından sağlam bir **image preprocessing pipeline python** oluşturulmasına ve sonunda **Cyrillic image** dosyalarından **metin çıkarma** işlemlerine kadar her şeyi kapsadık. Görüntüyü OCR motoruna vermeden önce deskew, binarize ve denoise uygulayarak, özellikle zorlayıcı Kiril betikleri için **OCR doğruluğunu nasıl artıracağınız** konusunda belirgin bir artış göreceksiniz.

Bir sonraki meydan okumaya hazır mısınız? Dil modelini Arapça’ya değiştirin, adaptif eşikleme ile deney yapın veya boru hattını gerçek zamanlı belge işleme için bir Flask API’sine bağlayın. Gökyüzü sınırdır ve bu temelle dağınık taramaları temiz, aranabilir metne dönüştürmek için iyi donanımlısınız.

İyi kodlamalar ve OCR sonuçlarınızın her zaman kristal gibi net olmasını dileriz!

## Sonra Ne Öğrenmelisiniz?

Bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsayan aşağıdaki öğreticiler bulunmaktadır. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı eksiksiz çalışan kod örnekleri içerir.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [OCR Görüntü Ön İşleme için Eğim Açısını Hesaplama](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [OCR Görüntü Tanıma’da Eşik Değerini Nasıl Ayarlarsınız](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}