---
category: general
date: 2026-04-26
description: Aspose.OCR kullanarak C#'ta görüntüden metin çıkarın ve görüntüyü dakikalar
  içinde JSON ve XML formatlarına nasıl dönüştüreceğinizi öğrenin.
draft: false
keywords:
- extract text from image
- convert image to json
- convert image to xml
- Aspose OCR C#
- image to JSON C#
- image to XML C#
language: tr
og_description: C# ile Aspose.OCR kullanarak görüntüden metin çıkarın. Sonucu anında
  JSON ve XML'e nasıl dönüştüreceğinizi adım adım öğrenin.
og_title: C#'ta görüntüden metin çıkarma – JSON ve XML'ye dönüştürme
tags:
- OCR
- C#
- Aspose
- JSON
- XML
title: C#'ta görüntüden metin çıkarma – JSON ve XML'e dönüştürme
url: /tr/net/text-recognition/extract-text-from-image-in-c-convert-to-json-xml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Görüntüden Metin Çıkarma – JSON ve XML'e Dönüştürme

Hiç .NET projesinde **görüntüden metin çıkarma** ihtiyacı duydunuz ama “verileri nasıl alırım?” sorusunda takıldınız mı? Yalnız değilsiniz. Gerçek dünyadaki birçok uygulamada—fatura işleme, fiş tarama veya kimlik doğrulama gibi—bir resimden ham karakterleri çekmek ilk ve kritik adımdır.  

İyi haber? Aspose.OCR ile bunu sadece birkaç satırda yapabilir, ardından **görüntüyü JSON'a dönüştürme** veya **görüntüyü XML'e dönüştürme** işlemlerini anında gerçekleştirebilirsiniz. Bu rehberde tam, çalıştırılabilir kodu adım adım inceleyecek, her parçanın neden önemli olduğunu açıklayacak ve yaygın tuzaklardan kaçınmanız için birkaç ipucu göstereceğiz.

---

## İhtiyacınız Olanlar

- **.NET 6+** (herhangi bir yeni SDK çalışır; örnek .NET 6 hedefler)
- **Aspose.OCR for .NET** NuGet paketi  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Yazdırılabilir metin içeren bir görüntü dosyası (PNG, JPG vb.); örnek olarak `invoice.png` kullanacağız.
- Bir kod editörü—Visual Studio, VS Code veya Rider—istediğiniz gibi.

Hepsi bu. Ek OCR motorları, dış hizmetler yok, sadece tek bir NuGet paketi.

---

## Adım 1: OCR Motorunu Kurun – Görüntüden Metin Nasıl Çıkarılır

İlk olarak bir `OcrEngine` örneği oluşturup görüntü dosyasına işaret ediyoruz. Bu adım temeldir; doğru şekilde yüklenmemiş bir görüntü olmadan motor hiçbir şeyi tanıyamaz.

```csharp
using Aspose.OCR;
using System.IO;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process
// Replace YOUR_DIRECTORY with the actual folder path
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");

// Optional: verify the image was loaded
if (ocrEngine.Image == null)
{
    throw new FileNotFoundException("Image not found. Check the path and filename.");
}
```

**Neden Önemli:**  
- `OcrEngine`, düşük seviyeli tüm görüntü ön işleme (ikiliye çevirme, eğikliği giderme) işlemlerini kapsar.  
- `ImageStream.FromFile` ile görüntüyü yüklemek, motorun tam baytları okumasını, DPI ve renk derinliğini korumasını sağlar—her ikisi de tanıma doğruluğunu etkileyebilir.  

> **Pro tip:** Kaynak görüntüleriniz bir akışta (ör. bir web API üzerinden yüklenmiş) ise `FromFile` yerine `ImageStream.FromStream(yourStream)` kullanın.

---

## Adım 2: Motorun Beklediği Dili Belirtin – Görüntüden Metni Doğru Çıkarın

Aspose.OCR birçok alfabeyi destekler. Doğru dili belirtmek karakter setini daraltır ve doğruluğu artırır.

```csharp
// Set the language; Latin covers English, French, German, etc.
ocrEngine.Language = Language.Latin;
```

**Neden:**  
`Language.Latin` ayarlandığında OCR motoru Kiril veya Asya gliflerini yok sayar, yanlış pozitifleri azaltır. Daha sonra çok‑dilli belgelerle çalışmanız gerekirse `Language.Multilingual` ya da birden fazla dili birleştirerek kullanabilirsiniz.

---

## Adım 3: Tanıma İşlemini Çalıştırın – Görüntüden Tek Çağrıda Metin Çıkarın

Şimdi gerçekten metni tanıyoruz. `Recognize` yöntemi, ham metin, güven skorları ve hatta yerleşim verilerini içeren bir `RecognitionResult` nesnesi döndürür.

```csharp
// Perform OCR
RecognitionResult recognitionResult = ocrEngine.Recognize();

// Quick sanity check
if (recognitionResult == null || string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text was detected. Verify the image quality.");
    return;
}

// Print the raw extracted text to the console
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(recognitionResult.Text);
```

**Neden:**  
`Recognize` tek seferde çağrılması yeterlidir çünkü motor içinde ön işleme, segmentasyona ve karakter sınıflandırmasına zaten yer verilir. `Text` özelliği, günlükleme ya da hızlı doğrulama için mükemmel bir düz‑metin temsili sunar.

---

## Adım 4: Sonucu JSON'a Dönüştürün – Görüntüyü Kolayca JSON'a Dönüştürün

Modern hizmetlerin çoğu JSON yüklerini tercih eder. Aspose.OCR, tüm `RecognitionResult` nesnesini, güven değerleri ve sınırlama kutuları dahil olmak üzere serileştiren kullanışlı bir `ToJson` yöntemi sunar.

```csharp
// Serialize the result to JSON
string jsonResult = recognitionResult.ToJson();

// Save the JSON to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonResult);

Console.WriteLine("JSON file saved at YOUR_DIRECTORY/invoice.json");
```

**Neden JSON İsteyebilirsiniz:**  
- **Birliktelik:** Front‑end uygulamaları (React, Angular) JSON'u doğrudan tüketebilir.  
- **Hata Ayıklama:** JSON, karakter bazında güven değerlerini içerir; düşük güvenli kelimeleri manuel inceleme için işaretleyebilirsiniz.  

> **Kenar durumu:** Alt sisteminiz sadece düz metni gerekiyorsa, `recognitionResult.Text` değerini alıp tam Aspose yükü yerine özel bir JSON nesnesi içinde paketleyebilirsiniz.

---

## Adım 5: Sonucu XML'e Dönüştürün – Miras Sistemler İçin Görüntüyü XML'e Dönüştürün

Bazı işletmeler hâlâ veri değişimi için XML şemalarına güvenir. `ToXml` yöntemi, `ToJson`'a eşdeğer şekilde XML çıktısı üretir.

```csharp
// Serialize the result to XML
string xmlResult = recognitionResult.ToXml();

// Save the XML to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlResult);

Console.WriteLine("XML file saved at YOUR_DIRECTORY/invoice.xml");
```

**Neden XML:**  
- **Şema doğrulama:** Aspose'un ürettiği yapıya uygun bir XSD tanımlayabilir, sözleşme uyumluluğunu garanti edebilirsiniz.  
- **Entegrasyon:** Eski ERP veya belge‑yönetim sistemleri genellikle XML'i kutudan çıkar çıkmaz ayrıştırabilir.

---

## Tam Çalışan Örnek – Tek Durak Kod

Aşağıda her şeyi bir araya getiren tam program yer alıyor. Yeni bir konsol projesine (`dotnet new console`) kopyalayıp çalıştırın.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Initialize OCR engine and load the image
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();
            // Adjust the path to point at your PNG/JPG file
            string imagePath = "YOUR_DIRECTORY/invoice.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image at {imagePath}");
                return;
            }

            // -------------------------------------------------
            // Step 2: Specify language (Latin for most European scripts)
            // -------------------------------------------------
            ocrEngine.Language = Language.Latin;

            // -------------------------------------------------
            // Step 3: Run OCR and get the result
            // -------------------------------------------------
            RecognitionResult result = ocrEngine.Recognize();

            if (result == null || string.IsNullOrWhiteSpace(result.Text))
            {
                Console.WriteLine("No text detected – check image quality or language setting.");
                return;
            }

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();

            // -------------------------------------------------
            // Step 4: Convert to JSON (convert image to json)
            // -------------------------------------------------
            string json = result.ToJson();
            string jsonPath = "YOUR_DIRECTORY/invoice.json";
            File.WriteAllText(jsonPath, json);
            Console.WriteLine($"JSON output written to {jsonPath}");

            // -------------------------------------------------
            // Step 5: Convert to XML (convert image to xml)
            // -------------------------------------------------
            string xml = result.ToXml();
            string xmlPath = "YOUR_DIRECTORY/invoice.xml";
            File.WriteAllText(xmlPath, xml);
            Console.WriteLine($"XML output written to {xmlPath}");
        }
    }
}
```

**Beklenen çıktı (konsol):**

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

JSON file saved at YOUR_DIRECTORY/invoice.json
XML file saved at YOUR_DIRECTORY/invoice.xml
```

JSON ve XML dosyaları daha zengin bir yapı içerir, örneğin:

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
  "Confidence": 0.96,
  "Blocks": [
    { "Text": "Invoice #12345", "Confidence": 0.98, "Rectangle": { "X": 12, "Y": 30, "Width": 200, "Height": 20 } },
    ...
  ]
}
```

```xml
<RecognitionResult>
  <Text>Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00</Text>
  <Confidence>0.96</Confidence>
  <Blocks>
    <Block>
      <Text>Invoice #12345</Text>
      <Confidence>0.98</Confidence>
      <Rectangle X="12" Y="30" Width="200" Height="20"/>
    </Block>
    ...
  </Blocks>
</RecognitionResult>
```

---

## Yaygın Sorular ve Kenar Durumlar

### Görüntü bulanık veya döndürülmüşse ne olur?

Aspose.OCR çoğu görüntünün eğikliğini otomatik olarak düzeltir, ancak aşırı durumlarda `ocrEngine.Image = ImageProcessor.Deskew(ocrEngine.Image)` ile ön işleme yapabilirsiniz. Biraz kontrast artırma (`ImageProcessor.AdjustContrast`) da güven skorunu yükseltebilir.

### PDF'lerden metin çıkarabilir miyim?

Evet—her PDF sayfasını önce bir görüntüye dönüştürün (ör. Aspose.PDF veya PDFium gibi ücretsiz bir kütüphane kullanarak) ve ardından aynı OCR akışına besleyin.

### Tek bir belgede birden fazla dili nasıl yönetirim?

`ocrEngine.Language = Language.Multilingual;` ya da belirli dilleri birleştirin:

```csharp
ocrEngine.Language = Language.English | Language.French | Language.German;
```

Daha geniş dil setlerinin ...

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}