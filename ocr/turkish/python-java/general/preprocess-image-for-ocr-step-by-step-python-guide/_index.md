---
category: general
date: 2026-06-22
description: Aspose OCR'i Python'da kullanarak görüntüden metin çıkarmak ve OCR doğruluğunu
  artırmak için görüntüyü ön işleme. Tam, çalıştırılabilir örnek dahil.
draft: false
keywords:
- preprocess image for OCR
- extract text from image
- improve OCR accuracy
language: tr
og_description: OCR için görüntüyü ön işleyin, görüntüden metin çıkarın ve Aspose
  OCR ile OCR doğruluğunu artırın. Python’da tam iş akışını öğrenin.
og_title: OCR için Görüntü Ön İşleme – Tam Python Eğitimi
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Preprocess image for OCR to extract text from image and improve OCR
    accuracy using Aspose OCR in Python. Complete, runnable example included.
  headline: Preprocess Image for OCR – Step‑by‑Step Python Guide
  type: TechArticle
- description: Preprocess image for OCR to extract text from image and improve OCR
    accuracy using Aspose OCR in Python. Complete, runnable example included.
  name: Preprocess Image for OCR – Step‑by‑Step Python Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Aspose OCR’s wheels target modern interpreters. | | `aspose-ocr` package
      (`pip install aspose-ocr`) | Provides the `OcrEngine`, `ImagePreprocessor`,
      and filter classes. | | A sample image (e.g., `noisy-document.jpg`) |'
  - name: – Initialise the OCR Engine and Load Your Source Image
    text: '```python import aspose.ocr as ocr'
  - name: – Build a Preprocessing Chain to Clean the Image
    text: '```python # Initialise the preprocessor – a container for a series of filters
      preprocessor = ocr.ImagePreprocessor()'
  - name: – Attach the Preprocessor to the Engine
    text: '```python # Hook the preprocessing pipeline into the OCR engine ocr_engine.set_preprocessor(preprocessor)
      ```'
  - name: – Run OCR and Extract Text from Image
    text: '```python # Perform the recognition on the pre‑processed image recognition_result
      = ocr_engine.recognize()'
  - name: – Verify the Output and Fine‑Tune for Better Accuracy
    text: '```python # Quick sanity check: print length and a sample snippet print(f"Detected
      {len(extracted_text)} characters.") print("First 200 chars:", extracted_text[:200])
      ```'
  type: HowTo
- questions:
  - answer: Yes. Convert each page to an image (e.g., using `pdf2image`) and feed
      it through the same pipeline in a loop. The same `preprocess image for OCR`
      steps apply per page.
    question: Does this work with multi‑page PDFs?
  - answer: 'Set the language before recognition: `engine.set_language(ocr.Language.FRENCH)`.
      The preprocessing filters stay the same; only the language model changes.'
    question: What if my document is in a language other than English?
  - answer: 'Absolutely. The `ImagePreprocessor` is extensible—just call `add_filter`
      again. For heavy‑dotted backgrounds, `ocr.Filters.MedianFilter(kernel=3)` can
      be useful. --- ## Wrap‑Up We’ve just **preprocess image for OCR**, run Aspose’s
      engine, and **extract text from image** while showcasing several tric'
    question: Can I chain more filters?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: OCR için Görüntü Ön İşleme – Adım Adım Python Rehberi
url: /tr/python-java/general/preprocess-image-for-ocr-step-by-step-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR için Görüntü Ön İşleme – Tam Python Eğitimi

Eğer **OCR için görüntü ön işleme** yapmanız gerekiyorsa, muhtemelen gürültülü taramalar, eğik sayfalar veya düşük kontrastlı fotoğraflarla karşılaştınız ve bunlar iş birliği yapmaz. Görüntüden metin çıkarmaya çalışıp karışık bir karmaşa mı elde ettiniz? İşte sağlam bir ön işleme zinciri, okunabilir birkaç kelime ile tam bir transkripsiyon kabusunun arasındaki farkı yaratabilir.

Bu rehberde, Aspose OCR for Python kullanarak **görüntüden metin çıkarma** ve **OCR doğruluğunu artırma** konularını gösteren tam bir uçtan uca örnek üzerinden ilerleyeceğiz. Belirsiz referanslar yok—kopyalayıp yapıştırabileceğiniz kod, her satırın ardındaki mantık ve gerçek dünya kenar durumları için ipuçları.

## Öğrenecekleriniz

- Gürültülü bir belgeyi yükleyen, temizleyen ve tanınan metni ekrana yazdıran hazır bir Python betiği.  
- Her ön işleme filtresinin neden önemli olduğu ve parametrelerinin nasıl ayarlanacağı konusunda bir anlayış.  
- Yoğun nokta gürültüsü, aşırı dönüş veya düşük kontrastlı taramalar gibi yaygın tuzakları ele almak için stratejiler.  

### Gereksinimler

| Gereksinim | Neden Önemli |
|-------------|----------------|
| Python 3.8+ | Aspose OCR’un tekerlekleri modern yorumlayıcıları hedefler. |
| `aspose-ocr` paketi (`pip install aspose-ocr`) | `OcrEngine`, `ImagePreprocessor` ve filtre sınıflarını sağlar. |
| Örnek bir görüntü (ör. `noisy-document.jpg`) | Ön işlemeden elde edilen faydaları göstermek için kasıtlı olarak dağınık bir resim kullanacağız. |
| Python fonksiyonlarına temel aşinalık | Betiğinizi kendi iş akışınıza uyarlamanıza yardımcı olur. |

> **Pro ipucu:** Windows kullanıyorsanız, sürüm çakışmalarını önlemek için betiği bir sanal ortam içinde çalıştırın.

---

## Aspose OCR (Python) ile OCR için Görüntü Ön İşleme

Aşağıda, ihtiyacınız olan kodun adım adım açıklaması yer alıyor. Her bölüm, **ne** yaptığımızı *ve* **neden** yaptığımızı açıklıyor, böylece tahmin etmeden pipeline'ı daha sonra ayarlayabilirsiniz.

![OCR için görüntü ön işleme örneği](ocr-preprocess.png){alt="OCR için görüntü ön işleme"}

### Adım 1 – OCR Motorunu Başlatın ve Kaynak Görüntünüzü Yükleyin

```python
import aspose.ocr as ocr

# Create the OCR engine – the central object that drives recognition
ocr_engine = ocr.OcrEngine()

# Load the raw image file. Using ImageStream lets Aspose handle various formats.
ocr_engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/noisy-document.jpg"))
```

- **Neden** bir `OcrEngine`? Tanıyıcıyı, dil ayarlarını ve (daha sonra) ön işleyiciyi kapsüller.  
- **Neden** `ImageStream.from_file`? Dosya türü işleme detaylarını soyutlar, böylece kod değişikliği yapmadan JPEG'i PNG ile değiştirebilirsiniz.

### Adım 2 – Görüntüyü Temizlemek İçin Bir Ön İşleme Zinciri Oluşturun

```python
# Initialise the preprocessor – a container for a series of filters
preprocessor = ocr.ImagePreprocessor()

# 1️⃣ Deskew – corrects any rotation so text lines become horizontal.
preprocessor.add_filter(ocr.Filters.Deskew())

# 2️⃣ Despeckle – removes isolated noise pixels; strength=2 is a good middle ground.
preprocessor.add_filter(ocr.Filters.Despeckle(strength=2))

# 3️⃣ ContrastBoost – lifts faint characters; level=1.5 amplifies contrast without blowing out highlights.
preprocessor.add_filter(ocr.Filters.ContrastBoost(level=1.5))
```

**Bu filtrelerin OCR doğruluğunu nasıl artırdığı:**  
- **Deskew** karakter segmentasyonunu karıştıran yaygın “eğik sayfa” sorununu ortadan kaldırır.  
- **Despeckle** düşük kaliteli tarayıcılardan kaynaklanan nokta gürültüsünü hedefler; daha yüksek güç daha fazla gürültüyü temizler ancak ince detayları aşındırabilir.  
- **ContrastBoost** koyu metnin açık arka plan üzerinde öne çıkmasını sağlar, çoğu OCR motoru için klasik bir kazançtır.

> **Kenar durumu:** Belgeniz zaten tamamen düzse, birkaç milisaniye tasarruf etmek için `Deskew()`'i atlayabilirsiniz.

### Adım 3 – Ön İşleyiciyi Motorla Bağlayın

```python
# Hook the preprocessing pipeline into the OCR engine
ocr_engine.set_preprocessor(preprocessor)
```

Şimdi `ocr_engine.recognize()` her çalıştığında, tanımladığımız üç filtre tam olarak belirttiğimiz sırayla çalıştırılacak. Sıra önemlidir: **deskew** öncelikle uygulanmalı, aksi takdirde speckle filtresi döndürülmüş kenarları gürültü olarak algılayabilir.

### Adım 4 – OCR'ı Çalıştırın ve Görüntüden Metin Çıkarın

```python
# Perform the recognition on the pre‑processed image
recognition_result = ocr_engine.recognize()

# Pull out the plain text string
extracted_text = recognition_result.get_text()
print(extracted_text)
```

- `recognize()` çağrısı, ham metnin yanı sıra güven skorları, sınırlama kutuları ve dil detaylarını da içeren bir `RecognitionResult` nesnesi döndürür.  
- Burada sadece düz metin yeterli, ancak hızlı bir **OCR doğruluğunu artırma** kontrolü için `recognition_result.get_confidence()`'ı inceleyebilirsiniz.

### Adım 5 – Çıktıyı Doğrulayın ve Daha İyi Doğruluk İçin İnce Ayar Yapın

```python
# Quick sanity check: print length and a sample snippet
print(f"Detected {len(extracted_text)} characters.")
print("First 200 chars:", extracted_text[:200])
```

Çıktı hâlâ bozuk semboller içeriyorsa, aşağıdaki ayarlamaları göz önünde bulundurun:

| Sorun | Önerilen Çözüm |
|-------|----------------|
| Metin hâlâ bulanık | `ContrastBoost(level)` değerini 2.0'a yükseltin veya desenleme öncesinde `ocr.Filters.GaussianBlur(radius=1)` ekleyin. |
| Çok fazla rastgele karakter | `Despeckle(strength)` değerini 3'e yükseltin veya yatay çizgileri kaldırmak için `ocr.Filters.RemoveLines()` ekleyin. |
| Eğiklik devam ediyor | Düzeltmeyi hafif dönüşlere sınırlamak için `ocr.Filters.Deskew(max_angle=5)` çağırın. |

---

## Tam, Çalıştırılabilir Betik

Aşağıdaki bloğu `ocr_preprocess.py` adlı bir dosyaya kopyalayın. `YOUR_DIRECTORY/noisy-document.jpg` kısmını gerçek görüntü yolunuzla değiştirin, ardından `python ocr_preprocess.py` komutunu çalıştırın.

```python
import aspose.ocr as ocr

def main():
    # Initialise engine and load image
    engine = ocr.OcrEngine()
    engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/noisy-document.jpg"))

    # Build preprocessing pipeline
    preproc = ocr.ImagePreprocessor()
    preproc.add_filter(ocr.Filters.Deskew())
    preproc.add_filter(ocr.Filters.Despeckle(strength=2))
    preproc.add_filter(ocr.Filters.ContrastBoost(level=1.5))

    # Attach pipeline
    engine.set_preprocessor(preproc)

    # Recognise and extract text
    result = engine.recognize()
    text = result.get_text()

    # Display results
    print("\n--- OCR Output ---")
    print(text)
    print("\n--- Summary ---")
    print(f"Characters detected: {len(text)}")
    print("Snippet:", text[:200].replace("\n", " "))

if __name__ == "__main__":
    main()
```

Bu betiği gürültülü, hafif döndürülmüş bir JPEG üzerinde çalıştırdığınızda temiz, okunabilir bir metin elde edeceksiniz—iyi tasarlanmış bir ön işleme zincirinin **OCR doğruluğunu** dramatik şekilde artırdığını gösterir.

---

## Sık Sorulan Sorular & Cevaplar

**S: Bu çok sayfalı PDF'lerle çalışır mı?**  
C: Evet. Her sayfayı bir görüntüye dönüştürün (ör. `pdf2image` kullanarak) ve aynı pipeline'ı bir döngü içinde besleyin. `preprocess image for OCR` adımları sayfa başına aynı şekilde uygulanır.

**S: Belgem İngilizce dışındaki bir dilde ise ne yapmalıyım?**  
C: Tanıma öncesinde dili ayarlayın: `engine.set_language(ocr.Language.FRENCH)`. Ön işleme filtreleri aynı kalır; sadece dil modeli değişir.

**S: Daha fazla filtre ekleyebilir miyim?**  
C: Kesinlikle. `ImagePreprocessor` genişletilebilir—sadece `add_filter` metodunu tekrar çağırın. Yoğun noktalı arka planlar için `ocr.Filters.MedianFilter(kernel=3)` faydalı olabilir.

---

## Özet

Şimdi **OCR için görüntü ön işleme** yaptık, Aspose motorunu çalıştırdık ve **görüntüden metin çıkarma** işlemini gerçekleştirdik; ayrıca **OCR doğruluğunu artırma** için birkaç püf noktası gösterdik. Tam örnek, herhangi bir projeye eklenmeye hazır ve modüler filtre tasarımı, verinizin gereksinimlerine göre adımları değiştirebilmenizi, ekleyebilmenizi veya kaldırabilmenizi sağlar.

İleride şunları keşfedebilirsiniz:

- `concurrent.futures` ile onlarca taramayı **toplu işleme**.  
- `pyspellchecker` gibi yazım denetimi kütüphaneleriyle **son işleme** yaparak OCR kaynaklı hataları temizleme.  
- Betiği Flask veya FastAPI kullanarak bir web servisine **entegrasyon** edip, isteğe bağlı OCR mikro hizmeti haline getirme.

Deneyin, filtre güçlerini ayarlayın ve tanıma oranlarınızın yükseldiğini izleyin. Bir sorunla karşılaşırsanız yorum bırakın—mutlu kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [AspOCR Nasıl Kullanılır: .NET için Görüntü OCR Filtrelerini Ön İşleme](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Görüntüden Metin Çıkarma – .NET için Aspose.OCR ile OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}