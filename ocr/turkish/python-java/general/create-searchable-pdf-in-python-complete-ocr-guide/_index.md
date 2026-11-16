---
category: general
date: 2026-06-22
description: OCR kullanarak Python’da aranabilir PDF oluşturun – görüntüyü PDF’ye
  dönüştürmeyi, metin PDF’sini tanımayı öğrenin ve iş akışınızı otomatikleştirin.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- recognize text pdf
- python ocr pdf
language: tr
og_description: OCR kullanarak Python'da aranabilir PDF oluşturun. Görüntüyü PDF'ye
  dönüştürmek, metin PDF'sini tanımak ve belge işleme otomasyonunu sağlamak için bu
  adım adım öğreticiyi izleyin.
og_title: Python’da aranabilir PDF oluşturma – Tam OCR rehberi
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  headline: Create searchable PDF in Python – Complete OCR Guide
  type: TechArticle
- description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  name: Create searchable PDF in Python – Complete OCR Guide
  steps:
  - name: Initialise the OCR engine
    text: The first thing you do is spin up an `OcrEngine` object. Think of it as
      turning on a scanner that’s ready to read your image.
  - name: Load the image you want to convert
    text: Next we feed the engine with an image stream. The `ImageStream.from_file`
      helper reads the file and wraps it in a format the OCR engine understands.
  - name: Tell the engine to output a searchable PDF
    text: By default many OCR SDKs output plain text. We need to switch the output
      format to PDF so the resulting file is both visual and searchable.
  - name: Prepare an in‑memory stream for the PDF data
    text: Instead of writing directly to disk, we capture the PDF in a `MemoryStream`.
      This keeps I/O fast and lets you pipe the bytes elsewhere (e.g., upload to S3)
      if you wish.
  - name: Run the recognition and write the PDF
    text: Now the heavy lifting happens. The `recognize` call reads the image, runs
      OCR, and streams the searchable PDF into `pdf_stream`.
  - name: Save the generated PDF to a file
    text: Finally, we dump the bytes from the memory stream onto disk. The resulting
      file can be opened in Adobe Reader, Preview, or any PDF viewer with full‑text
      search.
  type: HowTo
tags:
- OCR
- Python
- PDF
title: Python'da Aranabilir PDF Oluşturma – Tam OCR Rehberi
url: /tr/python-java/general/create-searchable-pdf-in-python-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da aranabilir PDF oluşturma – Tam OCR Rehberi

Tar scanned bir sözleşmeden **searchable PDF oluşturma** ihtiyacı hiç duydunuz mu ama nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz—birçok geliştirici, bir bitmap görüntüyü metin‑aranabilir bir belgeye dönüştürmeye ilk kez çalıştıklarında aynı duvara çarpar. İyi haber şu ki, küçük bir Python betiğiyle **convert image to PDF** yapabilir, OCR motorunun her kelimeyi tanımasını sağlayabilir ve tamamen aranabilir bir dosyayla sonuçlanabilirsiniz.

Bu öğreticide, doğru kütüphaneyi kurmaktan çok sayfalı belgeler gibi uç durumları ele almaya kadar tüm süreci adım adım inceleyeceğiz. Sonuna geldiğinizde **ocr image to pdf**, **recognize text pdf** yapabilecek ve iş akışını daha büyük otomasyon hatlarına entegre edebileceksiniz.

## İhtiyacınız olanlar

İçeriğe girmeden önce, makinenizde aşağıdakilerin olduğundan emin olun:

| Gereksinim | Neden önemli |
|-------------|----------------|
| Python 3.8 or newer | Modern sözdizimi ve daha iyi tip ipuçları |
| `ocr` Python package (or any compatible OCR SDK) | `OcrEngine`, `ImageStream` ve PDF çıktısı sağlar |
| A scanned image (JPEG, PNG, or TIFF) | Dönüştüreceğiniz kaynak |
| Write access to a folder for the output PDF | Oluşturulan dosyayı kaydedebilmeniz için |

Eğer SDK'yı henüz kurmadıysanız, şu komutu çalıştırın:

```bash
pip install ocr-sdk   # replace with the actual package name
```

> **Pro ipucu:** Bağımlılıkları düzenli tutmak için bir sanal ortam (`python -m venv .venv`) kullanın.

## İş akışının genel görünümü

1. **Create an OCR engine instance** – tanımanın arkasındaki beyin.  
2. **Load the image** – işlemek istediğiniz görüntüyü yükleyin.  
3. **Configure the engine** – motoru düz metin yerine aranabilir PDF üretmesi için yapılandırın.  
4. **Prepare an in‑memory stream** – PDF baytlarını tutacak bir bellek içi akış hazırlayın.  
5. **Run the recognition** – motor görüntüyü okur, metni çıkarır ve PDF'yi yazar.  
6. **Persist the PDF to disk** – böylece herhangi bir görüntüleyicide açabilirsiniz.  

Bu, kodun sadece altı satırında tüm hikaye. Şimdi her adımı ayrıntılandıralım.

---

## Aranabilir PDF Oluşturma – Adım‑Adım Python OCR Öğreticisi

### Adım 1: OCR motorunu başlatma

İlk yapmanız gereken bir `OcrEngine` nesnesi oluşturmak. Bunu, görüntünüzü okumaya hazır bir tarayıcıyı açmak gibi düşünün.

```python
import ocr

# Initialise the OCR engine – this is where all the magic begins
engine = ocr.OcrEngine()
```

> **Neden önemli:** Motoru örneklemek, iç tamponları ayırır ve dil verilerini yükler. Bu adımı atlamak, görüntüyü ayarlamaya çalıştığınızda `NoneType` hatasına neden olur.

### Adım 2: Dönüştürmek istediğiniz görüntüyü yükleyin

Sonra motoru bir görüntü akışıyla besleriz. `ImageStream.from_file` yardımcı fonksiyonu dosyayı okur ve OCR motorunun anlayacağı bir formatta sarar.

```python
# Load the source image – replace the path with your own file
image_path = "YOUR_DIRECTORY/contract.jpg"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

> **Uç durum:** Kaynağınız çok sayfalı bir TIFF ise, bunun yerine `ocr.MultiPageImageStream.from_file` kullanın. Motor, her sayfayı otomatik olarak ayrı bir PDF sayfası olarak ele alır.

### Adım 3: Motoru aranabilir PDF üretmesi için söyleyin

Varsayılan olarak birçok OCR SDK'sı düz metin üretir. Çıktı formatını PDF'ye geçirmemiz gerekir, böylece ortaya çıkan dosya hem görsel hem de aranabilir olur.

```python
# Configure the engine to produce a searchable PDF
engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
```

> **Arka planda ne oluyor?** Motor, bitmap'in arkasına görünmez bir metin katmanı ekler, böylece yerel bir PDF'de olduğu gibi kelimeleri arayabilirsiniz.

### Adım 4: PDF verileri için bellek içi bir akış hazırlayın

Doğrudan diske yazmak yerine, PDF'yi bir `MemoryStream` içinde yakalarız. Bu, I/O'yu hızlı tutar ve isterseniz baytları başka bir yere (ör. S3'e yükleme) yönlendirmenizi sağlar.

```python
# Create a memory buffer that will receive the PDF bytes
pdf_stream = ocr.MemoryStream()
```

### Adım 5: Tanıma işlemini çalıştırın ve PDF'yi yazın

Şimdi zor iş burada gerçekleşir. `recognize` çağrısı görüntüyü okur, OCR'ı çalıştırır ve aranabilir PDF'yi `pdf_stream` içine akıtır.

```python
# Perform OCR and write the searchable PDF into the memory stream
engine.recognize(pdf_stream)
```

> **Yaygın tuzak:** `engine.recognize` çağrısını unutmak, `pdf_stream`'i boş bırakır ve kaydetmeye çalışmak bir `ValueError` hatası verir. Veri üretildiğini doğrulamanız gerekiyorsa her zaman `pdf_stream.length`'i kontrol edin.

### Adım 6: Oluşturulan PDF'yi bir dosyaya kaydedin

Son olarak, bellek akışındaki baytları diske yazarız. Ortaya çıkan dosya Adobe Reader, Preview veya tam metin arama özelliği olan herhangi bir PDF görüntüleyicide açılabilir.

```python
output_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Write the PDF bytes to a file
with open(output_path, "wb") as f:
    f.write(pdf_stream.to_bytes())
print(f"✅ Searchable PDF saved to {output_path}")
```

> **Görürsünüz sonuç:** PDF'yi açın, `Ctrl+F` tuşlarına basın, orijinal taramada görülen bir kelimeyi yazın ve görüntüleyicinin anında vurguladığını izleyin. Bu, bir **searchable PDF**'in özelliğidir.

## Görüntüyü PDF'ye Dönüştürme – En iyi sonuçlar için ayarları ince ayar

Eğer temel amacınız OCR olmadan sadece **convert image to PDF** yapmaksa, adım 3'ü atlayabilir ve çıktı formatını `ocr.OutputFormat.IMAGE_PDF` olarak ayarlayabilirsiniz. Motor, bitmap'i gizli bir metin katmanı olmadan PDF sayfası olarak gömecektir.

```python
engine.get_settings().set_output_format(ocr.OutputFormat.IMAGE_PDF)
```

Bu modu, görsel olarak tam bir kopyaya ihtiyacınız olduğunda ancak aranabilirlik istemediğinizde kullanın—belki OCR'ın gerekli olmadığı arşivleme amaçları için.

## Metin PDF'si Tanıma – Dil paketleri ekleme ve DPI kontrolü

Sağlam bir **recognize text PDF** deneyimi için aşağıdaki isteğe bağlı ayarları göz önünde bulundurun:

```python
settings = engine.get_settings()
settings.set_language("eng+spa")          # English + Spanish support
settings.set_dpi(300)                     # Higher DPI improves accuracy
settings.enable_auto_rotate(True)         # Auto‑rotate skewed scans
```

> **Neden DPI ayarlansın?** Daha yüksek çözünürlük, OCR motoruna analiz etmesi için daha fazla piksel verir, düşük kaliteli taramalarda hatalı tanıma oranını azaltır.

## Python OCR PDF – Daha büyük hatlara entegrasyon

Artık bir avuç satırda **python ocr pdf** yapabildiğinize göre, bu mantığı bir Flask API'sine gömmeyi hayal edin:

```python
from flask import Flask, request, send_file
import io, ocr

app = Flask(__name__)

@app.route("/upload", methods=["POST"])
def upload():
    file = request.files["image"]
    engine = ocr.OcrEngine()
    engine.set_image(ocr.ImageStream.from_bytes(file.read()))
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
    pdf_stream = ocr.MemoryStream()
    engine.recognize(pdf_stream)

    return send_file(
        io.BytesIO(pdf_stream.to_bytes()),
        mimetype="application/pdf",
        as_attachment=True,
        download_name="searchable.pdf"
    )
```

Bu küçük uç nokta, bir istemcinin bir görüntüyü POST etmesine ve anında bir **searchable PDF** almasına olanak tanır—SaaS belge‑işleme hizmetleri için mükemmeldir.

## **ocr image to pdf** yaparken yaygın tuzaklar

| Semptom | Muhtemel neden | Çözüm |
|---------|----------------|-------|
| Boş PDF sayfaları | Görüntü yüklenmedi (`engine.set_image` yanlış yol ile çağrıldı) | Yolu doğrulayın ve `os.path.abspath` kullanın |
| Aranabilir metin yok | Çıktı formatı hâlâ `IMAGE_PDF` olarak ayarlı | `set_output_format(ocr.OutputFormat.PDF)` metodunu açıkça çağırın |
| Bozuk karakterler | Yanlış dil paketi | `settings.set_language("eng")` ile doğru dili yükleyin |
| Büyük dosyalarda yavaş işleme | Yüksek çözünürlüklü görüntülerde varsayılan DPI (72) kullanılması | DPI'yi 300'e yükseltin veya sayfaları tek tek toplu işleyin |

## Tam, çalıştırılabilir örnek (kopyala‑yapıştır hazır)

```python
import ocr

def create_searchable_pdf(image_path: str, output_path: str) -> None:
    """
    Convert a scanned image to a searchable PDF using the ocr SDK.
    """
    # 1️⃣ Initialise engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # 3️⃣ Set output to searchable PDF
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)

    # Optional: improve accuracy
    settings = engine.get_settings()
    settings.set_language("eng")   # adjust as needed
    settings.set_dpi(300)

    # 4️⃣ Prepare in‑memory stream
    pdf_stream = ocr.MemoryStream()

    # 5️⃣ Run OCR
    engine.recognize(pdf_stream)

    # 6️⃣ Persist PDF
    with open(output_path, "wb") as f:
        f.write(pdf_stream.to_bytes())
    print(f"✅ Searchable PDF created at: {output_path}")

if __name__ == "__main__":
    create_searchable_pdf(
        image_path="YOUR_DIRECTORY/contract.jpg",
        output_path="YOUR_DIRECTORY/contract_searchable.pdf"
    )
```

Betik çalıştırın, oluşturulan PDF'yi açın ve orijinal taramada bulunduğunu bildiğiniz bir kelimeyi aramayı deneyin. Her şey sorunsuz çalıştıysa, Python ile **create searchable pdf** konusunda uzmanlaştınız demektir.

## Sonuç

Python OCR kütüphanesi kullanarak **create searchable PDF** dosyaları oluşturmak için ihtiyacınız olan her şeyi ele aldık: motoru başlatma, bir görüntüyü yükleme, PDF çıktısını yapılandırma, sonucu akıtarak ve sonunda diske kaydetme. Ayrıca **convert image to PDF** nasıl yapılacağını ve **

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [PDF Metni Tanıma – Aspose.OCR for Java ile OCR İşlemleri](/ocr/english/java/ocr-operations/)
- [.NET'te Aspose.OCR ile PDF'yi OCR Yapma](/ocr/english/net/text-recognition/recognize-pdf/)
- [C# ile Görüntüleri PDF'ye Dönüştürme – Çok Sayfalı OCR Sonucunu Kaydet](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}