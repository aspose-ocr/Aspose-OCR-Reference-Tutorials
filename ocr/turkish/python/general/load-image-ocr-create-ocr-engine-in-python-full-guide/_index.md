---
category: general
date: 2026-01-12
description: Python ile görüntü OCR'sini hızlıca yükleyin. OCR motoru oluşturmayı,
  hataları yönetmeyi ve adım adım bir öğreticide metin çıkarmayı öğrenin.
draft: false
keywords:
- load image OCR
- create OCR engine
- OCR error handling
- Python OCR tutorial
- image preprocessing OCR
language: tr
og_description: Python ile basit bir OCR motoru kullanarak görüntü OCR'si yükleyin.
  Bu kılavuz hata yönetimini, en iyi uygulamaları ve tam kodu gösterir.
og_title: Resim Yükle OCR – Python'da OCR Motoru Oluştur
tags:
- OCR
- Python
- Image Processing
title: Görüntü Yükleme OCR – Python'da OCR Motoru Oluşturma – Tam Kılavuz
url: /tr/python/general/load-image-ocr-create-ocr-engine-in-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntü OCR Yükleme – Python'da OCR Motoru Oluşturma

Hiç **görüntü OCR** yüklemeniz gerekti ama nereden başlayacağınızı bilemediniz mi? Belki bir kütüphane denediniz, gizemli bir istisna aldınız ve “Şimdi ne yapacağım?” diye düşündünüz. Yalnız değilsiniz. Bu öğreticide sıfırdan bir OCR motoru oluşturmayı, görüntüleri güvenli bir şekilde yüklemeyi ve bir dosya eksik ya da bozuk olduğunda ortaya çıkan kaçınılmaz sorunları ele almayı adım adım göstereceğiz.

Bu rehberin sonunda **OCR motoru oluşturma**, görüntüleri yükleme, hataları kontrol etme ve hatta çıkarılan metni yazdırma işlevine sahip tam çalışan bir betiğiniz olacak. Dış dökümantasyon referansları yok—sadece bugün projenize ekleyebileceğiniz eksiksiz, çalıştırılabilir bir örnek.

## Gereksinimler

- Python 3.9 veya daha yeni (kullandığımız sözdizimi 3.x sürümleri arasında standarttır)  
- Hayali `ocr` paketi (`pip install ocr‑lib` ile kurun – gerçek kütüphanenizle değiştirin)  
- Birkaç test görüntüsü içeren bir klasör (var olan bir tane, kasıtlı olarak bulunmayan bir tane)  

Hepsi bu. Ağır bağımlılıklar yok, karmaşık derleme adımları yok. Hadi başlayalım.

## Adım 1: OCR Motoru Oluşturma – Çekirdek Nesneyi Ayarlama

**görüntü OCR** yükleyebilmeden önce, temel OCR motoru ile iletişim kurabilen bir motor örneğine ihtiyacınız var. Bunu bir TV uzaktan kumandası gibi düşünün; olmadan kanalı değiştiremezsiniz.

```python
# step_1_create_engine.py
import ocr

def init_engine():
    """
    Initializes and returns an OCR engine instance.
    This is where we 'create OCR engine' for the rest of the tutorial.
    """
    try:
        engine = ocr.OcrEngine()
        print("✅ OCR engine created successfully.")
        return engine
    except ocr.OcrException as e:
        # If the library itself fails to initialise, we bail out early.
        print(f"❌ Failed to create OCR engine (code {e.code}): {e.message}")
        raise
```

**Neden önemli:**  
Motoru bir kez oluşturup yeniden kullanmak, her görüntüde yerel kütüphanelerin yüklenmesi maliyetinden kaçınır. Ayrıca yapılandırmayı (dil paketleri, DPI ayarları vb.) tek bir yerde toplar, böylece tek bir yerden ayarlayabilirsiniz.

## Adım 2: Görüntü OCR Yükleme – İstisnalarla Güvenli Yükleme

Artık bir motorumuz olduğuna göre, bir sonraki mantıklı adım ona bir görüntü vermektir. En basit yol `engine.load_image(path)` çağırmaktır. Ancak, gerçek dünyadaki kod eksik dosyalar, desteklenmeyen formatlar veya izin sorunlarını öngörmelidir.

```python
# step_2_load_with_exception.py
def load_image_with_exception(engine, path):
    """
    Attempts to load an image using a try/except block.
    Demonstrates the classic 'load image OCR' pattern with Python exceptions.
    """
    try:
        engine.load_image(path)
        print(f"✅ Image loaded: {path}")
    except ocr.OcrException as ex:
        # The OCR library packages its own error codes.
        print(f"❌ Failed to load image (code {ex.code}): {ex.message}")
        # Optionally re‑raise or handle gracefully.
```

**Profesyonel ipucu:**  
Birçok görüntü bekliyorsanız, çağrıyı bir döngü içinde sarın ve hataları daha sonra analiz için bir CSV'ye kaydedin. Bu, tek bir dosya sorun çıkarsa bile veri akışınızı sağlam tutar.

## Adım 3: Görüntü OCR Yükleme – Motorun Yerleşik Hata API'sini Kullanma

Bazı OCR kütüphaneleri, istisna temelli olmayan bir hata alma yöntemi sunar. Bu, sıkı döngülerde Python istisnalarının performans etkisinden kaçınmak istediğinizde faydalıdır.

```python
# step_3_load_with_error_api.py
def load_image_with_error_api(engine, path):
    """
    Loads an image and then checks the engine's internal error state.
    This pattern complements the exception approach and shows another way
    to 'load image OCR' safely.
    """
    engine.load_image(path)           # No try/except here.
    load_error = engine.get_last_error()
    if load_error:
        print(f"❌ Load error: {load_error.message} (code {load_error.code})")
    else:
        print(f"✅ Image loaded without error: {path}")
```

**Ne zaman tercih edilmeli:**  
Dakikada binlerce görüntü işliyorsanız, istisnalardan kaçınmak değerli milisaniyeler kazandırabilir. Hata API'si her çağrıdan sonra hafif bir durum kontrolü sağlar.

## Adım 4: Metin Çıkarma – Burada Olmanızın Gerçek Nedeni

Görüntüyü yüklemek sadece hikayenin yarısıdır. Başarılı bir yüklemenin ardından genellikle OCR metnini istersiniz. İşte metni alıp yazdıran kısa bir yardımcı.

```python
# step_4_extract_text.py
def extract_text(engine):
    """
    Retrieves OCR results from the previously loaded image.
    Returns a string; empty string indicates no text found.
    """
    try:
        result = engine.recognize()
        text = result.text
        if text:
            print("📝 Extracted Text:")
            print(text)
        else:
            print("⚠️ No text detected in the image.")
        return text
    except ocr.OcrException as e:
        print(f"❌ OCR failed (code {e.code}): {e.message}")
        return ""
```

**Neden çalışıyor:**  
`engine.recognize()` çoğu OCR SDK'sında standart çağrıdır. Ham dizeyi, güven skorlarını ve sınırlama kutularını içeren bir sonuç nesnesi döndürür. Bu öğreticide basit tutuyor ve sadece düz metni gösteriyoruz.

## Adım 5: Hepsini Birleştirme – Tam, Çalıştırılabilir Bir Betik

Aşağıda her parçayı birleştiren son betik var. `load_image_ocr_demo.py` olarak kaydedin ve komut satırından çalıştırın.

```python
# load_image_ocr_demo.py
import os
import ocr

def init_engine():
    try:
        engine = ocr.OcrEngine()
        print("✅ OCR engine created.")
        return engine
    except ocr.OcrException as e:
        print(f"❌ Could not create OCR engine (code {e.code}): {e.message}")
        raise

def load_image_with_exception(engine, path):
    try:
        engine.load_image(path)
        print(f"✅ Loaded image via exception method: {path}")
    except ocr.OcrException as ex:
        print(f"❌ Exception while loading '{path}': {ex.message}")

def load_image_with_error_api(engine, path):
    engine.load_image(path)
    err = engine.get_last_error()
    if err:
        print(f"❌ Error API reported for '{path}': {err.message}")
    else:
        print(f"✅ Loaded image via error API: {path}")

def extract_text(engine):
    try:
        result = engine.recognize()
        txt = result.text
        if txt:
            print("📝 OCR Result:")
            print(txt)
        else:
            print("⚠️ No recognizable text.")
        return txt
    except ocr.OcrException as e:
        print(f"❌ Recognition error: {e.message}")
        return ""

def main():
    # 1️⃣ Create the OCR engine
    engine = init_engine()

    # Paths – adjust to your environment
    existing_img = os.path.join("samples", "document.png")
    missing_img = os.path.join("samples", "nonexistent.png")

    # 2️⃣ Load a valid image using exception handling
    load_image_with_exception(engine, existing_img)
    extract_text(engine)

    # 3️⃣ Attempt to load a missing image using the error API
    load_image_with_error_api(engine, missing_img)

if __name__ == "__main__":
    main()
```

**Beklenen çıktı (`document.png` mevcut olduğunda):**

```
✅ OCR engine created.
✅ Loaded image via exception method: samples/document.png
📝 OCR Result:
[Here you’ll see the extracted text from the image]

✅ Loaded image via error API: samples/nonexistent.png
❌ Error API reported for 'samples/nonexistent.png': File not found
```

Görüntü eksik olduğunda, betik çökmeden sorunu nazikçe raporlar—üretimde tam istediğiniz şey.

## Yaygın Tuzaklar ve Profesyonel İpuçları

- **Dosya yolu tuhaflıkları:** Windows ters eğik çizgi (`\`) kullanır ve bu kaçış karakteri olarak yorumlanabilir. Ham dizgileri (`r"C:\path\file.png"`) veya gösterildiği gibi `os.path.join` kullanın.  
- **Desteklenmeyen formatlar:** Tesseract gibi çoğu OCR motoru PNG, JPEG, TIFF kabul eder. BMP verirseniz bir hata kodu alırsınız. Yüklemeden önce Pillow (`Image.save(..., format="PNG")`) ile dönüştürün.  
- **Bellek sızıntıları:** Aynı motoru yeniden kullanmak verimlidir, ancak işiniz bittiğinde özellikle uzun süren hizmetlerde `engine.close()` (veya kütüphanenin eşdeğeri) çağırmayı unutmayın.  
- **Toplu işleme:** Yükleme ve çıkarma adımlarını bir dizin üzerinde `for` döngüsüyle sarın. Her hatayı ayrı bir dosyaya kaydedin; bu, büyük veri setlerini hata ayıklamayı zahmetsiz kılar.

## Görsel Genel Bakış

![OCR motoru oluşturma, hata yönetimi ve metin çıkarma adımlarını gösteren Görüntü OCR diyagramı](load_image_ocr_diagram.png "OCR İş Akışı")

*Alt metin: OCR motoru oluşturma, hata yönetimi ve metin çıkarma adımlarını gösteren Görüntü OCR diyagramı.*

## Sonuç

Python'da **görüntü OCR** yüklemeyi ve **OCR motoru oluşturmayı** güvenilir bir şekilde nasıl yapacağınızı tüm adımlarla ele aldık. Motoru başlatmaktan eksik dosyaları hem istisnalar hem de kütüphanenin hata API'siyle ele almaya, sonunda tanınan metni çıkarmaya kadar, tam betik artık herhangi bir projeye eklenebilir.

Unutmayın: sağlam OCR sadece seçtiğiniz kütüphane ile ilgili değildir; aynı zamanda nazik hata yönetimi, mantıklı kaynak yönetimi ve net günlükleme ile ilgilidir. Burada gösterilen desenlerle tek‑görüntülü bir demodan üretim‑düzeyinde bir toplu iş akışına ölçeklendirebilir, tekerleği yeniden icat etmeden ilerleyebilirsiniz.

### Sıradaki Adımlar

- **Görüntü ön işleme** (kontrast artırma, eğikliği düzeltme) deneyerek doğruluğu artırın.  
- `ocr` yer tutucu paketini Tesseract, EasyOCR veya bir bulut hizmetiyle değiştirin ve `init_engine` fonksiyonunu buna göre ayarlayın.  
- OCR çıktısını bir veritabanına veya belge‑geri getirme senaryoları için bir arama indeksine entegre edin.

Sorularınız veya karşılaştığınız tuhaf bir durum var mı? Aşağıya yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}