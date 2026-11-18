---
category: general
date: 2026-03-26
description: Aspose OCR kullanarak görüntüyü metne dönüştürün ve OCR metnini Python
  tarzında temizleyin. Tek bir betikte görüntü metnini nasıl çıkaracağınızı ve son
  işleme nasıl yapacağınızı öğrenin.
draft: false
keywords:
- convert image to text
- how to extract image text
- clean ocr text python
- Aspose OCR Python
- AI spell‑checker Python
- post‑process OCR output
language: tr
og_description: Görseli hızlıca metne dönüştürün. Bu kılavuz, Aspose OCR ve bir AI
  imla denetleyicisi kullanarak görüntü metnini çıkarmayı ve OCR metnini python tarzında
  temizlemeyi gösterir.
og_title: Python ile Görüntüyü Metne Dönüştür – Tam Kılavuz
tags:
- OCR
- Python
- Aspose
- AI
title: Python ile Görüntüyü Metne Dönüştür – Tam Adım Adım Rehber
url: /tr/python/general/convert-image-to-text-with-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüyü Metne Dönüştür – Tam Python Öğreticisi

Hiç **görüntüyü metne dönüştür**mek istediniz ama dağınık sonuçlar aldınız mı? Yalnız değilsiniz. Birçok geliştirici, OCR çıktısının yazım hataları, rastgele semboller veya hatalı satır sonlarıyla dolu olduğunda takılıp kalıyor. İyi haber? Birkaç satır Python ve Aspose OCR ile herhangi bir görüntüden doğrudan metin alabilir **ve** bunu otomatik olarak temizleyebilirsiniz.

Bu rehberde **görüntü metnini nasıl çıkaracağınızı** gösterecek, ardından AI destekli bir yazım denetleyicisiyle cilalı, okunabilir içerik üreteceğiz. Sonunda, bir PNG dosyasından temiz bir `.txt` dosyasına kadar tek bir betiğiniz olacak — manuel kopyala‑yapıştırmaya gerek kalmayacak.  

> **Öğrenecekleriniz**  
> * Aspose OCR’yi kurma ve yapılandırma.  
> * Bir görüntü dosyasından metni tanıma.  
> * Yazım denetimi için bir Aspose AI modeli başlatma.  
> * OCR çıktısını düzenlemek için post‑processörü uygulama.  
> * Sonucu kaydetme ve kaynakları serbest bırakma.  

Tüm bunlar **clean OCR text python** tarzı bir temizlikle çalışır — yani kod, ekstra sarmalayıcılara ihtiyaç duymadan herhangi bir projeye bırakılmaya hazır.

---

## Önkoşullar

Başlamadan önce şunların olduğundan emin olun:

| Gereksinim | Neden Önemli |
|-------------|----------------|
| Python 3.9 ve üzeri | Modern sözdizimi & tip ipuçları |
| `asposeocr` paketi (`pip install asposeocr`) | Çekirdek OCR motoru |
| İnternet erişimi (ilk çalıştırmada) | Modelin Hugging Face’den otomatik indirilmesi |
| Okumak istediğiniz bir PNG/JPEG görüntüsü | Girdi kaynağı |

GPU zorunlu değildir, ancak bir GPU’nuz varsa AI modeli otomatik olarak daha hızlı yazım denetimi için onu kullanacaktır.

---

## Adım 1: Aspose OCR ile Görüntüyü Metne Dönüştür

İlk olarak güvenilir bir OCR motoruna ihtiyacımız var. Aspose OCR ticari bir kütüphane, ancak geliştirme için cömert bir ücretsiz katman sunar. Aşağıda motoru başlatıyor, dili İngilizce olarak ayarlıyor ve eğimli taramaları ele almak için otomatik kaydırma düzeltmeyi etkinleştiriyoruz.

```python
import asposeocr as ocr

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English   # English language pack
ocr_engine.auto_skew = True                  # Auto‑deskew images
```

> **`auto_skew` neden etkinleştirilmeli?**  
> Birçok taranmış belge mükemmel düz değildir. Otomatik kaydırma, karakter tanımasını iyileştirmek için görüntüyü yeterince döndürür; bu da daha sonra temizlemeniz gereken bozuk kelime sayısını azaltır.

Şimdi bir görüntü dosyasını motorun içine besliyoruz:

```python
# Recognise text from the input image (replace with your own path)
ocr_result = ocr_engine.recognize_image("YOUR_DIRECTORY/input_image.png")
print("Raw OCR output:")
print(ocr_result.text[:200])  # Show first 200 characters for sanity check
```

`ocr_result.text` özelliği, fotoğraftan çıkarılan ham dizeyi içerir. Bu aşamada muhtemelen rastgele noktalama işaretleri, satır sonu tuhaflıkları veya birkaç yazım hatası göreceksiniz — tam da çözmek istediğimiz sorun.

![convert image to text workflow](image.png){alt="görüntüyü metne dönüştürme iş akışı diyagramı"}

---

## Adım 2: AI Yazım Denetleyicisini Kur (Clean OCR Text Python)

OCR çıktısını temizlemek bir regex değişimi kadar basit olabilir, ancak gerçekten okunabilir bir metin için Aspose AI ve yazım denetimine odaklanmış hafif bir LLM kullanacağız. Model, betiği ilk kez çalıştırdığınızda Hugging Face’den indirilir, böylece manuel bir indirme yapmanız gerekmez.

```python
from asposeocr import AsposeAI, AsposeAIModelConfig

# Model configuration – auto‑download enabled
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="bartowski/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=30                # Use GPU if available, otherwise CPU fallback
)

# Initialise the AI spell‑checker
spell_checker = AsposeAI()
spell_checker.initialize(model_cfg)
spell_checker.set_post_processor("spell_check")
```

**Neden bu model?**  
`Qwen2.5‑3B‑Instruct‑GGUF` 3 milyar parametreli, talimat‑tuned bir modeldir ve bir dizüstü GPU’sunda (ya da int8 kuantizasyonlu CPU’da) rahatça çalışır. Satır‑satır yazım denetimi için belleği zorlamadan yeterince hızlıdır.

---

## Adım 3: OCR Çıktısına Yazım Denetimi Uygulama

OCR metni elinizde ve AI modeli hazır olduğunda, ham dizeyi post‑processöre beslemek yeterlidir. Metot, doğrudan diske yazabileceğiniz temizlenmiş bir versiyon döndürür.

```python
# Run the spell‑checking post‑processor
corrected_text = spell_checker.run_postprocessor(ocr_result.text)

print("\nCleaned OCR output (first 200 chars):")
print(corrected_text[:200])
```

Gözleyeceğiniz tipik iyileştirmeler:

* “teh” → “the”  
* “recieve” → “receive”  
* Noktalama işaretlerinden sonra eksik boşluklar – otomatik olarak düzeltildi  
* Garip satır sonları düzgün cümlelere dönüştürüldü  

Daha fazla kontrol isterseniz `run_postprocessor`a özel bir prompt geçirebilirsiniz, ancak varsayılan “spell_check” ön ayarı çoğu durumda yeterlidir.

---

## Adım 4: Temiz Metni Bir Dosyaya Kaydetme

Metin artık düzenli, onu kalıcı hâle getiriyoruz. UTF‑8 kullanmak, özel karakterlerin (ör. aksanlı harfler) korunmasını sağlar.

```python
output_path = "YOUR_DIRECTORY/output_text.txt"

with open(output_path, "w", encoding="utf-8") as out_file:
    out_file.write(corrected_text)

print(f"\n✅ Processing complete: input_image.png → {output_path}")
```

Herhangi bir editörde dosyayı açtığınızda, dil modeli beslemek, arama için indekslemek ya da sadece arşivlemek gibi sonraki işlemler için hazır, insan tarafından okunabilir bir belge göreceksiniz.

---

## Adım 5: AI Kaynaklarını Serbest Bırakma (İyi Bakım)

Aspose AI, model ağırlıklarını bellekte tutar. İşiniz bittiğinde bunları serbest bırakmak, özellikle uzun‑çalışan servislerde bellek sızıntılarını önler.

```python
spell_checker.free_resources()
```

Hepsi bu! Görüntüden temiz metne kadar tüm işlem hattı, 30 satırın altında bir Python kodu ile tamamlanabilir.

---

## Yaygın Sorular ve Kenar Durumlar

### Görüntü İngilizce değilse ne olur?
`ocr_engine.language`ı uygun enum ile ayarlayın, ör. `ocr.Language.French`. Yazım denetleyici modeli temel yazım için dil bağımsızdır, ancak en iyi sonuçlar için çok dilli bir model tercih edebilirsiniz.

### GPU’mda sadece 20 katman var — yine de modeli kullanabilir miyim?
Kesinlikle. `gpu_layers`ı `20` (veya sadece CPU için `0`) olarak düşürün. Kütüphane, kalan katmanlar için otomatik olarak CPU’ya geçiş yapar.

### Model indirme, kurumsal bir proxy’nin arkasında başarısız oluyor?
Betik çalıştırmadan önce ortam değişkenleri (`HTTP_PROXY`, `HTTPS_PROXY`) aracılığıyla proxy yapılandırmasını geçin. İndirme prosedürü bu ayarları dikkate alır.

### AI yerine hızlı bir regex temizliği yeterli mi?
AI adımını atlayıp basit bir temizlik çalıştırabilirsiniz:

```python
import re
clean = re.sub(r'\s+', ' ', ocr_result.text).strip()
```

Ancak unutmayın, regex gerçek yazım hatalarını düzeltmez — AI bunu sizin için yapar.

---

## Tam Çalışan Betik

Aşağıda, doğrudan çalıştırılabilir tam betik yer alıyor. `YOUR_DIRECTORY` kısmını, görüntünüzün bulunduğu ve çıktının kaydedileceği klasörle değiştirin.

```python
import asposeocr as ocr
from asposeocr import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Initialise OCR engine
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
ocr_engine.auto_skew = True

# -------------------------------------------------
# Step 2 – Recognise text from image
# -------------------------------------------------
ocr_result = ocr_engine.recognize_image("YOUR_DIRECTORY/input_image.png")
print("Raw OCR (first 200 chars):")
print(ocr_result.text[:200])

# -------------------------------------------------
# Step 3 – Configure AI spell‑checker
# -------------------------------------------------
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="bartowski/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=30
)

spell_checker = AsposeAI()
spell_checker.initialize(model_cfg)
spell_checker.set_post_processor("spell_check")

# -------------------------------------------------
# Step 4 – Clean the OCR output
# -------------------------------------------------
corrected_text = spell_checker.run_postprocessor(ocr_result.text)
print("\nCleaned OCR (first 200 chars):")
print(corrected_text[:200])

# -------------------------------------------------
# Step 5 – Write to file
# -------------------------------------------------
output_path = "YOUR_DIRECTORY/output_text.txt"
with open(output_path, "w", encoding="utf-8") as out_file:
    out_file.write(corrected_text)

print(f"\nProcessing complete: input_image.png → {output_path}")

# -------------------------------------------------
# Step 6 – Free AI resources
# -------------------------------------------------
spell_checker.free_resources()
```

Bu betiği çalıştırdığınızda, `output_text.txt` içinde görüntünüzün cilalı bir transkripsiyonunu bulacaksınız.

---

## Sonuç

Aspose OCR kullanarak **görüntüyü metne dönüştür**meyi, ardından **clean OCR text python** tarzı bir AI yazım denetleyicisiyle metni temizlemeyi pratik bir şekilde gösterdik. Çözüm tek bir Python dosyasıyla kendine yetiyor, Windows, macOS veya Linux üzerinde çalışıyor.

Bir sonraki adım için şunları düşünebilirsiniz:

* **PDF’lerden görüntü metni** çıkarmak için sayfaları önce görüntülere dönüştürmek.  
* Temiz metni otomatik rapor üretimi için bir özetleme modeline beslemek.  
* Sonuçları anlamsal arama için bir vektör veritabanında saklamak.

Deneyin, model parametreleriyle oynayın ve OCR‑to‑text hattının veri alım aracınızın temel bir parçası olmasına izin verin. Mutlu kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}