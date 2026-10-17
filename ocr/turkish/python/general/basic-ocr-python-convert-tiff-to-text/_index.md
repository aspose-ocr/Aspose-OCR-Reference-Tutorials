---
category: general
date: 2026-03-18
description: Temel OCR Python öğreticisi, TIFF'i metne dönüştürmeyi, görüntü OCR'yi
  yüklemeyi, GPU katmanlarını ayarlamayı ve Aspose AI ile önde gelen sıfırları düzeltmeyi
  gösterir.
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: tr
og_description: Temel OCR Python öğreticisi, TIFF dosyalarını temiz metne dönüştürme,
  görüntüleri yükleme, GPU katmanlarını ayarlama ve baştaki sıfırları düzeltme konularında
  size rehberlik eder.
og_title: temel OCR Python – TIFF'i metne dönüştür
tags:
- OCR
- Python
- AI
- Aspose
title: Temel OCR Python – TIFF'i Metne Dönüştür
url: /tr/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – TIFF'i Metne Dönüştürme ve AI Son İşleme

Tarayıcı belgelerinizde **basic ocr python** yapmanın bir yolunu mu arıyorsunuz? Bu rehberde Aspose OCR ve bir AI son işlemci kullanarak bir TIFF dosyasını temiz, aranabilir metne dönüştürmeyi adım adım göstereceğiz.  

Eğer ham çıktının yazım hataları ya da garip sembollerle dolu olduğu için **convert TIFF to text** yaparken zorlandığınız olduysa, yalnız değilsiniz. Ayrıca **load image OCR** nasıl yapılır, motoru **set GPU layers** ile nasıl ayarlarsınız ve fatura numaralarında sıkça görülen **fix leading zeroes** nasıl düzeltilir, göstereceğiz.

## Öğrenecekleriniz

- Aspose OCR motorunu basılı belgeler için nasıl başlatacağınızı.  
- Bir TIFF dosyasından **load image OCR** yapıp ham metni almanın kesin adımları.  
- Bir AI modelini yapılandırma, otomatik olarak indirme ve daha hızlı çıkarım için **setting GPU layers** ayarlama.  
- Yerleşik imla denetimini ekleme ve **fixes leading zeroes** yapan özel bir işlev ekleme.  
- OCR sonucunu temizleme ve kaynakları düzgün bir şekilde serbest bırakma.  

Bu öğreticinin sonunda, herhangi bir TIFF dosyasını cilalı, aranabilir metne dönüştüren tek bir yeniden kullanılabilir Python betiğine sahip olacaksınız—manuel kopyala‑yapıştırma gerekmez.  

### Önkoşullar

- Makinenizde yüklü Python 3.8+.  
- `aspose-ocr` paketi (`pip install aspose-ocr`).  
- İsteğe bağlı: **set GPU layers** yapmak istiyorsanız en az 4 GB VRAM'li bir GPU; aksi takdirde kod otomatik olarak CPU'ya geçer.  

---

## basic ocr python – görüntüyü yükle ve metni tanı

İlk yapmamız gereken **load image OCR** işlemi, böylece motor pikselleri okuyabilir. Aspose'un `OcrEngine`i birçok formatı destekler, ancak burada taranmış faturalar için en yaygın olan TIFF'e odaklanıyoruz.

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **Pro tip:** Çok sayfalı TIFF'lerle çalışıyorsanız, Aspose her sayfayı otomatik olarak sırayla işler, bu yüzden ekstra döngülere ihtiyacınız yok.

Görüntü yüklendiğine göre, temel bir tanıma geçişi çalıştıralım.

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

Şuna benzer bir şey göreceksiniz:

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Harflerin önündeki *sıfırları* fark ettiniz mi? Bu, daha sonra temizleyeceğimiz klasik bir OCR artefaktıdır.

![basic ocr python iş akışı](/images/ocr-workflow.png "basic ocr python iş akışı diyagramı")

---

## Adım 2: TIFF'i metne dönüştür – AI son işlemcisini hazırlama

Ham OCR faydalıdır, ancak çoğu üretim hattı cilalı bir sürüm gerektirir. Aspose, Hugging Face'ten bir model indirebilen, GPU'da çalıştırabilen ve otomatik olarak imla denetimi uygulayan bir `AsposeAI` sarmalayıcısı sunar.  

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# Configure the AI model – we’ll download Qwen2.5‑3B‑Instruct automatically
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    directory_model_path="YOUR_DIRECTORY/ocr_ai_models",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25          # <-- this is where we **set GPU layers**
)

ocr_ai = AsposeAI(ai_config)
```

### Neden `set GPU layers` önemli

`gpu_layers` parametresi, temel GGUF modeline GPU'da kaç transformer katmanı tutulacağını söyler. Daha fazla katman = daha hızlı çıkarım ama daha yüksek VRAM kullanımı. Daha mütevazı bir dizüstü bilgisayar kullanıyorsanız, değeri `10`'a düşürün ya da tamamen kaldırarak CPU'da kalın.

---

## Adım 3: İmla denetimini uygula ve **fix leading zeroes**

Aspose AI, çoğu İngilizce yazım hatasını yakalayan yerleşik bir imla denetleyicisiyle birlikte gelir. Ancak, fatura kodları için baştaki `0`'ı `O`'ya dönüştürmek gibi alan‑özel düzeltmeler, özel bir son işlemci gerektirir.

```python
# Enable the built‑in spell‑check
ocr_ai.set_post_processor("spellcheck")

# Custom function to replace a leading zero before three capital letters
def invoice_fix(txt: str) -> str:
    import re
    # Example: "0ABC" -> "OABC"
    return re.sub(r"\b0([A-Z]{3})\b", r"O\1", txt)

# Register the custom fix – it runs after spellcheck
ocr_ai.set_post_processor(invoice_fix)
```

> **Neden işe yarıyor:** Düzenli ifade bir kelime sınırı (`\b`), bir sıfır ve ardından tam üç büyük harf arar. Daha sonra sıfırı “O” harfiyle değiştirir. Deseni diğer tuhaflıklar için genişletebilirsiniz (ör. `0[0-9]{2}` yanlış okunan sayılar için).

---

## Adım 4: OCR sonucunu AI son işlemcisiyle temizle

Şimdi her şeyi birleştiriyoruz: **basic ocr python**'dan gelen ham dize, imla denetimi ve sıfır düzeltmemiz. `run_postprocessor` yöntemi, sonraki sistemler için hazır temizlenmiş bir sürüm döndürür.

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

Post‑işlemciden sonraki tipik çıktı:

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Başlangıçtaki sıfırın `O`'ya dönüştüğünü ve yaygın yazım hatalarının düzeltildiğini görebilirsiniz. Metin artık bir arama motorunda indeksleme veya veri‑çıkarma hattına besleme için uygun.

---

## Adım 5: AI kaynaklarını serbest bırak – GPU'nuzu mutlu tutun

Uzun süren bir hizmette birden fazla OCR işi çalıştırıyorsanız, işiniz bittiğinde modelin GPU belleğini serbest bırakmak iyi bir uygulamadır.

```python
ocr_ai.free_resources()
```

Bu adımı atlamak, özellikle **set GPU layers** değerini yüksek ayarladığınızda, sonraki çağrılarda “bellek yetersiz” hatalarına yol açabilir.

---

## İsteğe Bağlı Varyasyonlar ve Kenar Durumları

| Durum | Ne değiştirilmeli |
|-----------|----------------|
| **El yazısı belgeler** | `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` kullanın, `PRINTED` yerine. |
| **GPU yok** | `gpu_layers=0` ayarlayın veya argümanı atlayın; model CPU'da çalışır (daha yavaş ama güvenli). |
| **Farklı dil** | Hugging Face repo kimliğini dil‑spesifik bir modele değiştirin, ör. `microsoft/Florence-2-base`. |
| **Toplu işleme** | Adımları `for file in glob("*.tif"):` döngüsü içinde sarın ve sonuçları bir liste ya da CSV'de biriktirin. |
| **Daha karmaşık sıfır desenleri** | `invoice_fix`i ek regex'lerle genişletin, ör. `r"\b0+([A-Z]{2,})\b"` birden fazla baştaki sıfır için. |

---

## Sonuç

Şimdi **basic ocr python** boru hattını tamamladık; TIFF'i yükler, ham metni çıkarır ve ardından performans için **setting GPU layers** kullanarak bir AI modeliyle temizler. Özel son işlemci, **fix leading zeroes** nasıl yapılır gösterir; bu, genellikle gözden kaçan ancak sonraki analizleri bozabilen küçük bir detaydır.

Denemekten çekinmeyin: farklı bir kuantizasyon deneyin (`float16` daha yüksek doğruluk için), imla denetimini alan‑spesifik bir sözlükle değiştirin veya birden fazla özel düzeltmeyi zincirleyin. Desen aynı kalır—yükle, tanı, AI'yi yapılandır, son‑işlem yap ve temizle.

**İleri adımlar** şunları içerebilir:

- Temizlenmiş çıktıyı bir veritabanı veya Elasticsearch indeksine entegre etmek.  
- Aynı yaklaşımı çok‑dilli PDF'ler için **convert TIFF to text** yapmak.  
- Flask veya FastAPI ile bir UI ekleyerek teknik olmayan kullanıcıların dosya yükleyip anında temiz metin almasını sağlamak.  

Kodlamaktan keyif alın, ve OCR sonuçlarınız her zaman net ve sıfır‑sız olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}