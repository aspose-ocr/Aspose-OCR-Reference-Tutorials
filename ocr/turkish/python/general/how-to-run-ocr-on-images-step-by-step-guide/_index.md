---
category: general
date: 2026-01-02
description: OCR'ı hızlı bir şekilde çalıştırma ve görüntüden metin çıkarma. OCR için
  görüntüyü nasıl yükleyeceğinizi, OCR doğruluğunu nasıl artıracağınızı ve güvenilir
  sonuçlar almayı öğrenin.
draft: false
keywords:
- how to run OCR
- extract text from image
- how to load image
- improve OCR accuracy
- load image for OCR
language: tr
og_description: Herhangi bir resimde OCR nasıl çalıştırılır. Bu rehber, OCR için resmi
  nasıl yükleneceğini, resimden metni nasıl çıkaracağınızı ve AI sonrası işleme ile
  OCR doğruluğunu nasıl artıracağınızı gösterir.
og_title: OCR Nasıl Çalıştırılır – Doğru Metin Çıkarma İçin Tam Kılavuz
tags:
- OCR
- Python
- image processing
title: Görüntülerde OCR Nasıl Çalıştırılır – Adım Adım Rehber
url: /tr/python/general/how-to-run-ocr-on-images-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Nasıl Çalıştırılır – Doğru Metin Çıkarma İçin Tam Kılavuz

Ekran görüntüsünde çok sayıda yazım hatası bulunan bir resimde **how to run OCR**'ı merak ettiniz mi? Yalnız değilsiniz. Birçok projede geliştiriciler taranmış belgelerden, fişlerden ya da hatta memlerden temiz, aranabilir metin çıkarmak zorundadır ve ham çıktı karışık olabilir. İyi haber? Birkaç Python satırıyla bir resmi yükleyebilir, OCR motorunu çalıştırabilir ve ardından sonuçları AI‑destekli bir post‑processor ile artırabilirsiniz.  

Bu öğreticide bilmeniz gereken her şeyi adım adım anlatacağız: motor içine **how to load image**'dan, resimden metin çıkarmaya ve sonunda akıllı bir post‑processor kullanarak OCR doğruluğunu artırmaya. Harici hizmet yok, bugün çalıştırabileceğiniz bağımsız bir örnek.

---

## İhtiyacınız Olanlar

- **Python 3.9+** (herhangi bir yeni sürüm çalışır)
- Bir OCR motoru örneği (demo için tipik `load_image → recognize → run_postprocessor` desenini izleyen genel bir `engine` nesnesi varsayıyoruz)
- Örnek bir resim, örn. `sample_with_typos.png`, referans alabileceğiniz bir klasöre yerleştirilmiş
- Opsiyonel: bağımlılıkları düzenli tutmak için bir sanal ortam

> **Pro tip:** Tesseract kullanıyorsanız, işletim sisteminizin paket yöneticisiyle kurun ve ardından `pytesseract` gibi bir Python sarmalayıcı ile paketleyin. Aşağıdaki kod motoru soyutlar, böylece çevreleyen mantığı değiştirmeden uygulamaları değiştirebilirsiniz.

---

## 1. Adım – OCR İçin Resim Nasıl Yüklenir

İlk yapmanız gereken, OCR motorunu okumak istediğiniz dosyaya yönlendirmektir. İşte **how to load image** ifadesinin kelimenin tam anlamıyla gerçekleştiği yer: motora bir yol verirsiniz ve motor tanıma için bitmap'i hazırlar.

```python
# Step 1: Load the image into the OCR engine
ocr_engine = engine               # assume the OCR engine instance is already created
ocr_engine.load_image("YOUR_DIRECTORY/sample_with_typos.png")
```

**Neden önemli?**  
Resmi doğru şekilde yüklemek, motorun işlemek istediğiniz tam piksel verisini görmesini sağlar. Ön işleme (yeniden boyutlandırma veya gri tonlamaya dönüştürme gibi) atlamak, özellikle düşük kontrastlı taramalarda motorun karakterleri yanlış yorumlamasına neden olabilir.

---

## 2. Adım – Resimden Metin Çıkarmak İçin OCR Çalıştırma

Resim hazır olduğunda, temel OCR rutinini çağırıyoruz. Metot, `.text` özelliği ham stringi tutan bir nesne döndürür.

```python
# Step 2: Run the basic OCR to obtain the raw text output
raw_result = ocr_engine.recognize()   # returns an object with a .text attribute
```

**Ne elde edersiniz:**  
`raw_result.text` motorun algılayabildiği her kelimeyi, yazım hataları veya gürültü kaynaklı artefaktlar dahil, içerir. Bunu **raw extraction** (ham çıkarım) olarak düşünün—her türlü sonraki iyileştirmenin temeli.

---

## 3. Adım – AI‑Destekli Post‑Processing ile OCR Doğruluğunu Artırma

Çoğu modern OCR pipeline'ı post‑processing için bir kanca sunar. Örneğimizde, `run_postprocessor` yaygın yazım hatalarını düzelten, noktalama işaretlerini normalleştiren ve düzen karışık olduğunda kelimeleri yeniden sıralayan hafif bir AI modeli uygular.

```python
# Step 3: Apply the AI‑enhanced post‑processor to improve accuracy
enhanced_result = ocr_engine.run_postprocessor(raw_result)
```

**Neden bir post‑processor kullanmalı?**  
En iyi OCR motorları bile bozuk fontlar veya gürültülü arka planlarda zorlanır. AI‑tabanlı bir katman, düzeltilmiş metinlerden oluşan bir korpustan öğrenerek manuel müdahale olmadan OCR doğruluğunu büyük ölçüde **artırabilir**.

---

## 4. Adım – Hem Ham Hem AI‑Geliştirilmiş OCR Sonuçlarını Yazdırma

Farkı yan yana görmek, post‑processor'ın etkinliğini ölçmenize ve ek ayarlamaların gerekip gerekmediğine karar vermenize yardımcı olur.

```python
# Step 4: Print the raw and AI‑enhanced OCR results
print("Raw OCR:      ", raw_result.text)
print("AI‑enhanced:  ", enhanced_result.text)
```

### Beklenen Çıktı

```
Raw OCR:       Th1s 1s 4  s@mple w1th typ0s.
AI‑enhanced:   This is a sample with typos.
```

Ham çıktıda bariz hataları görebilirsiniz (`Th1s` → `This`, `4` → `a`, `s@mple` → `sample`). AI‑geliştirilmiş sürüm bunları temizleyerek insan tarafından okunabilir bir cümle sunar.

---

## Tam Çalışan Örnek (Tüm Adımlar Birleştirildi)

Aşağıda `ocr_demo.py` adlı bir dosyaya kopyalayıp yapıştırabileceğiniz tam betik yer alıyor. `"YOUR_DIRECTORY"` ifadesini resminizin gerçek yolu ile değiştirdiğinizden emin olun.

```python
# ocr_demo.py
# Complete, runnable example that shows how to run OCR,
# extract text from image, and improve OCR accuracy.

# -------------------------------------------------
# 1️⃣ Import the OCR engine (replace with your actual import)
# -------------------------------------------------
# Example placeholder:
# from my_ocr_lib import OCRengine
# engine = OCRengine()

# For this tutorial we assume `engine` is already instantiated.
# -------------------------------------------------

# -------------------------------------------------
# 2️⃣ Load the image
# -------------------------------------------------
ocr_engine = engine                     # existing OCR engine instance
ocr_engine.load_image("YOUR_DIRECTORY/sample_with_typos.png")

# -------------------------------------------------
# 3️⃣ Recognize raw text
# -------------------------------------------------
raw_result = ocr_engine.recognize()    # returns an object with .text

# -------------------------------------------------
# 4️⃣ Post‑process to improve accuracy
# -------------------------------------------------
enhanced_result = ocr_engine.run_postprocessor(raw_result)

# -------------------------------------------------
# 5️⃣ Display both results
# -------------------------------------------------
print("Raw OCR:      ", raw_result.text)
print("AI‑enhanced:  ", enhanced_result.text)
```

Run it with:

```bash
python ocr_demo.py
```

Konsola ham ve temizlenmiş stringlerin yazdırıldığını görmelisiniz; tıpkı yukarıdaki “Beklenen Çıktı” bölümünde olduğu gibi.

---

## Yaygın Sorular & Kenar Durumları

### Resmim farklı bir formatta (örneğin PDF veya TIFF) olsaydı ne olur?

Çoğu OCR motoru bir dosya yolunu kabul eder, ancak çok sayfalı PDF'ler için bir dönüşüm adımına ihtiyaç duyabilir. Motorun önüne beslemeden önce her sayfayı PNG'ye dönüştürmek için `pdf2image` kullanabilirsiniz.

### İngilizce dışındaki dilleri nasıl ele alırım?

Motoru başlatırken dil kodunu iletin, örn. `engine = OCRengine(lang='fra')`. Post‑processor da diakritik işaretleri doğru düzeltmek için dil‑spesifik bir modele ihtiyaç duyabilir.

### OCR çıktım hâlâ garip karakterler içeriyor—şimdi ne yapmalı?

Resmi ön işlemeyi düşünün:  
- **Yeniden boyutlandırma** daha yüksek DPI'ye (300 dpi iyi bir temel).  
- **Gri tonlamaya dönüştürme** renk gürültüsünü azaltmak için.  
- **Eşikleme uygulama** (`cv2.threshold`) kontrastı keskinleştirmek için.

Bu adımlar, AI post‑processor çalışmadan önce genellikle **OCR doğruluğunu artırır**.

---

## OCR İş Akışınızdan En İyi Şekilde Yararlanmak İçin İpuçları

- **Batch processing:** Görüntü klasörünü döngüye alıp her sonucu daha sonra analiz için bir CSV'ye kaydedin.  
- **Caching:** Aynı resmi birden çok kez çalıştırıyorsanız, ham sonucu önbelleğe alarak gereksiz hesaplamayı önleyin.  
- **Model updates:** Yeni düzeltilmiş örneklerle AI post‑processor'ı periyodik olarak yeniden eğitin veya güncelleyin; model zamanla iyileşir.  
- **Error logging:** `recognize()` ve `run_postprocessor()`'dan gelen istisnaları yakalayarak sorunlu dosyaları daha sonra tespit edin.

---

## Sonuç

Artık **how to run OCR**'ı herhangi bir resimde, resmi yüklemekten metin çıkarmaya ve sonunda AI‑destekli bir post‑processor ile çıktıyı parlatmaya kadar biliyorsunuz. Yukarıdaki adımları izleyerek, bir fiş tarayıcı, belge arşivleyici ya da basit bir hobi projesi geliştiriyor olsanız da, sürekli daha temiz ve güvenilir stringler elde edeceksiniz.

Bir sonraki meydan okumaya hazır mısınız? **extract text from image**'ı aranabilir bir veritabanına entegre etmeyi deneyin ya da alanınıza özel özelleştirilmiş post‑processing kurallarıyla deney yapın. Gökyüzü sınırdır ve doğru pipeline ile bir yazım hatasının tekrar kaçmasına nadiren şahit olursunuz.

Kodlamanın tadını çıkarın! 🚀

![how to run OCR example](https://example.com/ocr-demo.png "how to run OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}