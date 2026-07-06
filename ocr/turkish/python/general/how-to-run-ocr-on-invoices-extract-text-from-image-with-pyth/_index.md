---
category: general
date: 2026-01-07
description: Fatura işleme için OCR'yi çalıştırma ve görüntüden metin çıkarma. OCR
  doğruluğunu artırmayı, OCR için görüntü yüklemeyi ve fatura OCR'sini verimli bir
  şekilde işlemeyi öğrenin.
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: tr
og_description: Faturalar üzerinde adım adım OCR çalıştırma. Görüntüden metin çıkarma,
  OCR doğruluğunu artırma ve Aspose AI kullanarak OCR için görüntüyü yükleme.
og_title: Faturalar Üzerinde OCR Nasıl Çalıştırılır – Tam Python Rehberi
tags:
- OCR
- Python
- Image Processing
title: Faturalar Üzerinde OCR Nasıl Çalıştırılır – Python ile Görüntüden Metin Çıkarma
url: /tr/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Faturalar Üzerinde OCR Nasıl Çalıştırılır – Görüntüden Metin Çıkarma Python ile

Tarama yapılan bir faturada **OCR nasıl çalıştırılır** ve temiz, aranabilir metin elde edilir diye hiç merak ettiniz mi? Yalnız değilsiniz. Birçok geliştirici, ham OCR çıktısının yazım hataları, bozuk satır sonları ve eksik noktalama işaretleriyle dolu olduğu bir duvara çarpar. Bu öğreticide, yalnızca **görüntüden metin çıkarma** değil, aynı zamanda bir Aspose AI modeliyle post‑işleme yaparak **OCR doğruluğunu artırma** sağlayan tam bir çözümü adım adım inceleyeceğiz.

Nasıl **OCR için görüntü yükleneceğini**, yerleşik motorun çalıştırılacağını ve ardından sonucu sonraki analizler için hazır hâle getiren hafif bir yazım denetimi uygulanacağını göreceksiniz. Sonunda, herhangi bir fatura‑işleme hattına eklenebilecek yeniden kullanılabilir bir betiğe sahip olacaksınız.

> **İhtiyacınız olanlar**  
> * Python 3.9 ve üzeri  
> * `aspose-ocr` ve `aspose-ai` paketleri (`pip` ile kurulur)  
> * Bir fatura görüntüsüPNG, JPEG veya TIFF) – örnek olarak `sample_invoice.png` kullanacağız  
> * İsteğe bağlı: Daha hızlı model çıkarımı için en az 4 GB VRAM'lı bir GPU (betik CPU'da da çalışır)

---

## Adım 1: Gerekli Paketleri Yükleyin ve Ortamı Hazırlayın

OCR için **görüntü yüklemeden** önce gerekli kütüphanelerin mevcut olduğundan emin olmalıyız. Aspose OCR motoru basit bir Python sarmalayıcı ile gelirken, AI post‑işlemcisi bir Hugging Face kuantize modeli üzerine dayanır.

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **Pro ipucu:** GPU hızlandırması kullanmayı planlıyorsanız, CUDA desteğiyle `torch` kurun (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`).

---

## Adım 2: Fatura Görüntüsünü Yükleyin

Görüntüyü yüklemek basittir, ancak yolu açıkça ham dize (`r"..."`) olarak ayarlamamızı neden belirttiğimizi açıklamakta fayda var. Bu, Windows yollarında istenmeyen kaçış karakteri hatalarını önler.

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*Neden önemli?*: `ocr.Image.load` kullanmak, görüntünün Aspose’un optimal varsayılanlarına göre ön‑işlemden (ikiliye dönüştürme, eğikliği düzeltme) geçirilmesini garanti eder; bu da herhangi bir AI sihrinden önce **OCR doğruluğunu artırır**.

---

## Adım 3: Yerleşik OCR Motorunu Çalıştırın

Şimdi gerçekten **OCR çalıştırıyoruz** ve ham metni yakalıyoruz. Bu adım, standart bir OCR çalıştırmasından alacağınız tipik çıktıyı gösterir—genellikle satır sonları karışıklığı ve ara sıra yazım hataları içerir.

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**Tipik ham çıktı** (kısaltılmıştır):

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

“Invoice” kelimesinin “Invo1ce” olarak göründüğünü veya noktalama işaretlerinin eksik olduğunu fark edebilirsiniz. İşte AI post‑işlemcisi burada devreye girer.

---

## Adım 4: Aspose AI Modelini Yapılandırın

Kullanacağımız AI modeli **Qwen2.5‑3B‑Instruct‑GGUF**, orta seviye bir GPU’da rahatça çalışabilen hafif bir talimat‑tuned LLM'dir. Aşağıdaki yapılandırma, Aspose'a modeli nereden alacağını, GPU'da kaç katmanın tutulacağını ve uzun paragrafları işlemek için bağlam boyutunu bildirir.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **Bu yapılandırma neden?**  
> * `gpu_layers=30` hız ve bellek arasında denge kurar—çoğu çıkarım GPU'da gerçekleşirken, kalan katmanlar OOM hatalarını önlemek için CPU'da kalır.  
> * `context_size=4096` modelin tüm faturayı bir kerede görebilmesini sağlar, önemli alanların kesilmesini önler.

---

## Adım 5: Basit Bir Yazım‑Denetimi Post‑İşlemcisi Oluşturun

AI çağrısını `simple_spell_check` adlı küçük bir fonksiyon içinde saracağız. İstem kasıtlı olarak özlü: “Correct spelling and punctuation:” ardından ham OCR metni. Model temizlenmiş bir sürüm döndürür.

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**Nasıl çalışır:** `ai.run_prompt` istemi yerel olarak yüklenmiş LLM'ye gönderir ve ardından düzeltilmiş yazım, doğru noktalama ve daha doğal bir satır‑sonu düzeni içeren tek bir dize döndürür.

---

## Adım 6: Post‑İşlemciyi Ham OCR Metnine Uygulayın

Şimdi sihir gerçekleşir. Ham OCR çıktısını post‑işlemcimize verir ve geliştirilmiş sonucu yazdırırız.

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**Örnek geliştirilmiş çıktı**:

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Düzeltilmiş “Invoice” yazımını, doğru iki nokta kullanımını ve tutarlı satır sonlarını fark edin—güvenilir sonraki ayrıştırma için tam da ihtiyacınız olan şey.

---

## Adım 7: Kaynakları Temizleyin

Hem OCR motoru hem de AI modeli yerel kaynaklar tahsis eder. Özellikle uzun süren hizmetlerde işiniz bittiğinde bunları serbest bırakmak iyi bir uygulamadır.

```python
ai.free_resources()
engine.dispose()
```

---

## Tam Betik – Yapıştırmaya Hazır

Aşağıda, tüm adımları birleştiren eksiksiz, çalıştırılabilir betik yer alıyor. `invoice_ocr.py` olarak kaydedin, `YOUR_DIRECTORY` kısmını fatura görüntünüzün bulunduğu klasörle değiştirin ve `python invoice_ocr.py` ile çalıştırın.

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

Betik çalıştırıldığında, gürültülü ham OCR dökümünü ve yan yana **geliştirilmiş OCR doğruluğu** sürümünü göreceksiniz.

---

## Sık Sorulan Sorular & Kenar Durumları

### 1. Fatura görüntüm çok sayfalı bir PDF ise ne olur?

Aspose OCR doğrudan PDF sayfalarını yükleyebilir. Görüntü yükleme satırını şu şekilde değiştirin:

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

`page_index`'i yineleyerek her sayfayı sırasıyla işleyin.

### 2. GPU belleğim tükeniyor—sadece CPU kullanabilir miyim?

Kesinlikle. `AsposeAIModelConfig` içinde `gpu_layers=0` ayarlayın. Model tamamen CPU'da çalışacak, bu daha yavaş ama düşük donanım için güvenlidir.

### 3. İngilizce olmayan faturalarla nasıl başa çıkılır?

Model depo kimliğini dil‑spesifik bir modelle değiştirin, örneğin çok dilli destek için `"mistralai/Mistral-7B-Instruct-v0.2"`. Boru hattının geri kalanı değişmez.

### 4. Birden fazla post‑işlemciyi zincirleyebilir miyim (ör. tarih formatlama, toplamları çıkarma)?

Evet. `ai.set_post_processor` çağrılabilir bir liste alır. Örneğin:

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

Çıktı önce yazım denetiminden geçecek, ardından toplamlar çıkarılacaktır.

---

## Performans İpuçları & En İyi Uygulamalar

| Tip | Neden Yardımcı Olur |
|-----|---------------------|
| **Batch multiple invoices** – load them into a list and process in a loop. | Python yorumlayıcı yükünü azaltır ve AI modelini bellekte sıcak tutar. |
| **Cache the model** – avoid calling `initialize` repeatedly in a web service. | Model yükleme ~30 s sürebilir; önbellekleme anlık yanıt verir. |
| **Resize large images** to 1500 px width before OCR. | Daha küçük görüntüler OCR ve AI çıkarımını hızlandırır, doğruluktan ödün vermez. |
| **Set `allow_auto_download="false"` in production** – ship the model with your deployment. | Belirli başlangıç süreleri garantilenir ve ağ kesintileri önlenir. |

---

## Sonuç

Faturalar üzerinde **OCR nasıl çalıştırılır** konusunu, görüntüyü yüklemekten AI‑destekli bir yazım denetimiyle sonucu iyileştirmeye kadar ele aldık. Bu adımları izleyerek güvenilir bir şekilde **görüntüden metin çıkarabilir**, **OCR doğruluğunu artırabilir** ve herhangi bir Python‑tabanlı iş akışında **fatura OCR işleme** işlemini sorunsuz bir şekilde gerçekleştirebilirsiniz.

Farklı fatura düzenleriyle bir deneme yapın—belki el yazısı bir fiş ya da taranmış bir sözleşme. Aynı boru hattı minimal ayarlamalarla uyum sağlar ve iyi yapılandırılmış bir OCR + AI kombinasyonunun her belge‑otomasyon projesi için çok yönlü bir araç olduğunu kanıtlar.

Bu rehberi faydalı bulduysanız, ekip arkadaşlarınızla paylaşmayı veya Aspose paketlerini barındıran depoyu yıldızlamayı düşünün.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}