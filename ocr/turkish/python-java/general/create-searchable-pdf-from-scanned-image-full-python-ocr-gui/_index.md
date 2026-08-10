---
category: general
date: 2026-07-05
description: Python ile aranabilir PDF oluşturun. Tarama yapılan bir PNG'yi OCR'lamak,
  taranmış görüntü PDF'sini dönüştürmek ve dakikalar içinde aranabilir bir PDF elde
  etmeyi öğrenin.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: tr
og_description: Aranabilir PDF'yi hızlıca oluşturun. Bu kılavuz, bir PNG'yi OCR'lamak,
  taranmış görüntü PDF'sini dönüştürmek ve Python kullanarak aranabilir bir PDF üretmek
  için nasıl yapılacağını gösterir.
og_title: Tarama Görüntüsünden Aranabilir PDF Oluştur – Python OCR Eğitimi
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: Tarama Görüntüsünden Aranabilir PDF Oluşturma – Tam Python OCR Rehberi
url: /tr/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tarama Görüntüsünden Aranabilir PDF Oluşturma – Tam Python OCR Kılavuzu

Hiç pahalı bir yazılım ödemeden taranmış bir fotoğraftan **aranabilir PDF** oluşturmayı düşündünüz mü? Yalnız değilsiniz. Birçok ofiste PDF'ler düz görüntüler olarak gelir—aramak zor, kopyala‑yapıştır imkânsız ve uyum denetimleri için bir kabus. İyi haber? Birkaç satır Python koduyla bu statik PNG'yi tamamen aranabilir bir PDF'ye dönüştürebilirsiniz ve süreç düşündüğünüzden çok daha kolay.

Bu öğreticide **tam bir OCR tanıma örneği** üzerinden adım adım ilerleyeceğiz; doğru kütüphaneyi kurmaktan son PDF dosyasını yazmaya kadar her şeyi kapsayacağız. Sonunda **taranmış görüntü PDF** dosyalarını nasıl **ocr pdf** programlı bir şekilde dönüştüreceğinizi tam olarak öğrenecek ve herhangi bir projeye ekleyebileceğiniz yeniden kullanılabilir bir betiğe sahip olacaksınız.

## Öğrenecekleriniz

- Python OCR kütüphanesini (biz `pytesseract` ve `pdf2image` kullanacağız) kurup yapılandırma.
- OCR motorunu başlatma ve dili ayarlama.
- Taranmış bir PNG'yi (veya herhangi bir görüntüyü) yükleyip OCR çalıştırma.
- OCR sonucunu **aranabilir PDF** (bayt dizisi) haline getirip kaydetme.
- Çok sayfalı belgeler, farklı diller ve yaygın tuzaklar için ipuçları.

OCR konusunda önceden deneyim gerekmez—sadece çalışan bir Python 3 ortamı ve biraz merak yeterli.

---

## Aranabilir PDF Oluşturma – Genel Bakış

Aşağıda uygulayacağımız adımların yüksek seviyeli akış diyagramı yer alıyor.  

![Aranabilir PDF oluşturma iş akışı diyagramı](https://example.com/flowchart.png "Aranabilir PDF oluşturma iş akışı diyagramı")

*Alt metin: Aranabilir PDF oluşturma iş akışı diyagramı, motor başlatma, görüntü yükleme, OCR tanıma, PDF dönüşümü ve dosya yazma adımlarını gösterir.*

---

## Adım 1: OCR Motorunu Başlatma (how to ocr pdf)

Neden bir şey başlatmamız gerekiyor? OCR motoru, piksel desenlerini karakter olarak yorumlayan beyin gibidir. Bir motor örneği oluşturup dili açıkça ayarladığımızda, kütüphane hangi alfabeyi bekleyeceğini bilir ve bu da doğruluğu büyük ölçüde artırır.

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**Pro ipucu:** Belgeleri birden fazla dilde OCR'lamak istiyorsanız, Tesseract için ilgili dil paketlerini kurun ve `ocr_language` parametresine `"eng+spa"` gibi bir liste geçin.

---

## Adım 2: Taranmış Görüntüyü Yükleme (convert scanned image pdf)

Bulmacanın bir sonraki parçası, görüntü verisini Python'a alabilmektir. Tek bir PNG'niz ya da çok sayfalı bir TIFF'iniz olsun, `PIL.Image` sınıfı bunu açabilir. Zaten taranmış görüntüler içeren bir PDF'niz varsa, `pdf2image` her sayfayı bir görüntüye dönüştürür.

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**Neden önemli:** Görüntüyü bir Pillow nesnesi olarak yüklemek, OCR motorunun ihtiyaç duyduğu ham piksel verisine erişmemizi sağlar. Bu adımı atlayıp ham baytları doğrudan vermek hatalara yol açar.

---

## Adım 3: Görüntü Üzerinde OCR Tanıma Yapma (ocr recognition example)

Şimdi eğlenceli kısım—motorun metni okumasına izin vermek. `pytesseract.image_to_pdf_or_hocr` zaten içinde görünmez bir metin katmanı barındıran bir PDF bayt akışı döndürür; bu da **aranabilir PDF** için tam ihtiyacımızdır.

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**Köşe durumu:** Görüntünüz düşük kontrastlıysa, OCR'dan önce basit bir eşikleme uygulamayı düşünün:

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

Bu küçük ön işleme adımı doğruluğu büyük ölçüde artırabilir.

---

## Adım 4: PDF Baytlarını Dosyaya Yazma (convert png searchable pdf)

OCR kütüphanesi bize bir bayt dizisi verir—bunu bir PDF dosyasının ham içeriği olarak düşünebilirsiniz. Tek yapmamız gereken bu baytları diske yazmak.

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**Gördükleriniz:** Ortaya çıkan dosyayı herhangi bir PDF görüntüleyicide açın ve orijinal görüntüde bulunduğunu bildiğiniz bir kelimeyi aramayı deneyin. Vurgulama doğrudan konuma atlamalı, görünmez metin katmanının çalıştığını kanıtlamalıdır.

---

## Adım 5: Çok Sayfalı Belgelere Genişletme (convert scanned image pdf)

Gerçek dünyadaki sözleşmeler genellikle birden fazla sayfadan oluşur. **taranmış görüntü pdf** dosyalarını birden fazla sayfa içeriyorsa, her sayfayı döngüyle OCR'layıp elde edilen PDF'leri birleştirin.

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**Neden birleştiriyoruz?** `image_to_pdf_or_hocr` her çağrıda bağımsız bir PDF üretir. Bunları birleştirmek, son belgenin orijinal sayfa sırasını korumasını sağlar.

---

## Yaygın Tuzaklar & Çözüm Önerileri

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|-------|
| PDF açıldıktan sonra aranabilir metin yok | Tesseract hiçbir karakter bulamıyor (boş çıktı) | Görüntü kalitesini kontrol edin, DPI'yi artırın veya ön işleme (kontrast, ikilileştirme) uygulayın. |
| bozuk karakterler (ör. �) | Yanlış dil paketi ya da eksik fontlar | Doğru dil verisini (`tesseract‑lang‑eng`) kurun ve `ocr_language` değerinin eşleştiğinden emin olun. |
| PDF dosya boyutu çok büyük (>10 MB tek sayfalı bir görüntü için) | Kaynak olarak kayıpsız PNG kullanılıyor; OCR tam çözünürlüklü bir görüntü ekliyor | OCR'dan önce görüntüyü küçültün (`image.thumbnail((1240, 1754))` A4 için). |
| Windows'ta “tesseract.exe not found” hatası | Tesseract ikili dosyası PATH'te yok | `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"` ekleyin (yolu ayarlayın). |

---

## Tam, Hazır‑Çalıştır Script

Hepsini bir araya getirdiğimizde, kopyalayıp çalıştırabileceğiniz tek bir dosya elde ediyoruz:

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

Bu dosyayı `create_searchable_pdf.py` olarak kaydedin, yer tutucuları gerçek yollarla değiştirin ve çalıştırın:

```bash
python create_searchable_pdf.py
```

Bir şey görmelisiniz


## Sonra Ne Öğrenmelisiniz?


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Nasıl .NET'te Aspose.OCR ile PDF OCR yapılır](/ocr/english/net/text-recognition/recognize-pdf/)
- [Görüntüleri PDF'ye Dönüştür C# – Çok Sayfalı OCR Sonucunu Kaydet](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Aspose.OCR for Java'da PDF Belgelerini OCR ile Tanıma](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}