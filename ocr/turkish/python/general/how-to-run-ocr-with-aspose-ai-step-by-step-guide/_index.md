---
category: general
date: 2026-02-09
description: Aspose AI ve Hugging Face modeli kullanarak OCR nasıl çalıştırılır –
  Hugging Face modelini indirmeyi, OCR hatalarını düzeltmeyi ve GPU belleğini boşaltmayı
  öğrenin.
draft: false
keywords:
- how to run OCR
- download hugging face model
- free gpu memory
- how to free gpu
- correct OCR errors
language: tr
og_description: Aspose AI ile OCR çalıştırma yöntemi ilk paragrafta açıklanıyor –
  hugging face modelini nasıl indireceğinizi, OCR hatalarını nasıl düzelteceğinizi
  ve GPU belleğini nasıl boşaltacağınızı keşfedin.
og_title: Aspose AI ile OCR Nasıl Çalıştırılır – Tam Kılavuz
tags:
- OCR
- Aspose
- AI
- HuggingFace
title: Aspose AI ile OCR Nasıl Çalıştırılır – Adım Adım Rehber
url: /tr/python/general/how-to-run-ocr-with-aspose-ai-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose AI ile OCR Nasıl Çalıştırılır – Tam Kılavuz

Tarayıcıyla taranmış bir faturada **OCR nasıl çalıştırılır** ve saatlerce yazım hatalarını düzeltmeden tamamen temiz sayılar elde edilir diye hiç merak ettiniz mi? Yalnız değilsiniz. Birçok gerçek‑dünya projesinde klasik bir OCR motorundan çıkan ham metin hâlâ rastgele karakterler, bozuk para birimi sembolleri veya karışık rakamlar içerir—özellikle kaynak görüntü gürültülü olduğunda.  

İyi haber şu ki, bir LLM'yi Aspose OCR'a bağlayabilir, Hugging Face modelini anında indirebilir ve AI'nın çıktıyı sizin için parlatmasına izin verebilirsiniz. Bu öğreticide, modeli çekmekten (evet, **download hugging face model** otomatik olarak nasıl yapılır göstereceğiz) GPU kaynaklarını serbest bırakmaya kadar tüm süreci adım adım inceleyeceğiz. Sonunda **corrects OCR errors** yapan, mütevazı bir GPU'da hızlı çalışan ve kendini temizleyerek bellek israfını önleyen tekrarlanabilir bir betiğe sahip olacaksınız.

## Neler Öğreneceksiniz

- Aspose AI'yi, Hugging Face'den bir **Qwen2.5‑3B‑Instruct‑GGUF** modeli alacak şekilde yapılandırın.
- Bir görüntü dosyası üzerinde standart Aspose OCR motorunu çalıştırın.
- Sayıları ve para birimi sembollerini bozulmadan tutan özel bir LLM istemi kullanın.
- Yerleşik **free gpu memory** rutinini kullanarak GPU belleğini serbest bırakın.
- Çok sayfalı PDF'ler veya düşük özellikli GPU'lar gibi uç durumlar için iş akışını ayarlayın.

> **Prerequisites** – Python 3.9+, `aspose-ocr` paketi, modelin ilk indirilmesi için internet erişimi ve en az 4 GB VRAM'li bir GPU (isteğe bağlı ama önerilir). GPU'nuz yoksa, betik kalan katmanlar için otomatik olarak CPU'ya geçecektir.

---

## OCR Nasıl Çalıştırılır ve Sonuçlar Nasıl İyileştirilir

Aşağıda tam, çalıştırmaya hazır Python betiği yer almaktadır. `ocr_with_ai.py` olarak kaydedin ve yer tutucu yolları kendi dosyalarınızla değiştirin.

```python
# ocr_with_ai.py
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Configure the AI engine (download hugging face model)
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # auto‑download if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # tiny memory footprint
    gpu_layers=20,                                  # 20 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY/Models"  # optional custom folder
)
ai = AsposeAI(ai_config)

# -------------------------------------------------
# Step 2 – Load an image and run the classic OCR engine
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()   # returns plain‑text string

# -------------------------------------------------
# Step 3 – Register a custom LLM prompt (correct OCR errors)
# -------------------------------------------------
def financial_prompt():
    # Bias the model toward financial terminology
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# -------------------------------------------------
# Step 4 – Let the LLM polish the output
# -------------------------------------------------
corrected_text = ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Enhanced :", corrected_text)

# -------------------------------------------------
# Step 5 – Release resources (free gpu memory)
# -------------------------------------------------
ai.free_resources()
```

> **Pro tip:** `gpu_layers` parametresi, kaç transformer katmanının GPU'da kalacağını belirlemenizi sağlar. Bellek yetersizliği hataları alıyorsanız, bu sayıyı düşürün ve geri kalan CPU'da çalışır – daha sonra `ai.free_resources()` ile **free gpu memory** yapmaya devam edersiniz.

### Beklenen Çıktı

Betik bir örnek fatura üzerinde çalıştırıldığında aşağıdaki gibi bir çıktı verir:

```
Original : Invoic # 12345 \n Total: $1O0.00\n Date: 2023-07-15
Enhanced : Invoice # 12345
Total: $100.00
Date: 2023-07-15
```

AI'nın `$1O0.00` içindeki “O” harfini doğru sıfıra dönüştürürken dolar işaretini koruduğuna dikkat edin. Bu, finansal belgeler için **correct OCR errors** özünün kendisidir.

## Hugging Face Modeli İndirme – Arkada Ne Olur?

`allow_auto_download="true"` ayarını yaptığınızda Aspose AI sarmalayıcısı `directory_model_path`'i kontrol eder. Model dosyaları orada yoksa, Hugging Face Hub'a bağlanır, `Qwen2.5‑3B‑Instruct‑GGUF`'in **int8‑quantized** sürümünü çeker ve yerel olarak depolar. Bu tek seferlik indirme genellikle 2 GB'den azdır, bu da mütevazı SSD'lerde bile uygulanabilir kılar.

> **Neden int8?** 8‑bit'e kuantize etmek bellek kullanımını büyük ölçüde azaltır—işlem sonrası **free gpu memory** yapmak istediğinizde kritik öneme sahiptir. Taviz, doğrulukta çok küçük bir düşüştür, ancak OCR metninin son işlenmesi için etkisi ihmal edilebilir.

Modeli kendiniz barındırmayı tercih ederseniz, `.gguf` dosyalarını `YOUR_DIRECTORY/Models` klasörüne bırakmanız yeterlidir; Aspose internete tekrar bağlanmadan bunları alacaktır.

## GPU'yu Nasıl Serbest Bırakılır – En İyi Uygulamalar

GPU kaynakları birçok iş istasyonunda paylaşılan bir emtiadır. Betiğiniz tamamlandıktan sonra tensörlerin hâlâ bellekte kalması, sonraki işler için “CUDA out of memory” hatalarına yol açabilir. `ai.free_resources()` çağrısı üç şey yapar:

1. **Alttaki transformer'ı serbest bırakır** – tüm GPU‑resident ağırlıklar serbest bırakılır.
2. **PyTorch önbelleğini temizler** – `torch.cuda.empty_cache()` dahili olarak çağrılır.
3. **Geçici dosyaları siler** – indirme sırasında oluşturulan disk üzerindeki önbellekler kaldırılır.

Aspose AI'yi diğer PyTorch iş yükleriyle karıştırıyorsanız `torch.cuda.empty_cache()`'i manuel olarak da çağırabilirsiniz, ancak yerleşik yöntem genellikle yeterlidir.

## Adım‑Adım Yolculuk (İkincil Anahtar Kelimelerle H2'ler)

### Hugging Face Modelini Otomatik Olarak İndir

`AsposeAIModelConfig` yapıcı, Hugging Face API'siyle uğraşmanın karmaşıklığını gizler. Betiği ilk kez çalıştırdığınızda internet erişiminizin olduğundan emin olun. Bundan sonra model `YOUR_DIRECTORY/Models` içinde bulunur ve sonraki çalıştırmalar anında başlar.

### Çıkarım Sonrası GPU Belleğini Serbest Bırakma

Bunu uzun süren bir hizmet içinde (ör. Flask API) çalıştırıyorsanız, her isteğin ardından `ai.free_resources()` çağırın. Bu, bellek sızıntılarını önler ve bir sonraki isteğin aynı GPU'yu sorunsuz kullanmasını sağlar.

### Özel Bir İstemle OCR Hatalarını Düzeltme

Our `financial_prompt` function returns a dictionary with a single key `prompt`. You can tailor this to any domain:

```python
def medical_prompt():
    return {"prompt": "Fix OCR mistakes, keep dosage numbers and units unchanged"}
```

`ai.set_post_processor(...)` içindeki fonksiyon adını değiştirerek tıbbi kayıtlar için bir **correct OCR errors** boru hattına sahip olursunuz.

### Çok Sayfalı PDF'lerde OCR Nasıl Çalıştırılır

Aspose OCR can handle PDFs out of the box:

```python
ocr_engine.load_document(r"YOUR_DIRECTORY/multi_page.pdf")
raw_text = ocr_engine.recognize()  # concatenates pages automatically
```

Ham dizeyi aldıktan sonra aynı LLM post‑processor her sayfanın metnini temizleyecek. Ek bir kod gerekmez.

### GPU'nuz Olmadığında – GPU'yu Nasıl Serbest Bırakırsınız (Bir Olmasa Bile)

Sadece CPU'lu makinelerde bile `ai.free_resources()` çağırmak zararsızdır. Sadece dahili önbellekleri temizler, bu da RAM'i serbest bırakabilir. Bu yüzden **how to free gpu** önerisi evrensel olarak geçerlidir: her zaman kendinizi temizleyin.

## Yaygın Tuzaklar ve Nasıl Çözdük

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| **GPU'da Bellek Yetersizliği** | `gpu_layers` kartınız için çok yüksek ayarlandı | `gpu_layers` değerini 10 veya 5'e düşürün, geri kalan CPU'da çalışsın |
| **Model Asla İndirilemiyor** | Kurumsal güvenlik duvarı huggingface.co'ya HTTPS erişimini engelliyor | Modeli farklı bir ağda manuel olarak indirin, ardından `directory_model_path`'i yerel klasöre yönlendirin |
| **Rakamlar Bozuluyor** | İstem, rakamları koruma konusunda yeterince açık değil | İsteme “tüm sayısal değerleri ve para birimi sembollerini tam olarak göründükleri gibi koru” ifadesini ekleyin |
| `free_resources` bir istisna fırlatıyor | Eski bir Aspose OCR sürümü kullanılıyor | En son `aspose-ocr` paketine yükseltin (pip install --upgrade aspose-ocr) |

## Tam Örnek Özeti

Here’s the script again, this time with inline comments that explain every line for future reference:

```python
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Configure AI – will auto‑download the model if needed
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,                     # adjust based on your GPU size
    directory_model_path=r"YOUR_DIRECTORY/Models"
)
ai = AsposeAI(ai_config)               # initialise the engine

# 2️⃣ Run classic OCR on an image (or PDF)
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()      # plain‑text result

# 3️⃣ Define a prompt that tells the LLM to keep numbers intact
def financial_prompt():
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# 4️⃣ Let the LLM clean the text
corrected_text = ai.run_postprocessor(raw_text)

# 5️⃣ Show before/after
print("Original :", raw_text)
print("Enhanced :", corrected_text)

# 6️⃣ Clean up – this frees GPU memory for the next run
ai.free_resources()
```

## Sonuç

Aspose ile **how to run OCR** konusunu, talep üzerine bir Hugging Face modeli indirmeyi, **corrects OCR errors** yapan bir istem oluşturmayı ve sonunda **free gpu memory** yaparak çalışma istasyonunuzun yanıt verebilir kalmasını ele aldık. Tüm iş akışı tek, bağımsız bir Python dosyasına sığar—harici betikler, manuel model yönetimi ve kalıcı GPU tahsisleri yok.

Sonraki adımlar? `financial_prompt`'u şu şekilde değiştirmeyi deneyin:

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}