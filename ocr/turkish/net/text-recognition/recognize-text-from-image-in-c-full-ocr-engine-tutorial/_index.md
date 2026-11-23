---
category: general
date: 2026-06-06
description: C# OCR motoru kullanarak görüntüden metni tanıyın. Görüntüyü JSON'a,
  görüntüyü XML'e dönüştürmeyi öğrenin ve OCR için görüntüyü dakikalar içinde yükleyin.
draft: false
keywords:
- recognize text from image
- convert image to json
- convert image to xml
- ocr engine c#
- load image for ocr
language: tr
og_description: C# OCR motoru ile görüntüden metin tanıyın. Sonuçları JSON ve XML
  olarak dışa aktarın ve OCR için görüntü yüklemeyi ustalaşın.
og_title: C#'ta Görüntüden Metin Tanıma – Tam OCR Motoru Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Recognize text from image using C# OCR engine. Learn to convert image
    to JSON, convert image to XML, and load image for OCR in minutes.
  headline: Recognize Text from Image in C# – Full OCR Engine Tutorial
  type: TechArticle
tags:
- OCR
- C#
- Image Processing
title: C#'ta Görüntüden Metin Tanıma – Tam OCR Motoru Öğreticisi
url: /tr/net/text-recognition/recognize-text-from-image-in-c-full-ocr-engine-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Metin Tanıma C# – Tam OCR Motoru Öğreticisi

Hiç **görüntüden metin tanıma** ihtiyacı duydunuz mu ama hangi C# kütüphanesini seçeceğinize karar veremediniz mi? Tek başınıza değilsiniz—geliştiriciler sürekli taranmış fişleri, ekran görüntülerini veya el yazısı notları aranabilir metne dönüştürmekle uğraşıyor. İyi haber? Modern bir **OCR engine C#** ile bunu sadece birkaç satır kodla yapabilir, ardından **convert image to JSON** veya **convert image to XML** işlemleriyle sonraki aşamalara geçebilirsiniz.

Bu rehberde her adımı ele alacağız: OCR paketini kurmak, OCR için bir görüntü yüklemek, metni çıkarmak ve sonuçları JSON ve XML olarak dışa aktarmak. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz, tamamen bağımsız bir console uygulamanız olacak. Belirsiz referanslar yok, sadece çalıştırılabilir bir çözüm.

## Öğrenecekleriniz

- Popüler bir C# OCR motoru kullanarak **load image for OCR** nasıl yapılır, net bir anlayış.  
- **recognize text from image** yapan ve zengin bir sonuç nesnesi döndüren çalışan kod.  
- Ek kütüphane gerektirmeden **convert image to JSON** ve **convert image to XML** yapan basit snippet'ler.  
- Çok sayfalı PDF'ler, farklı görüntü formatları ve düşük kontrast taramalar gibi yaygın sorunlarla başa çıkma ipuçları.

### Önkoşullar

- .NET 6 SDK veya daha yeni bir sürüm (isteğe bağlı olarak .NET Framework 4.8 de hedefleyebilirsiniz).  
- Temel C# bilgisi—sınıflar ve `async`/`await` kavramlarını bilmek yeterli.  
- OCR yapmak istediğiniz bir görüntü dosyası (`structured.png` örneklerde).  

Eğer bunlara sahipseniz, hemen başlayalım.

---

## Görüntüden Metin Tanıma – OCR Motorunu Kurma

İlk iş olarak güvenilir bir OCR kütüphanesine ihtiyacımız var. Bu öğreticide **IronOcr** kullanacağız; NuGet'te ücretsiz bir community sürümü sunan ticari‑grade bir motor. İngilizceyi kutudan çıkar çıkmaz destekliyor ve orijinal snippet'te gösterilen `OcrEngine` sınıfını sağlıyor.

```bash
dotnet add package IronOcr --version 2024.3.0
```

> **Pro ipucu:** Daha sıkı bir bütçeniz varsa `IronOcr` yerine `Tesseract`'ı deneyin—API biraz farklı ama kavramlar aynı kalır.

Şimdi yeni bir console projesi oluşturup gerekli `using` ifadelerini ekleyin:

```csharp
using IronOcr;
using System.IO;
```

### Adım‑Adım Motor Yapılandırması

```csharp
// Step 1: Create and configure the OCR engine
var ocrEngine = new IronTesseract();           // IronOcr’s engine class
ocrEngine.Language = OcrLanguage.English;     // Load English language data
```

*Bu neden önemli:* Motoru bir kez başlatıp birçok görüntüde yeniden kullanmak, işlem süresini azaltır. Ayrıca dili açıkça ayarlamak, motorun otomatik algılama rutinini devre dışı bırakır; bu da daha hızlı ve daha doğru sonuçlar verir.

---

## OCR İçin Görüntü Yükleme – Motoru Doğru Veriyle Besleme

Motor bir `OcrInput` nesnesi bekler. Dosya yolu, akış (stream) ya da hatta bir `Bitmap` gösterebilirsiniz. En basit yaklaşım şu şekildedir:

```csharp
// Step 2: Load the image to be processed
var input = new OcrInput(@"YOUR_DIRECTORY\structured.png");

// Optional: improve accuracy on low‑contrast images
input.Deskew();          // Straighten tilted pages
input.Contrast(10);      // Boost contrast by 10%
```

> **Köşe durumu:** Kaynağınız çok sayfalı bir PDF ise `input.AddPdf("file.pdf")` çağrısını PNG yerine kullanın. OCR motoru her sayfayı ayrı bir görüntü olarak otomatik işler.

---

## Görüntüden Metin Tanıma – OCR İşlemini Çalıştırma

Motor ve giriş hazır olduğunda, gerçek tanıma tek bir satırda gerçekleşir:

```csharp
// Step 3: Recognize text in the image
using var result = ocrEngine.Read(input);
```

`result` bir `OcrResult` nesnesidir ve şunları içerir:

- `Text` – ham çıkarılan dize.  
- `Lines` – güven puanlarıyla birlikte `OcrLine` nesnelerinin koleksiyonu.  
- `Words` – aynı şekilde güven puanlarıyla bireysel kelimeler.  

Doğrudan hata ayıklayıcıda inceleyebilirsiniz, ancak çoğu zaman veriyi serileştirmeniz gerekir.

---

## Görüntüyü JSON'a Dönüştürme – OCR Sonuçlarını Dışa Aktarma

IronOcr, `System.Text.Json` aracılığıyla yerleşik JSON serileştirmesi sunar. Aşağıdaki snippet, kaynak görüntünüzün yanına düzenli bir JSON dosyası yazar:

```csharp
// Step 4: Export the recognition result to JSON and save it
string jsonResult = System.Text.Json.JsonSerializer.Serialize(result, new System.Text.Json.JsonSerializerOptions
{
    WriteIndented = true
});
File.WriteAllText(@"YOUR_DIRECTORY\result.json", jsonResult);
```

**Gördükleriniz:** ham metin, güven puanları ve her satır ve kelime için sınırlama kutularını içeren güzel biçimlendirilmiş bir JSON belgesi. Bu yapı, ElasticSearch ya da Azure Cognitive Search gibi downstream servislerine beslemek için idealdir.

---

## Görüntüyü XML'e Dönüştürme – Yapılandırılmış Veri Çıktısı

Bazı eski sistemler hâlâ XML bekler. IronOcr'un `ToXml()` metodu hızlı bir dönüşüm sağlar:

```csharp
// Step 5: Export the recognition result to XML and save it
string xmlResult = result.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY\result.xml", xmlResult);
```

XML, JSON hiyerarşisini yansıtır; `<Line>` ve `<Word>` öğeleri `Confidence` özniteliklerine sahiptir. Özel bir şema gerekiyorsa, `result` nesnesini manuel olarak bir `XDocument`'e dönüştürebilirsiniz—API tam anlamıyla LINQ‑uyumludur.

---

## Tam Uç‑Uç Örnek Kod

Her şeyi bir araya getirdiğimizde, çalıştırmaya hazır bir `Program.cs` elde ederiz:

```csharp
using IronOcr;
using System;
using System.IO;
using System.Text.Json;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure the OCR engine
        var ocrEngine = new IronTesseract();
        ocrEngine.Language = OcrLanguage.English;

        // 2️⃣ Load the image (adjust the path to your file)
        var input = new OcrInput(@"YOUR_DIRECTORY\structured.png");
        input.Deskew();
        input.Contrast(10);

        // 3️⃣ Perform recognition
        using var result = ocrEngine.Read(input);
        Console.WriteLine("✅ OCR completed. Extracted text:");
        Console.WriteLine(result.Text);

        // 4️⃣ Convert image to JSON
        string json = JsonSerializer.Serialize(result, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = @"YOUR_DIRECTORY\result.json";
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"📄 JSON saved to {jsonPath}");

        // 5️⃣ Convert image to XML
        string xml = result.ToXml();
        string xmlPath = @"YOUR_DIRECTORY\result.xml";
        File.WriteAllText(xmlPath, xml);
        Console.WriteLine($"📄 XML saved to {xmlPath}");
    }
}
```

**Beklenen çıktı** (kısaltılmış):

```
✅ OCR completed. Extracted text:
Invoice #12345
Date: 2024‑04‑01
Total: $1,234.56
...
📄 JSON saved to YOUR_DIRECTORY\result.json
📄 XML saved to YOUR_DIRECTORY\result.xml
```

Programı `dotnet run` ile çalıştırın. Her şey doğru bağlandıysa, konsolda döküm görür ve `YOUR_DIRECTORY` içinde iki dosya oluşur.

---

## Yaygın Sorular & Tuzaklar

| Soru | Cevap |
|------|-------|
| *Görüntü bir EXIF dönüşümüne sahip JPEG ise ne yapmalıyım?* | `Deskew()`'den önce `input.AutoRotate()` kullanın. IronOcr EXIF etiketini okuyup yönü düzeltecek. |
| *Bir klasördeki tüm görüntüleri toplu olarak OCR'lamak mümkün mü?* | Kesinlikle. Yukarıdaki mantığı `foreach (var file in Directory.GetFiles(folder, "*.png"))` döngüsüyle sarmalayın. |
| *Gürültülü taramalarda doğruluğu nasıl artırırım?* | `input.Denoise()` değerini yükseltin ve `input.BlackWhiteThreshold(120)` gibi ayarları deneyin. Ayrıca belge diline uygun bir dil paketi ekleyin. |
| *JSON formatı diğer OCR kütüphaneleriyle uyumlu mu?* | Şema yeterince genel—`Text`, `Lines`, `Words`—bu yüzden Tesseract çıktısına minimum dönüşümle eşlenebilir. |

---

## Performans İpuçları (Pro‑Seviye)

- **Motoru yeniden kullanın**: `IronTesseract`'ı sık bir döngü içinde yeniden örneklemek, verimliliği %30’a kadar düşürebilir. Uygulama alanı başına bir singleton tutun.  
- **I/O'yu paralelleştirin**: Onlarca görüntü işliyorsanız, onları aynı anda belleğe (`Task.WhenAll`) okuyun ve her `OcrInput`'u aynı motorla besleyin—IronOcr thread‑safe'dir.  
- **Toplu dışa aktarım**: Her JSON/XML dosyasını ayrı ayrı yazmak yerine sonuçları tek bir koleksiyonda toplayıp bir kez serileştirin. Bu, disk erişimini azaltır.

---

## Sonraki Adımlar & İlgili Konular

Artık **görüntüden metin tanıma** yapabildiğinize göre, pipeline'ı şu yönlerde genişletebilirsiniz:

- **Arama entegrasyonu** – JSON'u Elasticsearch'e iterek tam metin arama sağlayın.  
- **Belge sınıflandırması** – OCR çıktısını hafif bir ML modeline besleyerek faturaları, sözleşmeleri veya fişleri otomatik etiketleyin.  
- **El yazısı metin** – Dil paketini `OcrLanguage.EnglishHandwritten` (IronOcr premium seviyesinde) olarak değiştirin.  

Bu adımlar, şu ana kadar kurduğunuz temelin üzerine inşa edilir ve haftalarca süren projeler için size yol gösterir.

---

## Sonuç

**görüntüden metin tanıma** için modern bir **OCR engine C#** kullandık, ardından **convert image to JSON** ve **convert image to XML** işlemlerini gerçekleştirdik ve **load image for OCR** sürecini sağlam bir şekilde yönettik. Tam örnek bir dakikadan kısa sürede çalışıyor ve dışa aktarılan dosyalar herhangi bir downstream sistem için hazır.

Kodu çalıştırın, ayarları ince ayarlayın ve kendi senaryolarınıza göre özelleştirin.

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakın konuları ele alır. Her kaynak, adım‑adım açıklamalar ve tam çalışan kod örnekleri içerir; böylece ek API özelliklerini öğrenebilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}