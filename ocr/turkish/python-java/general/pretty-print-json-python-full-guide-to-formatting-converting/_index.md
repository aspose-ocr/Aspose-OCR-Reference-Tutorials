---
category: general
date: 2026-06-16
description: JSON'u Python'da hızlıca güzel bir şekilde yazdırın ve JSON'u sözlüğe
  (dict) dönüştürmeyi ya da veri manipülasyonu için JSON dizesini Python'da yüklemeyi
  öğrenin. Adım adım öğretici.
draft: false
keywords:
- pretty print json python
- convert json to dict
- load json string python
language: tr
og_description: JSON'u Python'da güzel bir şekilde biçimlendirin ve JSON'u dict'e
  nasıl dönüştüreceğinizi ya da JSON dizesini Python'da nasıl yükleyeceğinizi anında
  görün. Dakikalar içinde JSON işlemede uzmanlaşın.
og_title: JSON'u Güzel Yazdırma Python – Tam Biçimlendirme ve Dönüştürme Rehberi
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Pretty print JSON Python quickly and learn how to convert JSON to dict
    or load JSON string Python for data manipulation. Step‑by‑step tutorial.
  headline: Pretty Print JSON Python – Full Guide to Formatting & Converting
  type: TechArticle
tags:
- python
- json
- data‑processing
title: Python ile JSON'ı Güzel Yazdırma – Biçimlendirme ve Dönüştürme İçin Tam Kılavuz
url: /tr/python-java/general/pretty-print-json-python-full-guide-to-formatting-converting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JSON Python'ı Güzel Yazdırma – Biçimlendirme ve Dönüştürme İçin Tam Kılavuz

Hiç **pretty print JSON Python** yapmanız gerektiğinde çıktının neden her zaman tek, okunaksız bir satır gibi göründüğünü merak ettiniz mi? Yalnız değilsiniz. Birçok projede ham JSON dizesi karışık bir karmaşa halindedir ve hata ayıklama, samanlıkta iğne aramak gibi hissettirir.

İyi haber? Sadece birkaç yerleşik fonksiyonla bu kaotik yığını güzel bir girintili görünüme dönüştürebilir ve ardından **convert JSON to dict** yaparak sorunsuz bir sonraki işleme geçebilirsiniz. Bu öğreticide, Python'da bir JSON dizesi yüklemekten verileri yinelemeye kadar her adımı adım adım göstereceğiz—böylece formatlama ile uğraşmak yerine mantığa odaklanabilirsiniz.

## Bu Öğreticinin Kapsadığı Konular

- `json.dumps` ve `indent` argümanını kullanarak **pretty print JSON Python** nasıl yapılır.  
- **load JSON string Python**'ı yerel bir sözlüğe (dictionary) yüklemenin tam yolu.  
- Ortaya çıkan sözlüğü faydalı Python nesnelerine dönüştürmek, her kelimeyi güven skoru ile birlikte yazdıran pratik bir örnek dahil.  
- Yaygın tuzaklar (örneğin ASCII olmayan karakterlerin işlenmesi) ve hızlı çözümler.  
- Anında kopyalayıp yapıştırabileceğiniz ve uyarlayabileceğiniz tam, çalıştırılabilir bir betik.

Bu kılavuzun sonunda, herhangi bir JSON yükünü insan tarafından okunabilir bir formata dönüştürebilecek ve saf Python ile manipüle edebileceksiniz—harici kütüphanelere gerek yok.

---

## Önkoşullar

- Python 3.8 veya daha yeni ( `json` modülü standart kütüphanenin bir parçasıdır).  
- Sözlükler ve döngüler hakkında temel bir anlayış.  
- İsteğe bağlı olarak, JSON döndüren bir OCR motoru veya herhangi bir hizmet—örneğimiz, bir taklit `engine.recognize()` çağrısı kullanıyor, ancak bunu kendi veri kaynağınızla değiştirebilirsiniz.

## Adım 1: OCR (veya Herhangi Bir JSON‑Üreten) Tanıma Gerçekleştirin

İlk olarak, JSON uyumlu bir sonuca ihtiyacınız var. Birçok bilgisayarlı görü iş akışında OCR motoru, JSON'a serileştirilebilen yapılandırılmış bir nesne üretir. İşte minimal bir yer tutucu:

```python
# Step 1: Simulate an OCR engine that returns a result object
class MockResult:
    def __init__(self):
        self.words = [
            {"text": "Hello", "confidence": 0.98},
            {"text": "World", "confidence": 0.95},
        ]

    # The real engine would have a .to_json() method; we mimic it
    def to_json(self, indent=None):
        import json
        return json.dumps({"words": self.words}, indent=indent)

# Imagine `engine` is your pre‑configured OCR engine
engine = MockResult()
result = engine  # In real code: result = engine.recognize()
```

> **Bu adımın önemi:**  
> OCR yapmasanız bile, genellikle bir API, dosya veya mesaj kuyruğundan veri alırsınız. Nesne, **pretty print** yapabilmemiz için JSON olarak serileştirilebilir olmalıdır.

## Adım 2: JSON Python'ı Güzel Yazdırma

Şimdi ham veriyi güzel bir girintili dizeye dönüştürüyoruz. `indent` parametresi işi yapar.

```python
# Step 2: Serialize the result with pretty printing
json_str = result.to_json(indent=2)  # <-- pretty print JSON Python
print("🔍 Pretty‑printed JSON output:")
print(json_str)   # optional: view the raw JSON output
```

Çıktı şöyle görünecek:

```json
{
  "words": [
    {
      "text": "Hello",
      "confidence": 0.98
    },
    {
      "text": "World",
      "confidence": 0.95
    }
  ]
}
```

> **Pro ipucu:** Daha geniş bir boşluk isterseniz `indent=4` kullanın, ya da anahtarları alfabetik sıraya koymak için `sort_keys=True` ekleyin.

## Adım 3: JSON Dizesini Python → Yerel Sözlüğe Yükleme

İnsanlar için güzel biçimlendirilmiş bir dize harika, ancak Python gerçek iş için sözlükleri sever. İşte **load JSON string Python**'ı yerel bir yapıya yüklediğimiz yer.

```python
# Step 3: Convert the JSON string to a Python dict
import json

result_dict = json.loads(json_str)   # <-- load json string python
print("\n✅ Loaded dict type:", type(result_dict))
```

Şöyle göreceksiniz:

```
✅ Loaded dict type: <class 'dict'>
```

> **Bunu neden yapıyoruz:**  
> Sözlükler O(1) arama, değiştirilebilir veri ve Python ekosisteminin geri kalanıyla sorunsuz entegrasyon sağlar. JSON dizesiyle doğrudan çalışmaya çalışmak sizi zahmetli dize ayrıştırmaya zorlar.

## Adım 4: Tanınan Kelimeler Üzerinde Döngü – Gerçek Dünya Kullanım Durumu

Her kelimeyi ve güven skorunu çıkaralım. Bu, hem **convert json to dict** (zaten sahip olduğumuz sözlük) hem de pratik yinelemeyi gösterir.

```python
# Step 4: Display each word with its confidence score
print("\n🗣️ Recognized words and confidence values:")
for word in result_dict["words"]:
    # f‑string gives us a clean, readable line
    print(f'{word["text"]} (conf: {word["confidence"]})')
```

Beklenen çıktı:

```
🗣️ Recognized words and confidence values:
Hello (conf: 0.98)
World (conf: 0.95)
```

> **Köşe durum ipucu:** JSON'da `"words"` anahtarı eksik olabilecekse, `KeyError`'a karşı koruma ekleyin:

```python
for word in result_dict.get("words", []):
    # safe iteration even when "words" is absent
    print(f'{word.get("text", "<unknown>")} (conf: {word.get("confidence", 0)})')
```

## Adım 5: ASCII Olmayan Karakterlerle Başa Çıkma (Unicode Desteği)

OCR motorları sık sık “é” veya “ü” gibi karakterler döndürür. Varsayılan `json.dumps` bunları `\u00e9` olarak kaçırır. Okunabilir tutmak için `ensure_ascii=False` geçirin.

```python
# Example with non‑ASCII text
result.words.append({"text": "café", "confidence": 0.92})
json_str_utf8 = result.to_json(indent=2)
json_str_utf8 = json.dumps(json.loads(json_str_utf8), indent=2, ensure_ascii=False)

print("\n🌍 Pretty‑printed JSON with Unicode:")
print(json_str_utf8)
```

Artık çıktı kaçırılmış sürüm yerine **café** gösterir. Bu, daha sonra **convert json to dict** yaparken önemlidir; sözlük doğru Unicode dizeleri içerecektir.

## Adım 6: Güzel Yazdırılmış JSON'ı Kaydetme ve Yeniden Yükleme (İsteğe Bağlı)

Bazen biçimlendirilmiş JSON'ı daha sonra incelemek üzere bir dosyada saklamak istersiniz.

```python
# Step 6: Write pretty JSON to a file
with open("ocr_result_pretty.json", "w", encoding="utf-8") as f:
    f.write(json_str_utf8)

# Later you can read it back and still have a dict
with open("ocr_result_pretty.json", "r", encoding="utf-8") as f:
    loaded_dict = json.load(f)   # <-- load json string python from file
print("\n📂 Loaded back from file, type:", type(loaded_dict))
```

Dosya güzel girintili JSON'ı içerecek ve `json.load` otomatik olarak tekrar bir sözlüğe ayrıştıracaktır.

## Adım 7: Hepsini Bir Araya Getirme – Tek Dosyalı Çözüm

Aşağıda, tartışılan her adımı içeren bağımsız bir betik var. `pretty_json_demo.py` adlı bir dosyaya koyup çalıştırabilirsiniz.

```python
#!/usr/bin/env python3
"""
Complete example: pretty print JSON Python, convert JSON to dict,
and load JSON string Python for further processing.
"""

import json

# ----------------------------------------------------------------------
# Mock OCR engine – replace with your real engine when ready
# ----------------------------------------------------------------------
class MockResult:
    def __init__(self):
        self.words = [
            {"text": "Hello", "confidence": 0.98},
            {"text": "World", "confidence": 0.95},
        ]

    def to_json(self, indent=None, ensure_ascii=True):
        # Produce a JSON string; indent triggers pretty printing
        return json.dumps({"words": self.words}, indent=indent, ensure_ascii=ensure_ascii)

# ----------------------------------------------------------------------
# Main workflow
# ----------------------------------------------------------------------
def main():
    # Step 1: Get the result object (real code would call engine.recognize())
    result = MockResult()

    # Step 2: Pretty print JSON Python
    json_str = result.to_json(indent=2)          # pretty print JSON Python
    print("🔍 Pretty‑printed JSON:")
    print(json_str)

    # Step 3: Load JSON string Python → dict
    result_dict = json.loads(json_str)          # load json string python
    print("\n✅ Dictionary type:", type(result_dict))

    # Step 4: Iterate over words
    print("\n🗣️ Words with confidence:")
    for word in result_dict.get("words", []):
        print(f'{word.get("text", "<missing>")} (conf: {word.get("confidence", 0)})')

    # Step 5: Demonstrate Unicode handling
    result.words.append({"text": "café", "confidence": 0.92})
    json_utf8 = result.to_json(indent=2, ensure_ascii=False)
    print("\n🌍 Unicode‑friendly pretty JSON:")
    print(json_utf8)

    # Step 6: Save to file and reload
    with open("pretty_output.json", "w", encoding="utf-8") as f:
        f.write(json_utf8)

    with open("pretty_output.json", "r", encoding="utf-8") as f:
        reloaded = json.load(f)                 # load json string python from file
    print("\n📂 Reloaded dict, size:", len(reloaded.get("words", [])))

if __name__ == "__main__":
    main()
```

Çalıştırın:

```bash
python pretty_json_demo.py
```

Şöyle göreceksiniz: güzel biçimlendirilmiş JSON, sözlük tipi, her kelime ve güven skoru, ve `pretty_output.json`'a kaydedilmiş Unicode‑dostu bir sürüm.  

**İşte bütün hikaye**—ham OCR çıktısından temiz, manipüle edilebilir bir Python sözlüğüne.

## Sıkça Sorulan Sorular (SSS)

| Soru | Cevap |
|------|-------|
| **Harici bir kütüphane gerekir mi?** | Hayır. Yerleşik `json` modülü hem güzel yazdırmayı hem de yüklemeyi yönetir. |
| **JSON'ım çok büyük olursa ne olur?** | `json.dump`'ı bir dosya tutamacı ile kullanarak her şeyi belleğe yüklemekten kaçının; yine de güzel bir dosya için `indent` ayarlayabilirsiniz. |
| **Anahtarları sıralayabilir miyim?** | Evet—deterministik sıralama için `json.dumps`'a `sort_keys=True` ekleyin, bu diff‑tabanlı testlerde yardımcı olur. |
| **Bozuk JSON ile nasıl başa çıkılır?** | `json.loads`'ı bir `try/except json.JSONDecodeError` bloğuna sarın ve sorunlu dizeyi kaydedin. |
| **Daha hızlı bir alternatif var mı?** | Büyük yükler için `orjson` veya `ujson` gibi kütüphaneler daha hızlıdır, ancak `indent` özelliğini desteklemezler— |

## Sonra Ne Öğrenmelisiniz?

Bu öğreticiler, bu rehberde gösterilen tekniklere dayanan yakın konuları kapsar. Her kaynak, adım adım açıklamalarla tam çalışan kod örnekleri içerir ve ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olur.

- [Aspose OCR'ı Görüntü Tanıma'da JSON Sonucu İçin Nasıl Kullanılır](/ocr/english/net/text-recognition/get-result-as-json/)
- [Aspose OCR'ı Görüntü Tanıma'da JSON Sonuçları Almak İçin Nasıl Kullanılır](/ocr/spanish/net/text-recognition/get-result-as-json/)
- [Aspose OCR'ı Görüntü Tanıma'da JSON Sonuçları İçin Nasıl Kullanılır](/ocr/german/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}