---
category: general
date: 2026-06-06
description: Python kullanarak PDF'yi OCR'leyin ve görüntülerden aranabilir PDF dosyaları
  oluşturun. Dakikalar içinde aranabilir metin eklemeyi ve görüntüyü PDF/A'ya dönüştürmeyi
  öğrenin.
draft: false
keywords:
- how to ocr pdf
- create searchable pdf
- add searchable text
- ocr image to pdf
- convert image to pdf/a
language: tr
og_description: PDF'yi adım adım OCR'lamak. Basit bir Python betiğiyle aranabilir
  metin eklemeyi ve görüntüyü PDF/A'ya dönüştürmeyi öğrenin.
og_title: PDF'yi OCR'lamak – Aranabilir PDF'ler Oluşturmak için Hızlı Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  headline: How to OCR PDF in Python – Create Searchable PDF from Images
  type: TechArticle
- description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  name: How to OCR PDF in Python – Create Searchable PDF from Images
  steps:
  - name: Why this matters
    text: '- **Preserving graphics** means the visual layout (tables, logos, stamps)
      stays exactly as the scanner captured it. - The `result` object typically contains
      a hidden text layer that we’ll later embed into the PDF. - Using `recognize_image`
      instead of `recognize_pdf` avoids an extra conversion step, '
  - name: Why this matters
    text: '- **Searchable PDF**: The output file contains a hidden, selectable text
      layer. You can now Ctrl + F through the document. - **PDF/A compliance**: Some
      organizations (legal, finance) require PDF/A for audit trails; this step satisfies
      that rule automatically. - The method also **adds searchable text'
  - name: Expected output
    text: 'When you run the script, the console prints:'
  type: HowTo
tags:
- OCR
- PDF
- Python
- Automation
title: Python'da PDF'yi OCR ile İşlemek – Görsellerden Aranabilir PDF Oluşturma
url: /tr/python-java/general/how-to-ocr-pdf-in-python-create-searchable-pdf-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF'yi OCR'lamak – Tarama Görüntülerini Aranabilir PDF'lere Dönüştürmek

Hiç **PDF'yi OCR'lamak** istediğinizde elinizde sadece bir fatura ya da makbuzun taranmış görüntüsü olduğunu düşündünüz mü? Tek başınıza değilsiniz. Birçok ofiste gelen evraklar düz PNG ya da JPEG dosyaları olarak gelir ve bir sonraki adım—içeriği aranabilir hâle getirmek—bir kara kutu gibi görünür.  

İyi haber? Sadece birkaç satır Python ile **aranabilir PDF** dosyaları **oluşturabilir**, **aranabilir metin ekleyebilir** ve hatta **görüntüyü PDF/A'ya dönüştürebilirsiniz** uzun vadeli arşivleme için. Bu öğreticide her adımı adım adım inceleyecek, neden önemli olduğunu açıklayacak ve herhangi bir projeye ekleyebileceğiniz çalıştırmaya hazır bir betik sunacağız.

> **Pro tip:** Aynı yaklaşım çok sayfalı taramalar için de çalışır; sadece dosyalar üzerinde döngü kurun ve motor ağır işi halleder.

---

## Gereksinimler

İşe başlamadan önce makinenizde aşağıdakilerin olduğundan emin olun:

| Gereksinim | Neden Önemli |
|-------------|----------------|
| Python 3.9 ve üzeri | Modern sözdizimi ve daha iyi kütüphane desteği |
| `pdfium`‑tabanlı OCR motoru (ör. `pdfocr` veya ticari bir SDK) | Hem görüntü tanıma hem de PDF/A üretimini yönetir |
| Aranabilir PDF'ye dönüştürmek istediğiniz bir görüntü dosyası (PNG, JPEG, TIFF) | Metnin kaynağı |
| Çıktı klasörüne yazma izni | Betiğin yeni PDF'yi kaydedebilmesi için |

OCR SDK'sını henüz kurmadıysanız, şu komutu çalıştırın:

```bash
pip install pdfocr   # replace with your vendor's package name
```

Hepsi bu—karmaşık sistem bağımlılıkları yok, sadece bir pip kurulumu.

---

## PDF'yi OCR'lamak – Genel Bakış

Yüksek seviyede süreç üç basit adımdan oluşur:

1. **Metni** görüntünün içinde tanı, orijinal grafikleri koruyarak.  
2. OCR sonucunu **aranabilir PDF/A** (arşiv dostu PDF çeşidi) olarak orijinal görüntüyle birlikte dışa aktar.  
3. Oluşan dosyanın, orijinal resmin üzerine seçilebilir, aranabilir bir metin katmanı içerdiğini **doğrula**.

Aşağıda her adımı kod içinde görecek, komutların *neden* gerektiğini açıklayacağız.

---

## Adım 1: Görüntüden Metni Tanıma

İlk olarak OCR motoruna pikselleri okumasını ve hem ham görüntüyü hem de çıkarılan metni tutan bir sonuç nesnesi döndürmesini söylüyoruz. Motorun faturayı sizin için “okuduğunu” düşünün.

```python
# Step 1: Recognize text from the image and keep the original graphics
result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

### Neden Önemli

- **Grafiklerin korunması**, görsel düzenin (tablolar, logolar, damgalar) tarayıcı tarafından yakalanan haliyle kalmasını sağlar.  
- `result` nesnesi genellikle PDF'ye daha sonra gömeceğimiz gizli bir metin katmanı içerir.  
- `recognize_image` kullanmak, `recognize_pdf` yerine ekstra bir dönüşüm adımını ortadan kaldırır; tek sayfalı görüntülerde işleme süresini hızlandırır.

#### Yaygın varyasyonlar

- **Çok sayfalı TIFF** dosyanız varsa, dosya yolunu doğrudan geçirin; çoğu motor her sayfayı ayrı bir görüntü olarak işler.  
- Zaten içinde görüntü barındıran PDF'ler için `engine.recognize_pdf("file.pdf")` çağrısı yapabilir ve bu adımı tamamen atlayabilirsiniz.

---

## Adım 2: OCR Sonucunu Aranabilir PDF/A Olarak Dışa Aktarma

Şimdi adım 1'deki `result` nesnesini alıp motorun yeni bir dosya yazmasını sağlıyoruz. Buradaki kilit bayrak *PDF/A*—uzun vadeli koruma için tasarlanmış ISO‑standart PDF sürümüdür.

```python
# Step 2: Export the OCR result together with the original image as a searchable PDF/A
result.save_as_pdfa("YOUR_DIRECTORY/invoice_searchable.pdf")
```

### Neden Önemli

- **Aranabilir PDF**: Çıktı dosyası gizli, seçilebilir bir metin katmanı içerir. Artık belge içinde Ctrl + F yapabilirsiniz.  
- **PDF/A uyumu**: Bazı kuruluşlar (hukuk, finans) denetim izleri için PDF/A zorunluluğu getirir; bu adım kuralı otomatik olarak karşılar.  
- Metod aynı zamanda **aranabilir metni** eklerken görüntüyü düzleştirmez, böylece görsel bütünlük mükemmel kalır.

#### Kenar durumu: Normal PDF mi istiyorsunuz?

PDF/A ile ilgilenmiyorsanız, `save_as_pdfa` yerine `save_as_pdf` kullanın. İş akışının geri kalanı aynı kalır.

---

## Adım 3: Aranabilir PDF'yi Doğrulama

Kısa bir tutarlılık kontrolü, ileride ortaya çıkabilecek gizemli hatalardan sizi korur. Oluşturulan dosyayı herhangi bir PDF görüntüleyicide açın, bir kelimeyi seçmeye çalışın ve arama fonksiyonunu kullanın.

```python
# Step 3: The file "invoice_searchable.pdf" now contains selectable text layered over the original invoice image
import subprocess, os

pdf_path = "YOUR_DIRECTORY/invoice_searchable.pdf"
if os.path.exists(pdf_path):
    print(f"✅ PDF created successfully: {pdf_path}")
    # Optionally open the file (works on macOS, Windows, Linux with appropriate commands)
    subprocess.run(["open", pdf_path] if os.name == "posix" else ["start", pdf_path], shell=True)
else:
    print("❌ Something went wrong – PDF not found.")
```

### Beklenen çıktı

Betik çalıştırıldığında konsola şu bilgiler basılır:

```
✅ PDF created successfully: YOUR_DIRECTORY/invoice_searchable.pdf
```

Dosyayı açtığınızda, orijinal fatura görüntüsünün üzerine hafif, görünmez bir metin katmanı olduğunu görmelisiniz. Herhangi bir kelimeyi vurguladığınızda seçilebilir olduğunu fark edeceksiniz—**tam da eklediğiniz aranabilir metin**.

---

## Mevcut PDF'lere Aranabilir Metin Ekleme (Bonus)

Bazen zaten bir PDF'niz olur ve **aranabilir metin** eklemeniz gerekir. Aynı motor OCR sonuçlarını mevcut bir PDF üzerine bindirebilir:

```python
# Bonus: Add searchable text to an existing PDF file
existing_pdf = engine.load_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result = engine.recognize_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result.apply_to(existing_pdf).save_as_pdfa("YOUR_DIRECTORY/old_scanned_searchable.pdf")
```

Burada `apply_to`, gizli katmanı orijinal sayfalarla birleştirir ve **yeniden taramaya gerek kalmadan aranabilir PDF** oluşturmanızı sağlar.

---

## Yaygın Tuzaklar ve İpuçları

| Tuzak | Nasıl Önlenir |
|---------|-----------------|
| **Düşük çözünürlüklü kaynak görüntüler** (< 150 dpi) | Görüntüyü yükseltin veya daha yüksek çözünürlükte tarama talep edin; OCR doğruluğu 150 dpi altında ciddi şekilde düşer. |
| **Eksik dil verisi** | OCR motorunuz için uygun dil paketlerini kurun (`pip install pdfocr[eng,spa]`). |
| **Çıktı klasörü yazılabilir değil** | Betiği yeterli izinlerle çalıştırın veya farklı bir dizin seçin. |
| **PDF/A doğrulaması başarısız** | Desteklenmeyen fontları veya JavaScript'i gömmediğinizden emin olun; çoğu SDK `save_as_pdfa` kullandığınızda bunu otomatik halleder. |

---

## Tam Betik – Tek‑Dosya Çözümü

Aşağıda her şeyi bir araya getiren, bağımsız bir betik bulunuyor. Kopyalayıp yapıştırın, yer tutucu yolları değiştirin ve **görüntüyü PDF/A'ya** saniyeler içinde dönüştürmeye hazır olun.

```python
#!/usr/bin/env python3
"""
How to OCR PDF – Complete script to create a searchable PDF/A from an image.
Works with any OCR engine exposing `recognize_image` and `save_as_pdfa`.
"""

import os
import subprocess

# ----------------------------------------------------------------------
# CONFIGURATION – change these paths to match your environment
# ----------------------------------------------------------------------
INPUT_IMAGE = "YOUR_DIRECTORY/invoice.png"
OUTPUT_PDF  = "YOUR_DIRECTORY/invoice_searchable.pdf"

# ----------------------------------------------------------------------
# INITIALIZE THE OCR ENGINE (replace with your SDK's init call)
# ----------------------------------------------------------------------
# Example for a fictional `pdfocr` package:
# from pdfocr import Engine
# engine = Engine(api_key="YOUR_API_KEY")
# If you use a different library, adjust the import and init accordingly.
engine = Engine()  # placeholder – insert real initialization here

def main():
    # Step 1 – Recognize the image
    print(f"🔎 Recognizing text from {INPUT_IMAGE} …")
    result = engine.recognize_image(INPUT_IMAGE)

    # Step 2 – Save as searchable PDF/A
    print(f"💾 Saving searchable PDF/A to {OUTPUT_PDF} …")
    result.save_as_pdfa(OUTPUT_PDF)

    # Step 3 – Verify the file exists
    if os.path.isfile(OUTPUT_PDF):
        print("✅ Success! Searchable PDF/A created.")
        # Open the file for a quick visual check (optional)
        try:
            if os.name == "posix":
                subprocess.run(["open", OUTPUT_PDF])
            else:
                subprocess.run(["start", OUTPUT_PDF], shell=True)
        except Exception:
            pass
    else:
        print("❌ Error: PDF not created.")

if __name__ == "__main__":
    main()
```

**Bu betik ne yapar:**  
1. OCR motorunu yükler.  
2. Seçilen görüntüyü okur ve metni çıkarır.  
3. **Aranabilir PDF/A** yazar; hemen dağıtabilir veya arşivleyebilirsiniz.  

`main` mantığını bir fonksiyona sarıp bir klasörü işlemek isterseniz—sadece `os.listdir()` ile döngü kurun ve her dosya için üç adımı tekrarlayın.

---

## Sonraki Adımlar & İlgili Konular

Artık **PDF'yi OCR'lamak** konusunda uzmanlaştığınıza göre, aşağıdaki ileri fikirleri keşfetmeyi düşünün:

- **Toplu işleme:** `concurrent.futures` kullanarak onlarca faturayı paralel olarak OCR'layın.  
- **Metadata ekleme:** PDF metadata'sına oluşturma tarihleri veya fatura numaraları ekleyerek indekslemeyi kolaylaştırın.  
- **Hibrit PDF'ler:** Aranabilir metni gömülü orijinal görüntülerle birleştirerek “dijital ikiz” oluşturun.  
- **Alternatif çıktılar:** Alt sistemlerin düzenlenebilir formatlara ihtiyacı varsa **DOCX** ya da **HTML** olarak dışa aktarın.

Bu konular, yeni öğrendiğiniz temel kavramlar—tanıma, dışa aktarma, doğrulama—üzerine inşa edilir.

---

## Özet

Kısaca, sadece üç satır Python ile basit bir görüntüyü **aranabilir PDF/A**'ya dönüştürerek **PDF'yi OCR'lamak** konusunda uzmanlaştınız. Betik ağır işi halleder, orijinal grafikleri korur ve arama, arşivleme veya paylaşım için standartlara uygun bir belge sunar.  

Kendi faturalarınız, makbuzlarınız veya taranmış sözleşmelerinizle deneyin. Sorun yaşarsanız, aşağıya yorum bırakın ya da SDK'nın resmi dokümantasyonuna göz atın—genellikle ekstra örneklerle doludur. İyi kodlamalar ve herhangi bir görüntüyü anında aranabilir hâle getirme yeteneğinin tadını çıkarın! 

![PDF'yi OCR'lamak örneği, orijinal görüntü ve aranabilir PDF katmanı gösteriyor](placeholder.png "PDF'yi OCR'lamak örneği")


## Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, tam çalışan kod örnekleri ve adım adım açıklamalar içerir; böylece ek API özelliklerini ustalaşabilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}