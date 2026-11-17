---
category: general
date: 2026-04-29
description: Python kullanarak görüntüde OCR gerçekleştir, HuggingFace modelini otomatik
  indir ve OCR metnini temizlerken GPU belleğini verimli bir şekilde serbest bırak.
draft: false
keywords:
- perform OCR on image
- download HuggingFace model python
- release GPU memory python
- clean OCR text python
language: tr
og_description: Python'da görüntü üzerinde OCR nasıl yapılır, HuggingFace modelini
  otomatik olarak nasıl indirilir, metni nasıl temizlenir ve GPU belleği nasıl boşaltılır
  öğrenin.
og_title: Python ile Görüntüde OCR Yapma – Adım Adım Rehber
tags:
- OCR
- Python
- Aspose
- HuggingFace
title: Python ile Görüntüde OCR Yapma – Tam Kılavuz
url: /tr/python/general/perform-ocr-on-image-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python ile Görüntü Üzerinde OCR Yapma – Tam Kılavuz

Görüntü dosyalarında **görüntü üzerinde OCR gerçekleştirme** yapmanız gerektiğinde model indirme veya GPU bellek temizleme aşamasında takıldınız mı? Tek başınıza değilsiniz—birçok geliştirici, optik karakter tanıma ile büyük dil modellerini birleştirmeye ilk kez çalıştıklarında bu duvara çarpıyor.

Bu öğreticide, **downloads a HuggingFace model in Python** yapan, Aspose OCR çalıştıran, ham çıktıyı temizleyen ve sonunda **releases GPU memory Python** yapan tek bir uçtan uca çözüm üzerinden geçeceğiz. Sonunda taranmış bir PNG'yi düzenli, aranabilir metne dönüştüren çalıştırmaya hazır bir betiğe sahip olacaksınız.

> **Ne elde edeceksiniz:** tam, çalıştırılabilir kod örneği, her adımın neden önemli olduğuna dair açıklamalar, yaygın hatalardan kaçınma ipuçları ve kendi projeleriniz için pipeline'ı nasıl ayarlayabileceğinize dair bir bakış.

## Gereksinimler

- Python 3.9 ve üzeri (örnek 3.11 üzerinde test edilmiştir)  
- `aspose-ocr` paketi (`pip install aspose-ocr` ile kurulur)  
- **download HuggingFace model python** adımı için bir internet bağlantısı  
- Hız artışı istiyorsanız CUDA uyumlu bir GPU (isteğe bağlı ancak önerilir)  

Ek sistem düzeyinde bağımlılıklar gerekmez; Aspose OCR motoru ihtiyacınız olan her şeyi içinde barındırır.

![perform OCR on image example](image.png "Example of performing OCR on image with Aspose OCR and an LLM post‑processor")

*Image alt text: “görüntü üzerinde OCR – AI temizlemeden önce ve sonra Aspose OCR çıktısı”*

## Görüntü Üzerinde OCR – Adım Adım Genel Bakış

Aşağıda iş akışını mantıksal bölümlere ayırıyoruz. Her bölümün kendi başlığı var, böylece AI asistanları ilgilendiğiniz bölüme hızlıca atlayabilir ve arama motorları ilgili anahtar kelimeleri indeksleyebilir.

### 1. Python’da HuggingFace Modelini İndir

İlk yapmamız gereken, ham OCR çıktısı için bir post‑işlemci görevi görecek bir dil modeli almaktır. Aspose OCR, HuggingFace hub'ından otomatik olarak model çekebilen `AsposeAI` adlı bir yardımcı sınıfla birlikte gelir.

```python
import aspose.ocr as aocr
from aspose.ocr import AsposeAI, AsposeAIModelConfig, OcrEngine

# Configure the model – it will auto‑download the first time you run it
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # <-- enables auto‑download
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # smaller footprint on GPU
    gpu_layers=20,                                  # how many layers stay on GPU
    directory_model_path=r"YOUR_DIRECTORY"         # where the model files live
)
```

**Neden Önemli:**  
- **download HuggingFace model python** – zip dosyalarını veya token kimlik doğrulamasını manuel olarak yönetmek zorunda kalmazsınız.  
- `int8` kuantizasyonu kullanmak, modeli orijinal boyutunun yaklaşık dörtte birine küçültür; bu, daha sonra **release GPU memory python** gerektiğinde kritik öneme sahiptir.

> **İpucu:** `directory_model_path`'i daha hızlı yükleme süreleri için bir SSD'de tutun.  

### 2. AI Yardımcısını Başlat ve Yazım Denetimini Etkinleştir

Şimdi bir `AsposeAI` örneği oluşturup bir yazım‑düzeltici post‑işlemci ekliyoruz. İşte **clean OCR text python** sihrinin başladığı yer.

```python
# Initialise the AI helper
ai_helper = AsposeAI()
ai_helper.set_post_processor(
    processor="spell_corrector",
    custom_settings={"max_edits": 2}   # allows up to two character edits per word
)
```

**Açıklama:**  
Yazım‑düzeltici, OCR motorundan gelen her token'ı inceler ve `max_edits` ile sınırlı düzenlemeler önerir. Bu küçük ayar, ağır bir dil modeli olmadan “rec0gn1tion”ı “recognition”a dönüştürebilir.

### 3. AI Yardımcısını OCR Motoruna Bağla

Aspose, sürüm 23.4'te AI motorunu doğrudan OCR pipeline'ına bağlamanızı sağlayan yeni bir yöntem tanıttı.

```python
# Initialise the OCR engine and attach the AI helper
ocr_engine = OcrEngine()
ocr_engine.set_ai_engine(ai_helper)   # new in v23.4
```

**Neden Bunu Yapıyoruz:**  
AI yardımcısını erken bağlayarak, OCR motoru modeli isteğe bağlı olarak anlık iyileştirmeler için (ör. düzen algılama) kullanabilir. Ayrıca kodu düzenli tutar—sonradan ayrı post‑işlem döngülerine ihtiyaç kalmaz.

### 4. Taranmış Görüntüde OCR Yap

İşte **görüntü üzerinde OCR gerçekleştirme** dosyalarında gerçek adım. `YOUR_DIRECTORY/input.png` ifadesini kendi taramanızın yolu ile değiştirin.

```python
image_path = r"YOUR_DIRECTORY/input.png"
ocr_result = ocr_engine.recognize(image_path)

print("Raw OCR text:")
print(ocr_result.text)
```

Tipik ham çıktı, garip yerlerde satır sonları, hatalı tanınan karakterler veya gereksiz semboller içerebilir. Bu yüzden bir sonraki adıma ihtiyacımız var.

**Beklenen ham çıktı (örnek):**

```
Th1s 1s 4n ex4mpl3 0f r4w OCR t3xt.
It c0ntains numb3rs 123 and s0me m1stakes.
```

### 5. AI Post‑İşlemcisi ile Python’da OCR Metnini Temizle

Şimdi AI'ye karışıklığı temizletiyoruz. Bu, **clean OCR text python** sürecinin kalbidir.

```python
cleaned_result = ocr_engine.run_postprocessor(ocr_result)

print("\nAI‑enhanced text:")
print(cleaned_result.text)
```

**Görürsünüz Sonuç:**

```
This is an example of raw OCR text.
It contains numbers 123 and some mistakes.
```

Yazım‑düzelticinin “Th1s” → “This” hatasını düzelttiğine ve gereksiz “4n”i sildiğine dikkat edin. Model ayrıca boşlukları normalleştirir; bu, metni sonraki NLP pipeline'larına beslerken sıkça sorun yaratır.

### 6. Python’da GPU Belleğini Serbest Bırak – Temizleme Adımları

İşiniz bittiğinde, özellikle uzun süreli bir hizmette birden fazla OCR işi çalıştırıyorsanız GPU kaynaklarını serbest bırakmak iyi bir uygulamadır.

```python
# Release resources – crucial for GPU memory
ai_helper.free_resources()
ocr_engine.dispose()
```

**Arka planda ne olur:**  
`free_resources()` modeli GPU'dan kaldırır, belleği CUDA sürücüsüne geri verir. `dispose()` OCR motorunun iç tamponlarını kapatır. Bu çağrıları atlamak, sadece birkaç görüntüden sonra bellek yetersizliği hatalarına yol açabilir.

> **Unutmayın:** Bir döngüde toplu işlem yapmayı planlıyorsanız, her batch'ten sonra temizleme işlemini çağırın veya `ai_helper`'ı sonuna kadar serbest bırakmadan yeniden kullanın.

## Bonus: Farklı Senaryolar İçin Pipeline’ı Ayarlama

### Model Kuantizasyonunu Ayarlama

Güçlü bir GPU'nuz (ör. RTX 4090) varsa ve daha yüksek doğruluk istiyorsanız, `hugging_face_quantization` değerini `"fp16"` olarak değiştirin ve `gpu_layers`'ı `30`'a yükseltin. Bu daha fazla bellek tüketir, bu yüzden her batch'ten sonra **release GPU memory python** daha agresif bir şekilde yapmanız gerekir.

### Özel Bir Yazım‑Denetleyici Kullanma

Yerleşik `spell_corrector`'ı, alan‑spesifik düzeltmeler yapan (ör. tıbbi terminoloji) özel bir post‑işlemci ile değiştirebilirsiniz. Gerekli arayüzü uygulayın ve adını `set_post_processor`'a iletin.

### Birden Çok Görüntüyü Toplu İşleme

OCR adımlarını bir `for` döngüsü içinde sarın, `cleaned_result.text`'i bir listeye toplayın ve yeterli GPU RAM'ınız varsa döngüden sonra sadece `ai_helper.free_resources()`'ı çağırın. Bu, modeli tekrar tekrar yüklemenin getirdiği yükü azaltır.

## Sonuç

Python’da **görüntü üzerinde OCR gerçekleştirme** dosyalarını nasıl **download a HuggingFace model** otomatik olarak **clean OCR text** yapıp, işiniz bittiğinde güvenli bir şekilde **release GPU memory** serbest bırakacağınızı gösterdik. Tam script kopyala‑yapıştır için hazır ve açıklamalar, onu daha büyük projelere uyarlama konusunda size güven verir.

Sonraki adımlar? Qwen 2.5 modelini daha büyük bir LLaMA varyantıyla değiştirmeyi deneyin, farklı post‑işlemcilerle deney yapın veya temizlenmiş çıktıyı aranabilir bir Elasticsearch indeksine entegre edin. Olanaklar sonsuz ve artık üzerine inşa edebileceğiniz sağlam bir temele sahipsiniz.

Kodlamaktan keyif alın, ve OCR pipeline'larınız her zaman temiz ve bellek dostu olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}