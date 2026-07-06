---
category: general
date: 2026-06-25
description: Python'da OCR motorunu başlatarak, özel sözlükler, dil ayarları ve bölge
  hedefleme kullanarak çok sayfalı PDF'lerden metin çıkarın.
draft: false
keywords:
- initialize OCR engine
- configure OCR language
- OCR image preprocessing
- OCR custom dictionary
- recognize multi-page PDF
language: tr
og_description: Python'da OCR motorunu başlatarak Vietnamca PDF'leri güvenilir bir
  şekilde okuyun; dil, ön işleme ve doğru sonuçlar için özel sözlüğü yapılandırın.
og_title: OCR Motorunu Başlat – Adım Adım PDF Çıkarma Rehberi
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  headline: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  type: TechArticle
- description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  name: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed. - An OCR library that exposes an `OcrEngine` class
      (the sample uses a hypothetical `ocr` package; replace with your actual SDK).
      - A sample multi‑page PDF (`sample.pdf`) placed in a known directory. - Basic
      familiarity with Python dictionaries and loops.'
  - name: Pro tip
    text: If you ever need to support multiple languages in the same run, you can
      switch `ocr_engine.language` on the fly before processing each page. Just remember
      to re‑initialize any heavy models if the SDK requires it.
  - name: Expected Output
    text: 'Running the script against a three‑page invoice PDF might produce:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: OCR Motorunu Başlat – PDF Metin Çıkarma İçin Tam Rehber
url: /tr/python-java/general/initialize-ocr-engine-complete-guide-for-pdf-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Motorunu Başlatma – PDF Metin Çıkarma için Tam Kılavuz

Vietnamca faturalar topluluğu için **OCR motorunu başlatma** ihtiyacı hiç duydunuz mu ama nereden başlayacağınızı bilemediniz mi? Tek başınıza değilsiniz. Gerçek dünyadaki birçok projede ilk engel, OCR kütüphanesini PDF'lerinizle çalıştırmak, özellikle dili, ön işleme ya da özel bir sözlüğü ayarlamanız gerektiğinde.

Bu rehberde, **OCR motorunu başlatma**, dili yapılandırma, akıllı görüntü ön işleme etkinleştirme, özel bir sözlük ekleme ve sonunda çok sayfalı bir PDF'in her sayfasından yapılandırılmış veri çıkarma konularını gösteren tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Sonunda, kendi projenize ekleyebileceğiniz eksiksiz bir betiğe sahip olacaksınız—eksik parça yok, “belgelere bak” kısayolları da yok.

## Öğrenecekleriniz

- Vietnamca dil desteğiyle **OCR motorunu başlatma** nasıl yapılır.  
- Doğruluk için **OCR dilini yapılandırmanın** neden önemli olduğu.  
- **OCR görüntü ön işleme** seçeneklerini, otomatik eğik düzeltme ve otomatik ikilileştirme gibi, kullanma.  
- Alan‑spesifik terimlerin tanınmasını artırmak için **OCR özel sözlüğü** ekleme.  
- **Çok sayfalı PDF** dosyalarını tanıma ve belirli bir bölgeyi (ör. toplam tutar) çıkarma.  
- Ham sonuçları sonraki işlem için temiz bir JSON‑benzeri yapıya dönüştürme.

### Önkoşullar

- Python 3.8+ yüklü.  
- `OcrEngine` sınıfını sunan bir OCR kütüphanesi (örnek, varsayımsal bir `ocr` paketi kullanıyor; gerçek SDK'nızla değiştirin).  
- Bilinen bir dizine yerleştirilmiş örnek çok sayfalı PDF (`sample.pdf`).  
- Python sözlükleri ve döngülerine temel aşinalık.

Eğer bunlara sahipseniz, başlayalım.

---

## Adım 1: Python'da OCR Motorunu Nasıl Başlatılır

Yapmanız gereken ilk şey **OCR motorunu başlatmaktır**. Bunu, bir makineyi açıp ona hangi dili besleyeceğinizi söylemek gibi düşünün.

```python
import ocr  # Replace with your actual OCR package

# Create the engine instance
ocr_engine = ocr.OcrEngine()

# Set the language to Vietnamese – this tells the engine which character set to expect
ocr_engine.language = ocr.Language.Vietnamese
```

> **Neden önemli:**  
> Çoğu OCR motoru genel dil paketleriyle gelir. `ocr_engine.language` değerini açıkça ayarlayarak motorun yanlış karakter tahmin etmesini önlersiniz, bu da Vietnamca'da yaygın olan diakritik işaretlerin hatalı tanınmasını büyük ölçüde azaltır.

### Pro ipucu
Aynı çalıştırmada birden fazla dili desteklemeniz gerekirse, her sayfayı işlemden önce `ocr_engine.language` değerini anlık olarak değiştirebilirsiniz. SDK bunu gerektiriyorsa ağır modelleri yeniden başlatmayı unutmayın.

---

## Adım 2: OCR Görüntü Ön İşleme Seçeneklerini Etkinleştirme

Ham taramalar nadiren mükemmeldir. Eğik sayfalar, dengesiz aydınlatma veya düşük kontrast en iyi tanıyıcıları bile zorlayabilir. Bu yüzden başlatmadan hemen sonra **OCR görüntü ön işleme** yapılandırıyoruz.

```python
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,      # Auto‑rotate to correct tilt
    auto_binarize=True    # Convert to black‑and‑white for sharper edges
)
```

Bu iki bayrak çoğu taranmış faturayı temizlemek için genellikle yeterlidir. Kaynak PDF'leriniz zaten yüksek kalitedeyse, sayfa başına birkaç milisaniye tasarruf etmek için bunları kapatabilirsiniz.

---

## Adım 3: OCR Özel Sözlüğü Eklemek

Alan‑spesifik terimler—örneğin sipariş kodları, ürün kimlikleri veya yasal kısaltmalar—genel dil modellerinde nadiren bulunur. Bir **OCR özel sözlüğü** besleyerek motoru bir kopya kağıdıyla donatırsınız.

```python
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]
```

> **Arka planda ne oluyor?**  
> Motor, bu listedeki bir girişle eşleşen her kelimenin güven skorunu artırır, böylece başka bir şey olarak yanlış okunma olasılığı çok azalır.

---

## Adım 4: Çok Sayfalı PDF'i Tanıma – Tüm Metni Bir Seferde Çekme

Motor tamamen yapılandırıldığından, **çok sayfalı PDF** dosyalarını tanıyabiliriz. `recognize_multi_page` yöntemi, her öğesi zaten OCR‑işlenmiş tek bir sayfayı temsil eden bir liste döndürür.

```python
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)
```

Yüzlerce sayfalık dev PDF'lerle çalışıyorsanız, bellek kullanımını düşük tutmak için onları parçalar halinde işlemeyi düşünün. SDK genellikle bu senaryo için bir akış API'si sunar.

---

## Adım 5: Her Sayfadan Belirli Bir Bölgeyi Çıkarma

Çoğu faturada her sayfada aynı konumda bulunan bir “Toplam Tutar” alanı vardır. Tüm sayfa metnini ayrıştırmak yerine, motoru bir dikdörtgene odaklamasını söyleyebiliriz.

```python
from ocr import Rectangle  # Adjust import based on your SDK

for page_index, page in enumerate(pages, start=1):
    # Define the rectangle (x, y, width, height) that encloses the total amount
    total_region = Rectangle(400, 650, 200, 50)

    # Run OCR only on that region
    region_result = ocr_engine.recognize_region(page.image, total_region)
```

> **Neden bir bölge hedefleniyor?**  
> OCR'yi küçük bir alana sınırlamak işleme hızını artırır ve özellikle sayfanın geri kalanı gürültülü olduğunda yanlış pozitifleri azaltır.

---

## Adım 6: Her Sayfa için JSON‑Benzeri Sözlük Oluşturma

Ham metne sahip olmak harika, ancak sonraki sistemler genellikle yapılandırılmış veri bekler. Aşağıda, sayfa numarasını, tam sayfa metnini, çıkarılan toplamı ve güven skorlarıyla tanınan tüm kelimelerin bir listesini içeren temiz bir sözlük oluşturuyoruz.

```python
    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    # Step 7: Output the result for the current page
    print(page_output)
```

Betik çalıştırıldığında, sayfa başına bir sözlük olacak şekilde bir dizi sözlük üretir; örnek olarak şöyle görünebilir:

```json
{
  "page": 1,
  "full_text": "....",
  "total_amount": "1,250,000 VND",
  "words": [
    {"text": "MãĐơnHàng", "conf": 0.98},
    {"text": "KháchHàng", "conf": 0.96},
    ...
  ]
}
```

Çıktıyı daha sonra toplu işleme için bir dosyaya (`> results.jsonl`) kolayca yönlendirebilirsiniz.

---

## Tam Çalışan Örnek

Hepsini bir araya getirerek, kopyalayıp çalıştırabileceğiniz tam betik burada:

```python
import ocr
from ocr import Rectangle

# -------------------------------------------------
# 1️⃣ Initialize the OCR engine and configure it
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.Vietnamese
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]

# -------------------------------------------------
# 2️⃣ Recognize all pages of a multi‑page PDF
# -------------------------------------------------
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)

# -------------------------------------------------
# 3️⃣ Iterate through each page, extract region, and build output
# -------------------------------------------------
for page_index, page in enumerate(pages, start=1):
    total_region = Rectangle(400, 650, 200, 50)          # region of interest
    region_result = ocr_engine.recognize_region(page.image, total_region)

    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    print(page_output)   # Replace with logging or file write as needed
```

### Beklenen Çıktı

Betik, üç sayfalı bir fatura PDF'i üzerinde çalıştırıldığında şu çıktıyı üretebilir:

```
{'page': 1, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.99}, ...]}
{'page': 2, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.98}, ...]}
{'page': 3, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.97}, ...]}
```

Bu çıktıyı `jq` ya da herhangi bir JSON ayrıştırıcıya yönlendirerek yapıyı doğrulayabilirsiniz.

---

## Yaygın Sorular & Özel Durumlar

| Soru | Cevap |
|----------|--------|
| **PDF'im şifre korumalıysa ne olur?** | Çoğu SDK, `recognize_multi_page` çağrısına bir `password` argümanı geçirmenize izin verir. Çağrıya sadece `password="mySecret"` ekleyin. |
| **Taramalarım gri tonlamalı, siyah‑beyaz değil.** | `auto_binarize` seçeneği bunu halleder, ancak görüntüyü `recognize_region`'a vermeden önce `Pillow` ile manuel olarak da dönüştürebilirsiniz. |
| **Toplam tutar bazen farklı bir koordinatta görünüyor.** | Ya dikdörtgeni dinamik olarak (ör. şablon eşleştirme ile) hesaplayın ya da tam sayfa OCR çalıştırıp ardından metni `r'\d{1,3}(,\d{3})* VND'` gibi bir regex ile arayın. |
| **500 sayfalık PDF'lerde performans yavaş.** | Sayfaları toplu işleyin: 50 sayfayı işleyin, sonuçları yazın, ardından bellek boşaltmak için `pages` listesini temizleyin. Ayrıca, taramalarınız zaten düzse `auto_deskew` seçeneğini devre dışı bırakın. |
| **Daha sonra diğer dilleri nasıl ele alırım?** | `recognize_multi_page` çağırmadan önce sadece `ocr_engine.language = ocr.Language.English` (veya desteklenen herhangi bir enum) olarak değiştirin. İş akışının geri kalanı aynı kalır. |

---

## Üretim‑Hazır Dağıtımlar İçin İpuçları

1. Hata yönetimi – OCR çağrılarını `try/except` bloklarıyla sarın; başarısızlıkta sayfa indeksini kaydedin böylece daha sonra yeniden deneyebilirsiniz.  
2. Günlükleme – Esnek ayrıntı seviyesi için `print` yerine Python'un `logging` modülünü kullanın.  
3. Paralellik – OCR kütüphaneniz iş parçacığı‑güvenliyse, sayfaları eşzamanlı işlemek için bir `ThreadPoolExecutor` başlatın.  
4. Yapılandırma dosyası – Dil, sözlük ve dikdörtgen koordinatlarını bir JSON/YAML dosyasında saklayın; bu, betiği projeler arasında yeniden kullanılabilir kılar.  
5. Test – Bilinen PDF'lerle küçük bir test paketi oluşturun ve çıkarılan `total_amount` değerinin beklenenle eşleştiğini doğrulayın.

---

## Sonuç

Şimdi **OCR motorunu başlatma** ve ilgili adımları öğrendiniz.

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanıza ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [PDF Metin Tanıma – Aspose.OCR for Java ile OCR İşlemleri](/ocr/english/java/ocr-operations/)
- [Birden çok dil için Aspose OCR ile metin görüntüsü tanıma](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Görüntüden Metin Çıkarma – Aspose.OCR for .NET ile OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}