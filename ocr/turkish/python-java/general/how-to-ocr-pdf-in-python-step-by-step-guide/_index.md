---
category: general
date: 2026-03-28
description: Python ile PDF'yi hızlıca OCR yapmayı öğrenin. Bu rehber, PDF'den metin
  çıkarmayı, PDF'deki metni tanımayı ve taranmış PDF'yi Aspose OCR kullanarak metne
  dönüştürmeyi gösterir.
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: tr
og_description: Python ile PDF OCR'ını nasıl yapacağınızı öğrenin. PDF'den metin çıkarın,
  PDF'den metni tanıyın ve taranmış PDF'yi dakikalar içinde metne dönüştürün.
og_title: Python'da PDF OCR Nasıl Yapılır – Tam Kılavuz
tags:
- PDF
- OCR
- Python
- Aspose
title: Python’da PDF’yi OCR’lamak – Adım Adım Kılavuz
url: /tr/python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python’da PDF OCR Nasıl Yapılır – Adım‑Adım Kılavuz

Bir dosya sadece bir sayfanın fotoğrafı olduğunda **PDF OCR nasıl yapılır** diye merak ettiniz mi? Tek başınıza değilsiniz. Bu öğreticide PDF dosyalarını OCR ile işlemek, PDF’ten metin çıkarmak ve taranmış bir PDF’yi aranabilir metne dönüştürmek için tam adımları göstereceğiz – hepsi sade Python kodu ile.

Aspose OCR kütüphanesinin kurulumundan her sayfanın tanınan metnini almaya kadar her şeyi ele alacağız. Sonunda **Python ile PDF OCR**, **PDF’ten metin çıkarma** ve **taranmış PDF’yi metne dönüştürme** işlemlerini dağınık dokümanlar arasında kaybolmadan yapabilecek olacaksınız. Gereksiz ayrıntı yok, sadece kopyalayıp‑yapıştırabileceğiniz çalıştırılabilir bir örnek.

## Gereksinimler

Başlamadan önce şunların olduğundan emin olun:

* Python 3.8+ (en yeni kararlı sürüm en iyisidir)  
* Aspose OCR for Python lisansı ya da ücretsiz deneme anahtarı – Aspose web sitesinden alabilirsiniz.  
* İşlemek istediğiniz taranmış PDF (biz buna `input.pdf` diyeceğiz).  

Eğer bunlar zaten elinizdeyse harika—başlayalım. Yoksa paketi kurmak çok kolay ve nasıl yapılacağını göstereceğiz.

## PDF OCR – Ortamı Hazırlama

İlk yapmanız gereken Aspose OCR modülünü makinenize getirmek. Paketin adı `aspose-ocr` ve pip ile kurulabilir:

```bash
pip install aspose-ocr
```

> **İpucu:** Bağımlılıklarınızı düzenli tutmak için bir sanal ortam (`python -m venv venv`) kullanın.

Paket kurulduktan sonra import edip OCR motorunu başlatmaya hazırsınız. Bu, daha sonra oluşturacağınız her **ocr pdf with python** iş akışının temelini oluşturur.

## Python’da PDF OCR – Aspose OCR’u İçe Aktarma

Kütüphane artık kullanılabilir olduğuna göre, onu betiğimize ekleyelim. Motoru *direct PDF mode*’da çalışacak şekilde ayarlayacağız; bu, Aspose’un PDF baytlarını doğrudan dosyadan okumasını, her sayfayı önce görüntüye dönüştürmemesini sağlar.

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

Neden `PdfMode.DIRECT` kullanıyoruz? Çünkü ekstra rasterleştirme adımını atlayarak süreci hızlandırır ve orijinal düzeni korur—özellikle **recognize text from PDF** işlemini doğru yapmak istediğinizde çok işe yarar.

## PDF’ten Metin Tanıma – Motoru Çalıştırma

Motor hazır olduğunda, taranmış dosyanıza yönlendirin. `recognize_from_pdf` metodu tüm işi yapar: her sayfayı ayrıştırır, OCR algoritmasını çalıştırır ve `OcrResult` nesnesi içinde `Page` nesnelerinin bir koleksiyonunu döndürür.

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

Şifreli PDF’lerle çalışıp çalışmadığını merak ediyorsanız—evet, `ocr_engine.password = "secret"` satırını `recognize_from_pdf` çağrısından önce eklediğiniz sürece çalışır. Birçok öğreticide atlanan bu durum, gerçek dünyadaki akışlarda oldukça faydalıdır.

## PDF’ten Metin Çıkarma – Sayfa Sonuçlarına Erişim

`ocr_result.pages` listesi her sayfa için bir giriş tutar. Her `Page` nesnesinin `.text` özelliği, taranmış sayfanın düz metin temsilini içerir. Döngüyle geçelim ve sonuçları ekrana yazdıralım, böylece tam olarak ne çıkarıldığını görebilirsiniz.

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

Betik çalıştırıldığında aşağıdakine benzer bir çıktı alırsınız:

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Bu çıktı, **extract text from PDF** ve **recognize text from PDF** işlemlerini Aspose OCR ile başarıyla gerçekleştirdiğinizi kanıtlar. Artık bu metinleri bir veritabanına, arama indeksine ya da herhangi bir sonraki NLP işlem hattına yönlendirebilirsiniz.

![how to ocr pdf example](placeholder-image.png "how to ocr pdf example")

*Görsel alt metni:* **how to ocr pdf example** – sayfa başına tanınan metnin konsol çıktısını gösterir.

## Taranmış PDF’yi Metne Dönüştürme – Çıktıyı Kaydetme

Çoğu geliştirici sadece konsolda metni görmek istemez; kalıcı bir dosyaya ihtiyaç duyar. Aşağıda, her sayfanın metnini ayrı bir `.txt` dosyasına yazan küçük bir yardımcı kod bulunuyor; bu sayede **convert scanned PDF to text** işlemini `output` adlı klasörde gerçekleştirirsiniz.

```python
import os

output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Betik tamamlandığında düzenli bir dizininiz olur:

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

Artık **convert scanned PDF to text** işlemini tam olarak yaptınız ve bu dosyaları herhangi bir sonraki süreçte—arama, analiz ya da basit bir `grep`—kullanabilirsiniz.

## Yaygın Sorular & Kenar Durumlar

**PDF’imde gerçek metinle karışık görüntüler varsa ne olur?**  
Aspose OCR her şeyi tanımaya çalışır, ancak seçilebilir metin zaten bulunan sayfalarda OCR’ı devre dışı bırakarak işlemi hızlandırabilirsiniz. `ocr_engine.auto_detect_page_orientation = True` ayarlayın ve bilinen iyi sayfalar için `ocr_engine.recognize_from_pdf(..., detect_text=False)` çağrısını yapın.

**Dil modelini kontrol edebilir miyim?**  
Kesinlikle. `ocr_engine.language = aocr.Language.English` (veya desteklenen başka bir dil) ayarını `recognize_from_pdf` çağrısından önce yapın. Bu, İngilizce dışı belgelerde doğruluğu artırır.

**100+ sayfalık çok büyük PDF’lerle nasıl başa çıkılır?**  
Parçalara bölerek işleyin. `recognize_from_pdf` metodu bir `page_range` argümanı alır; örneğin `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))`. Bellek kullanımını düşük tutmak için aralıklar üzerinden döngü kurun.

## Tam Çalışan Örnek

Hepsini bir araya getirdiğimizde, `ocr_pdf.py` adlı bir dosyaya koyup çalıştırabileceğiniz tek bir betik elde edersiniz:

```python
import os
import aspose.ocr as aocr

# -------------------------------------------------
# 1️⃣  Initialize the OCR engine (direct PDF mode)
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
# Optional: set language for better accuracy
ocr_engine.language = aocr.Language.English

# -------------------------------------------------
# 2️⃣  Path to the scanned PDF you want to process
# -------------------------------------------------
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# -------------------------------------------------
# 3️⃣  Run OCR – this is where we actually recognize text from PDF
# -------------------------------------------------
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)

# -------------------------------------------------
# 4️⃣  Print the extracted text (shows how to extract text from PDF)
# -------------------------------------------------
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)

# -------------------------------------------------
# 5️⃣  Save each page as a .txt file (convert scanned PDF to text)
# -------------------------------------------------
output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Şu komutla çalıştırın:

```bash
python ocr_pdf.py
```

Her sayfanın metnini ve kaydedilen `.txt` dosyalarının konumunu onaylayan bir konsol çıktısı görmelisiniz.

## Sonuç

**Python ile PDF OCR** nasıl yapılır, **ocr pdf with python** için temiz bir yol gösterdik, **PDF’ten metin çıkarma** ve **recognize text from PDF** mekaniklerini anlattık ve son olarak **convert scanned PDF to text** işlemini gerçekleştiren hazır bir snippet sunduk. Tüm süreç

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}