---
category: general
date: 2026-04-26
description: AsposeAI OCR sonrası işleme kullanarak kredi kartı numaralarını hızlıca
  maskeleyin. PCI uyumluluğu, düzenli ifade maskelemesi ve veri temizleme konularını
  adım adım bir öğreticide öğrenin.
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: tr
og_description: AsposeAI ile OCR sonuçlarındaki kredi kartı numaralarını maskeleyin.
  Bu öğreticide PCI uyumluluğu, düzenli ifade maskesi ve veri temizleme konuları ele
  alınmaktadır.
og_title: Kredi Kartı Numaralarını Maskele – Tam Python OCR Son İşleme Rehberi
tags:
- OCR
- Python
- security
title: OCR Çıktısındaki Kredi Kartı Numaralarını Maskele – Tam Python Rehberi
url: /tr/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kredi Kartı Numaralarını Maskeleme – Tam Python Rehberi

OCR motorundan doğrudan gelen metinde **kredi kartı numaralarını maskelemeye** hiç ihtiyaç duydunuz mu? Tek başınıza değilsiniz. Düzenlenmiş sektörlerde, tam bir PAN (Primary Account Number) ifşa etmek, PCI uyumluluk denetçileriyle başınızı belaya sokabilir. İyi haber? Birkaç satır Python ve AsposeAI’nin post‑processing kancasıyla, orta sekiz rakamı otomatik olarak gizleyebilir ve güvende kalabilirsiniz.

Bu öğreticide gerçek bir senaryoyu adım adım inceleyeceğiz: bir fiş görüntüsü üzerinde OCR çalıştırmak, ardından herhangi bir PCI verisini temizleyen özel bir **OCR post‑processing** işlevi uygulamak. Sonunda, herhangi bir AsposeAI iş akışına ekleyebileceğiniz yeniden kullanılabilir bir kod parçacığına ve kenar durumlarını yönetmek ve çözümü ölçeklendirmek için birkaç pratik ipucu elde edeceksiniz.

## Öğrenecekleriniz

- **AsposeAI** ile özel bir post‑processor nasıl kaydedilir.
- **regular expression masking** yaklaşımının neden hem hızlı hem de güvenilir olduğu.
- Veri temizleme ile ilgili **PCI compliance** temelleri.
- Birden fazla kart formatı veya uluslararası numaralar için deseni genişletme yolları.
- Beklenen çıktı ve maskenin doğru çalıştığını nasıl doğrulayacağınız.

> **Önkoşullar** – Çalışan bir Python 3 ortamına, Aspose.AI for OCR paketinin kurulmuş olmasına (`pip install aspose-ocr`), ve içinde bir kredi kartı numarası bulunan örnek bir görüntüye (ör. `receipt.png`) sahip olmalısınız. Başka bir dış hizmete ihtiyaç yok.

---

## Adım 1: Kredi Kartı Numaralarını Maskeleyen Bir Post‑Processor Tanımlayın

Çözümün kalbi, OCR sonucunu alan, bir **regular expression masking** rutini çalıştıran ve temizlenmiş metni döndüren küçük bir işlevde yatar.

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**Neden bu çalışıyor:**  
- Regex `(\d{4})\d{8}(\d{4})` tam olarak 16 ardışık rakama eşleşir; Visa, MasterCard ve birçok diğer kartın yaygın formatıdır.  
- İlk ve son dört rakamı (`\1` ve `\2`) yakalayarak, tam PAN saklamayı yasaklayan **PCI compliance** kurallarına uyarak hata ayıklama için yeterli bilgi tutarız.  
- `\1****\2` değişimi, hassas orta sekiz rakamı gizler ve `1234567812345678` → `1234****5678` haline getirir.

> **Pro ipucu:** 15 haneli American Express numaralarını desteklemeniz gerekiyorsa, `r'(\d{4})\d{6}(\d{5})'` gibi ikinci bir desen ekleyin ve iki değişikliği ardışık olarak çalıştırın.

---

## Adım 2: AsposeAI Motorunu Başlatın

Post‑processor'ımızı eklemeden önce, OCR motorunun bir örneğine ihtiyacımız var. AsposeAI, OCR modelini ve özel işleme için basit bir API'yi bir arada sunar.

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**Neden burada başlatılıyor?**  
`AsposeAI` nesnesini bir kez oluşturup birden fazla görüntüde yeniden kullanmak, aşırı yükü azaltır. Motor ayrıca dil modellerini önbelleğe alır, bu da sonraki çağrıları hızlandırır—fiş toplu tararken kullanışlıdır.

---

## Adım 3: Özel Maskeleme Fonksiyonunu Kaydedin

AsposeAI, herhangi bir çağrılabilir nesneyi takmanıza izin veren bir `set_post_processor` yöntemi sunar. `mask_pci` fonksiyonumuzu, şu an için boş bir opsiyonel ayar sözlüğüyle birlikte geçiriyoruz.

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**Arka planda ne oluyor?**  
Daha sonra `run_postprocessor` çağırdığınızda, AsposeAI ham OCR sonucunu `mask_pci`'ye verir. Fonksiyon, tanınan metni içeren hafif bir nesne (`data`) alır ve yeni bir string döndürürsünüz. Bu tasarım, çekirdek OCR'yi dokunulmaz tutarken **veri temizleme** politikalarını tek bir yerde uygulamanıza olanak tanır.

---

## Adım 4: Fiş Görüntüsü Üzerinde OCR Çalıştırın

Motorun çıktıyı nasıl temizleyeceğini bildiğine göre, ona bir görüntü veriyoruz. Bu öğretici için, doğru dil ve çözünürlük ayarlarıyla yapılandırılmış bir `engine` nesnesine zaten sahip olduğunuzu varsayıyoruz.

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**İpucu:** Önceden yapılandırılmış bir nesneniz yoksa, aşağıdaki gibi bir tane oluşturabilirsiniz:

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

`recognize_image` çağrısı, `text` özelliği ham, maskesiz stringi tutan bir nesne döndürür.

---

## Adım 5: Kaydedilen Post‑Processor'ı Uygulayın

Ham OCR verisi elinizde olduğunda, bunu AI örneğine veriyoruz. Motor, daha önce kaydettiğimiz `mask_pci` fonksiyonunu otomatik olarak çalıştırır.

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**Fonksiyonu manuel olarak çağırmak yerine `run_postprocessor` kullanmanın nedeni nedir?**  
Böyle yapmak, özellikle birden fazla post‑processor (ör. yazım denetimi, dil algılama) olduğunda iş akışını tutarlı tutar. AsposeAI, kaydettiğiniz sıraya göre bunları kuyruğa alır ve belirli bir çıktı garantiler.

---

## Adım 6: Temizlenmiş Çıktıyı Doğrulayın

Son olarak, temizlenmiş metni yazdıralım ve kredi kartı numaralarının doğru şekilde maskelendiğini doğrulayalım.

```python
print(final_result.text)
```

**Beklenen çıktı** (alıntı):

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

Fişte kart numarası yoksa, metin değişmeden kalır—maskelenecek bir şey yok, endişelenecek bir şey de yok.

---

## Kenar Durumlarını ve Yaygın Varyasyonları Ele Alma

### Tek Bir Belgede Birden Fazla Kart Numarası
Bir fiş birden fazla PAN içeriyorsa (ör. bir sadakat kartı ve bir ödeme kartı), regex global olarak çalışır ve tüm eşleşmeleri otomatik olarak maskeler. Ek bir koda gerek yok.

### Standart Olmayan Biçimlendirme
Bazen OCR boşluklar veya tireler ekler (`1234 5678 1234 5678` veya `1234-5678-1234-5678`). Bu karakterleri yok sayacak şekilde deseni genişletin:

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

Eklenen `[ -]?` digit blokları arasında isteğe bağlı boşluk veya tireye tolerans gösterir.

### Uluslararası Kartlar
Bazı bölgelerde kullanılan 19 haneli PAN'lar için deseni genişletebilirsiniz:

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

Sadece **PCI compliance**'in uzunluk ne olursa olsun orta rakamları maskelemesi gerektiğini unutmayın.

### Maskelenmiş Değerleri Günlüğe Kaydetme (Opsiyonel)
Denetim izlerine ihtiyacınız varsa, `custom_settings` aracılığıyla bir bayrak geçirin ve fonksiyonu ayarlayın:

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

Ardından şu şekilde kaydedin:

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

`4111111111111111` içeren bir fiş üzerinde bu betiği çalıştırmak şu çıktıyı üretir:

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

Bu, ham OCR'dan **veri temizleme**'ye kadar tüm boru hattıdır—birkaç temiz Python satırıyla sarılmıştır.

---

## Sonuç

AsposeAI’nin post‑processing kancasını, kısa bir regular‑expression rutinini ve **PCI compliance** için bir dizi en iyi uygulama ipucunu kullanarak OCR sonuçlarında **kredi kartı numaralarını nasıl maskeleyebileceğinizi** gösterdik. Çözüm tamamen bağımsızdır, OCR motorunun okuyabildiği herhangi bir görüntüde çalışır ve daha karmaşık kart formatlarını veya günlük gereksinimlerini kapsayacak şekilde genişletilebilir.

Bir sonraki adıma hazır mısınız? Bu maskeyi yalnızca son dört rakamı saklayan bir **veritabanı ekleme** rutinine bağlamayı deneyin veya bir **toplu işlemci** entegre ederek bir klasördeki tüm fişleri gece boyunca tarayın. Ayrıca adres standartlaştırma veya dil algılama gibi diğer **OCR post‑processing** görevlerini de keşfedebilirsiniz—her biri burada kullandığımız aynı deseni izler.

Kenar durumları, performans veya kodu farklı bir OCR kütüphanesine uyarlama hakkında sorularınız mı var? Aşağıya bir yorum bırakın, sohbeti devam ettirelim. Mutlu kodlamalar ve güvende kalın!  

![OCR işlem hattında kredi kartı numaralarının nasıl maskelendiğini gösteren diyagram](https://example.com/images/ocr-mask-flow.png "OCR post‑processing maskleme akış diyagramı")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}