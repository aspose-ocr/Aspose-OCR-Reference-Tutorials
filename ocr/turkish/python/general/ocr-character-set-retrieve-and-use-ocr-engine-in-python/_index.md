---
category: general
date: 2026-06-06
description: 'OCR karakter seti rehberi: OCR motorunu kullanarak Latin ve Kiril alfabeleri
  için desteklenen karakterleri tam Python örnekleriyle nasıl listeleyeceğinizi öğrenin.'
draft: false
keywords:
- ocr character set
- use OCR engine
- supported OCR characters
- script detection OCR
- OCR library Python
language: tr
og_description: 'OCR karakter seti rehberi: Python’da OCR motorunu nasıl kullanarak
  çeşitli yazı tipleri için desteklenen karakterleri listeleyeceğinizi keşfedin, kod
  ve ipuçlarıyla birlikte.'
og_title: OCR Karakter Seti – OCR Motorunu Al ve Kullan
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: 'OCR character set guide: learn how to use OCR engine to list supported
    characters for Latin and Cyrillic scripts with full Python examples.'
  headline: OCR Character Set – Retrieve and Use OCR Engine in Python
  type: TechArticle
tags:
- OCR
- Python
- Character Sets
title: OCR Karakter Seti – Python’da OCR Motorunu Al ve Kullan
url: /tr/python/general/ocr-character-set-retrieve-and-use-ocr-engine-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Karakter Seti – Python'da OCR Motorunu Al ve Kullan

Kütüphanenizin desteklediği **ocr character set**'i öğrenmek ister misiniz? Bu öğreticide, farklı betikler için desteklenen karakterleri sorgulamak ve bunun gerçek dünya projelerinde neden önemli olduğunu göstermek için **use OCR engine**'i nasıl kullanacağınızı göstereceğiz.

Eğer OCR işleme sonrasında bazı harflerin neden hiç görünmediğini merak ederek boş bir ekrana bakıyorsanız, yalnız değilsiniz. Cevap genellikle motorun bildiği karakter setinde gizlidir. Bu rehberin sonunda şunları yapabilecek:

* Belirli bir betik için bir OCR motorunun tanıyabileceği tüm karakterleri listeleyin.  
* Bir betik desteklenmediğinde durumları yönetin.  
* Karakter‑seti bilgisini sonraki doğrulama veya UI mantığına entegre edin.

Sihirli kara kutu hileleri yok—sadece saf Python, birkaç satır kod ve biraz açıklama.

---

## Önkoşullar

İlerlemeye başlamadan önce, şunların yüklü olduğundan emin olun:

* Python 3.8+ yüklü (kod f‑string'leri kullanıyor).  
* `ocr.OcrEngine` sağlayan OCR kütüphanesi—bu örnek için `ocr` adlı paketin `pip install ocr-lib` ile zaten yüklü olduğunu varsayacağız.  
* Python'un import sistemi ve çıktı verme konusunda temel bilgi.

Eğer kütüphane eksikse, şu komutu çalıştırın:

```bash
pip install ocr-lib
```

Bu kadar—temel karakter‑seti sorguları için ekstra ikili dosyalar veya yerel bağımlılıklar gerekmez.

## Adım 1: OCR Motoru Örneğini Başlatma

Bir motor nesnesi oluşturmak, **use OCR engine** işlevselliğini kullandığınızda yaptığınız ilk şeydir. Bunu bir tarayıcıyı açmak gibi düşünün; olmadan hiçbir soru soramazsınız.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

`OcrEngine` sınıfı, temel tanıma motorunun hafif bir sarmalayıcısıdır. Bir şey talep edene kadar ağır işlemeye başlamaz, bu yüzden başlangıç maliyeti ihmal edilebilir.

> **Pro ipucu:** Uygulamanız birçok motor örneği oluşturuyorsa, tek bir örneği yeniden kullanın. Belleği tasarruf eder ve başlatma gecikmesini azaltır.

## Adım 2: Belirli Bir Betik İçin OCR Karakter Setini Sorgulama

Artık bir motorumuz olduğuna göre, ona belirli bir yazı sistemi için hangi karakterleri bildiğini sorabiliriz. `get_supported_characters(script_name)` yöntemi, Unicode karakterlerinin bir Python `list`'ini döndürür.

```python
# Step 2: Get the list of characters the engine can recognize for the Latin script
latin_chars = engine.get_supported_characters("Latin")
print(f"Supported Latin chars ({len(latin_chars)}): {latin_chars}")
```

Yukarıdaki kod parçasını çalıştırmak şöyle bir çıktı verir:

```
Supported Latin chars (26): ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
```

Tam çıktı OCR kütüphanesinin sürümüne bağlıdır, ancak her zaman düz bir karakter listesi alırsınız. Hem büyük hem küçük harflere ihtiyacınız varsa, sadece `"Latin"` betiğini isteyin ve ardından her öğeye `.lower()` uygulayın, ya da kütüphane ayırıyorsa ayrı bir `"Latin‑lower"` betiğini sorgulayın.

### Neden Önemli?

Alışılmadık diakritik işaretler içeren bir görüntü (ör. “ñ” veya “ø”) beslediğinizde, OCR motoru bunları sessizce bir yer tutucu ile değiştirebilir veya tamamen atabilir. **ocr character set**'i önceden bilmek, girdiyi ön‑doğrulamanıza, kullanıcıları uyarmanıza veya farklı bir motora geçmenize olanak tanır.

## Adım 3: Başka Bir Betik İçin Karakterleri Al – Kiril Örneği

Aynı yöntem, motorun desteklediğini iddia ettiği herhangi bir betik için çalışır. Kiril alfabesiyle ne olacağını görelim.

```python
# Step 3: Get the list of characters the engine can recognize for the Cyrillic script
cyrillic_chars = engine.get_supported_characters("Cyrillic")
print(f"Supported Cyrillic chars ({len(cyrillic_chars)}): {cyrillic_chars}")
```

Tipik çıktı:

```
Supported Cyrillic chars (33): ['А', 'Б', 'В', 'Г', 'Д', 'Е', 'Ё', 'Ж', 'З', 'И', 'Й', 'К', 'Л', 'М', 'Н', 'О', 'П', 'Р', 'С', 'Т', 'У', 'Ф', 'Х', 'Ц', 'Ч', 'Ш', 'Щ', 'Ъ', 'Ы', 'Ь', 'Э', 'Ю', 'Я']
```

Motor istenen betiği **desteklemiyorsa**, genellikle bir `ValueError` yükseltir (veya uygulamaya bağlı olarak boş bir liste döner). Buna karşı önlem alalım.

```python
def safe_get_characters(engine, script):
    try:
        chars = engine.get_supported_characters(script)
        if not chars:
            print(f"No characters returned for script '{script}'.")
        else:
            print(f"Supported {script} chars ({len(chars)}): {chars}")
        return chars
    except Exception as e:
        print(f"Error retrieving characters for script '{script}': {e}")
        return []

# Example usage:
safe_get_characters(engine, "Arabic")   # Might trigger the error branch
```

## Adım 4: OCR Karakter Setini Görselleştirme (İsteğe Bağlı)

Bazen hızlı bir görsel yardımcı olur, özellikle paydaşlara hangi karakterlerin kapsandığını göstermeniz gerektiğinde. Aşağıda `matplotlib` kullanarak bir karakter ızgarasını çizen minimal bir örnek var.

```python
import matplotlib.pyplot as plt

def plot_character_grid(chars, title="OCR Character Set"):
    cols = 10
    rows = (len(chars) + cols - 1) // cols
    fig, ax = plt.subplots(figsize=(cols, rows))
    ax.set_axis_off()
    for idx, ch in enumerate(chars):
        row = idx // cols
        col = idx % cols
        ax.text(col / cols, 1 - row / rows, ch, fontsize=14, ha='center', va='center')
    plt.title(title)
    plt.show()

# Visualize Latin characters
plot_character_grid(latin_chars, title="Latin OCR Character Set")
```

> **Görsel alt metni:** ![OCR character set diagram](ocr_character_set.png){alt="OCR character set overview"}

Diagram temel çözüm için gerekli değildir, ancak **use OCR engine** meta verilerini düz yazdırmanın ötesinde nasıl kullanabileceğinizi gösterir.

## Adım 5: Karakter Setini Gerçek‑Dünya İş Akışlarına Entegre Etme

Artık **ocr character set**'i alabileceğimize göre, pratik bir senaryoya bakalım: OCR çıktısını bir veritabanına kaydetmeden önce doğrulama.

```python
def validate_ocr_output(text, allowed_chars):
    """Return True if every character in `text` exists in `allowed_chars`."""
    invalid = [c for c in text if c not in allowed_chars]
    if invalid:
        print(f"Invalid characters found: {invalid}")
        return False
    return True

# Suppose we ran OCR on an image and got this result:
ocr_result = "HELLO WORLD!"

# Use the previously fetched Latin set for validation:
if validate_ocr_output(ocr_result, set(latin_chars)):
    print("All characters are supported – safe to store.")
else:
    print("Result contains unsupported symbols – consider manual review.")
```

Bu desen, çok dilli belgelerle çalışırken sık karşılaşılan bir sorun olan hatalı verilerin sonraki işlem hatlarına sızmasını önler.

## Yaygın Tuzaklar ve Kenar Durumları

| Sorun | Neden Olur | Nasıl Önlenir |
|-------|------------|---------------|
| **Betik adı yazım hatası** (ör. `"Cyrillic "` sonundaki boşluk) | Motor dizeyi harfi harfine alır ve betiği bulamaz. | `get_supported_characters` çağırmadan önce `script.strip()` ile boşlukları temizleyin. |
| **Boş karakter listesi** | Bazı motorlar bir betiği gösterir ancak dil modelini henüz yüklememiştir. | Kütüphane böyle bir yöntem sağlıyorsa `engine.load_language_model(script)` çağırın veya model dosyalarının mevcut olduğundan emin olun. |
| **Unicode normalizasyon sorunları** | “é” gibi karakterler birleşik (`\u00E9`) veya ayrık (`e\u0301`) biçimde görünebilir. | Doğrulamadan önce `unicodedata.normalize('NFC', text)` ile dizeleri normalleştirin. |
| **Büyük betiklerde performans** (ör. Çince) | Binlerce karakteri almak yavaş olabilir. | İlk çağrıdan sonra sonucu önbelleğe alın; çoğu uygulama listeye sadece bir kez ihtiyaç duyar. |

## Tam Çalışan Örnek

Tüm parçaları birleştirerek, kopyalayıp yapıştırıp çalıştırabileceğiniz tek bir betik:

```python
import ocr
import matplotlib.pyplot as plt

def safe_get_characters(engine, script):
    try:
        chars = engine.get_supported_characters(script)
        if not chars:
            print(f"No characters returned for script '{script}'.")
        else:
            print(f"Supported {script} chars ({len(chars)}): {chars}")
        return chars
    except Exception as e:
        print(f"Error retrieving characters for script '{script}': {e}")
        return []

def plot_character_grid(chars, title="OCR Character Set"):
    cols = 10
    rows = (len(chars) + cols - 1) // cols
    fig, ax = plt.subplots(figsize=(cols, rows))
    ax.set_axis_off()
    for idx, ch in enumerate(chars):
        row = idx // cols
        col = idx % cols
        ax.text(col / cols, 1 - row / rows, ch, fontsize=14


## Sonra Ne Öğrenmelisiniz?

Bu öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose OCR Öğreticisi – Optik Karakter Tanıma](/ocr/english/)
- [OCR Son İşleme – Karakter Seçeneklerini Al](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [OCR Görüntü Tanıma'da Eşik Değerini Nasıl Ayarlarsınız](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}