---
category: general
date: 2026-03-18
description: PNG'den metin çıkarmak ve aranabilir PDF oluşturmak için görüntüde OCR
  çalıştırın. Metin görüntüsünü tanımayı ve PNG'yi dakikalar içinde PDF'ye dönüştürmeyi
  öğrenin.
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: tr
og_description: PNG'den metin çıkarmak için görüntüde OCR çalıştırın, metin görüntüsünü
  tanıyın ve aranabilir bir PDF oluşturun. Bu adım adım kılavuzu izleyin.
og_title: Görüntüde OCR Çalıştır – PNG'den Metni Hızlıca Çıkar
tags:
- OCR
- Python
- Image Processing
title: Görselde OCR Çalıştır – PNG'den Metni Hızlıca Çıkar
url: /tr/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüde OCR Çalıştırma – PNG'den Metni Hızlıca Çıkarma

Hiç **run OCR on image** dosyalarını çalıştırmanız gerekti, ama nereden başlayacağınızı bilmiyor muydunuz? Belki taranmış bir makaleniz `article.png` olarak kaydedildi ve sadece düz metni istiyorsunuz, ya da arşivleme için aranabilir bir PDF'ye ihtiyacınız var. Hangi durumda olursanız olun, doğru yerdesiniz. Bu öğreticide PNG'den metin çıkarmayı, metin görüntüsünü tanımayı ve hatta bu PNG'yi aranabilir bir PDF'ye dönüştürmeyi—birkaç satır kodla—adım adım göstereceğiz.

> **Ne elde edeceksiniz:** PNG'yi yükleyen, OCR çalıştıran, hOCR çıktısını kaydeden ve isteğe bağlı olarak aranabilir bir PDF oluşturan tam, çalıştırılabilir bir betik. Eksik importlar yok, “belgelere bak” gibi çıkmazlar yok—bugün projenize ekleyebileceğiniz bağımsız bir çözüm.

## Önkoşullar

- **Python 3.8+** (burada kullanılan sözdizimi herhangi bir yeni sürümde çalışır)
- Kullandığınız **`ocr_engine`** kütüphanesi (örnek, `OcrEngine` adlı bir sınıf varsayar; gerekirse Tesseract, EasyOCR vb. ile değiştirin)
- İşlemek istediğiniz bir PNG görüntüsü (örneğin `article.png` bir klasöre yerleştirilmiş)
- Çıktı dizinine yazma izni

Eğer Tesseract'ı altyapı olarak kullanıyorsanız, şu şekilde kurun:

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

Ardından Python sarmalayıcısını kurun:

```bash
pip install pytesseract Pillow
```

*Pro tip:* OCR kütüphanenizi güncel tutun—yeni dil paketleri ve performans iyileştirmeleri sık sık eklenir.

## Görüntüde OCR Çalıştırma – Adım Adım Kılavuz

Aşağıda **tam script** bulunuyor. `run_ocr.py` adlı bir dosyaya kopyalayıp yapıştırabilir ve `python run_ocr.py` ile çalıştırabilirsiniz.

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### Betik ne yapıyor, sade bir dille

1. **Instantiate** OCR motorunu başlatın, böylece ayarlarını kontrol edebilirsiniz.
2. **Load** PNG dosyasını (`article.png`) yükleyin. Dosya yoksa betik erken durur—sonradan gizemli `NoneType` hataları oluşmaz.
3. **Select** `hocr`'yi dışa aktarma formatı olarak seçin. Bu format, orijinal düzeni korur ve daha sonra görüntüyü aranabilir bir PDF'ye dönüştürmek için gereklidir.
4. **Run** tanıma motorunu çalıştırın; zor iş burada gerçekleşir.
5. **Write** hOCR XML'ini `article.hocr` dosyasına yazın. Artık metnin ve koordinatlarının makine tarafından okunabilir bir temsiline sahipsiniz.
6. *(Opsiyonel)* `"pdf"`'ye geçin ve ekstra bir adımda aranabilir bir PDF oluşturun.

**Beklenen çıktı**, şu şekilde görünen (kısaltılmış) UTF‑8 kodlu bir `.hocr` dosyasıdır:

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

PDF bölümünün yorumunu kaldırırsanız, `article_searchable.pdf` dosyasına da sahip olursunuz; bu dosyayı herhangi bir PDF görüntüleyicide açabilir ve **Ctrl + F** arama kutusunu kullanarak kelimeleri anında bulabilirsiniz.

![Görüntüde OCR Çalıştırma örnek çıktısı](example.png "Görüntüde OCR Çalıştırma – hOCR ve PDF sonuçları")

## OcrEngine Kullanarak PNG'den Metin Nasıl Çıkarılır

Eğer sadece ham metin (düzen, PDF yok) ihtiyacınız varsa, hOCR adımını tamamen atlayabilirsiniz:

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*Neden düz metin seçilmeli?* Hafiftir, indeksleme için mükemmeldir ve sonraki NLP işlem hatlarıyla harika çalışır.

## Metin Görüntüsünü Tanı ve Aranabilir PDF Oluştur

Aranabilir bir PDF oluşturmak iki aşamalı bir süreçtir:

1. **Run OCR** `hocr` ile (yukarıda yaptığımız gibi) düzen bilgilerini alın.
2. **Combine** orijinal PNG'yi hOCR ile birleştirerek motorun PDF dışa aktarıcısını kullanarak PDF oluşturun.

Çoğu modern OCR kütüphanesi (Tesseract, ABBYY, Google Vision) tam olarak bunu yapan bir `pdf` dışa aktarımı sunar. Ana betiğin *Opsiyonel* bloğundaki kod parçacığı bu deseni gösterir. Kütüphanenizde yerleşik bir PDF dışa aktarıcı yoksa, **`pdf2image`** + **`reportlab`** kullanarak görüntüyü ve hOCR'yi birleştirebilirsiniz—bana bildirin, hızlı bir ek örnek paylaşırım.

## OCR Çıktısı ile PNG'yi PDF'ye Dönüştür

Bazen sadece görüntüyü içeren **düz PDF** (aranabilir katman yok) istersiniz. Bu daha da basittir:

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

Eğer aranabilir bir sürüme ihtiyacınız varsa bu adımı OCR ile birleştirin, ya da arşivleme amaçlı sadık bir görsel kopya olarak tutun.

## Yaygın Tuzaklar ve İpuçları

| Sorun | Neden Oluşur | Hızlı Çözüm |
|-------|----------------|-----------|
| **Bulanık veya düşük çözünürlüklü PNG** | OCR doğruluğu ~300 DPI'nin altına düştüğünde büyük ölçüde azalır. | Motorun önüne göndermeden önce `Image.resize((width*2, height*2), Image.LANCZOS)` ile ölçeklendirin. |
| **Yanlış dil** | Motor varsayılan olarak İngilizce'yi kullanır; İngilizce dışı karakterler bozulur. | `recognize()`'den önce `ocr_engine.setLanguage('deu')` (veya uygun ISO kodu) çağırın. |
| **Eksik hOCR çıktısı** | `setExportFormat` çağrılmadığında bazı motorlar varsayılan olarak düz metin verir. | `setExportFormat("hocr")`'in **recognize()**'den **önce** çalıştığını iki kez kontrol edin. |
| **Dosya izin hataları** | Yalnızca okunabilir bir klasöre yazmaya çalışmak. | Önce projeniz içinde bir yol kullanın ya da `os.makedirs(..., exist_ok=True)` ile klasörü oluşturun. |
| **Büyük PDF'ler bellek dalgalanmalarına neden olur** | PDF dışa aktarıcı tüm görüntüyü RAM'de tutar. | Sayfaları parçalar halinde işleyin ya da akış tabanlı bir PDF yazıcı kullanın. |

*Pro tip:* her zaman binlerce görüntüye ölçeklendirmeden önce küçük bir örnek görüntüde test edin. Bu, saatlerce hata ayıklamayı önler.

## Özet

Artık **run OCR on image** dosyalarını nasıl çalıştıracağınızı, **PNG'den metin çıkaracağınızı**, sonraki görevler için **metin görüntüsünü tanıyacağınızı**, **aranabilir bir PDF oluşturacağınızı** ve basit bir arşiv gerektiğinde **PNG'yi PDF'ye dönüştüreceğinizi** biliyorsunuz. Sağlanan betik, kutudan çıkar çıkmaz çalışan tam bir kopyala‑yapıştır çözümüdür ve opsiyonel bölümler çıktıyı tam iş akışınıza göre özelleştirmenizi sağlar.

### Sırada ne var?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}