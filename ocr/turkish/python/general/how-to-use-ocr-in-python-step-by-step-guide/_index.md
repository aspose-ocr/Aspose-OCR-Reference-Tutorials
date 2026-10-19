---
category: general
date: 2026-08-12
description: Python'da OCR'yi kullanarak görüntüden metin tanıma, metni çıkarma, görüntüyü
  metne dönüştürme ve AI sonrası işleme ile OCR metnini temizleme.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- clean up OCR text
language: tr
lastmod: 2026-08-12
og_description: Python’da OCR’yi kullanarak resimleri düzenlenebilir metne dönüştürmeyi
  öğrenin. Görüntüden metin tanıma, metin çıkarma, resmi metne çevirme ve OCR metnini
  yapay zeka ile temizleme.
og_image_alt: Screenshot of Python code converting an image to clean text using OCR
  and AI post‑processing
og_title: Python'da OCR Nasıl Kullanılır – Tam Programlama Rehberi
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  headline: How to use OCR in Python – step‑by‑step guide
  type: TechArticle
- description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  name: How to use OCR in Python – step‑by‑step guide
  steps:
  - name: Loads an image file (PNG, JPEG, or TIFF).
    text: Loads an image file (PNG, JPEG, or TIFF).
  - name: Recognizes text from the image using an OCR engine.
    text: Recognizes text from the image using an OCR engine.
  - name: Improves the raw output with an AI‑driven post‑processor.
    text: Improves the raw output with an AI‑driven post‑processor.
  - name: Prints the cleaned‑up text to the console.
    text: Prints the cleaned‑up text to the console.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- AI post‑processing
title: Python'da OCR Nasıl Kullanılır – Adım Adım Rehber
url: /tr/python/general/how-to-use-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python’da OCR Nasıl Kullanılır – adım adım rehber

Eğer taranmış belgeleri veya ekran görüntülerini düzenlenebilir metne **how to use OCR** ile dönüştürmeniz gerekiyorsa, bu öğretici Python’da eksiksiz bir çözüm gösterir. Görüntüden metin tanıma, görüntüden metin çıkarma, görüntüyü metne çevirme ve hafif bir AI sonrası işleyiciyle OCR metnini temizleme konularını öğreneceksiniz.

Kılavuz, gerekli kütüphanelerin kurulumu부터 düşük kaliteli görüntülerin ele alınmasına kadar her şeyi kapsar; böylece eksik bir adım tahmin etmeden OCR’ı herhangi bir otomasyon hattına entegre edebilirsiniz.

## Ne oluşturacaksınız

Bu makalenin sonunda aşağıdaki tek Python betiğine sahip olacaksınız:

1. Bir görüntü dosyasını (PNG, JPEG veya TIFF) yükler.  
2. OCR motoru kullanarak görüntüden metni tanır.  
3. Ham çıktıyı bir AI‑destekli sonrası işleyiciyle iyileştirir.  
4. Temizlenmiş metni konsola yazdırır.

Harici bir hizmete ihtiyaç yoktur—her şey yerel olarak çalışır, bu da çözümü çevrim dışı ortamlar veya gizlilik‑duyarlı projeler için uygun kılar.

## Önkoşullar

- Python 3.9 ve üzeri.  
- `pytesseract` ve `Pillow` kütüphaneleri (`pip install pytesseract pillow`).  
- Sistem `PATH` içinde bulunabilen Tesseract‑OCR ikili dosyası.  
- Python’da fonksiyonlar hakkında temel bir anlayış.  

Bu öğelere zaten sahipseniz, doğrudan ilk kod bloğuna geçebilirsiniz.

## Python ile OCR Nasıl Kullanılır

**how to use OCR**’ın temeli, OCR motorunu başlatmak ve ona bir görüntü vermektir. Bu öğreticide `pytesseract` kullanıyoruz; bu, açık kaynak Tesseract motorunun ince bir sarmalayıcısıdır.

```python
import pytesseract
from PIL import Image

def load_image(path: str) -> Image.Image:
    """
    Open an image file and return a Pillow Image object.
    Pillow handles many formats (PNG, JPEG, TIFF) and ensures
    the image is in a mode that Tesseract can read.
    """
    return Image.open(path)
```

> **Bu adımın önemi** – Tesseract temiz, doğru yönlendirilmiş bir görüntü bekler. Pillow kullanmak, OCR çalışmadan önce görüntü verisinin normalleştirildiğini garanti eder ve sonraki **recognize text from image** işleminin doğruluğunu artırır.

## Görüntüden metni tanıma

Şimdi `pytesseract.image_to_string` çağırarak ham dizeyi çıkarıyoruz. Bu, klasik “recognize text from image” çağrısıdır.

```python
def ocr_recognize(image: Image.Image) -> str:
    """
    Run Tesseract OCR on the supplied image and return the raw text.
    """
    raw_text = pytesseract.image_to_string(image, lang='eng')
    return raw_text
```

> **Fonksiyonu ayırmamızın nedeni** – OCR adımını izole etmek, motoru daha sonra (ör. EasyOCR’a geçmek) değiştirmeyi, pipeline’ın geri kalanına dokunmadan mümkün kılar. Aynı zamanda birim testlerini de kolaylaştırır.

## Görüntüden metni çıkarma ve kaliteyi artırma

Ham OCR çıktısı genellikle satır sonları, yabancı karakterler veya hatalı tanınmış kelimeler içerir. Bir AI sonrası işleyici bu artefaktları otomatik olarak temizleyebilir. Aşağıda, `transformers` kütüphanesini kullanarak yerel bir küçük dil modeli çalıştıran minimal bir örnek bulunuyor. İsterseniz yerine herhangi bir özel hizmet koyabilirsiniz.

```python
from transformers import pipeline

# Initialize a zero‑shot text‑generation pipeline once (expensive operation)
_ai_postprocessor = pipeline("text2text-generation", model="google/flan-t5-small")

def clean_ocr_text(raw: str) -> str:
    """
    Send the raw OCR string to a lightweight AI model that rewrites
    the text, removing obvious errors and normalizing whitespace.
    """
    # The prompt guides the model to act as a post‑processor
    prompt = f"Clean up the following OCR output, fixing spelling mistakes and removing extra line breaks:\n\n{raw}"
    result = _ai_postprocessor(prompt, max_length=512, do_sample=False)
    # The pipeline returns a list of dicts; we take the generated text
    cleaned = result[0]["generated_text"]
    return cleaned.strip()
```

> **AI sonrası işleyicinin faydası** – Geleneksel OCR motorları karakter tanıma konusunda iyidir ancak düzen ve gürültüyle başa çıkmakta zorlanır. Bir dil modeli bağlamı anlar, bu yüzden “Th1s 1s 4 test.” ifadesini “This is a test.” hâline getirebilir. Bu adım, **clean up OCR text** gereksinimini doğrudan karşılar.

## Görüntüyü metne çevir – tam betik

Her şeyi bir araya getirdiğimizde, **convert image to text** işlemini uçtan uca yapan kısa bir betik elde ederiz.

```python
import sys
from pathlib import Path

def main(image_path: str):
    """
    Complete pipeline:
    1. Load image.
    2. Recognize text from image.
    3. Clean up OCR text.
    4. Print the final result.
    """
    # 1️⃣ Load the image file
    img = load_image(image_path)

    # 2️⃣ Recognize text from image (raw OCR)
    raw_text = ocr_recognize(img)
    print("=== Raw OCR output ===")
    print(raw_text)
    print("\n---\n")

    # 3️⃣ Clean up OCR text with AI post‑processor
    cleaned_text = clean_ocr_text(raw_text)
    print("=== Cleaned‑up text ===")
    print(cleaned_text)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python ocr_pipeline.py <path-to-image>")
        sys.exit(1)

    image_file = Path(sys.argv[1])
    if not image_file.is_file():
        print(f"Error: file '{image_file}' does not exist.")
        sys.exit(1)

    main(str(image_file))
```

### Beklenen çıktı

Örnek bir görüntü (`sample.png`) ile betiği çalıştırdığınızda şu çıktı alınabilir:

```
=== Raw OCR output ===
Th1s 1s 4 sampl3
text from an im4ge.

--- 

=== Cleaned‑up text ===
This is a sample text from an image.
```

AI sonrası işleyicinin hatalı karakterleri düzelttiğine ve gereksiz satır sonlarını kaldırdığına dikkat edin. Bu, tam **extract text from image** iş akışını gösterir ve OCR metninin temizlenmesinin faydasını ortaya koyar.

## Yaygın kenar durumlarını ele alma

| Durum                                   | Önerilen ayarlama                                                               |
|-----------------------------------------|---------------------------------------------------------------------------------|
| Düşük kontrastlı görüntü                | OCR’dan önce `ImageEnhance` ile gri tonlamaya çevirin ve kontrastı artırın.    |
| Çok‑dilli belge                        | `lang` parametresine virgülle ayrılmış bir liste verin (ör. `lang='eng+fra'`). |
| Çok büyük görüntüler ( > 2000 px )      | Tesseract’ı hızlandırmak için `img.thumbnail((2000, 2000))` ile küçültün.      |
| Tesseract ikili dosyası eksik           | `pytesseract.pytesseract.tesseract_cmd` yürütülebilir dosyaya işaret ettiğinden emin olun. |
| AI sonrası işleyici çok yavaş           | Daha küçük bir model (`t5-small`) kullanın veya GPU’da çalıştırın.            |

> **Pro ipucu:** AI model nesnesini (`_ai_postprocessor`) modül içe aktarımında önbelleğe alın; böylece her çağrıda yeniden yüklemek zorunda kalmazsınız. Bu, çok sayıda görüntü işlenirken gecikmeyi büyük ölçüde azaltır.

## Alternatif yaklaşımlar

- **EasyOCR**: Harici bir ikili dosya gerektirmeden 80’den fazla dili destekleyen saf‑Python OCR kütüphanesi. Pip‑only bir çözüm isterseniz `ocr_recognize` yerine `EasyOCR.Reader` kullanın.  
- **Bulut OCR API’leri**: Google Cloud Vision, Azure Computer Vision veya Amazon Textract, karmaşık düzenler için daha yüksek doğruluk sağlar ancak ağ erişimi ve faturalandırma gerektirir.  
- **Özel sonrası işleme**: Belirli kalıpları düzeltmek için düzenli ifadeler (`re.sub`) kullanılabilir (ör. tireli satır sonlarını kaldırma) ve AI modeli gerektirmez.

## Özet

Artık **how to use OCR** konusunda Python’da görüntüden metin tanıma, görüntüden metin çıkarma, görüntüyü metne çevirme ve AI sonrası işleyiciyle OCR metnini temizleme becerisine sahipsiniz. Tam betik, ek ön‑işleme (gürültü azaltma, eğikliği düzeltme) veya sonraki adımlar (veritabanına kaydetme, arama indeksine besleme) ekleyebileceğiniz üretim‑hazır bir pipeline sunar.

### Sonraki adımlar

- Farklı AI modelleri (ör. `gpt‑2`, `flan‑ul2`) deneyerek alanınıza en uygun temizlik performansını bulun.  
- Flask veya FastAPI kullanarak pipeline’ı bir web servisine entegre edin; betiği talep üzerine çalışan bir OCR uç noktasına dönüştürün.  
- Toplu işleme keşfedin: bir dizindeki tüm görüntüler üzerinde döngü kurun ve her temizlenmiş çıktıyı karşılık gelen `.txt` dosyasına yazın.

Kodunuzu özgün iş akışınıza göre uyarlamaktan çekinmeyin ve temiz, aranabilir metnin uygulamanızın bir sonraki aşamasına güç vermesine izin verin. İyi kodlamalar!

## Bir Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Görüntüyü Metne Dönüştür: Aspose OCR (Python) Kullanarak Görüntüden Metin Çıkarma](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım Adım Rehber](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Görüntüden Metin Çıkarma – .NET için Aspose.OCR ile OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}