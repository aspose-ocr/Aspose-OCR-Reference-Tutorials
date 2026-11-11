---
category: general
date: 2026-06-25
description: aocr kütüphanesini kullanarak OCR destekli karakterleri hızlıca alın.
  OCR karakterlerini listelemeyi, dilleri ayarlamayı ve Python'da OCR motorunuzu hata
  ayıklamayı öğrenin.
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: tr
og_description: aocr ile OCR destekli karakterleri edinin. Bu rehber, OCR karakterlerini
  listelemeyi, dilleri seçmeyi ve Python’da kenar durumlarını nasıl ele alacağınızı
  gösterir.
og_title: Python'da OCR Destekli Karakterleri Al – Tam Öğretici
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  headline: Get OCR Supported Characters in Python – Complete Guide
  type: TechArticle
- description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  name: Get OCR Supported Characters in Python – Complete Guide
  steps:
  - name: What if the language pack is missing?
    text: 'If you request a language that isn’t bundled, `aocr.Language` won’t contain
      the enum, and you’ll hit an `AttributeError`. Guard against this with a simple
      check:'
  - name: Empty character list
    text: 'Some niche languages might return an empty list if the underlying training
      data is incomplete. In that scenario, you can fall back to a default (e.g.,
      English) or raise a warning:'
  - name: Unicode normalization
    text: 'The list may contain combined characters (e.g., “é” as `e` + acute accent).
      If your downstream processing expects pre‑composed glyphs, run a normalization
      step:'
  type: HowTo
- questions:
  - answer: Yes, the `get_supported_characters()` method is stable across 1.x and
      2.x. The only change is that language enums were moved to `aocr.languages`.
    question: Does this work with aocr version 2.x?
  - answer: 'Absolutely. Use `ord(ch)` inside a list comprehension: ```python code_points
      = [hex(ord(ch)) for ch in supported_chars] ```'
    question: Can I get the Unicode code point for each character?
  - answer: 'aocr includes an `ARABIC` enum. The character list will contain Arabic
      glyphs, but you may need to enable RTL rendering in your downstream UI. ---
      ## Conclusion You now know **how to get OCR supported characters** using the
      aocr library in Python, how to switch between **supported OCR languages**, a'
    question: What about right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Python'da OCR Destekli Karakterleri Al – Tam Rehber
url: /tr/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python’da OCR Desteklenen Karakterleri Al – Tam Kılavuz

Belirli bir dil için **get OCR supported characters** nasıl alınır diye hiç merak ettiniz mi? Tek başınıza değilsiniz. İster bir fiş tarayıcısı, ister çok dilli bir belge ayrıştırıcı geliştirin, motorunuzun tanıyabildiği glifleri tam olarak bilmek hayat kurtarıcıdır. Bu öğreticide, kütüphaneyi kurmaktan dili yapılandırmaya ve sonunda bu karakterleri listelemeye kadar tüm süreci adım adım göstereceğiz— böylece OCR hattınızı dakikalar içinde hata ayıklayıp ince ayar yapabilirsiniz.

**aocr** kütüphanesini kullanacağız; hafif bir Python OCR motoru ve dil yeteneklerini sorgulamayı sorunsuz hâle getiriyor. Bu rehberin sonunda **list OCR characters**, **supported OCR languages** arasında geçiş yapabilecek ve üretimde sizi yakalamadan önce kapsama boşluklarını tespit edebileceksiniz.

---

## Ön Koşullar

İlerlemeye başlamadan önce şunların yüklü olduğundan emin olun:

* Python 3.8 ve üzeri (aocr paketi 3.7 desteğini bırakmıştır)
* İnternet erişimi olan bir terminal veya komut istemcisi
* Python betikleme konusunda temel bilgi (bir `print()` yazdıysanız yeterli)

Harici ağır bağımlılıklar yok—sadece `aocr` pip paketi.

---

## aocr Kütüphanesini (OCR Engine Python) Kurun

İlk olarak çalışan bir **OCR engine Python** kurulumuna ihtiyacınız var. aocr paketi PyPI’de bulunduğu için tek bir pip komutuyla halledilir:

```bash
pip install aocr
```

Sanal ortam (virtual environment) kullanıyorsanız (şiddetle tavsiye edilir), önce onu aktif edin:

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **Pro ipucu:** Beklenmedik API değişikliklerinden kaçınmak için sürümü sabitleyin (`pip install aocr==1.2.4`).

---

## Bir Dil Seçin (Supported OCR Languages)

aocr, birkaç yerleşik dil paketiyle birlikte gelir. Her paket, motorun tanıyabildiği Unicode kod noktalarının kümesini tanımlar. Bu paketleri sorgulamak için motor örneği üzerinde `language` özniteliğini ayarlamanız gerekir.

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

`aocr.Language.ENGLISH` ifadesini başka bir enum değeri (`FRENCH`, `GERMAN` vb.) ile değiştirebilirsiniz. Paketlenmemiş bir dil atamaya çalışırsanız, aocr bir `ValueError` fırlatır. Bu yüzden önce **supported OCR languages** listesini kontrol etmek iyi bir fikirdir:

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

---

## Karakter Kümesini Alın (Get OCR Supported Characters)

İşte öğreticinin kalbi: gerçekten **get OCR supported characters**. Motor, tek karakterlik stringler döndüren kullanışlı bir `get_supported_characters()` metoduna sahiptir.

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

Arka planda aocr, dil paketiyle birlikte gelen bir JSON dosyasını okur ve her Unicode kod noktasını bir Python stringine dönüştürür. Sonuç deterministiktir; aynı dil sürümünde betiği tekrar çalıştırdığınızda aynı listeyi alırsınız.

---

## Kaç Karakter Desteklendiğini Gösterin

Sayıyı bilmek, kapsama genişliğini hızlıca ölçmenizi sağlar. İngilizce için genellikle birkaç bin karakter (noktalama işaretleri ve rakamlar dahil) görürsünüz.

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

`len()` çağrısı O(1)’dir çünkü Python liste uzunluğunu dahili olarak saklar; büyük alfabeler için bile performans kaybı yoktur.

---

## İlk 100 Desteklenen Karakteri Önizleyin

Hızlı bir görsel kontrol, motorun ihtiyacınız olan sembolleri (Euro işareti ya da akıllı tırnaklar gibi) içerip içermediğini ortaya çıkarabilir. İlk yüz karakteri yazdıralım:

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

`join` işlemi dilimi tek bir stringe birleştirir; bu, bir Python listesi yazdırmaktan daha okunaklıdır.

---

## Tam Betik – Tüm Adımlar Tek Dosyada

Aşağıda her şeyi bir araya getiren tam, çalıştırılabilir örnek yer alıyor. `list_supported_chars.py` olarak kaydedin ve terminalinizden `python list_supported_chars.py` komutunu çalıştırın.

```python
# list_supported_chars.py
"""
Complete example showing how to get OCR supported characters
using the aocr library in Python.
"""

import aocr

def main():
    # 1️⃣ Create an OCR engine instance
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Select the language you want to work with (e.g., English)
    # You can change this to any language supported by aocr.
    ocr_engine.language = aocr.Language.ENGLISH

    # 3️⃣ Retrieve the set of characters that the engine can recognize
    supported_chars = ocr_engine.get_supported_characters()

    # 4️⃣ Show how many characters are supported
    print(f"{len(supported_chars)} characters supported for ENGLISH:")

    # 5️⃣ Preview the first 100 supported characters
    preview = "".join(supported_chars[:100])
    print(preview, "...")

if __name__ == "__main__":
    main()
```

**Beklenen çıktı (kısaltılmış):**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

Tam sayı, aocr sürümüne bağlı olarak biraz değişebilir, ancak her zaman uzun bir alfabe ve yaygın noktalama işaretleri göreceksiniz.

---

## Kenar Durumlarını Ele Alma

### Dil paketi eksikse ne olur?

Paketlenmemiş bir dil talep ederseniz, `aocr.Language` enum içinde bulunmaz ve bir `AttributeError` alırsınız. Bunu basit bir kontrolle önleyin:

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### Boş karakter listesi

Niş bazı diller, temel eğitim verileri eksik olduğunda boş bir liste döndürebilir. Bu durumda varsayılan (ör. İngilizce) bir dil kullanabilir ya da bir uyarı yükseltebilirsiniz:

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### Unicode normalizasyonu

Liste birleşik karakterler (ör. “é” = `e` + keskin aksan) içerebilir. Aşağı akış işlemleriniz önceden birleştirilmiş glifler bekliyorsa, bir normalizasyon adımı çalıştırın:

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

---

## Gerçek Dünya Projeleri İçin Pro İpuçları

* **Karakter listesini önbellekle** – Binlerce görüntüyü işlerken her yinelemede `get_supported_characters()` çağırmak gereksiz bir yük oluşturur. Listeyi modül‑seviyesinde bir değişkende tutun ya da daha sonra yeniden kullanmak için JSON olarak serileştirin.
* **Çok‑dilli doğrulama** – Tek bir uygulamada birden çok dili destekliyorsanız, karakter kümelerini kesiştirerek ortak bir alt küme bulun. Bu, yerel ayarlara göre tutarlı UI öğeleri tasarlamanıza yardımcı olur.
* **OCR hatalarını ayıklama** – Motor bir glifi yanlış sınıflandırıyorsa, sorumlu karakteri `list_supported_chars` çıktısıyla karşılaştırın. Eksikse, özel bir eğitim adımı gerektirebilecek bir kapsama boşluğu tespit etmiş olursunuz.
* **Özel fontlarla birleştirme** – aocr Unicode aralığını saygı gösterir, ancak render kalitesi fonta göre değişebilir. Üretimde kullanacağınız tam fontla desteklenen karakterleri test edin; sürprizlerle karşılaşmazsınız.

---

## Sık Sorulan Sorular

**S: Bu, aocr 2.x sürümüyle çalışır mı?**  
C: Evet, `get_supported_characters()` metodu 1.x ve 2.x arasında stabil kalmıştır. Tek değişiklik, dil enumlarının `aocr.languages` altına taşınmasıdır.

**S: Her karakterin Unicode kod noktasını alabilir miyim?**  
C: Kesinlikle. Bir liste kavraması içinde `ord(ch)` kullanın:

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**S: Sağ‑dan‑sol scriptler (Arabic gibi) nasıl ele alınır?**  
C: aocr bir `ARABIC` enum içerir. Karakter listesi Arapça glifleri barındırır, ancak aşağı akış UI’nizde RTL render’ı etkinleştirmeniz gerekebilir.

---

## Sonuç

Artık **how to get OCR supported characters** yöntemini Python’da aocr kütüphanesiyle biliyorsunuz, **supported OCR languages** arasında nasıl geçiş yapacağınızı ve **listing OCR characters**’ın sağlam metin‑tanıma hatları için neden kritik olduğunu anladınız. Tam betik ve yukarıdaki ipuçlarıyla dil kapsamanızı hızlıca doğrulayabilir, eksik glifleri ayıklayabilir ve daha akıllı OCR‑tabanlı uygulamalar geliştirebilirsiniz.

Bir sonraki adıma hazır mısınız? Bu karakter listesini özel bir kelime‑listesi filtresiyle eşleştirin ya da farklı bir OCR motoru (Tesseract, EasyOCR) deneyin ve sonuçları karşılaştırın. Ne kadar çok keşif yaparsanız, OCR çözümleriniz o kadar iyi olur.

İyi kodlamalar, ve karakter setleriniz her zaman eksiksiz olsun!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalar ve tam çalışan kod örnekleri içerir; böylece ek API özelliklerini ustalaşabilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Specify Allowed Characters OCR – Using Aspose.OCR for .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Post Processing – Get Character Choices](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}