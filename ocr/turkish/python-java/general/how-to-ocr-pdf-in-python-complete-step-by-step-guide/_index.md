---
category: general
date: 2026-06-06
description: Python kullanarak PDF'yi OCR'lamak, PDF'den metin çıkarmak, taranmış
  PDF metnini dönüştürmek ve sadece birkaç satır kodla OCR dilini değiştirmek.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert scanned pdf text
- perform ocr on pdf
- change ocr language
language: tr
og_description: 'Python ile PDF OCR: PDF''den metin çıkarmayı, taranmış PDF metnini
  dönüştürmeyi ve OCR dilini zahmetsizce değiştirmeyi gösteren pratik bir rehber.'
og_title: Python'da PDF OCR Nasıl Yapılır – Tam Programlama Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Python, extract text from PDF, convert scanned
    PDF text, and change OCR language in just a few lines of code.
  headline: How to OCR PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Python'da PDF'yi OCR ile İşlemek – Tam Adım Adım Rehber
url: /tr/python-java/general/how-to-ocr-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da PDF OCR Nasıl Yapılır – Tam Adım‑Adım Kılavuz

Pahalı SaaS araçları ödemeden **PDF OCR nasıl yapılır** dosyalarını merak ettiniz mi? Tek başınıza değilsiniz. İster eski kitapları dijitalleştiriyor olun, faturalarından veri çekiyor olun, ya da sadece taranmış bir rapordan aranabilir metne ihtiyacınız olsun, Python'da PDF OCR'ı ustalaşmak saatlerce manuel kopyalamayı tasarruf ettirebilir.

Bu öğreticide, **extracts text from PDF**, **convert scanned PDF text** ve **change OCR language** nasıl yapılır gösteren kısa ve çalışan bir örnek üzerinden ilerleyeceğiz. Sonunda, herhangi bir projeye ekleyebileceğiniz yeniden kullanılabilir bir kod parçacığına sahip olacaksınız.

## Önkoşullar ve Kurulum

- Python 3.8+ yüklü (kod 3.9, 3.10 ve daha yeni sürümlerde çalışır)
- `ocr` paketi, `OcrEngine` sınıfını sağlar (`pip install ocr-lib` ile kurabilirsiniz – kullandığınız gerçek paket adıyla değiştirin)
- İşlemek istediğiniz bir PDF dosyası; demo için `high_res_book.pdf` dosyasını `YOUR_DIRECTORY` adlı klasöre koyacağız

Sanal bir ortam (şiddetle önerilir) kullanıyorsanız, önce onu etkinleştirin:

```bash
python -m venv .venv
source .venv/bin/activate   # on Windows: .venv\Scripts\activate
pip install ocr-lib
```

> **Pro tip:** PDF dosyalarınızı daha sonra yol‑ile ilgili sorunlardan kaçınmak için ayrı bir `data/` dizini altında tutun.

## Adım 1: Bir OCR Motoru Örneği Oluşturun (PDF OCR Nasıl Yapılır – Başlatma)

PDF dosyalarında **perform OCR on PDF** istediğinizde yapmanız gereken ilk şey motoru örneklemektir. Motoru, her sayfayı okuyacak, glifleri yorumlayacak ve size düz metin döndürecek bir beyin olarak düşünün.

```python
# Step 1: Create an OCR engine instance
engine = OcrEngine()
```

Neden önemli: bir motor olmadan dil ayarları, render seçenekleri veya PDF işleme bağlamına sahip olmazsınız. `OcrEngine` nesnesi tüm bu varsayılanları tutar ve daha sonra ayarlamanıza izin verir.

## Adım 2: Tanıma Dilini Ayarlayın (OCR Dilini Değiştirme)

Çoğu OCR kütüphanesi varsayılan olarak İngilizce'dir, ancak belgeniz Fransızca, Almanca ya da hatta Japonca ise ne olur? Dili değiştirmek, `set_recognition_language` çağırmak kadar basittir. Bu, **change OCR language** gereksinimini karşılar ve daha yüksek doğruluk sağlar.

```python
# Step 2: Set the recognition language to English (or any supported language)
engine.set_recognition_language(ocr.Language.ENGLISH)   # swap ENGLISH for FRANCAIS, etc.
```

> **Neden buna ihtiyaç duyabilirsiniz:** Çok dilli bir arşiv genellikle karışık‑dil sayfaları içerir. Dilleri anında değiştirmek, “ß” veya “ñ” gibi karakterlerin hatalı tanınmasını önler.

## Adım 3: PDF Render Seçeneklerini Yapılandırın (Taranmış PDF Metnini Etkili Bir Şekilde Dönüştürme)

Taranmış PDF'lerle çalışırken, çözünürlük ve renk modu OCR kalitesini büyük ölçüde etkiler. Çoğu belge için 300 DPI'de gri tonlamada render etmek, detayları yakalamak için yeterli ama bellek kullanımını makul tutmak için düşük bir denge noktasıdır.

```python
# Step 3: Configure PDF rendering options (300 DPI, grayscale)
engine.pdf_render_options() \
      .set_dpi(300) \
      .set_color_mode("grayscale")
```

Zincirleme çağrılar şık görünebilir, ancak her seferinde aynı seçenekler nesnesini döndüren akıcı bir API'dir. Renk gerekiyorsa (ör. renkli diyagramlar için), `"grayscale"` yerine `"color"` kullanın.

## Adım 4: PDF'yi Tanıyın ve İlk Sayfa Metnini Alın (PDF'ten Metin Çıkarma)

Şimdi **how to OCR PDF**'in çekirdeği geliyor: motoru bir dosya yolu ile beslemek ve tanınan metni çıkarmak. Metot, sayfa sonuçlarının bir listesini döndürür; her sonuç bir `text` özelliği içerir.

```python
# Step 4: Recognize the PDF and print the text of the first page
results = engine.recognize_pdf("YOUR_DIRECTORY/high_res_book.pdf")
print(results[0].text)   # Text from the first page
```

Tüm belgeye ihtiyacınız varsa, `results` üzerinde döngü yapın:

```python
for i, page in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(page.text)
```

### PDF Şifreli Olursa Ne Olur?

Bazı PDF'ler şifre korumalı gelir. Bu durumda şifreyi `recognize_pdf` metoduna geçirebilirsiniz:

```python
results = engine.recognize_pdf(
    "YOUR_DIRECTORY/secure_doc.pdf",
    password="mySecret123"
)
```

Motor, OCR gerçekleştirmeden önce anlık olarak şifreyi çözer—ek bir adım gerekmez.

## Adım 5: Çıkarılan Metni Son İşleme (PDF'ten Metin Çıkarma İnce Ayarı)

Ham OCR çıktısı genellikle satır sonları, fazladan boşluklar veya zaman zaman hatalı tanınan karakterler içerir. Hızlı bir temizlik rutini, çıkarılan dizeyi sonraki işlemler (arama indeksleme, veritabanı depolama vb.) için hazır hâle getirir.

```python
import re

def clean_ocr_text(raw: str) -> str:
    # Remove multiple spaces and line breaks
    text = re.sub(r'\s+', ' ', raw)
    # Strip leading/trailing whitespace
    return text.strip()

clean_text = clean_ocr_text(results[0].text)
print(clean_text)
```

Artık güvenle **extract text from PDF** yapabilir ve herhangi bir NLP boru hattına, arama motoruna veya basit bir `open(...).write()` işlemine besleyebilirsiniz.

## Bonus: Birden Çok PDF'i Toplu İşleme (PDF'te OCR Performansını Ölçeklendirme)

Eğer içinde taranmış PDF'ler dolu bir klasörünüz varsa, mantığı bir döngü içinde sarın:

```python
import pathlib

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    print(f"Processing {pdf_path.name} …")
    pages = engine.recognize_pdf(str(pdf_path))
    full_text = "\n".join(page.text for page in pages)
    cleaned = clean_ocr_text(full_text)

    # Save the extracted text alongside the PDF
    txt_path = pdf_path.with_suffix(".txt")
    txt_path.write_text(cleaned, encoding="utf-8")
    print(f"Saved extracted text to {txt_path.name}")
```

Bu kod parçacığı, toplu olarak **perform OCR on PDF** dosyalarını nasıl yapacağınızı gösterir; bu, dijitalleştirme projelerinde yaygın bir ihtiyaçtır.

## Beklenen Çıktı

Tek sayfalık örneği (Adım 4) çalıştırmak aşağıdakine benzer bir çıktı vermelidir:

```
In the beginning God created the heavens and the earth. Now the earth was formless …
```

Eğer çok sayfalı bir kitap işlediyseniz, konsol her sayfanın temizlenmiş metnini gösterecek ve toplu script her PDF'in yanına bir `.txt` dosyası bırakacaktır.

## Yaygın Tuzaklar ve Nasıl Kaçınılır

| Sorun | Belirtiler | Çözüm |
|-------|------------|-------|
| Düşük çözünürlüklü kaynak PDF | Bozuk karakterler, eksik kelimeler | DPI'yi artırın (`set_dpi(400)` veya daha yüksek) |
| Yanlış dil ayarı | Birçok bilinmeyen sembol, özellikle aksanlı karakterler | `engine.set_recognition_language(ocr.Language.FRENCH)` veya uygun enum'u kullanın |
| Büyük PDF bellek hatasına neden oluyor | `MemoryError` veya birkaç sayfadan sonra çökme | Sayfaları parçalar halinde işleyin (`engine.recognize_pdf(..., max_pages=10)`) |
| PDF'de eksik fontlar | Belirli sayfalar için boş çıktı | PDF'in gerçekten raster görüntüler içerdiğinden emin olun; bazı PDF'ler yalnızca vektör olup farklı bir işleme ihtiyaç duyar |

## Görsel Açıklama

Aşağıda iş akışının hızlı bir görseli bulunmaktadır. Alt metin kasıtlı olarak SEO‑dostudur.

![pdf ocr nasıl yapılır iş akışı diyagramı, motor başlatma, dil ayarı, render seçenekleri, tanıma ve metin çıkarma](/images/ocr-workflow.png)

*Diyagram kodun çalışması için gerekli değildir, ancak görsel öğrenenlerin her adımın nerede olduğunu görmesine yardımcı olur.*

## Sonuç

Python'da **how to OCR PDF** dosyalarını baştan sona ele aldık: bir OCR motoru oluşturma, **changing OCR language**, render'ı **convert scanned PDF text** için yapılandırma ve sonunda **extracting text from PDF** işlemiyle metni elde etme. Tam, çalıştırılabilir örnek herhangi bir projeye eklenmeye hazır ve isteğe bağlı toplu script çözümü nasıl ölçeklendireceğinizi gösteriyor.

Next, you might want to explore:

- Çok dilli arşivler için bir dil listesi üzerinden döngü yaparak **perform OCR on PDF** eklemek.
- Çıkarılan metni Elasticsearch ile tam metin arama için entegre etmek.
- OCR kullanarak metin katmanını orijinal dosyaya geri yerleştirerek aranabilir PDF'ler oluşturmak (birçok kütüphane `save_as_searchable_pdf` metodunu sunar).

Dilediğiniz gibi denemeler yapın, DPI ayarlarını değiştirin veya farklı bir OCR arka ucuna geçin. Temeller aynı kalır ve artık üzerine inşa edebileceğiniz sağlam bir temele sahipsiniz.

Kodlamaktan keyif alın, ve taranmış belgeleriniz nihayet aranabilir olsun!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}