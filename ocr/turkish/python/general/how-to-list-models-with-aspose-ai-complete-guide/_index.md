---
category: general
date: 2026-07-05
description: Aspose AI ile modelleri nasıl listeleyeceğiniz, otomatik indirmeyi nasıl
  etkinleştireceğiniz ve Python’da Hugging Face modelini nasıl indireceğiniz. Önbelleği
  kurmak ve bugün Aspose AI’ı kullanmaya başlamak için bu adım‑adım öğreticiyi izleyin.
draft: false
keywords:
- how to list models
- enable auto download
- download hugging face model
- how to use aspose
- how to set cache
language: tr
og_description: Aspose AI ile modelleri nasıl listeleyeceğinizi, otomatik indirmeyi
  etkinleştirmeyi ve bir Hugging Face modelini indirmeyi öğrenin. Önbelleği ayarlamayı
  ve Aspose AI’ı dakikalar içinde kullanmayı keşfedin.
og_title: Aspose AI ile modelleri listeleme – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  headline: How to list models with Aspose AI – Complete Guide
  type: TechArticle
- description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  name: How to list models with Aspose AI – Complete Guide
  steps:
  - name: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
    text: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
  - name: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
    text: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
  - name: Initialise the AI, then call `list_local()` to see exactly what’s cached.
    text: Initialise the AI, then call `list_local()` to see exactly what’s cached.
  - name: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
    text: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
  type: HowTo
tags:
- Aspose
- Python
- LLM
- Model Management
title: Aspose AI ile modelleri listeleme – Tam Rehber
url: /tr/python/general/how-to-list-models-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose AI ile modelleri listeleme – Tam Kılavuz

Aspose AI ile modelleri listeleme, Python'da büyük dil modelleriyle denemeler yapmaya başladığınız anda ortaya çıkan bir sorudur. Bu öğreticide **auto download** özelliğini etkinleştirmeyi, yerel bir önbellek yapılandırmayı ve bir modeli doğrudan Hugging Face'den çekmeyi adım adım göstereceğiz—böylece dosyaları manuel olarak aramadan hemen çalışmaya başlayabilirsiniz.

Eğer *“Aspose'u OCR‑tabanlı AI için nasıl kullanırım?”* ya da *“model dosyaları için önbelleği ayarlamanın en kolay yolu nedir?”* gibi sorular merak ettiyseniz doğru yerdesiniz. Sonuna geldiğinizde, yerel olarak depolanan tüm modelleri listeleyen, eksik olanları otomatik olarak indiren ve dosyaların diskte tam olarak nerede olduğunu gösteren tam işlevsel bir betiğe sahip olacaksınız.

---

## Gereksinimler

- Python 3.9 veya daha yeni (kütüphane, güncel bir yorumlayıcı gerektiren tip ipuçları kullanır)
- `pip` erişimi ile **Aspose OCR** paketini (`aocr`) kurun.  
  ```bash
  pip install aocr
  ```
- Hugging Face'den ilk indirme için bir internet bağlantısı.
- Model önbelleğini tutmak istediğiniz bir klasör (ör. `./model_cache`).

Hepsi bu kadar—ek Docker konteynerleri yok, temiz bir Python kurulumu dışındaki ağır sanal ortamlar da yok.

---

## ## Aspose AI ile modelleri listeleme

Bu kılavuzun kalbi, Aspose AI'nin yerel olarak önbelleğe aldığı **modelleri listeleme** yeteneğidir. Önbellek kurulduktan sonra, kütüphane bildiği her şeyi enumerate edebilir, bu da hata ayıklamayı ve sürüm kontrolünü çok kolaylaştırır.

```python
import aocr

# 1️⃣ Create an Aspose AI instance
ai = aocr.AsposeAI()

# 2️⃣ Configure the model cache and auto‑download behavior
cfg = aocr.AsposeAIModelConfig()
cfg.allow_auto_download = "true"                     # ← enable auto download
cfg.directory_model_path = r"./model_cache"          # ← how to set cache
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

# 3️⃣ Initialise the AI with the config we just built
ai.initialize(cfg)

# 4️⃣ List the models that are already cached locally
print("🗂️ Models cached at:", ai.get_local_path())
print("📦 Available models:", ai.list_local())
```

**Neden bu çalışıyor:**  
- `AsposeAI()` temel çıkarım motoru ile iletişim kuran yüksek seviyeli giriş noktasını oluşturur.  
- `AsposeAIModelConfig()` ayarlanabilir tüm seçenekleri tutar; `allow_auto_download` `"true"` olarak ayarlamak, kütüphaneye belirtilen depodan eksik dosyaları otomatik olarak indirmesini söyler.  
- `directory_model_path` *önbellek dizini*'dir—indirilen tüm ikili dosyaların bulunduğu yerdir.  
- `initialize()` yapılandırmayı uygular, önbellek boşsa ilk indirmeyi gerçekleştirir.  
- Son olarak, `list_local()` önbellek klasörünü tarar ve model tanımlayıcılarının bir Python listesini döndürür; biz de bunu ekrana basarız.

### Beklenen çıktı (ilk çalıştırma)

```
🗂️ Models cached at: ./model_cache
📦 Available models: ['Qwen2.5-3B-Instruct-GGUF']
```

Betik tekrar çalıştırıldığında, kütüphane indirimi atlayıp zaten mevcut modeli listeler; bu da **önbelleği ayarlamanın** sonraki çalıştırmalarda ne kadar faydalı olduğunu kanıtlar.

---

## ## Eksik modeller için otomatik indirmeyi etkinleştirme

Genellikle projeler arasında birden fazla modelle çalışırsınız. Her birini Hugging Face'den manuel olarak çekmek zahmetli olabilir. Auto download'u etkinleştirerek, Aspose AI ağır işi halleder.

```python
cfg.allow_auto_download = "true"
```

> **Pro ipucu:** `allow_auto_download` ayarını sadece geliştirme veya CI ortamlarında `"true"` tutun. Üretimde, beklenmedik ağ trafiğini önlemek için önbelleği kilitlemek isteyebilirsiniz.

Daha sonra kapatmak isterseniz, `initialize()`'ı tekrar çağırmadan önce bayrağı `"false"` olarak ayarlamanız yeterlidir.

---

## ## Hugging Face modelini anında indirme

```python
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

satırı Aspose AI'ye hangi uzak depodan çekileceğini söyler. Kütüphane, GGUF dosyası sağlayan herhangi bir halka açık Hugging Face modelini destekler. Farklı bir model mi istiyorsunuz? Repo kimliğini değiştirin:

```python
cfg.hugging_face_repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
```

Betik çalıştırıldığında, Aspose AI önbelleği kontrol eder:

- **Model mevcutsa**, anında yükler.  
- **Model mevcut değilse**, auto‑download bayrağı bir indirme başlatır, dosyayı `directory_model_path` altında saklar ve ardından hemen kullanım için kaydeder.

Bu yaklaşım, birçok öğreticinin zorladığı “indir‑sonra‑çalıştır” iki adımlı süreci ortadan kaldırır.

---

## ## Model listelendikten sonra Aspose AI'yı nasıl kullanırsınız

Modelleri listelemek sadece hikayenin yarısıdır. Bir modelin mevcut olduğunu öğrendikten sonra çıkarım yapmaya başlayabilirsiniz:

```python
# Assume the model we just listed is the one we want to use
model_name = ai.list_local()[0]

# Create a simple prompt
prompt = "Explain the difference between supervised and unsupervised learning."

# Run inference
response = ai.run_inference(model_name, prompt)

print("🤖 Model response:", response)
```

**Neden bu önemli:**  
- `run_inference()` tokenleştirme, toplu işleme ve GPU yönetimini soyutlar.  
- `list_local()` ile elde ettiğiniz *model adını* geçirerek, çıkarım çağrısının diskteki tam dosyayla eşleştiğinden emin olursunuz.

---

## ## Birden fazla proje için önbellek konumunu ayarlama

Birden çok projeyle uğraşıyorsanız, her birinin kendi önbellek klasörüne sahip olmasını isteyebilirsiniz. `directory_model_path` alanı sadece düz bir string olduğundan, bunu dinamik olarak oluşturabilirsiniz:

```python
import os

project_name = "sentiment_analysis"
cache_root   = "./model_cache"
cfg.directory_model_path = os.path.join(cache_root, project_name)
```

Şimdi her proje izole bir alt‑klasör (`./model_cache/sentiment_analysis`) alır, sürüm çakışmalarını önler ve temizliği basitleştirir.

---

## ## Yaygın tuzaklar ve nasıl önlenir

| Semptom | Muhtemel neden | Çözüm |
|---------|----------------|-------|
| **`PermissionError` önbelleğe erişirken** | Önbellek klasörü başka bir kullanıcıya ait (paylaşımlı sunucularda yaygın) | Klasörü uygun izinlerle manuel olarak oluşturun: `mkdir -p ./model_cache && chmod 775 ./model_cache` |
| **Model `list_local()` içinde hiç görünmüyor** | `allow_auto_download` `"false"` olarak ayarlı ve model henüz önbelleğe alınmamış | Bayrağı geçici olarak açın, bir kez çalıştırın, ardından istenirse kapatın |
| **Beklenmeyen model sürümü** | İki farklı depo aynı ismi paylaşırken farklı dosyalar içeriyor | Tam repo kimliğini (etiket/commit dahil) sabitleyin veya ilk başarılı çekmeden sonra auto‑download'u devre dışı bırakarak önbelleği kilitleyin |
| **Bellek yetersizliği hataları** | Yeterli RAM/VRAM olmayan bir makinede büyük GGUF dosyaları | Daha küçük bir model kullanın (ör. `Qwen2.5-1.5B`) veya CPU çıkarımını zorlamak için `cfg.device = "cpu"` ayarlayın |

---

## ## Kopyala‑yapıştır yapabileceğiniz tam betik

Aşağıda, yukarıdaki tüm kavramları bir araya getiren, çalıştırmaya hazır tam örnek yer alıyor. `list_models_demo.py` olarak kaydedin ve `python list_models_demo.py` ile çalıştırın.

```python
# list_models_demo.py
import os
import aocr

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Create the Aspose AI instance
    # ------------------------------------------------------------------
    ai = aocr.AsposeAI()

    # ------------------------------------------------------------------
    # 2️⃣ Build configuration: enable auto download, set cache path,
    #    and point at a Hugging Face repo
    # ------------------------------------------------------------------
    cfg = aocr.AsposeAIModelConfig()
    cfg.allow_auto_download = "true"                               # enable auto download
    cfg.directory_model_path = os.path.abspath("./model_cache")   # how to set cache
    cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

    # ------------------------------------------------------------------
    # 3️⃣ Initialise the AI with the configuration
    # ------------------------------------------------------------------
    ai.initialize(cfg)

    # ------------------------------------------------------------------
    # 4️⃣ Verify cache location and list all locally available models
    # ------------------------------------------------------------------
    print("🗂️ Models cached at:", ai.get_local_path())
    print("📦 Available models:", ai.list_local())

    # ------------------------------------------------------------------
    # 5️⃣ (Optional) Run a quick inference using the first listed model
    # ------------------------------------------------------------------
    if ai.list_local():
        model_name = ai.list_local()[0]
        prompt = "Give a short summary of the Python GIL."
        response = ai.run_inference(model_name, prompt)
        print("\n🤖 Model response:", response)

if __name__ == "__main__":
    main()
```

**Betik çalıştırıldığında** önceki örneğe benzer bir çıktı üretir, ardından modelden kısa bir yanıt alırsınız. İstediğiniz herhangi bir istemle değiştirmekten çekinmeyin—bu, modeli **modelleri listeleme** işleminden sonra gerçekten kullanılabilir olduğunu test etmenin en hızlı yoludur.

---

## ## Özet

Aspose AI kullanarak **modelleri listeleme** konusunda, **auto download**'u etkinleştirmeden kalıcı bir **önbellek** yapılandırmaya ve isteğe bağlı **Hugging Face modeli** çekmeye kadar ihtiyacınız olan her şeyi ele aldık. Temel çıkarımlar:

1. Bir `AsposeAI` nesnesi ve bir `AsposeAIModelConfig` oluşturun.  
2. `allow_auto_download = "true"` ayarlayın ve `directory_model_path`'i kontrol ettiğiniz bir klasöre yönlendirin.  
3. AI'yı başlatın, ardından `list_local()` çağırarak önbellekte ne olduğunu tam olarak görün.  
4. Listedeki model adını çıkarım için kullanın; böylece gerçek dünya uygulamaları geliştirmeye hazırsınız.

---

## Sonraki Adımlar

- **Farklı modellerle deney yapın** – `cfg.hugging_face_repo_id`'yi başka bir repo ile değiştirin ve listenin nasıl değiştiğini görün.  
- **Önbelleği ince ayarlayın**

## Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalarla birlikte tam çalışan kod örnekleri içerir; böylece ek API özelliklerini öğrenebilir ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Aspose.OCR for .NET'te Liste ile OCR Görüntülerini Toplu İşleme](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Aspose OCR Lisansını Ayarlama ve Java'da Doğrulama](/ocr/english/java/ocr-basics/set-license/)
- [Aspose.OCR for .NET ile Görüntüden Metin Çıkarma](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}