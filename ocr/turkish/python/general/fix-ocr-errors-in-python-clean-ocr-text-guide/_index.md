---
category: general
date: 2026-03-18
description: Python'da OCR hatalarını hızlıca düzeltin. OCR'ı nasıl temizleyeceğinizi,
  OCR metnini nasıl temizleyeceğinizi öğrenin, sıfırı O ile değiştirin ve Python OCR
  sonrası işleme uygulayın.
draft: false
keywords:
- fix OCR errors
- how to clean OCR
- clean OCR text python
- replace zero with O
- python OCR post processing
language: tr
og_description: Python'da OCR hatalarını hızlıca düzeltin. OCR'yi nasıl temizleyeceğinizi,
  sıfırı O ile nasıl değiştireceğinizi ve tek bir öğreticide Python OCR sonrası işleme
  nasıl kullanacağınızı öğrenin.
og_title: Python'da OCR Hatalarını Düzelt – OCR Metnini Temizleme Rehberi
tags:
- OCR
- Python
- Text Cleaning
title: Python'da OCR Hatalarını Düzelt – OCR Metnini Temizleme Rehberi
url: /tr/python/general/fix-ocr-errors-in-python-clean-ocr-text-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python’da OCR Hatalarını Düzelt – Temiz OCR Metni Rehberi

Hiç taranmış bir faturaya bakıp, *“Bu veriyi veritabanıma göndermeden önce OCR hatalarını nasıl düzeltebilirim?”* demiş miydiniz? Yalnız değilsiniz. Belge otomasyonu dünyasında tek bir yanlış okunan karakter tüm akışı bozabilir; bu yüzden **OCR çıktısını nasıl temizleyeceğinizi** öğrenmek çok önemlidir.  

Bu öğreticide, ürün kodlarında sıkça karşılaşılan “0” rakamının “O” harfiyle değiştirilmesini sağlayan küçük bir post‑processörü kullanarak **OCR hatalarını düzeltmenin** pratik, uçtan uca bir yolunu göreceksiniz. Sonunda, bu çözümü herhangi bir Python OCR iş akışına entegre edip daha temiz ve güvenilir metin elde edebileceksiniz.

> **Neler elde edeceksiniz:** çalıştırılabilir tam bir Python betiği, her satırın neden önemli olduğuna dair açıklamalar, mantığı genişletmek için ipuçları ve beklenen çıktının hızlı bir doğrulaması.

## Önkoşullar — Başlamadan Önce Gerekenler

- Python 3.8 ve üzeri (sözdizimi tüm yeni sürümlerde çalışır).  
- Raw string döndüren temel bir OCR kütüphanesi (ör. `pytesseract` üzerinden Tesseract).  
- Python’da fonksiyonlar ve nesneler hakkında temel bilgi.  

Eğer zaten bir OCR adımınız var ve string üretiyorsa, ek bir kurulum yapmanıza gerek yok – post‑processing kısmı için başka bir şey yüklemeniz gerekmeyecek.

## Adım 1: Minimal Bir AI‑Benzeri Sarmalayıcı Oluşturun (Neden Gerekli?)

Birçok projede OCR motoru, ön‑işleme, çıkarım ve post‑processing yapan daha büyük bir “AI” sınıfının içinde yer alır. Örneği bağımsız tutmak için, bu deseni taklit eden küçük bir `AIProcessor` sınıfı oluşturacağız. Bu, kodu mevcut bir kod tabanına yeniden yazmadan eklemenizi kolaylaştırır.

```python
# ai_wrapper.py
class AIProcessor:
    """
    Simple wrapper that stores a post‑processing callable.
    In real projects this could be a full‑fledged model class.
    """
    def __init__(self):
        self._post_processor = None

    def set_post_processor(self, func):
        """Register a function that will clean OCR output."""
        if not callable(func):
            raise TypeError("Post‑processor must be callable")
        self._post_processor = func

    def run_postprocessor(self, text):
        """Apply the registered post‑processor to raw OCR text."""
        if self._post_processor is None:
            raise RuntimeError("No post‑processor has been set")
        return self._post_processor(text)
```

**Neden önemli:** post‑processörü OCR motorundan ayrı tutmak, tek sorumluluk ilkesine uyar ve temizlik mantığını OCR koduna dokunmadan değiştirebilmenizi sağlar.

## Adım 2: **OCR Hatalarını Düzelt** Fonksiyonunu Yazın

Şimdi öğretinin kalbini oluşturuyoruz: **OCR hatalarını düzelt** fonksiyonu, “0” rakamını “O” harfiyle değiştiriyor. Bu desen, ürün kodları, seri numaraları ve OCR motorunun iki karakteri sıkça karıştırdığı tüm alfanümerik tanımlayıcılara uygulanabilir.

```python
# post_processors.py
def correct_ocr_errors(text: str) -> str:
    """
    Replace common OCR mis‑reads.
    Example: change digit "0" to letter "O" in product codes.
    """
    # You could add more rules here, e.g.:
    # text = text.replace('1', 'I')
    # text = text.replace('5', 'S')
    return text.replace("0", "O")
```

**Neden 0’ı O ile değiştiriyoruz:** Birçok yazı tipinde sıfır ve büyük O birbirine çok benzer, bu yüzden OCR sık sık yanlışını seçer. Erken düzeltme, aşağı akışta (ör. regex kontrolleri) doğrulamanın doğru çalışmasını sağlar.

## Adım 3: Post‑Processor’ı AI Örneğine Bağlayın

Sarmalayıcı ve temizlik fonksiyonu hazır olduğunda, bunları bir araya getiriyoruz. Bu, üretim hattında özel bir post‑processor kaydetmenin aynısıdır.

```python
# main.py
from ai_wrapper import AIProcessor
from post_processors import correct_ocr_errors

# Create the AI‑like object
ai = AIProcessor()

# Register our OCR‑fixing function
ai.set_post_processor(correct_ocr_errors)
```

Farklı bir dil ya da veri formatı için **OCR çıktısını nasıl temizleyeceğinizi** öğrenmek isterseniz, sadece yeni bir fonksiyon yazıp `set_post_processor`ı tekrar çağırmanız yeterlidir – pipeline’ın geri kalanına dokunmanıza gerek kalmaz.

## Adım 4: Raw OCR Metnini Besleyin ve Temiz Sonucu Alın

Korkulan “0” karakterinin bulunduğu ham bir OCR string’i simüle edelim. Gerçek senaryoda bu placeholder’ı `pytesseract.image_to_string(image)` ya da benzeri bir çağrı ile değiştirirsiniz.

```python
# Simulated OCR output (replace with your own OCR call)
raw_text = "Product code: 10A0B"

# Run the post‑processor to obtain cleaned text
cleaned_text = ai.run_postprocessor(raw_text)

print("Before cleaning :", raw_text)
print("After cleaning  :", cleaned_text)
```

**Beklenen çıktı**

```
Before cleaning : Product code: 10A0B
After cleaning  : Product code: 1OAOB
```

Sıfırların büyük O harflerine dönüştüğüne dikkat edin; böylece çoğu envanter sisteminin beklediği formatla uyumlu bir string elde ederiz.

## Adım 5: Mantığı Genişletin – Gerçek Dünya Varyasyonları

Yukarıdaki basit değişim dar bir durumu çözer, ancak üretimde başka tuhaflıklarla karşılaşırsınız:

| Yaygın hata | OCR Örneği | İstenen Düzeltme | Nasıl Eklenir |
|------------|------------|------------------|---------------|
| “1” okunurken “I” | `I23` | `123` | `text = text.replace('I', '1')` |
| “5” okunurken “S” | `S9` | `59` | `text = text.replace('S', '5')` |
| Fazla boşluk | `  ABC  ` | `ABC` | `text = text.strip()` |
| Karışık‑büyük/küçük harf | `oRder` | `Order` | `text = text.title()` |

`correct_ocr_errors` fonksiyonuna bu kurallardan istediğinizi ekleyebilirsiniz. Her dönüşümün **idempotent** (iki kez çalıştırıldığında sonuç değişmemeli) olmasına dikkat edin; aksi takdirde istenmeyen veri bozulmaları ortaya çıkabilir.

```python
def correct_ocr_errors(text: str) -> str:
    text = text.replace("0", "O")
    text = text.replace("I", "1")
    text = text.replace("S", "5")
    return text.strip()
```

**İpucu:** Geçerli kodların bir kataloğu varsa, temizlenmiş string’i bir regex ya da lookup tablosu ile doğrulamayı düşünün. Bu ek adım, basit karakter değişimlerinin kaçırdığı OCR hatalarını yakalar.

## Adım 6: Gerçek Bir OCR Motoru ile Entegre Edin (Opsiyonel)

Aşağıda, `pytesseract` kullanarak post‑processor’ı gerçek bir OCR akışına nasıl bağlayacağınızı gösteren hızlı bir örnek bulunuyor. Bu kısım isteğe bağlıdır ancak uçtan uca pipeline’ı gösterir.

```python
import pytesseract
from PIL import Image
from ai_wrapper import AIProcessor
from post_processors import correct_ocr_errors

# Initialize AI wrapper and register the cleaner
ai = AIProcessor()
ai.set_post_processor(correct_ocr_errors)

# Load an image containing a product label
image = Image.open("sample_label.png")

# Perform OCR (this returns raw text)
raw_ocr = pytesseract.image_to_string(image)

# Clean the OCR output
cleaned = ai.run_postprocessor(raw_ocr)

print("Raw OCR   :", raw_ocr)
print("Cleaned   :", cleaned)
```

> **Not:** `pytesseract`, sisteminizde Tesseract OCR’ın kurulu olmasını bekler. Yukarıdaki snippet, ikili dosya PATH içinde olduğu sürece Windows, macOS ve Linux’da çalışır.

## Adım 7: Sonuçları Programatik Olarak Doğrulayın

Büyük toplu işlemler otomatikleştirildiğinde, temizlik adımının beklendiği gibi çalıştığını doğrulamak faydalıdır. Kısa bir birim testi, ileride saatler sürecek hata ayıklamayı önleyebilir.

```python
def test_correct_ocr_errors():
    assert correct_ocr_errors("0O0") == "OOO"
    assert correct_ocr_errors(" 10A0B ") == "1OAOB"
    print("All tests passed!")

test_correct_ocr_errors()
```

Bu testi çalıştırmak, fonksiyonun **OCR hatalarını** tutarlı bir şekilde düzelttiğini, ekstra boşluklar gibi durumlarda bile doğrular.

## Görsel Açıklama

Aşağıda pipeline’ın görsel bir taslağı yer alıyor (SEO için anahtar kelime alt metinde bulunuyor).

![OCR hatalarını düzeltme pipeline diyagramı – ham OCR’un sıfırı O ile değiştiren bir post‑processor’a beslenmesini gösterir]()

## Sonuç – Ne Başardık?

Tamamen çalıştırılabilir bir örnek üzerinden **Python’da OCR çıktısını nasıl temizleyeceğinizi** gösterdik; özellikle **sıfırı O ile değiştirme** ve **OCR hatalarını düzeltme** için modüler bir post‑processor kullandık. Temizleme mantığını OCR motorundan ayırarak esneklik, test edilebilirlik ve gelecekte *başka karakter karışıklıkları için OCR nasıl temizlenir* gibi kurallar eklemek için net bir yer elde ettik.

Bir sonraki adımınıza hazır mısınız? Ürün kodları için bir regex doğrulayıcı ekleyin, gürültülü metinler için bulanık eşleşme deneyin ya da zaten post‑processing kancaları içeren tam özellikli bir kütüphane olan `ocrmypdf`’yi keşfedin. Ele aldığımız desen, birkaç fatura ya da milyonlarca taranmış belgeyle çalışsanız da sorunsuz ölçeklenir.

---

*Kodlamaktan keyif alın, OCR pipeline’larınız hatasız kalsın!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}