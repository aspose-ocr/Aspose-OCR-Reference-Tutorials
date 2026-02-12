---
category: general
date: 2025-12-27
description: Aspose OCR kullanarak görüntüden metin çıkarın ve OCR hatalarını düzeltin.
  OCR için görüntüyü nasıl yükleyeceğinizi öğrenin ve hataları hızlıca düzeltin.
draft: false
keywords:
- extract text from image
- load image for ocr
- how to correct ocr errors
- Aspose OCR Python
- OCR post‑processing
language: tr
og_description: Aspose OCR ile görüntüden metin çıkarın ve OCR hatalarını anında düzeltin.
  OCR için görüntüyü yüklemek ve sonuçları temizlemek için bu öğreticiyi izleyin.
og_title: Aspose OCR ile Görüntüden Metin Çıkarma – Tam Kılavuz
tags:
- OCR
- Python
- Aspose
- Text Extraction
title: Aspose OCR ile Görüntüden Metin Çıkarma – Adım Adım Kılavuz
url: /tr/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR ile Görüntüden Metin Çıkarma – Adım‑Adım Kılavuz

Görselden **metin çıkarmak** gerektiğinde, dağınık OCR çıktısı içinde kaybolduğunuz oldu mu? Yalnız değilsiniz. Birçok otomasyon projesinde—fatura işleme, fiş tarama veya eski belgeleri dijitalleştirme gibi—ilk engel, bir resimden temiz, aranabilir metin elde etmektir.  

Bu öğreticide, **load image for OCR** nasıl yapılır, tanıma nasıl çalıştırılır ve ardından Aspose'un AI destekli imla denetimi sonrası işlemcisi ile **OCR hatalarını düzeltir** gösteren eksiksiz, çalıştırılabilir bir örnek üzerinden geçeceğiz. Sonunda, bir fatura PNG'sini, aklınızdaki herhangi bir sonraki iş akışı için hazır, düzenli ve aranabilir metne dönüştüren tek bir betiğe sahip olacaksınız.

## Öğrenecekleriniz

- Python'da Aspose OCR ve AI kütüphanelerinin nasıl kurulup içe aktarılacağını.  
- **load image for OCR** için gereken tam kodu (tahmin yok).  
- OCR motorunu nasıl çalıştırıp ham dizeyi yakalayacağınızı.  
- OCR'nin neden sık sık yazım hataları ürettiğini ve yerleşik imla denetimi işlemcisinin **OCR hatalarını** otomatik olarak nasıl **düzeltilebileceğini**.  
- Çok sayfalı PDF'ler veya düşük çözünürlüklü taramalar gibi uç durumları ele almak için ipuçları.

> **Önkoşullar:** Python 3.8+, geçerli bir Aspose OCR lisansı (veya ücretsiz deneme), ve işlemek istediğiniz bir görüntü dosyası (ör. `invoice.png`).

---

## Görüntüden Metin Çıkarma – Aspose OCR Kurulumu

Herhangi bir şeye başlamadan önce doğru paketlere ihtiyacımız var. Aspose, OCR motorunu pip ile kurulabilir bir modül olarak dağıtır.

```bash
pip install aspose-ocr
```

Ayrıca AI son işlemcisini de istiyorsanız yardımcı paketi yükleyin:

```bash
pip install aspose-ocr-ai
```

> **Pro ipucu:** Paketlerinizi güncel tutun. Bu yazının yazıldığı tarihte en son sürümler `aspose-ocr 23.12` ve `aspose-ocr-ai 23.12`.

Kütüphaneler sisteminize girdikten sonra kullanacağınız sınıfları içe aktarın:

```python
# Step 1: Import the OCR and AI classes
from aspose.ocr import OcrEngine, AsposeAI
```

> **Neden önemli:** Belirli sınıfları içe aktarmak ad alanını temiz tutar ve hangi bileşenlerin tanıma, hangilerinin sonrası işleme sorumlu olduğunu açıkça gösterir.

---

## OCR için Görüntü Yükleme – Fatura PNG'nizi Hazırlama

Bir sonraki mantıklı adım, motoru okumak istediğiniz dosyaya yönlendirmektir. İşte burada **load image for OCR** ​​anahtar kelimesi önem kazanıyor.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 3: Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Açıklama:** `OcrEngine()` varsayılan ayarlarla (İngilizce dil, otomatik döndürme vb.) yeni bir motor oluşturur. `load_image()` yöntemi bir dosya yolu, bir akış veya hatta bir bayt dizisini kabul eder—bu sayede görüntüleri diskten, web'den veya bellek içi bir tampondan besleyebilirsiniz.

### Görüntü Yüklerken Yaygın Tuzaklar

| Sorun | Belirti | Çözüm |
|-------|---------|------|
| Düşük DPI (<300) | Bozuk karakterler, eksik sayılar | Görüntüyü yüklemeden önce 300 dpi veya daha yüksek bir değere yeniden örnekleyin |
| Yanlış renk modu (CMYK) | Yanlış karakter şekilleri | Pillow kullanarak RGB'ye dönüştürün (`Image.convert("RGB")`) |
| Çok sayfalı PDF | Sadece ilk sayfa işleniyor | Her sayfayı bir görüntüye dönüştürün ve döngüyle işleyin |

---

## OCR Yap ve Ham Metni Al

Artık motor resmin nerede olduğunu bildiğine göre, onu gerçekten okuyabiliriz.

```python
# Step 4: Perform OCR to extract raw text
raw_text = ocr_engine.recognize()
print("Raw OCR output:")
print(raw_text)
```

`recognize()` çağrısı düz bir Python dizesi döndürür. Birçok gerçek dünya senaryosunda, özellikle yoğunlaştırılmış yazı tipleri kullanan fişlerde, çıktı gereksiz boşluklar, yanlış okunan karakterler veya bozuk satır sonları içerecektir.

> **Neden önce raw_text'i yakalıyoruz:** Daha sonra temizlenmiş sürümle karşılaştırmak için bir temel sağlar; bu, hata ayıklama veya denetleme için faydalıdır.

---

## OCR Hatalarını Düzeltme – Aspose AI İmla Denetimi Kullanma

Aspose, ham çıktıya bir imla denetimi sonrası işlemcisi çalıştırabilen hafif bir AI sarmalayıcı sunar. Bu, **OCR hatalarını nasıl düzeltiriz** sorusuna doğrudan yanıt verir.

```python
# Step 5: Initialise the AI post‑processor and choose a spell‑check processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("spell_check")
```

You can swap `"spell_check"` for other processors like `"grammar_check"` or `"named_entity_recognition"` if your use‑case demands it.

```python
# Step 6: Clean the OCR output using the selected post‑processor
clean_text = ai_processor.run_postprocessor(raw_text)

# Step 7: Output the corrected text
print("\nCorrected OCR output:")
print(clean_text)
```

### İmla Denetimi Arkada Ne Yapıyor

1. **Tokenizasyon** – Ham dizeyi kelimelere ve noktalama işaretlerine ayırır.  
2. **Sözlük Sorgulaması** – Her tokeni bir İngilizce sözlük (veya sağlayabileceğiniz özel bir sözlük) ile karşılaştırır.  
3. **Bağlamsal Puanlama** – Küçük bir dil modeli kullanarak düzeltmenin çevredeki kelimelere uyup uymadığını belirler.  
4. **Değiştirme** – En olası düzeltmeler uygulanmış yeni bir dize döndürür.

> **Köşe durum:** Kaynak dil İngilizce değilse, `AsposeAI()` oluştururken uygun dil kodunu geçirin (ör. `AsposeAI(language="fr")`).

---

## Temizlenmiş Metni Doğrulama ve Kullanma

Bu noktada iki değişkeniniz var: `raw_text` (doğrudan OCR çıktısı) ve `clean_text` (yazım denetimi yapılmış sürüm). Hangisini saklayacağınız, sonraki ihtiyaçlarınıza bağlıdır.

```python
# Example: Save the cleaned text to a .txt file for later indexing
with open("invoice_extracted.txt", "w", encoding="utf-8") as f:
    f.write(clean_text)

print("\n✅ Cleaned text saved to invoice_extracted.txt")
```

Sonucu bir arama motoruna, veritabanına veya makine öğrenme modeline besliyorsanız, her zaman **temizlenmiş** sürümü tercih edin; aksi takdirde OCR gürültüsünü tüm işlem hattınıza yayarsınız.

---

## Tam Çalışan Örnek

Aşağıda, `extract_invoice.py` adlı bir dosyaya kopyalayıp yapıştırabileceğiniz tam komut dosyası bulunmaktadır. Bu komut dosyası, iki Aspose paketini zaten yüklediğinizi ve `YOUR_DIRECTORY/invoice.png` adresinde bir resminiz olduğunu varsaymaktadır.

```python
# extract_invoice.py
# -------------------------------------------------------------
# Complete example: extract text from image and correct OCR errors
# -------------------------------------------------------------

# 1️⃣ Import required classes
from aspose.ocr import OcrEngine, AsposeAI

# 2️⃣ Create OCR engine and load the target image
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

# 3️⃣ Run OCR – get raw text
raw_text = ocr_engine.recognize()
print("Raw OCR output:")
print(raw_text)

# 4️⃣ Initialise AI spell‑check post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("spell_check")

# 5️⃣ Clean the OCR output
clean_text = ai_processor.run_postprocessor(raw_text)

# 6️⃣ Show the corrected result
print("\nCorrected OCR output:")
print(clean_text)

# 7️⃣ Persist the cleaned text for later use
with open("invoice_extracted.txt", "w", encoding="utf-8") as out_file:
    out_file.write(clean_text)

print("\n✅ Cleaned text saved to invoice_extracted.txt")
```

Run it with:

```bash
python extract_invoice.py
```

Önce ham dökümü, ardından daha düzenli bir sürümünü göreceksiniz ve aynı klasörde `invoice_extracted.txt` adlı bir dosya belirecektir.

---

## Sıkça Sorulan Sorular (SSS)

**S: Bu PDF'lerle çalışır mı?**  
C: Doğrudan değil. Her PDF sayfasını bir görüntüye (ör. `pdf2image` kullanarak) dönüştürün ve betiği ortaya çıkan PNG'ler üzerinde döngüye alın.

**S: Dilim İngilizce değil—yine de imla denetimini kullanabilir miyim?**  
C: Evet. `AsposeAI(language="de")` gibi istediğiniz dil kodunu geçirin; Almanca için `"de"`, İspanyolca için `"es"` vb.

**S: OCR motoru tablo düzenini yanlış algılarsa ne olur?**  
C: Aspose OCR, `set_layout_analysis(True)` bayrağını sunar. Etkinleştirmek tablo algılamayı iyileştirir ancak işlem süresini artırabilir.

**S: Çok büyük toplu işlemleri nasıl yönetirim?**  
C: Çekirdek mantığı bir fonksiyon içinde paketleyin ve bir iş parçacığı havuzu veya async IO kullanarak birden fazla çekirdek veya makine üzerinde paralelleştirin.

---

## Özet

Aspose OCR kullanarak **görselden metin çıkarmayı**, **OCR için görüntü yüklemeyi** ve yerleşik AI imla denetimi ile **OCR hatalarını düzeltmenin** en basit yolunu gösterdik. Eksiksiz, çalıştırılabilir betik, fatura PNG'sini yüklemekten temiz, aranabilir bir `.txt` dosyasına kaydetmeye kadar uçtan uca akışı gösteriyor.

Deney yapmaktan çekinmeyin: imla denetimini dilbilgisi düzeltmesiyle değiştirin, çıktıyı bir NLP sınıflandırıcısına besleyin veya süreci daha büyük bir belge yönetim sistemine entegre edin. Güvenilir, düzeltilmiş metin elde ettiğinizde sınır yoktur.

OCR, Aspose veya Python otomasyonu hakkında daha fazla sorunuz mu var? Aşağıya bir yorum bırakın, iyi kodlamalar!

![Görselden metin çıkarma örneği](extract_text_image.png "Aspose OCR ile Görselden Metin Çıkarma")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}