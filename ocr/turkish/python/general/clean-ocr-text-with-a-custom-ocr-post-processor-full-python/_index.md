---
category: general
date: 2026-06-22
description: Python’da bir OCR sonrası işlemci kullanarak OCR metnini nasıl temizleyeceğinizi
  öğrenin. Adım adım kod, açıklamalar ve güvenilir yapılandırılmış JSON çıktısı için
  ipuçları.
draft: false
keywords:
- clean OCR text
- OCR post processor
- Python OCR workflow
- structured JSON OCR
- OCR confidence averaging
language: tr
og_description: Bir OCR sonrası işlemci ekleyerek OCR metnini anında temizleyin. Bu
  kılavuz, tam Python uygulamasını, neden işe yaradığını ve nasıl uyarlanacağını gösterir.
og_title: Özel OCR Son İşlemci ile OCR Metnini Temizleme – Python Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to clean OCR text using an OCR post processor in Python.
    Step‑by‑step code, explanations, and tips for reliable structured JSON output.
  headline: Clean OCR Text with a Custom OCR Post Processor – Full Python Guide
  type: TechArticle
tags:
- OCR
- Python
- post‑processing
title: Özel OCR Son İşlemci ile OCR Metnini Temizleme – Tam Python Kılavuzu
url: /tr/python/general/clean-ocr-text-with-a-custom-ocr-post-processor-full-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Özel OCR Son İşlemcisi ile OCR Metnini Temizleme – Tam Python Rehberi

Hiç **OCR metnini temizleme** ihtiyacı duydunuz mu, ancak ham çıktı satır sonları, gereksiz boşluklar ve düşük güvenilirlikli karakterler yüzünden sorun çıkarıyordu? Tek başınıza değilsiniz. Gerçek dünyadaki birçok işlem hattında OCR motoru size bir metin yığını ve bir güven skoru verir ve bunu nasıl faydalı bir şeye dönüştüreceğinizi siz bulmak zorundasınız.  

İyi haber? Küçük bir **OCR post processor** sonucu düzenleyebilir, ortalama güveni hesaplayabilir ve her şeyi şık bir JSON dizesine paketleyebilir—motorun çekirdeğine dokunmadan. Bu öğreticide o post‑processor’ı oluşturacağız, genel bir AI/OCR motoruna kaydedeceğiz ve her kod satırını adım adım inceleyeceğiz, böylece yarın kendi projenize ekleyebilirsiniz.

---

## Bu Öğreticide Neler Kapsanıyor

- **Temiz OCR metni** oluşturacak, boşlukları normalleştiren ve satır sonlarını kaldıran bir post‑processor nasıl oluşturulur.  
- **Ortalama güven** hesabının aşağı akış doğrulaması için neden değerli olduğu.  
- Post‑processor’ı bir OCR motoruna kaydetmek (`ai.set_post_processor` deseni).  
- Oluşturulan yapılandırılmış JSON’ı görüntülemek ve yaygın kenar durumlarını çözmek.  

Python standart kütüphanesi dışındaki bir kütüphane gerekmez, bu yüzden Python 3.8+ çalışan herhangi bir sistemde takip edebilirsiniz.  

---

## Önkoşullar

- `text`, `confidence` (float listesi) ve `bounding_boxes` içeren bir `ocr_result` nesnesi sunan çalışan bir OCR motoru.  
- Python fonksiyonları ve JSON işleme konusunda temel bilgi.  
- İsteğe bağlı: Bağımlılıkları düzenli tutmak için bir sanal ortam.  

Motorunuzun özel post‑processor’ları destekleyip desteklemediğinden emin değilseniz, `set_post_processor` metodunu kontrol edin—çoğu modern AI‑destekli OCR SDK’sı bunu sunar.

---

## Adım 1: **Temiz OCR Metni** Oluşturan OCR Post Processor’ı Tanımlama

İlk olarak, ham OCR sonucunu alan, metni temizleyen, bir güven metriği hesaplayan ve bir JSON dizesi döndüren bir fonksiyon yazarız. Her işlemin neden yapıldığını açıklayan yorumlara dikkat edin; bu yorumlar AI asistanlarının sevdiği “neden” kısmını oluşturur.

```python
import json

def create_structured_json(ocr_result, **kwargs):
    """
    Turn an OCR result into a clean, structured JSON payload.

    Parameters
    ----------
    ocr_result : object
        Must expose .text (raw string), .confidence (list of floats),
        and .bounding_boxes (list of box coordinates).

    Returns
    -------
    str
        JSON string with cleaned text, average confidence, and bounding boxes.
    """
    # 1️⃣ Clean the raw text: replace newlines with spaces and trim excess whitespace.
    clean_text = ocr_result.text.replace("\n", " ").strip()

    # 2️⃣ Compute the average confidence – useful for quality gating.
    # Guard against division by zero if the engine returns an empty list.
    if ocr_result.confidence:
        average_confidence = sum(ocr_result.confidence) / len(ocr_result.confidence)
    else:
        average_confidence = 0.0  # fallback when confidence data is missing

    # 3️⃣ Preserve the original bounding boxes for downstream layout analysis.
    boxes = ocr_result.bounding_boxes

    # 4️⃣ Assemble the dictionary and dump it as a JSON string.
    data = {
        "clean_text": clean_text,
        "average_confidence": average_confidence,
        "boxes": boxes
    }

    # ensure_ascii=False keeps Unicode characters intact (think accented letters, emojis, etc.)
    return json.dumps(data, ensure_ascii=False)
```

**Neden bu çalışır:**  
- `replace("\n", " ")` çok satırlı OCR çıktısını tek bir, aranabilir dizeye dönüştürür—çoğu işlem hattında “temiz OCR metni” tam da budur.  
- Baş ve son boşlukların kaldırılması, daha sonra tokenleştiricileri kırabilecek hayalet boş tokenları önler.  
- Ortalama güveni hesaplamak, tek bir kalite metriği sağlar; örneğin bir veritabanına kaydetmeden önce %0.85’in altındaki sonuçları reddedebilirsiniz.  
- Sınırlama kutularını (bounding boxes) dokunmadan bırakmak, düşük güvenli bölgeleri vurgulamanız gerektiğinde orijinal düzeni hâlâ render edebilmenizi sağlar.

---

## Adım 2: Özel **OCR Post Processor**’ı Motorunuza Kaydetme

Çoğu AI‑destekli OCR SDK’sı bir post‑processing geri çağırma fonksiyonunu takmanıza izin verir. Aşağıda `ai` (motor) nesnesinin `set_post_processor` sağladığını varsayıyoruz. Kütüphaneniz farklı bir isim kullanıyorsa, ona göre değiştirin.

```python
# Register the post‑processor; the second argument can hold custom settings.
ai.set_post_processor(create_structured_json, custom_settings={})
```

**İpucu:** Davranışları (ör. satır sonu kaldırma) açıp/kapatmanız gerektiğinde `custom_settings` üzerinden yapılandırma geçirin. Bu, işlemcinin projeler arasında yeniden kullanılabilir olmasını sağlar.

---

## Adım 3: OCR Motorunu Çalıştırın – Sonuç Artık Bir JSON Dizesi

Post‑processor bağlandığında, `engine.recognize()` (veya SDK’nızın kullandığı yöntem) otomatik olarak `create_structured_json` fonksiyonunu çağırır. Motor daha sonra `.text` özelliği zaten JSON yükünü içeren bir nesne döndürür.

```python
# The engine runs OCR, then our post‑processor formats the output.
structured_result = engine.recognize()
```

> **Not:** Bazı SDK’lar bir nesne yerine düz bir dize döndürebilir. Bir sonraki adımı buna göre ayarlayın.

---

## Adım 4: Yapılandırılmış JSON Çıktısını Görüntüleme (veya Saklama)

Son olarak, JSON’ı konsola yazdırıyoruz. Üretim ortamında bunu bir dosyaya, mesaj kuyruğuna veya veritabanına yazmak muhtemeldir.

```python
# Show the clean OCR text and additional metadata.
print("Structured JSON:", structured_result.text)
```

**Beklenen konsol çıktısı** (okunabilirlik için biçimlendirilmiş):

```json
{
  "clean_text": "The quick brown fox jumps over the lazy dog.",
  "average_confidence": 0.9375,
  "boxes": [
    [0, 0, 120, 30],
    [0, 35, 115, 30],
    ...
  ]
}
```

Eğer gereksiz satır sonu karakterleri ya da `0.0` güven görürseniz, OCR motorunuzun gerçekten `ocr_result.confidence` doldurup doldurmadığını kontrol edin. Post‑processor’daki koruma koşulu `ZeroDivisionError` hatasından sizi korur, ancak güven verisinin neden eksik olduğunu hâlâ öğrenmek isteyeceksiniz.

---

## Yaygın Kenar Durumlarını Ele Alma

| Durum | Dikkat Edilecek | Hızlı Çözüm |
|-----------|-------------------|-----------|
| **Boş OCR sonucu** | `ocr_result.text` `""` ve `confidence` listesi boş | İşlemci zaten boş `clean_text` ve `average_confidence` = 0.0 döndürür. JSON üretimini tamamen atlamak isterseniz koşullu erken dönüş ekleyebilirsiniz. |
| **ASCII dışı karakterler** | Unicode kaçışları (`\u00e9`) | Kodda zaten bulunan `ensure_ascii=False` kullanarak “é” gibi karakterlerin okunabilir kalmasını sağlayın. |
| **Çok uzun belgeler** | JSON boyutu API limitlerini aşabilir | Tek bir dize yerine çıktıyı akış (stream) olarak işleyin veya bir dosyaya yazın. |
| **Sınırlama kutuları eksik** | Bazı OCR motorları düzen verisini sağlamaz | `boxes` değerini `None` ya da boş liste yapın; aşağı akış tüketicileri eksikliği nazikçe ele almalıdır. |

---

## Pro İpuçları & En İyi Uygulamalar

- **Toplu işleme:** Yüzlerce sayfayı OCR’lamak gerekiyorsa, tanıma çağrısını bir döngü içinde sarın ve her JSON yükünü bir listeye toplayın. Ardından tüm listeyi tek bir dosyaya dökerek toplu analiz kolaylığı sağlayın.  
- **Güven eşikleri:** Saklamadan önce `average_confidence` değerini kontrol edin. Kritik veri girişi görevleri için genellikle `0.80` altındaki sonuçları reddetmek iyi bir kuraldır.  
- **Yazdırmak yerine loglamak:** Üretimde `print()` yerine yapılandırılmış bir logger (`logging.info(...)`) kullanın; böylece düşük güvenli sonuç üreten görselleri izleyebilirsiniz.  
- **Test:** Bilinen metin ve güven değerleriyle bir mock `ocr_result` besleyen bir birim testi yazın, ardından JSON yapısının beklentileri karşıladığını doğrulayın.  

---

## Tam Çalışan Örnek (Tüm Adımlar Birleştirildi)

Aşağıda `ocr_cleanup.py` adlı bir dosyaya kopyalayıp yapıştırabileceğiniz tam betik yer alıyor. Yer tutucu `engine` ve `ai` nesnelerini OCR SDK’nızın gerçek örnekleriyle değiştirin.

```python
import json

# ----------------------------------------------------------------------
# Step 1: Define the post‑processor that cleans OCR text and builds JSON.
# ----------------------------------------------------------------------
def create_structured_json(ocr_result, **kwargs):
    """
    Convert raw OCR output into a clean JSON string.
    """
    # Clean the raw text: collapse newlines, trim whitespace.
    clean_text = ocr_result.text.replace("\n", " ").strip()

    # Safely compute average confidence.
    if ocr_result.confidence:
        average_confidence = sum(ocr_result.confidence) / len(ocr_result.confidence)
    else:
        average_confidence = 0.0

    # Keep bounding boxes for layout work.
    boxes = ocr_result.bounding_boxes

    payload = {
        "clean_text": clean_text,
        "average_confidence": average_confidence,
        "boxes": boxes
    }
    return json.dumps(payload, ensure_ascii=False)

# ----------------------------------------------------------------------
# Step 2: Register the post‑processor with the OCR engine.
# ----------------------------------------------------------------------
# Replace `ai` with your actual engine/controller instance.
ai.set_post_processor(create_structured_json, custom_settings={})

# ----------------------------------------------------------------------
# Step 3: Run OCR – the result is automatically transformed.
# ----------------------------------------------------------------------
structured_result = engine.recognize()

# ----------------------------------------------------------------------
# Step 4: Output the structured JSON.
# ----------------------------------------------------------------------
print("Structured JSON:", structured_result.text)
```

Dosyayı kaydedin, `python ocr_cleanup.py` komutunu çalıştırın ve **temiz OCR metni**, ortalama güven skoru ve orijinal sınırlama kutularını içeren güzel biçimlendirilmiş bir JSON dizesi görmelisiniz.

---

## Sonuç

Artık Python’da özel bir **OCR post processor** kullanarak **OCR metnini temizleme** için eksiksiz, üretim‑hazır bir yönteme sahipsiniz. Çözüm boşlukları normalleştirir, eksik güven verilerine karşı koruma sağlar ve aşağı akış servislerinin ekstra ayrıştırma yapmadan tüketebileceği kendini tanımlayan bir JSON yükü döndürür.  

Bundan sonra şunları yapabilirsiniz:

- `clean_text` oluşturulmadan önce **düşük‑güvenli kelimeleri filtrelemek** için işlemciyi genişletmek.  
- **Dil tespiti** ekleyerek JSON’u yerel‑özel kanallara yönlendirmek.  
- **Yazım denetimi** kütüphaneleriyle bir katman daha kalite eklemek.  

Kodu istediğiniz gibi ayarlamaktan, farklı güven eşikleri denemekten veya geliştirmelerinizi yorumlarda paylaşmaktan çekinmeyin. Kodlamanın tadını çıkarın!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilişkili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım kod örnekleri içerir.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}