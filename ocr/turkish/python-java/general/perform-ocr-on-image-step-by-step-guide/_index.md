---
category: general
date: 2026-03-18
description: Resimdeki metni hızlı bir şekilde çıkarmak için OCR gerçekleştirin. OCR
  için resmi nasıl yükleyeceğinizi, OCR motoru oluşturmayı ve dil seçenekleriyle OCR
  doğruluğunu artırmayı öğrenin.
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: tr
og_description: Bu ayrıntılı rehberle görüntüde OCR gerçekleştirin. OCR için görüntüyü
  yüklemeyi, OCR motoru oluşturmayı ve güvenilir metin çıkarımı için OCR doğruluğunu
  artırmayı öğrenin.
og_title: Görselde OCR Yap – Tam Programlama Öğreticisi
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Görselde OCR Yap – Adım Adım Kılavuz
url: /tr/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüde OCR Yap – Tam Programlama Öğreticisi

Hiç **perform OCR on image** yapmanız gerektiğinde, hangi kütüphaneyi seçeceğinizden veya güvenilir sonuçlar almanın nasıl olacağından emin olmadınız mı? Yalnız değilsiniz. Bu rehberde **extract text from image** için ihtiyacınız olan her şeyi, resmi yüklemekten dil seçeneklerini ayarlamaya kadar adım adım ele alacağız, böylece **improve OCR accuracy** her adımda artırabilirsiniz.

**load image for OCR**, **create OCR engine** nasıl yapılacağını ve her ayarın neden önemli olduğunu ele alacağız. Sonunda tanınan metni ekrana yazdıran, çalıştırmaya hazır bir betiğiniz olacak ve her satırın “neden”ini anlayacaksınız—belirsiz “belgelere bak” kısayolları yok. Hadi başlayalım.

## Gereksinimler

- Python 3.8+ (kod f‑string ve tip ipuçları kullanır)
- Varsayımsal `ocr_lib` paketi – `pip install ocr_lib` ile kurun
- Açık, basılı metin içeren bir görüntü dosyası (ör. `lab_report.png`)
- Temel bir metin editörü veya IDE (VS Code, PyCharm, istediğiniz gibi)

Eğer zaten bunlara sahipseniz, harika—hazırsınız. Değilse, python.org'dan Python'u indirin ve pip komutunu çalıştırın; sadece bir dakikanızı alır.

![görüntüde OCR örnek](/images/ocr-example.png)

*Alt metin: perform OCR on image – çıkarılan metni gösteren örnek çıktı.*

## 1. Adım: OCR Motoru Oluşturma – Python'da **create OCR engine** Nasıl Yapılır

Herhangi bir tanıma gerçekleşmeden önce, kütüphanenin yapılandırma ve çalışma zamanını tutan bir motor nesnesine ihtiyacı vardır. Motoru, işlemin arkasındaki beyin olarak düşünün.

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**Neden önemli:** Motoru erken örneklemek, daha sonra dil seçeneklerini eklemenizi sağlar ve ayrıca dahili modelleri önbelleğe alarak sonraki çağrıları hızlandırır.

## 2. Adım: OCR için Görüntü Yükleme – **load image for OCR**'un doğru yolu

Artık bir motorumuz olduğuna göre, ona okunacak bir şey vermeliyiz. `setImageFromFile` yöntemi bir dosya sistemi yolu alır; yol mutlak ya da betiğin çalışma dizinine göre göreli olabilir.

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**Pro ipucu:** Betik farklı bir klasörden çalıştırıldığında “dosya bulunamadı” sürprizlerinden kaçınmak için mutlak yol veya `os.path.join` kullanın.

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## 3. Adım: OCR Doğruluğunu Artırma – **language options** ayarlayarak **improve OCR accuracy**

Kutudan çıkar çıkmaz OCR çalışır, ancak alan‑özgü sözlükler (ör. laboratuvar jargonları) genellikle hataya yol açar. Özel bir sözlük ve kara liste ekleyerek “0” ile “O” karıştırma gibi yanlış tanıma oranlarını azaltırsınız.

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**Neden yardımcı olur:** Sözlük, OCR modeline “HPLC”nin geçerli bir token olduğunu söyler, böylece kelimeyi anlamsız parçalara bölmesini engeller. Kara liste, modeli belirsiz sembolleri gürültü olarak ele alması için yönlendirir, bu da doğrudan **improve OCR accuracy** sağlar.

## 4. Adım: Görüntüde OCR Yap – Temel **perform OCR on image** çağrısı

Motor hazır ve görüntü eklendiğinde, metni gerçekten tanıma zamanı gelmiştir. Bu adım, ham metin, güven skorları veya sınırlama kutuları için sorgulayabileceğiniz bir `OcrResult` nesnesi döndürür.

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

Görüntü bulanıksa, sonuçta daha düşük güven sayılarını göreceksiniz. Bu, görüntüyü motorun önüne vermeden önce (ör. kontrastı artırarak) ön işleme yapmanız gerektiğinin bir işaretidir.

## 5. Adım: Görüntüden Metin Çıkarma – Son dizeyi elde etmek

Son olarak, `OcrResult`'tan metinsel temsilini isteriz. `getText()` yöntemi, dosyaya kaydetme, veritabanına gönderme gibi sonraki işlemler için hazır bir düz metin dizesi döndürür.

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**Beklenen çıktı:** `lab_report.png` basit bir tablo içerdiğini varsayarsak, aşağıdakine benzer bir şey görebilirsiniz:

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

Bu, **extract text from image** kısmının tamamlanmasıdır.

## Tam Çalışan Örnek – Hepsini Bir Araya Getirin

Aşağıda, önceki bölümlerden parçaları birleştiren tek bir betik var. `run_ocr.py` dosyasına kopyalayıp yapıştırabilir ve `python run_ocr.py` komutunu çalıştırabilirsiniz.

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### Hızlı doğrulama kontrol listesi

| ✅ | Öğe |
|---|------|
| ✔️ | Motor oluşturuldu (`create OCR engine`) |
| ✔️ | Görüntü yüklendi (`load image for OCR`) |
| ✔️ | Dil seçenekleri ayarlandı (`improve OCR accuracy`) |
| ✔️ | OCR gerçekleştirildi (`perform OCR on image`) |
| ✔️ | Metin çıkarıldı (`extract text from image`) |

Betik çalıştırın ve konsolu izleyin. “OCR Output” bloğunu raporunuzun içeriğiyle gördüğünüzde, **performed OCR on image** işlemini başarıyla tamamlamış olursunuz.

## Yaygın Tuzaklar ve Nasıl Kaçınılır

| Sorun | Neden olur | Çözüm |
|-------|------------|------|
| **Bulanık giriş** | OCR modeli karakterleri ayıramaz | OpenCV ile ön işleme yapın: `cv2.GaussianBlur` veya DPI'yi artırın |
| **Yanlış dil** | Varsayılan dil İngilizce dışındaki bir dil olarak ayarlanmış olabilir | `recognize()`'den önce `engine.setLanguage("eng")` çağırın |
| **Eksik sözlük terimleri** | Alan‑özgü kelimeler bozulur | Step 3'te gösterildiği gibi `setDictionary` ile ekleyin |
| **Blacklisted characters cause** |  |  |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}