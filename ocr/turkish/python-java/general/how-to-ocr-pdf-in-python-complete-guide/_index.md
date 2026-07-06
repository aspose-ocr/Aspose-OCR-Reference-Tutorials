---
category: general
date: 2026-06-16
description: Python ile dakikalar içinde PDF'yi OCR'lamak – PDF'den metin çıkarmayı,
  PDF üzerinde OCR çalıştırmayı ve taranmış PDF metnini verimli bir şekilde dönüştürmeyi
  öğrenin.
draft: false
keywords:
- how to OCR PDF
- extract text from PDF
- run OCR on PDF
- convert scanned PDF text
- load PDF for OCR
language: tr
og_description: 'Python ile PDF''yi OCR''lamak: PDF''den metin çıkarmak, PDF üzerinde
  OCR çalıştırmak ve taranmış PDF metnini dönüştürmek için adım adım talimatlar.'
og_title: Python'da PDF OCR Nasıl Yapılır – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to OCR PDF using Python in minutes – learn to extract text from
    PDF, run OCR on PDF, and convert scanned PDF text efficiently.
  headline: How to OCR PDF in Python – Complete Guide
  type: TechArticle
- description: How to OCR PDF using Python in minutes – learn to extract text from
    PDF, run OCR on PDF, and convert scanned PDF text efficiently.
  name: How to OCR PDF in Python – Complete Guide
  steps:
  - name: Initialized an OCR engine.
    text: Initialized an OCR engine.
  - name: Set the language (optional but recommended).
    text: Set the language (optional but recommended).
  - name: Limited the page range to speed things up.
    text: Limited the page range to speed things up.
  - name: Loaded the PDF file.
    text: Loaded the PDF file.
  - name: Ran OCR on the document.
    text: Ran OCR on the document.
  - name: '**Extracted text from PDF** for immediate use.'
    text: '**Extracted text from PDF** for immediate use.'
  - name: Exported detailed results to **convert scanned PDF text** into JSON.
    text: Exported detailed results to **convert scanned PDF text** into JSON.
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Python'da PDF'yi OCR Nasıl Yapılır – Tam Rehber
url: /tr/python-java/general/how-to-ocr-pdf-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python’da PDF’yi OCR ile Okuma – Tam Kılavuz

Hiç **PDF dosyalarını OCR ile nasıl okuyacağınızı** merak ettiniz mi? Tek başınıza değilsiniz; taranmış sayfaları aranabilir metne dönüştürmeye çalışan sayısız geliştirici aynı sorunu yaşıyor. İyi haber? Birkaç satır Python koduyla bir PDF’yi OCR için yükleyebilir, PDF sayfalarında OCR çalıştırabilir ve temiz, düzenlenebilir metinleri saniyeler içinde elde edebilirsiniz.

Bu öğreticide, PDF belgelerini nasıl OCR yapacağınızı, PDF sayfalarından metin çıkaracağınızı ve hatta taranmış PDF metnini JSON‑yapısına dönüştüreceğinizi gösteren gerçek bir örnek üzerinden adım adım ilerleyeceğiz. Gereksiz ayrıntı yok, sadece bugün projenize ekleyebileceğiniz çalışan bir betik.

## Gerekenler

- Python 3.8+ (herhangi bir yeni sürüm yeterli)
- `ocr` kütüphanesi (veya uyumlu bir sarmalayıcı – burada gösterilen API’ye uyan genel bir `ocr` paketi varsayıyoruz)
- İşlemek istediğiniz çok sayfalı taranmış PDF
- Tercih ettiğiniz IDE veya editör (VS Code, PyCharm, hatta basit bir metin editörü)

Hepsi bu. Bu gereksinimlere sahipseniz, PDF dosyalarından profesyonelce metin çıkarmaya hazırsınız.

## Adım 1 – OCR Motorunu Kurun (How to OCR PDF)

İlk iş: bir OCR motoru örneği oluşturun. Motor, belgenizdeki her pikseli okuyacak beyin gibidir.

```python
# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

> **Pro ipucu:** Motoru başlatmak maliyetli değildir, ancak bir toplu işlemde onlarca PDF işliyorsanız aynı `engine` nesnesini yeniden kullanarak bellek tasarrufu sağlayabilirsiniz.

![Diagram of the OCR pipeline illustrating how to OCR PDF](/images/ocr-pdf-workflow.png "How to OCR PDF workflow")

## Adım 2 – Doğru Dili Seçin (Run OCR on PDF)

Taramalarınız İngilizce ise dili açıkça ayarlayın. Bu adımı atlamak motorun tahmin yapmasına neden olur; bu da daha yavaş ve bazen daha az doğru sonuçlar verir.

```python
# Step 2 (optional): Set language to English
engine.language = ocr.Language.ENGLISH
```

Neden? Çünkü motorun **PDF üzerinde OCR çalıştırması** için bilinen bir dili belirtmek, tanıma oranlarını büyük ölçüde artırır—özellikle teknik terimler içeren belgelerde.

## Adım 3 – Belirli Sayfalara Odaklanın (Load PDF for OCR)

500 sayfalık dev bir arşivi işlemek, sadece ilk birkaç bölüme ihtiyacınız varsa gereksizdir. Sayfa aralığını şu şekilde sınırlayabilirsiniz:

```python
# Step 3 (optional): Process only pages 1‑5
engine.pdf_page_range = (1, 5)
```

Bu küçük ayar, motorun **PDF’yi OCR için yüklemesini** ancak sadece ihtiyacınız olan sayfalara dokunmasını sağlar; zaman ve CPU tasarrufu sağlar.

## Adım 4 – Belgenizi Yükleyin (Load PDF for OCR)

Şimdi motoru gerçek dosyaya yönlendirin. Yolun doğru olduğundan emin olun; aksi takdirde `FileNotFoundError` alırsınız.

```python
# Step 4: Load the multi‑page PDF file
engine.load_from_file("YOUR_DIRECTORY/multipage-document.pdf")
```

Bu noktada motor **PDF’yi OCR için yüklemiş**, iç yapıyı ayrıştırmış ve ağır işi yapmaya hazırdır.

## Adım 5 – Tanıma İşlemini Başlatın (Run OCR on PDF)

İşte sihrin gerçekleştiği an. `recognize()` çağrısı her pikseli tarar, dil modellerini uygular ve zengin bir sonuç nesnesi döndürür.

```python
# Step 5: Run OCR on the loaded document
pdf_result = engine.recognize()
```

Arka planda motor **PDF sayfalarında OCR çalıştırır**, metin katmanları oluşturur ve her kelime için güven skorları tutar.

## Adım 6 – Tüm Metni Çıkarın (Extract Text from PDF)

Çoğu kullanım senaryosu sadece düz metni ister. `text` özelliği, motorun gördüğü her şeyin birleştirilmiş dizesini verir.

```python
# Step 6: Retrieve the combined text of the entire PDF
print("Full PDF text:\n", pdf_result.text)
```

Artık **PDF’den metin çıkardınız**—arama indeksi, veritabanı ya da basit bir `print()` için hazır.

## Adım 7 – Ayrıntılı Sonuçları İnceleyin (Convert Scanned PDF Text)

Sadece ham dizeler yeterli değilse—örneğin sınırlayıcı kutular veya güven skorları istiyorsanız—JSON dışa aktarımını kullanın. Bu, temelde **taranmış PDF metnini** makine‑okunur bir formata dönüştürmektir.

```python
# Step 7: View detailed OCR results for each page in JSON
print(pdf_result.to_json(indent=2))
```

JSON, sayfa başına diziler içerir; her giriş tanınan metni, sayfadaki konumunu ve bir güven metriğini tutar. Varlık çıkarımı veya özel vurgulama gibi sonraki işlemler için mükemmeldir.

## Yaygın Tuzaklar ve Çözüm Önerileri

| Sorun | Neden Oluşur | Hızlı Çözüm |
|-------|--------------|------------|
| **Garbage karakterler** | Yanlış dil veya eksik fontlar | `engine.language` değerini doğru dile açıkça ayarlayın. |
| **Eksik sayfalar** | `pdf_page_range` çok dar | `(başlangıç, bitiş)` çiftinin belgenizle eşleştiğini kontrol edin. |
| **Performans yavaşlığı** | Büyük PDF’ler tek seferde işleniyor | PDF’yi parçalara bölün veya `concurrent.futures` ile sayfaları paralel işleyin. |
| **Boş çıktı** | Dosya yolu hatalı veya PDF okunamıyor | Dosyanın var olduğunu ve şifre korumalı olmadığını doğrulayın. |

Bu sorunları erken aşamada ele almak, ileride saatler süren hata ayıklamayı önler.

## Örneği Genişletmek

- **Toplu işleme:** Bir klasördeki PDF’ler üzerinde döngü kurarak aynı `engine` örneğini yeniden kullanın.
- **Özel çıktı:** `pdf_result.text` değerini bir `.txt` dosyasına yazın ya da doğrudan Elasticsearch gibi bir arama motoruna besleyin.
- **Görsel çıkarma:** Bazı OCR kütüphaneleri sayfa başına görüntüler sunar; bunları görsel doğrulama için dışa aktarabilirsiniz.

İşte bir klasörü toplu işlemek için küçük bir kod parçacığı:

```python
import pathlib, json

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    engine.load_from_file(str(pdf_path))
    result = engine.recognize()
    (pdf_folder / f"{pdf_path.stem}.txt").write_text(result.text)
    (pdf_folder / f"{pdf_path.stem}.json").write_text(result.to_json(indent=2))
    print(f"Processed {pdf_path.name}")
```

## Özet – Neler Öğrendik

Python’da **PDF’yi OCR ile nasıl okuyacağınızı** sorduktan sonra:

1. Bir OCR motoru başlattık.
2. Dili ayarladık (isteğe bağlı ama tavsiye edilir).
3. Sayfa aralığını sınırlayarak hızı artırdık.
4. PDF dosyasını yükledik.
5. Belge üzerinde OCR çalıştırdık.
6. **PDF’den metin çıkardık** ve hemen kullanıma hazır hale getirdik.
7. Ayrıntılı sonuçları **taranmış PDF metnini** JSON’a dönüştürerek dışa aktardık.

Bu adımlar, herhangi bir taranmış PDF’yi aranabilir, düzenlenebilir içeriğe dönüştürmek için sağlam bir temel oluşturur.

## Sonraki Adımlar

- Farklı dilleri deneyin (`ocr.Language.SPANISH`, `ocr.Language.FRENCH`) ve motorun çok dilli belgelerle nasıl başa çıktığını görün.
- Tarama kaliteniz düşükse `engine.dpi` ayarını değiştirin—daha yüksek DPI, doğruluğu artırabilir.
- OCR çıktısını spaCy gibi doğal dil işleme kütüphaneleriyle birleştirerek varlıkları, tarihleri veya anahtar ifadeleri otomatik olarak çıkarın.

**load PDF for OCR** ile ilgili sorularınız ya da **run OCR on PDF** sırasında takıldığınız bir nokta mı var? Aşağıya yorum bırakın, birlikte çözelim. İyi kodlamalar ve o inatçı taramaları aranabilir altına dönüştürmenin tadını çıkarın!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalarla tam çalışan kod örnekleri içerir; böylece ek API özelliklerini öğrenebilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}