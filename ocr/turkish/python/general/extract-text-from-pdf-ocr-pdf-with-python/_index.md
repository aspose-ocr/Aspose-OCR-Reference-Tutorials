---
category: general
date: 2026-04-29
description: Python'da Aspose OCR kullanarak PDF'den metin çıkarın. Toplu OCR PDF
  işleme, taranmış PDF metnini dönüştürme ve düşük güvenilirlikli sayfaları yönetmeyi
  öğrenin.
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: tr
og_description: Python'da Aspose OCR ile PDF'den metin çıkarın. Bu kılavuz, toplu
  OCR PDF işleme, taranmış PDF metnini dönüştürme ve düşük güvenilirlik sonuçlarını
  ele almayı gösterir.
og_title: PDF'den Metin Çıkar – Python ile PDF OCR
tags:
- OCR
- Python
- PDF processing
title: PDF'den Metin Çıkar – Python ile OCR PDF
url: /tr/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF'den Metin Çıkarma – Python ile OCR PDF

Hiç **PDF'den metin çıkarmak** istediğinizde dosyanın sadece taranmış bir görüntü olduğunu fark ettiniz mi? Yalnız değilsiniz—birçok geliştirici PDF'leri aranabilir veri haline getirmeye çalışırken bu engelle karşılaşıyor. İyi haber? Aspose OCR for Python ile taranmış PDF metnini birkaç satırda dönüştürebilir ve hatta **toplu OCR PDF işleme** yapabilirsiniz; dosyalarınız onlarca olduğunda bile.

Bu öğreticide tüm iş akışını adım adım inceleyeceğiz: kütüphaneyi kurma, tek bir PDF üzerinde OCR çalıştırma, toplu işleme ölçeklendirme ve düşük güvenilirlikli sayfalarla başa çıkma, böylece manuel inceleme gerektiğinde bunu bileceksiniz. Sonunda, herhangi bir taranmış PDF'den metin çıkaran hazır bir betiğe sahip olacak ve her adımın nedenini anlayacaksınız.

## Gerekenler

İlerlemeye başlamadan önce şunların olduğundan emin olun:

- Python 3.8 veya daha yeni bir sürüm (kod f‑string kullandığı için 3.6+ çalışır, ancak 3.8+ tavsiye edilir)
- Aspose OCR for Python lisansı ya da ücretsiz deneme anahtarı (Aspose web sitesinden alabilirsiniz)
- İşlemek istediğiniz bir veya birden fazla taranmış PDF içeren bir klasör
- Oluşturulan *.txt* raporları için makul bir disk alanı

Hepsi bu—harici ağır bağımlılıklar yok, OpenCV gibi ek kütüphaneler de yok. Aspose OCR motoru işi sizin yerinize yapar.

## Ortamı Kurma

İlk olarak Aspose OCR paketini PyPI üzerinden yükleyin:

```bash
pip install aspose-ocr
```

Lisans dosyanız (`Aspose.OCR.lic`) varsa proje kök dizinine koyun ve şu şekilde etkinleştirin:

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **İpucu:** Lisans dosyasını sürüm kontrolünden dışarı tutun; `.gitignore` dosyanıza ekleyerek yanlışlıkla ifşa edilmesini önleyin.

## Tek PDF Üzerinde OCR Çalıştırma

Şimdi tek bir taranmış PDF'den metin çıkaralım. Temel adımlar şunlar:

1. Bir `OcrEngine` örneği oluşturun.
2. PDF dosyasını ona gösterin.
3. Her sayfa için bir `OcrResult` alın.
4. Düz metin çıktısını diske yazın.
5. Motoru serbest bırakıp yerel kaynakları temizleyin.

Tam, çalıştırılabilir betik aşağıdadır:

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**Gözleyecekleriniz:** Her sayfa için betik `Page 1: confidence 97.45%` gibi bir satır yazdırır. Eğer bir sayfa %80 eşik değerinin altına düşerse, bir uyarı gösterilir ve OCR'un karakter kaçırmış olabileceği bildirilir.

### Neden Bu Şekilde Çalışıyor

- **`OcrEngine`** yerel Aspose OCR kütüphanesine erişim sağlar; görüntü ön işleme ve karakter tanımayı kendisi yönetir.
- **`extract_from_pdf`** her PDF sayfasını otomatik olarak rasterleştirir, böylece PDF'yi ayrı ayrı görüntülere çevirmenize gerek kalmaz.
- **Güven skorları** kalite kontrollerini otomatikleştirmenize olanak tanır—özellikle doğruluğun kritik olduğu hukuk veya tıp belgeleriyle çalışırken çok önemlidir.

## Python ile Toplu OCR PDF İşleme

Gerçek dünyadaki projeler genellikle birden fazla dosya içerir. Tek‑dosya betiğini **toplu OCR PDF işleme** boru hattına genişletelim; klasörü dolaşır, her PDF'yi işler ve sonuçları eşleşen bir alt‑klasöre kaydeder.

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### Bu Nasıl Yardımcı Olur

- **Ölçeklenebilirlik:** Fonksiyon klasörü bir kez dolaşır, her PDF için ayrı bir çıktı alt‑klasörü oluşturur. Bu, onlarca belgeyle çalışırken düzeni korur.
- **Yeniden Kullanılabilirlik:** `ocr_pdf_file` diğer betiklerden (ör. bir web servisi) çağrılabilir çünkü saf bir fonksiyondur.
- **Hata yönetimi:** Giriş klasörü boşsa dostça bir mesaj yazdırır, sessiz hatalardan kaçınmanızı sağlar.

## Taranmış PDF Metnini Dönüştürme – Kenar Durumlarıyla Baş Etme

Yukarıdaki kod çoğu PDF için çalışsa da bazı tuhaflıklarla karşılaşabilirsiniz:

| Durum | Neden Oluşur | Nasıl Çözülür |
|-----------|----------------|-----------------|
| **Şifreli PDF'ler** | PDF parola korumalıdır. | `extract_from_pdf(pdf_path, password="yourPwd")` ile şifreyi geçin. |
| **Çok‑dilli belgeler** | Aspose OCR varsayılan olarak İngilizce kullanır. | `ocr_engine.language = "spa"` ile İspanyolca ayarlayın veya karışık diller için bir liste sağlayın. |
| **Çok büyük PDF'ler (>500 sayfa)** | Her sayfa RAM'e yüklendiği için bellek kullanımı artar. | `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` gibi parçalar halinde işleyin ve döngü kullanın. |
| **Kötü tarama kalitesi** | Düşük DPI veya yüksek gürültü güveni düşürür. | `engine.image_preprocessing = True` ile ön işleme etkinleştirin veya `engine.dpi = 300` ile DPI'yi artırın. |

> **Dikkat:** Görüntü ön işleme etkinleştirildiğinde CPU süresi belirgin şekilde artabilir. Gece toplu bir iş çalıştırıyorsanız yeterli zamanı planlayın ya da ayrı bir çalışan (worker) başlatın.

## Çıktıyı Doğrulama

Betik tamamlandığında aşağıdaki gibi bir klasör yapısı göreceksiniz:

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

Herhangi bir `.txt` dosyasını açın; orijinal taranmış içeriği yansıtan temiz, UTF‑8 kodlu metin görmelisiniz. Eğer bozuk karakterler fark ederseniz, PDF'nin dil ayarlarını ve makinede doğru font paketlerinin kurulu olduğunu kontrol edin.

## Kaynakları Temizleme

Aspose OCR yerel DLL'lere dayanır; bu yüzden işiniz bittiğinde `engine.dispose()` çağırmak çok önemlidir. Bu adımı atlamak, özellikle uzun süren toplu işlerde bellek sızıntılarına yol açabilir.

```python
# Always the last line of your script
engine.dispose()
```

## Tam Uçtan Uca Örnek

Her şeyi bir araya getirerek, işte tek bir

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}