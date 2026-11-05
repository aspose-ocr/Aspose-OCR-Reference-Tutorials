---
category: general
date: 2026-03-18
description: Aspose OCR kullanarak C#'de görüntüden tablo çıkarın. Tabloyu JSON'a
  nasıl dönüştüreceğinizi, tablo JSON'ını almayı ve dakikalar içinde görüntüden metin
  çıkarmayı öğrenin.
draft: false
keywords:
- extract table from image
- convert table to json
- convert image to json
- extract text from image
- get table json
language: tr
og_description: Aspose OCR kullanarak C#'de görüntüden tablo çıkarın. Tabloyu JSON'a
  dönüştürmeyi, tablo JSON'ını almayı ve görüntüden metni hızlıca çıkarmayı öğrenin.
og_title: Aspose OCR ile Görüntüden Tablo Çıkarma – Tam C# Rehberi
tags:
- Aspose OCR
- C#
- Table Extraction
title: Aspose OCR ile Görüntüden Tablo Çıkarma – Tam C# Rehberi
url: /tr/net/text-recognition/extract-table-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Tablo Çıkarma – Tam C# Rehberi

Görüntüden **tablo çıkarmak** istediğinizde, bunu manuel ayrıştırma yığını olmadan yapabilecek bir kütüphanenin olup olmadığından emin olmadınız mı? Yalnız değilsiniz. Birçok fatura‑işleme veya fiş‑tarama projesinde asıl sorun, gürültülü bir bitmap'i, alt sisteminizin tüketebileceği yapılandırılmış bir tabloya dönüştürmektir.  

İyi haber? Aspose OCR ile birkaç satırda **convert table to JSON** yapabilirsiniz ve ayrıca tüm görüntünün düz metnini elde edersiniz, böylece **extract text from image** bir bonus olur. Bu öğreticide, bir görüntüyü yüklemekten algılanan tablonun düzenli bir JSON temsiline ulaşmaya kadar tüm süreci adım adım göstereceğiz.

> **Quick win:** Sonunda, ham OCR metnini ve doğrudan bir veritabanına ya da API'ye besleyebileceğiniz bir JSON dizesini yazdıran çalıştırılabilir bir C# konsol uygulamanız olacak.

## Önkoşullar

- .NET 6.0 SDK (veya herhangi bir güncel .NET sürümü) yüklü.  
- Geçerli bir Aspose OCR lisansı veya ücretsiz deneme (kütüphane lisans olmadan çalışır ancak filigran ekler).  
- Gerçekten bir tablo içeren bir görüntü – örneğin `invoice_table.png`.  
- Visual Studio 2022, VS Code veya tercih ettiğiniz herhangi bir editör.

`Aspose.OCR` dışındaki ekstra NuGet paketlerine gerek yok.

## Adım 1: Projeyi Kurun ve Aspose OCR'yi Yükleyin

İlk olarak, yeni bir konsol projesi oluşturun ve OCR kütüphanesini ekleyin.

```bash
dotnet new console -n TableJsonDemo
cd TableJsonDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Kurumsal bir proxy kullanıyorsanız, `--no-restore` bayrağını ekleyin ve daha sonra uygun ortam değişkenleriyle `dotnet restore` komutunu çalıştırın.

## Adım 2: OCR Motorunu Başlatın ve Tablo Tanıma Özelliğini Etkinleştirin

Çözümün kalbi `OcrEngine`'dir. `EnableTableRecognition` özelliğini açarak Aspose OCR'ye her şeyi düz metin olarak ele almak yerine ızgara‑benzeri yapıları aramasını söylüyoruz.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;

class TableJsonDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable table detection – this is what lets us get a JSON table later
        ocrEngine.Settings.EnableTableRecognition = true;
```

Bu adım neden kritik? Tablo tanıma olmadan, motor görüntüyü tek bir dizeye indirger ve daha sonra satır ve sütunları yeniden oluşturmayı imkânsız hâle getirir. Bunu etkinleştirmek, performansta neredeyse hiç maliyet getirmeyen hafif bir düzen analizi aşaması ekler ancak sonraki aşamalarda büyük faydalar sağlar.

## Adım 3: Görüntünüzü Yükleyin ve Tanıma İşlemini Çalıştırın

Şimdi motoru tabloyu içeren dosyaya yönlendiriyoruz. `ImageStream.FromFile` çoğu yaygın formatı (PNG, JPEG, TIFF) destekler.

```csharp
        // Load the image that contains the table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Perform OCR – this returns an OcrResult object with multiple helpers
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

Görüntü büyükse, işleme hızını artırmak için önce yeniden boyutlandırmayı düşünün. Aspose OCR otomatik olarak DPI'yi algılar, ancak 300 DPI tarama çoğu tablo için ideal bir noktadır.

## Adım 4: Düz Metni Çıkar – “extract text from image”

Ana hedefimiz tablo olsa da, genellikle günlükleme veya yedek işleme için ham metne hâlâ ihtiyaç duyarsınız.

```csharp
        // Output the full recognized text
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);
```

`Text` özelliği motorun gördüğü her şeyi birleştirir ve satır sonlarını korur. Bu, OCR'nin tablo alanının dışındaki başlıkları veya altbilgileri doğru okuduğunu doğrulamanız gerektiğinde kullanışlıdır.

## Adım 5: Algılanan Tabloyu JSON Olarak Al – “convert table to json” & “get table json”

İşte sihrin gerçekleştiği yer. `GetTableAsJson()` algılanan satırları, sütunları ve hücre içeriklerini temiz bir JSON dizesine serileştirir.

```csharp
        // Retrieve the table structure as a JSON string
        string tableJson = ocrResult.GetTableAsJson();

        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);
    }
}
```

Ortaya çıkan JSON şöyle bir şey gibi görünür (okunabilirlik için biçimlendirilmiş):

```json
{
  "Rows": [
    {
      "Cells": [
        { "Text": "Item", "ColumnIndex": 0 },
        { "Text": "Quantity", "ColumnIndex": 1 },
        { "Text": "Price", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget A", "ColumnIndex": 0 },
        { "Text": "10", "ColumnIndex": 1 },
        { "Text": "$5.00", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget B", "ColumnIndex": 0 },
        { "Text": "7", "ColumnIndex": 1 },
        { "Text": "$8.50", "ColumnIndex": 2 }
      ]
    }
  ]
}
```

JSON neden tercih edilen format? Dil bağımsızdır, nesnelere kolayca serileştirilebilir ve modern web API'leriyle harika çalışır. Bunun yerine bir CSV'ye ihtiyacınız varsa, satırları döngüyle gezip hücre metinlerini virgülle birleştirmeniz yeterlidir.

## Adım 6: (İsteğe Bağlı) JSON'ı .NET Nesnesine Dönüştür – “convert image to json”

Güçlü tiplerle çalışmayı tercih ediyorsanız, JSON'u `System.Text.Json` kullanarak serileştirin.

```csharp
using System.Text.Json;

...

        // Deserialize into a C# class (optional)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
```

`TableModel`, `RowModel` ve `CellModel` sınıflarını JSON şemasına uygun şekilde tanımlarsınız. Bu adım, **convert image to json** işleminden tiplenmiş bir nesneye kadar nasıl gidebileceğinizi gösterir ve sonraki doğrulamaları çok kolay hâle getirir.

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, işte tam, çalıştırmaya hazır program. Bunu daha önce oluşturduğunuz proje klasörünün içine `Program.cs` olarak kaydedin.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;
using System.Text.Json;

class TableJsonDemo
{
    static void Main()
    {
        // Step 1: Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable table recognition
        ocrEngine.Settings.EnableTableRecognition = true;

        // Step 3: Load image containing a table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Step 4: Run OCR
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 5: Print full text (extract text from image)
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);

        // Step 6: Get table as JSON (convert table to json, get table json)
        string tableJson = ocrResult.GetTableAsJson();
        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);

        // Optional: Deserialize JSON to C# objects (convert image to json)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
    }
}

// Helper classes matching Aspose's JSON structure
public class TableModel
{
    public RowModel[] Rows { get; set; }
}
public class RowModel
{
    public CellModel[] Cells { get; set; }
}
public class CellModel
{
    public string Text { get; set; }
    public int ColumnIndex { get; set; }
}
```

### Beklenen Çıktı

`dotnet run` komutunu çalıştırdığınızda, aşağıdakine benzer bir şey görmelisiniz:

```
Full text:
Item Quantity Price
Widget A 10 $5.00
Widget B 7 $8.50

Detected table (JSON):
{
  "Rows":[
    {"Cells":[{"Text":"Item","ColumnIndex":0},{"Text":"Quantity","ColumnIndex":1},{"Text":"Price","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget A","ColumnIndex":0},{"Text":"10","ColumnIndex":1},{"Text":"$5.00","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget B","ColumnIndex":0},{"Text":"7","ColumnIndex":1},{"Text":"$8.50","ColumnIndex":2}]}
  ]
}

First cell value: Item
```

Çıktı boş görünüyorsa, `EnableTableRecognition`'ın `true` olarak ayarlandığını ve görüntünün gerçekten net ızgara çizgileri içerdiğini iki kez kontrol edin.

## Yaygın Tuzaklar ve Nasıl Kaçınılır

| Sorun | Neden Oluşur | Çözüm |
|-------|----------------|-----|
| **JSON döndürülmedi** | Tablo algılaması devre dışı bırakıldı veya görüntü çok düşük kontrastlı. | `ocrEngine.Settings.EnableTableRecognition = true` olduğundan emin olun ve görüntü kalitesini artırın (kontrastı yükseltin, ikilileştirin). |
| **Kısmi satırlar** | OCR, birleştirilmiş hücreler veya döndürülmüş metin nedeniyle karıştı. | Görüntüyü ön‑işleyin: eğriliği düzeltin (`ImageProcessor.Rotate`) veya birleştirilmiş hücreleri manuel olarak bölün. |
| **Unicode bozukluğu** | Yazı tipi tanınmadı (örneğin el yazısı). | `ocrEngine.Language = Language.English;` ile dil paketlerini değiştirin veya el yazısı için farklı bir OCR motoru kullanın. |
| **Performans yavaşlaması** | Çok büyük görüntü (>5 MP). | DPI'yi koruyarak genişliği ~1500 px'e küçültün. |

## Sonraki Adımlar: Temelin Ötesine Geçmek

Artık **extract table from image** ve **convert table to JSON** yapabildiğinize göre, şu uzantıları göz önünde bulundurun:

- **JSON'ı** Entity Framework ile bir veritabanına kalıcı hale getirin.  
- **JSON'ı** para birimi formatlarını normalleştirmek için (örneğin `$` işaretini kaldırarak) sonradan işleyin.  
- `Directory.GetFiles` kullanarak bir fatura klasörünü **toplu işleyin** ve `Parallel.ForEach` ile paralel hale getirin.  
- Sunucusuz OCR hatları için Azure Functions veya AWS Lambda ile **entegrasyon** sağlayın.

Bu konuların her biri doğal olarak **convert image to json** (tüm OCR sonucunu bir bulut uç noktasına gönderdiğinizde) ve **get table json** gibi ikincil anahtar kelimeleri de içerir ve sonraki analizler için faydalıdır.

---

### Sonuç

Az önce Aspose OCR kullanarak **extract table from image** nasıl yapılacağını, tabloyu temiz JSON'a dönüştürmeyi ve hatta C# nesnelerine serileştirmeyi gösterdik. Aynı desen{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}