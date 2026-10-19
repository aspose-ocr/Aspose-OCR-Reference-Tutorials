---
category: general
date: 2026-06-22
description: Modeli CPU’da çalıştırın ve Aspose AI’da GPU katmanlarını yapılandırarak
  GPU bellek kullanımını azaltmayı öğrenin. Kod parçacıklarıyla adım adım rehber.
draft: false
keywords:
- run model on cpu
- reduce gpu memory usage
- limit gpu layers
- configure gpu layers
language: tr
og_description: Modeli CPU’da çalıştırın ve GPU katmanlarını yapılandırarak GPU bellek
  tüketimini azaltın. Aspose AI model kurulumu için tam öğretici.
og_title: Modeli CPU'da Çalıştır – GPU Bellek Kullanımını Azalt
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Run model on CPU and learn to reduce GPU memory usage by configuring
    GPU layers in Aspose AI. Step-by-step guide with code snippets.
  headline: Run Model on CPU – Reduce GPU Memory Usage with Aspose AI
  type: TechArticle
- description: Run model on CPU and learn to reduce GPU memory usage by configuring
    GPU layers in Aspose AI. Step-by-step guide with code snippets.
  name: Run Model on CPU – Reduce GPU Memory Usage with Aspose AI
  steps:
  - name: Attach any required post‑processors.
    text: Attach any required post‑processors.
  - name: Choose a configuration (`gpu_layers=0` for pure CPU, or a modest number
      for mixed mode).
    text: Choose a configuration (`gpu_layers=0` for pure CPU, or a modest number
      for mixed mode).
  - name: Initialize the model with that configuration.
    text: Initialize the model with that configuration.
  - name: Verify placement and run a test inference.
    text: Verify placement and run a test inference.
  type: HowTo
tags:
- AsposeAI
- CPU inference
- GPU optimization
title: Modeli CPU’da Çalıştır – Aspose AI ile GPU Bellek Kullanımını Azaltın
url: /tr/python/general/run-model-on-cpu-reduce-gpu-memory-usage-with-aspose-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Modeli CPU'da Çalıştır – Aspose AI ile GPU Bellek Kullanımını Azaltma

Sunucunuzda GPU yokken **modeli CPU'da çalıştırmanın** nasıl olduğunu hiç merak ettiniz mi? Ya da mütevazı bir GPU'da bellek yetersizliği hatalarıyla mücadele ediyor ve **GPU bellek kullanımını** çok fazla hız kaybı yaşamadan azaltmanız mı gerekiyor? Bu rehberde tam olarak bunu adım adım göstereceğiz: bir post‑işlemci eklemek, Aspose AI'yi CPU'da başlatmak ve bellek ayak izini küçültmek için GPU katman sayısını ince ayar yapmak.

Her şeyi ilk kod satırından modelin gerçekten istediğiniz yapılandırmayı kullandığını doğrulamaya kadar ele alacağız. Sonunda **modeli CPU'da çalıştır**, **GPU katmanlarını sınırlayın** ve **GPU katmanlarını yapılandırın** herhangi bir iş yükü için—sihir yok, sadece sade Python.

## Gereksinimler

- Python 3.8+ yüklü (kod tip ipuçları kullanıyor ancak daha eski sürümlerde de çalışır)
- `asposeai` paketi (`pip install asposeai` ile kurun)
- Sinir ağı çıkarım (inference) kavramlarına temel aşinalık (PhD'ye ihtiyacınız yok, sadece merak)
- İsteğe bağlı: CPU ve GPU çalıştırmalarının karşılaştırmasını test etmek için GPU destekli bir makine

![Diagram illustrating how to run model on cpu instead of gpu](run-model-on-cpu-diagram.png)

## Adım 1: Yazım Denetimi Post‑İşlemcisini Ekleyin (Özel Ayar Gerekmez)

CPU veya GPU'yu düşünmeden önce, Aspose AI'nin sunduğu yazım denetimi post‑işlemcisini bağlayalım. Post‑işlemcileri erken eklemek, her çıkarım çağrısının bir parçası olmalarını sağlamak için iyi bir alışkanlıktır.

```python
from asposeai import AI, spell_check_processor

# Create the AI client
ai = AI()

# Attach the built‑in spell‑check processor; no custom settings required
ai.set_post_processor(spell_check_processor, custom_settings={})
```

*Neden önemli?*: Post‑işlemciler model ham token'ları ürettikten **sonra** çalışır. Şimdi bağlayarak, daha sonra üreteceğiniz metnin—CPU ya da GPU'da olsun—otomatik olarak temizlenmesini garantilersiniz. Bu, sonraki hataları önleyen küçük bir adımdır.

## Adım 2: Modeli CPU'da Çalıştır – Aspose AI'yi GPU'suz Başlat

Şimdi rehberin özüne geliyoruz: Aspose AI'ye **modeli CPU'da çalıştır** demek. SDK, `AsposeAIModelConfig`'i sunar; burada `gpu_layers` parametresi kaç katmanın GPU'da kalacağını kontrol eder. Bunu `0` olarak ayarlamak, tüm ağı CPU'ya zorlar.

```python
from asposeai import AsposeAIModelConfig

# Initialize the model configuration to use zero GPU layers (i.e., CPU only)
cpu_config = AsposeAIModelConfig(gpu_layers=0)

# Apply the configuration; this will load the model onto the CPU
ai.initialize(cpu_config)

print("✅ Model initialized on CPU – ready for inference.")
```

*Arka planda ne oluyor?*: `gpu_layers=0` olduğunda, çalışma zamanı tüm tensörleri ana bellek içinde tahsis eder. Bu, CUDA sürücülerine ihtiyaç duyulmasını ortadan kaldırır ve betiğin neredeyse her sunucuda çalışmasını sağlar. Değiş tokuş, daha yavaş işleme hızıdır; ancak toplu işler veya düşük gecikmeli prototipler için sadelik genellikle ham hızı aşar.

## Adım 3: GPU Katmanlarını Sınırlayarak GPU Bellek Kullanımını Azaltma

Eğer bir GPU'nuz varsa ancak bellek sıkıntısı yaşıyorsa, her şeyi CPU'ya taşımak yerine **GPU katmanlarını sınırlayabilirsiniz**. Sadece birkaç erken katmanı GPU'da tutarak, hâlâ donanım hızlandırmasından faydalanırken bellek tüketimini büyük ölçüde azaltırsınız.

```python
# Example: keep only the first 10 layers on the GPU; the rest run on CPU
limited_gpu_config = AsposeAIModelConfig(gpu_layers=10)

ai.initialize(limited_gpu_config)

print("✅ Model initialized with 10 GPU layers – memory usage trimmed.")
```

*GPU katmanlarını sınırlamanın nedeni:* Modern transformer modelleri belleğin çoğunu katman başına tahsis eder. GPU'dan birkaç katmanı çıkarmak bile yüzlerce megabayt boşaltabilir. Bu yaklaşım, en yoğun hesaplamalar için hâlâ bir hız artışı istediğiniz “bellek‑kısıtlı işler” için mükemmeldir.

## Adım 4: Esnek Bellek Yönetimi İçin GPU Katmanlarını Yapılandırma

Bazen daha ayrıntılı bir yaklaşım gerekir—belki belirli iş boyutuna göre **GPU katmanlarını yapılandırmak** istersiniz. SDK, modelin toplam katman sayısını okumanıza ve çalışma zamanında güvenli bir GPU katman sayısı hesaplamanıza izin verir.

```python
# Determine total number of layers (this is model‑specific; assume 36 for illustration)
total_layers = ai.model_info.total_layers  

# Choose a safe percentage, e.g., 25% of layers on GPU
gpu_layer_fraction = 0.25
desired_gpu_layers = int(total_layers * gpu_layer_fraction)

# Build the config dynamically
dynamic_config = AsposeAIModelConfig(gpu_layers=desired_gpu_layers)

ai.initialize(dynamic_config)

print(f"✅ Configured {desired_gpu_layers}/{total_layers} layers on GPU.")
```

*Pro ipucu:* Paylaşımlı bir sunucuda çalışırken önce kullanılabilir GPU belleğini sorgulayın (`torch.cuda.get_device_properties(0).total_memory`) ve `desired_gpu_layers` değerini buna göre ayarlayın. Bu ek adım, GPU'yu aşırı tahsis etmenizi engeller; aksi takdirde OOM çöküşlerine yol açar.

## Adım 5: Yapılandırmayı Doğrulama ve Çıkarımı Test Etme

Yapılandırmayı kurduktan sonra, her katmanın nerede bulunduğunu iki kez kontrol etmek akıllıca olur. Aspose AI, katmanların cihazlara eşlemesini döndüren tanılayıcı bir yöntem sunar.

```python
# Retrieve the device placement map
placement = ai.get_layer_placement()

cpu_layers = [l for l, dev in placement.items() if dev == "cpu"]
gpu_layers = [l for l, dev in placement.items() if dev == "gpu"]

print(f"Layers on CPU: {len(cpu_layers)}")
print(f"Layers on GPU: {len(gpu_layers)}")
```

Memnun kaldığınızda, her şeyi harekete geçirmek için hızlı bir çıkarım çalıştırın:

```python
input_text = "The quick brown fox jumps over the lazy dog."
output = ai.process(input_text)

print("Model output:", output)
```

Eğer betik beklenen metni yazdırır ve yerleşim raporu yapılandırmanızla eşleşirse, senaryonuz için **modeli CPU'da çalıştır**, **GPU bellek kullanımını azalt** ve **GPU katmanlarını yapılandır** işlemlerini başarıyla tamamlamış olursunuz.

## Yaygın Tuzaklar ve Nasıl Kaçınılır

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|------|
| `CUDA out of memory` hatası | Çok fazla GPU katmanı | `gpu_layers` değerini azaltın veya `gpu_layers=0`'a geçin |
| `ai.process`'ten çıktı yok | Model başlatılmadı | `ai.initialize`'ın post‑işlemciler eklendikten **sonra** çağrıldığından emin olun |
| GPU'da yavaş çıkarım | Tüm katmanlar hâlâ CPU'da | `gpu_layers` > 0 olduğundan ve cihaz haritasının GPU kullanımını gösterdiğinden emin olun |
| Beklenmeyen yazım hataları | Post‑işlemci eklenmemiş | `initialize`'dan önce `set_post_processor`'ı çağırın |

## Bonus: Çalışma Anında CPU ve GPU Arasında Geçiş

SDK, `initialize`'ı her çağırdığınızda modeli yeniden başlattığı için, betiği yeniden başlatmadan CPU ve GPU arasında geçiş yapabilirsiniz.

```python
def switch_to_cpu():
    ai.initialize(AsposeAIModelConfig(gpu_layers=0))
    print("🔄 Switched to CPU mode.")

def switch_to_gpu(layers=12):
    ai.initialize(AsposeAIModelConfig(gpu_layers=layers))
    print(f"🔄 Switched to GPU mode with {layers} layers.")
```

Düşük bellekli bir çalıştırma gerektiğinde `switch_to_cpu()`'u, hız artışı istediğinizde ise `switch_to_gpu(12)`'yi çağırın.

## Sonuç

Aspose AI ile **modeli CPU'da çalıştır**, **GPU bellek kullanımını azalt**, **GPU katmanlarını sınırlı tut** ve **GPU katmanlarını yapılandır** nasıl yapılır konusunda eksiksiz, uygulamalı bir örnek üzerinden ilerledik. Adımlar basittir:

1. Gerekli tüm post‑işlemcileri ekleyin.  
2. Bir yapılandırma seçin (`gpu_layers=0` saf CPU için, ya da karışık mod için makul bir sayı).  
3. Modeli bu yapılandırma ile başlatın.  
4. Yerleşimi doğrulayın ve bir test çıkarımı çalıştırın.  

Bu tekniklerle, çıkarım hatlarınızı hafif tutabilir, maliyetli OOM çöküşlerinden kaçınabilir ve mevcut olduğunda mütevazı bir GPU'dan performans elde edebilirsiniz. Sonraki adımda toplu işleme stratejileri, kuantizasyon veya modelin bazı bölümlerini CPU'ya aktarırken dikkat başlıklarını GPU'da tutmayı keşfedebilirsiniz—bu konuların her biri, yeni öğrendiğiniz **GPU katmanlarını yapılandır** temeline doğrudan dayanır.

Belirli bir model mimarisi hakkında sorularınız mı var ya da katman sayısını ayarlamak için yardıma mı ihtiyacınız var

## Sonra Ne Öğrenmelisiniz?

Bu rehberde gösterilen tekniklere dayanan, yakından ilgili konuları kapsayan aşağıdaki öğreticiler bulunmaktadır. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Aspose OCR Tutorial – Optical Character Recognition](/ocr/english/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}