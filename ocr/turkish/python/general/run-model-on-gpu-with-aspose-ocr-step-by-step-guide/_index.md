---
category: general
date: 2026-03-26
description: Aspose OCR kullanarak modeli GPU’da çalıştırın. Hugging Face deposunu
  nasıl indireceğinizi, GPU katmanlarını nasıl ayarlayacağınızı, Aspose OCR’yi nasıl
  içe aktaracağınızı ve Qwen2.5 modelini dakikalar içinde nasıl yükleyeceğinizi öğrenin.
draft: false
keywords:
- run model on gpu
- download hugging face repo
- import aspose ocr
- set gpu layers
- load qwen2.5 model
language: tr
og_description: Aspose OCR ile modeli GPU’da çalıştırın. Bu öğreticide, bir Hugging
  Face deposunu nasıl indireceğinizi, GPU katmanlarını nasıl ayarlayacağınızı, Aspose
  OCR’yi nasıl içe aktaracağınızı ve Qwen2.5 modelini nasıl yükleyeceğinizi gösterir.
og_title: Aspose OCR ile GPU’da modeli çalıştırma – Tam Kılavuz
tags:
- Aspose OCR
- GPU acceleration
- Hugging Face
- Python AI
title: Aspose OCR ile GPU’da Model Çalıştırma – Adım Adım Kılavuz
url: /tr/python/general/run-model-on-gpu-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPU’da Aspose OCR ile Model Çalıştırma – Tam Kılavuz

Büyük bir dil modelini hızlandırmak istediğinizde düşük‑seviye CUDA kodlarıyla uğraşmadan **modeli GPU’da çalıştırmak** nasıl mümkün olur, hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici, yüksek seviyeli bir kütüphanenin sadeliğini korurken modeli hızlandırmakta zorlanıyor. İyi haber? Aspose OCR, Hugging Face’den bir modeli doğrudan çekebilen, kuantize edebilen ve ilk birkaç katmanı GPU’ya itebilen kullanımı kolay bir AI motoru sunuyor—hepsi sadece birkaç Python satırıyla.

Bu rehberde tüm süreci adım adım inceleyeceğiz: **Hugging Face deposunu indirme**, **Aspose OCR’yi içe aktarma**, **GPU katmanlarını yapılandırma** ve sonunda **Qwen2.5 modelini yükleme**. Sonunda, grafik kartınızda çalışan hazır bir OCR motorunuz olacak ve her ayarın neden önemli olduğunu anlayacaksınız.

## Gerekenler

- Python 3.9 ve üzeri (kod tip ipuçları ve f‑stringler içeriyor)
- CUDA‑uyumlu bir GPU (isteğe bağlı ama hız için tavsiye edilir)
- Hugging Face’den modeli çekmek için internet erişimi
- `asposeocr` paketi (`pip install asposeocr`)  

Başka bir dış bağımlılık gerekmez—Aspose OCR sizin yerinize ağır işleri halleder.

## Adım 1: Hugging Face deposunu indirin ve Aspose OCR’yi içe aktarın

İlk yapmanız gereken, model dosyalarının yerel olarak erişilebilir olduğundan emin olmaktır. Aspose OCR’nin `AsposeAIModelConfig` nesnesi, Hugging Face’den bir depoyu otomatik olarak çekebilir, bu yüzden manuel olarak bir şey klonlamanıza gerek yoktur.

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
from asposeocr import AsposeAI, AsposeAIModelConfig
```

**Neden önemli:** Paketi içe aktarmak, temel transformer modelini saran `AsposeAI` sınıfına erişmenizi sağlar. `AsposeAIModelConfig` nesnesi, motorun *nereden* modeli alacağını ve *nasıl* işleyeceğini (ör. kuantizasyon, GPU tahsisi) belirttiğiniz yerdir.

> **İpucu:** Kurumsal bir proxy’nin arkasındaysanız, scripti çalıştırmadan önce `HTTPS_PROXY` ortam değişkenini ayarlayın—Aspose OCR standart Python proxy ayarlarını dikkate alır.

## Adım 2: Optimum performans için GPU katmanlarını ayarlayın

Bir modeli GPU’da çalıştırmak basit bir “aç/kapat” anahtarı değildir. Erken transformer katmanlarının kaç tanesinin GPU’da kalacağını, geri kalanının CPU’ya düşeceğini siz belirleyebilirsiniz. Bu hibrit yaklaşım, GPU belleğiniz sınırlı olduğunda faydalıdır.

```python
# Step 2: Define the model configuration
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # automatically pull repo if missing
    hugging_face_repo_id="bartowski/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # int8 reduces memory footprint
    gpu_layers=20                                   # first 20 layers run on GPU
)
```

**Neden 20 katman?** Qwen2.5‑3B modelinin 32 transformer bloğu vardır. İlk 20 katmanı GPU’ya tahsis etmek, 12 GB bir kartta bellek kullanımını kontrol altında tutarken belirgin bir hız artışı sağlar. Donanımınıza göre `gpu_layers` değerini istediğiniz gibi ayarlayabilirsiniz—`0` CPU‑only çalıştırır, `32` ise her şeyi GPU’ya sığdırmaya çalışır (düşük kapasiteli kartlarda OOM hatası verebilir).

## Adım 3: AI motorunu oluşturun ve Qwen2.5 modelini yükleyin

Şimdi motoru örnekleyip az önce oluşturduğumuz yapılandırmayı ona veriyoruz. Açık `initialize` çağrısı isteğe bağlıdır—Aspose OCR ilk kullanımda tembel bir şekilde başlatılır—but önceden çağırmak hazırlık kontrolünü netleştirir.

```python
# Step 3: Create and initialize the AI engine with the configuration
ocr_engine = AsposeAI()
ocr_engine.initialize(model_config)   # explicit call for clarity
```

**Arka planda ne oluyor?**  
1. Aspose OCR, Hugging Face ile iletişime geçer ve GGUF dosyasını (önceden önbelleğe alınmamışsa) indirir.  
2. Dosya, iç runtime’ın anlayabileceği bir formata dönüştürülür.  
3. İlk `gpu_layers` blokları CUDA belleğine taşınır; geri kalan CPU’da kalır.  
4. Motor kendini *başlatılmış* olarak işaretler; bunu `is_initialized()` ile sorgulayabilirsiniz.

## Adım 4: Modelin GPU’da çalışmaya hazır olduğunu doğrulayın

Hızlı bir tutarlılık kontrolü, ileride karşılaşabileceğiniz gizemli çalışma zamanı hatalarını önler. `is_initialized()` metodu bir Boolean döndürür ve indirme, dönüşüm ve GPU tahsisinin başarılı olduğunu onaylamanızı sağlar.

```python
# Step 4: Confirm that the engine is ready
print("AI ready:", ocr_engine.is_initialized())
```

Her şey sorunsuz giderse şu çıktıyı görmelisiniz:

```
AI ready: True
```

Eğer `False` alırsanız, CUDA sürücülerinizin güncel olduğundan ve GPU’nuzun istediğiniz 20 katman için yeterli boş belleğe sahip olduğundan emin olun.

## Opsiyonel: GPU’yu görmek için hızlı bir OCR çıkarımı çalıştırın

Kılavuzun odak noktası modeli yüklemek olsa da, çoğu okuyucu yakında gerçek OCR çalıştırmak isteyecektir. İşte yerel bir görüntüyü (`sample.png`) işleyen ve algılanan metni ekrana yazdıran minimal bir örnek.

```python
# Optional: Perform a single OCR inference
image_path = "sample.png"
result = ocr_engine.recognize_image(image_path)

print("Detected text:")
print(result.text)
```

**Neden şimdi çalıştırmalı?** Çünkü ilk çıkarım genellikle CUDA kernel’lerinin JIT derlemesini tetikler. Çağrıyı `time.perf_counter()` ile zamanlarsanız, ikinci çalışmanın çok daha hızlı olduğunu fark edeceksiniz—bu, modelin gerçekten GPU’da çalıştığının net bir göstergesidir.

## Yaygın Tuzaklar & Çözüm Önerileri

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|------|
| `RuntimeError: CUDA out of memory` | `gpu_layers` kartınız için çok yüksek ayarlanmış | `gpu_layers` değerini azaltın (ör. 12) veya `int8` kuantizasyonuna geçin (zaten yapılmış). |
| `OSError: Unable to download repository` | İnternet yok veya proxy engelliyor | `HTTPS_PROXY`/`HTTP_PROXY` ortam değişkenlerini ayarlayın ya da GGUF dosyasını manuel indirin ve `hugging_face_repo_id`’yi yerel bir yola yönlendirin. |
| `AttributeError: 'AsposeAI' object has no attribute 'recognize_image'` | `asposeocr` sürümünüz eski | `pip install --upgrade asposeocr` ile yükseltin. |
| `False` from `is_initialized()` | CUDA sürücü uyumsuzluğu | `nvidia-smi` komutuyla sürücü sürümünün CUDA toolkit’inizle uyumlu olduğunu doğrulayın. |

## Görsel Özet

![GPU’da model çalıştırma diyagramı](run-model-on-gpu.png "Model indirme, GPU katman tahsisi ve çıkarım akışını gösteren diyagram")

*Alt metin:* *GPU’da model çalıştırma diyagramı, bir Hugging Face deposunun indirilmesini, GPU katmanlarının ayarlanmasını ve Aspose OCR aracılığıyla Qwen2.5 modelinin yürütülmesini gösterir.*

## Özet – Neler Başardık

- **Aspose OCR** ve AI yardımcı sınıflarını içe aktardık.  
- `allow_auto_download` sayesinde **Hugging Face deposunu** otomatik olarak indirdik.  
- **GPU katmanlarını** (`gpu_layers=20`) ayarlayarak en yoğun hesaplamaları grafik kartına taşıdık.  
- **Qwen2.5‑3B‑Instruct** modelini int8 kuantizasyonu ile yükleyerek bellek kullanımını büyük ölçüde azalttık.  
- **Motorun hazır olduğunu** `is_initialized()` `True` döndürdüğünde doğruladık.  

Tüm bunlar 30 satırdan az Python koduyla, özel CUDA kernel’lerine ihtiyaç duymadan gerçekleştirildi.

## Sonraki Adımlar & İlgili Konular

1. **Farklı kuantizasyonları** (`float16`, `bfloat16`) deneyerek hız ve doğruluk arasındaki dengeyi keşfedin.  
2. **Daha büyük modellere** (ör. Qwen2.5‑7B) geçiş yapın; `gpu_layers` ayarını değiştirin ve yeterli VRAM’e sahip olduğunuzdan emin olun.  
3. **Batch OCR işleme**: `ocr_engine.recognize_images()` ile bir dizi görüntü yolunu işleyerek verimliliği artırın.  
4. **FastAPI ile bütünleştirme**: Gelen dosyalar üzerinde OCR çalıştıran bir REST uç noktası oluşturun—mikroservisler için ideal.  

Daha ileri GPU ayarlamalarıyla ilgileniyorsanız, resmi Aspose OCR performans kılavuzuna veya `CUDA_VISIBLE_DEVICES` gibi ortam değişkenlerini açıklayan CUDA Toolkit belgelerine göz atın.

---

*Kodlamanız keyifli olsun! Bu kılavuz modelinizi GPU’da çalıştırmanıza yardımcı olduysa, yorumlarda bana bildirin ya da kendi ayarlamalarınızı paylaşın. Ne kadar çok birlikte deneme yaparsak, topluluk o kadar hızlı öğrenir.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}