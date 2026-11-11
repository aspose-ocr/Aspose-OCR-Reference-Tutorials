---
category: general
date: 2026-03-26
description: Görüntünün eğriliğini nasıl düzelteceğinizi, görüntüden metni nasıl tanıyacağınızı
  öğrenin ve taramadan gelen gürültüyü kaldırmak ve taranmış görüntüyü metne dönüştürmek
  için bir görüntü ön işleme hattı oluşturun.
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: tr
og_description: Görüntüyü düzeltme ve eğimli taramayı aranabilir metne dönüştürme.
  Görüntüden metni tanımak, taramadan gürültüyü kaldırmak ve taranmış görüntüyü metne
  dönüştürmek için bu kılavuzu izleyin.
og_title: Görüntüyü Eğri Düzeltme – Adım Adım OCR Rehberi
tags:
- OCR
- image-processing
- Python
title: Görüntüyü Düzeltme – OCR ile Tam Rehber
url: /tr/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüyü Eğikliği Giderme – OCR ile Tam Kılavuz

Uçuk bir tarayıcıdan çıkan **how to deskew image** hakkında hiç merak ettiniz mi? Yalnız değilsiniz. Eğri bir sayfa profesyonel görünmez ve daha da önemlisi, eğim, **recognize text from image** yapmaya çalışan herhangi bir OCR motorunu yanıltabilir.  

Bu öğreticide, bir taramayı eğikliği gideren, ikiliye çeviren ve gürültüyü temizleyen tam bir **image preprocessing pipeline** üzerinden geçeceğiz, ardından bir OCR motoruna aktaracağız, böylece **convert scanned image to text** işlemini minimum zahmetle yapabilirsiniz. Sihir yok, sadece sade‑vanilla Python ve işi ağır kaldıran küçük bir kütüphane.

## İhtiyacınız Olanlar

- Python 3.9+ (kod 3.10 ve daha yeni sürümlerde çalışır)
- The `ocr` package (install via `pip install ocr‑toolkit` – gerçek kütüphane adınızla değiştirin)
- Belirgin şekilde eğik bir taranmış JPEG veya PNG (örnek: `skewed_scan.jpg`)
- Her bir ön işleme adımının neden önemli olduğuna dair biraz merak

Hepsi bu. OpenCV gibi ağır bağımlılıklar yok, daha sonra daha derine inmek istemediğiniz sürece.

## Adım 1: Taranmış Görüntüyü Yükleme

İlk adım dosyayı belleğe çekmektir. Bu adım basit ama çok önemli—yol yanlışsa, her şey çökebilir.

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **Neden?**  
> Görüntüyü yüklemek, `ocr.ImagePreprocessor`'ın çalışabileceği manipüle edilebilir bir nesne sağlar. Bu adımı atlamak, pipeline'ı gerçek piksel verilerinden kör bırakır.

## Görüntüyü Eğikliği Giderme ve OCR İçin Hazırlama

Artık görüntümüz olduğuna göre, onu düzeltebiliriz. `deskew()` yöntemi eğim açısını tahmin eder ve resmi yatay konuma geri döndürür.

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **Pro ipucu:** Taramalarınız sadece hafifçe eğikse (≤ 3°), varsayılan algoritma genellikle tam isabet eder. Aşırı açılar için iç parametreleri ayarlamanız gerekebilir—`max_angle` için kütüphane belgelerine bakın.

## Görüntüyü İkiliye Çevirme – Siyah‑Beyaz Yapma

OCR motorları yüksek kontrastlı girişi sever. Resmi ikili (siyah‑beyaz) temsile dönüştürmek, karakter tanımını karıştırabilecek ince tonları ortadan kaldırır.

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **Ne oluyor?**  
> 128'den daha parlak pikseller beyaz olur; diğer tüm pikseller siyah olur. Taramanız olağandışı karanlık ya da aydınlık ise eşik değerini ayarlayın.

## OCR Öncesinde Tarama Gürültüsünü Kaldırma

Mükemmel bir şekilde eğikliği giderilmiş bir görüntü bile nokta, toz ya da sıkıştırma artefaktları içerebilir. Bu küçük lekeler, herhangi bir OCR motorunun baş belasıdır.

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **Neden gürültü kaldırılır?**  
> Gürültü, OCR motorunun karakter olarak yorumlayabileceği sahte kenarlar oluşturur. Küçük bir yarıçap çoğu tarama için işe yarar; yoğun taneli belgeler için artırın.

## Görüntü Ön İşleme Pipeline'ını Uygulama

Tüm yapılandırma ayarlandı—şimdi pipeline'ı orijinal görüntü üzerinde çalıştırıyoruz.

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **Sonuç:** `processed_image` temizlenmiş, düz, yüksek kontrastlı bir bitmap olup metin çıkarımı için hazır.

## OCR Motoru ile Görüntüden Metin Tanıma

Metni gerçekten okumak zamanı. OCR motorunu başlatıyoruz, işlenmiş görüntüyü ona veriyoruz ve ham dizeyi istiyoruz.

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Beklenen çıktı** (örnek):

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Eğer bozuk karakterler görürseniz, eğikliği giderme adımını tekrar kontrol edin ya da farklı bir `threshold` değeriyle deney yapın.

## Görüntü Ön İşleme Pipeline'ı Oluşturma – Tam Betik

Her şeyi bir araya getirerek, `.py` dosyasına koyup çalıştırabileceğiniz tek bir çalıştırılabilir betik burada:

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **İpucu:** Birçok dosyayı toplu işlemek istiyorsanız, tüm süreci bir fonksiyon içinde paketleyin (`def ocr_from_file(path): …`).

## Yaygın Sorular ve Kenar Durumları

- **Görüntü zaten dikse ne olur?**  
  `deskew()` yöntemi neredeyse sıfır açı tespit eder ve resmi dokunulmaz bırakır, böylece her dosyada güvenle çalıştırabilirsiniz.

- **Tarama renkli—korumalı mı?**  
  Renk, çoğu OCR görevine değer katmaz. Binarizasyon onu kaldırır, işleme hızını artırır ve bellek kullanımını azaltır.

- **Birden fazla ön işleme adımını zincirleyebilir miyim?**  
  Kesinlikle. `ImagePreprocessor` sınıfı pipeline'lar için tasarlanmıştır; `apply()` çağırmadan önce `sharpen()`, `contrast_enhance()` veya özel filtreler ekleyebilirsiniz.

- **OCR çıktısında istenmeyen satır sonları var—nasıl düzeltilir?**  
  Dizeyi `text.replace("\n", " ").strip()` ile son işleme tabi tutun veya Tesseract’ın `--psm` modları gibi daha gelişmiş bir yerleşim analizi kütüphanesi kullanın.

## Sonraki Adımlar

Artık **how to deskew image** ve sağlam bir **image preprocessing pipeline**'a sahip olduğunuza göre, şunları keşfedebilirsiniz:

- **recognize text from image**'ı Flask API'ye entegre ederek anlık belge yüklemeleri.
- Pipeline'ı, korunmanın kritik olduğu tarihî belgelerin **remove noise from scan** işlemi için kullanmak.
- `pdfminer` veya `PyMuPDF` kullanarak binlerce sayfayı toplu işleyip aranabilir PDF çıkarmak.

Farklı eşik değerleri, gürültü azaltma yarıçaplarıyla denemeler yapmaktan çekinmeyin, hatta çok dilli destek gerekiyorsa OCR arka ucunu Tesseract ile değiştirebilirsiniz. Temel prensip aynı kalır: düzelt, temizle, sonra oku.

---

*Kodlamaktan keyif alın! Sorun yaşarsanız, aşağıya yorum bırakın—pipeline'ı ince ayar yapmanızda memnuniyetle yardımcı olurum.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}