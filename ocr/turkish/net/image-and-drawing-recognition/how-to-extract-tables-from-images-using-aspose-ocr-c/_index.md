---
category: general
date: 2026-03-28
description: Aspose OCR ile C#’ta görüntülerden tablo çıkarmayı öğrenin. Bu kılavuz,
  görüntüdeki tabloları nasıl tespit edeceğinizi, OCR için görüntüyü nasıl yükleyeceğinizi
  ve PNG dosyalarından tabloları nasıl çıkaracağınızı kapsar.
draft: false
keywords:
- how to extract tables
- extract table from image
- detect tables in image
- load image for ocr
- extract tables from png
language: tr
og_description: Aspose OCR ile C#’ta görüntülerden tablo çıkarmanın adım adım öğreticisi.
  Kod, açıklamalar ve görüntü dosyalarındaki tabloları tespit etme ipuçlarını içerir.
og_title: Aspose OCR (C#) Kullanarak Görüntülerden Tablo Nasıl Çıkarılır
tags:
- Aspose OCR
- C#
- Table Extraction
title: Aspose OCR (C#) kullanarak Görüntülerden Tablo Nasıl Çıkarılır
url: /tr/net/image-and-drawing-recognition/how-to-extract-tables-from-images-using-aspose-ocr-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görsellerden Tablo Çıkarma Aspose OCR (C#) Kullanarak

Tarayıcıdan taranmış bir faturadan veya bir elektronik tablo ekran görüntüsünden **tabloları nasıl çıkaracağınızı** hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok gerçek dünya projesinde bir tablo resmini sorgulayabileceğimiz bir şeye dönüştürmemiz gerekir—genellikle bir CSV veya DataTable. İyi haber? Aspose OCR bunu çocuk oyuncağı haline getiriyor ve sadece birkaç C# satırıyla yapabilirsiniz.

Bu öğreticide, **load image for OCR**, **detect tables in image** ve sonunda **extract table from image** adımlarını içeren tüm süreci adım adım göstereceğiz ve CSV dosyası olarak kaydedeceğiz. Sonunda, **extract tables from PNG** dosyalarından (veya desteklenen herhangi bir bitmap'ten) sorunsuz bir şekilde tablo çıkarabilen, çalıştırmaya hazır bir konsol uygulamanız olacak.

## Önkoşullar

Before we dive in, make sure you have:

- .NET 6.0 SDK veya daha yenisi (kod .NET Framework ile de çalışır)
- Visual Studio 2022 (veya tercih ettiğiniz herhangi bir IDE)
- Aspose.OCR for .NET lisans dosyası (ücretsiz deneme ile başlayabilirsiniz)
- Tablo içeren bir örnek görüntü (örnek: `invoice_table.png`)

Eğer bunlardan herhangi biri size yabancı geliyorsa endişelenmeyin—sadece .NET SDK'yı kurun ve NuGet paketini alın, böylece hazırsınız.

## Çözümün Genel Görünümü

At a high level the workflow looks like this:

1. **Load the image** işlemek istediğiniz görseli.
2. **Run OCR recognition** motorun metnin nerede olduğunu bilmesi için.
3. **Create a TableExtractor** OCR sonuçlarını ızgara benzeri yapılar için tarar.
4. **Extract all detected tables** ve ihtiyacınız olanı seçer.
5. **Save the table** CSV olarak (veya tercih ettiğiniz başka bir formatta) kaydeder.

Her adım aşağıda ayrıntılı olarak açıklanmıştır, kopyalayıp yapıştırabileceğiniz tam kod parçacıklarıyla birlikte.

<img src="table_extraction_example.png" alt="görselden tablo çıkarma örneği" width="600">

*(Yukarıdaki görsel, çıkaracağımız örnek bir fatura tablosunu göstermektedir.)*

## 1. Adım – Görseli OCR için Yükleme

İlk yapmanız gereken, Aspose OCR'a hangi dosyayı okuyacağını söylemektir. Kütüphane PNG, JPEG, BMP, TIFF ve birkaç diğer formatı destekler. İşte en temel kod:

```csharp
using Aspose.OCR;
using System.Drawing;   // Required for Image.FromFile

// ...

// Load the image that contains the table
var ocrEngine = new OcrEngine
{
    Image = Image.FromFile(@"C:\Images\invoice_table.png") // <-- adjust the path
};
```

**Neden önemli?**  
`Image.FromFile`, PNG'yi (veya diğer bitmap'i) OCR motorunun anlayabileceği bir formata dönüştürme işini yapar. Bu adımı atlayıp bozuk bir dosya verirseniz, sonraki `Recognize()` çağrısı bir istisna fırlatır.

> **Pro ipucu:** Büyük PDF'lerle çalışıyorsanız, önce her sayfayı bir görsele çıkarın—aksi takdirde OCR motoru belleği tükenir.

## 2. Adım – Sayfayı Tanıma (Tablo Algılamadan Önce Gereklidir)

Tanıma, ham piksel verilerini aranabilir bir metin düzenine dönüştürür. Bu adım olmadan `TableExtractor` çalışacak bir şey bulamaz.

```csharp
// Perform OCR recognition – this populates internal structures
ocrEngine.Recognize();
```

**Arka planda ne oluyor?**  
Aspose OCR, sinir ağı tabanlı bir metin algılayıcı çalıştırır, ardından `Page`, `Paragraph` ve `Word` nesnelerinin bir hiyerarşisini oluşturur. Tablo algılayıcı daha sonra bu kelimeler arasındaki uzamsal ilişkileri inceler.

Bir döngüde birçok görsel işliyorsanız, aynı `OcrEngine` örneğini yeniden kullanıp sadece `Image` özelliğini değiştirin—bu, tahsis yükünü azaltır.

## 3. Adım – TableExtractor Oluşturma ve Görselde Tablo Algılama

OCR verileri mevcut olduğuna göre, Aspose'tan tabloları bulmasını isteyebiliriz. `TableExtractor` sınıfı tam da bunu yapar.

```csharp
using Aspose.OCR.Table;

// ...

// Initialize the TableExtractor with the recognized engine
var tableExtractor = new TableExtractor(ocrEngine);

// Extract all tables detected on the page
List<Table> extractedTables = tableExtractor.ExtractAll();
```

**Neden `ExtractAll()` kullanmalı?**  
Tek bir görsel birden fazla tablo içerebilir (çok bölümlü bir rapor gibi). `ExtractAll()` bir `List<Table>` döndürür, böylece döngüyle işleyebilir, doğru olanı seçebilir veya sonradan birleştirebilirsiniz.

Sadece ilk tabloya ihtiyacınız varsa, güvenle `extractedTables[0]` kullanabilirsiniz, ancak `IndexOutOfRangeException` almamak için her zaman listenin boş olup olmadığını kontrol edin.

```csharp
if (extractedTables.Count == 0)
{
    Console.WriteLine("No tables were detected. Check the image quality or try adjusting OCR settings.");
    return;
}
```

## 4. Adım – Çıkarılan Tabloyu CSV Olarak Kaydetme (veya Başka Bir Format)

Aspose, dışa aktarmayı çok basit hale getirir. `Table` sınıfı yerleşik `SaveCsv`, `SaveXls` ve `SaveJson` yöntemlerine sahiptir. CSV dosyası yazmanın yolu şu şekildedir:

```csharp
// Save the first detected table to CSV
string outputPath = @"C:\Output\invoice_table.csv";
extractedTables[0].SaveCsv(outputPath);

Console.WriteLine($"Table extraction completed. CSV saved to {outputPath}");
```

**CSV nasıl görünüyor?**  
Kaynak görsel 4 × 3 bir ızgara içeriyorsa, CSV şu şekilde görünebilir:

```
Item,Quantity,Price
Widget A,2,19.99
Widget B,5,9.50
Service C,1,150.00
```

Bu dosyayı Excel, Power BI'de açabilir veya doğrudan veri hattınıza besleyebilirsiniz.

## Tam Uçtan Uca Örnek

Aşağıda tam, bağımsız program yer almaktadır. Yeni bir konsol projesine (`dotnet new console`) kopyalayıp çalıştırın. `Aspose.OCR` NuGet paketinin kurulu olduğundan emin olun (`dotnet add package Aspose.OCR`).

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;          // For Image
using Aspose.OCR;
using Aspose.OCR.Table;

namespace TableExtractTutorial
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the image that contains the table
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                Image = Image.FromFile(@"C:\Images\invoice_table.png")
            };

            // -------------------------------------------------
            // Step 2: Recognize the page (required before table detection)
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 3: Create a TableExtractor and detect tables
            // -------------------------------------------------
            var tableExtractor = new TableExtractor(ocrEngine);
            List<Table> extractedTables = tableExtractor.ExtractAll();

            // Guard against no tables found
            if (extractedTables.Count == 0)
            {
                Console.WriteLine("No tables detected. Verify image quality or OCR settings.");
                return;
            }

            // -------------------------------------------------
            // Step 4: Save the first extracted table as CSV
            // -------------------------------------------------
            string csvPath = @"C:\Output\invoice_table.csv";
            extractedTables[0].SaveCsv(csvPath);

            Console.WriteLine($"Table extraction completed. CSV saved at: {csvPath}");
        }
    }
}
```

### Beklenen Çıktı

Programı çalıştırdığınızda aşağıdakine benzer bir çıktı görmelisiniz:

```
Table extraction completed. CSV saved at: C:\Output\invoice_table.csv
```

`invoice_table.csv` dosyasını açın ve satırların ve sütunların orijinal görseli yansıttığını göreceksiniz.

## Yaygın Sorular ve Kenar Durumları

### Görsel PNG yerine JPEG olsaydı ne olur?

Aynı kod çalışır—sadece `Image.FromFile` içinde dosya uzantısını değiştirin. Aspose OCR formatı otomatik olarak algılar, bu yüzden **extract tables from png** zor bir gereklilik değildir; herhangi bir desteklenen bitmap ile çalışır.

### Tablom birleştirilmiş hücrelere sahip. Bunlar korunur mu?

Birleştirilmiş hücreler CSV çıktısında ayrı sütunlar olarak ele alınır çünkü CSV kapsamı desteklemez. Daha zengin bir format (ör. birleştirilmiş hücreli Excel) gerekiyorsa, bunun yerine `SaveXls` kullanın:

```csharp
extractedTables[0].SaveXls(@"C:\Output\invoice_table.xls");
```

### Algılama bir sütunu kaçırdı. Doğruluğu nasıl artırabilirim?

- Görüntü çözünürlüğünü artırın (≥300 dpi ideal).
- Görseli ön‑işleme tabi tutun: gri tonlamaya çevirin, kontrastı artırın veya eğikliği düzelten bir filtre uygulayın.
- Tablo Latin dışı karakterler içeriyorsa `PageSegMode` veya `Language` gibi Aspose OCR ayarlarını değiştirin.

### PDF'den doğrudan tablo çıkarabilir miyim?

Evet. Önce her PDF sayfasını bir görsele dönüştürün (`Aspose.PDF` veya herhangi bir PDF‑to‑image kütüphanesi kullanarak), ardından bu görselleri aynı iş akışına besleyin.

## Üretim‑Hazır Uygulamalar İçin İpuçları

1. **OCR'ı try/catch içinde sarmalayın** – ağ‑lisanslı ortamlar lisans istisnaları fırlatabilir.
2. **`Image` nesnelerini dispose edin** – yerel kaynakları serbest bırakmak için `using` blokları içinde sarın.
3. **Güven skorlarını kaydedin** – `TableExtractor`, kalite izleme için saklayabileceğiniz `Table.Confidence` değerini ortaya çıkarır.
4. **Toplu işleme** – Yüzlerce fatura işlerken OCR çağrılarını paralelleştirin ancak lisansın thread‑safety yönergelerine uyun.

## Sonraki Adımlar

Now that you know **how to extract tables** from images, you might want to explore:

- **Detect tables in image** videoları (her karede Aspose’un `TableExtractor`'ını kullanarak).
- **Load image for OCR** bir web API'den, bulut tabanlı tablo çıkarma hizmetlerini etkinleştirerek.
- **Extract tables from PNG** dosyalarını Azure Blob Storage'da saklayarak, Azure Functions ile sunucusuz işleme entegre edin.

Farklı dosya formatlarıyla denemeler yapmaktan, OCR ayarlarını ince ayar yapmaktan veya CSV çıktısını doğrudan bir veritabanına yönlendirmekten çekinmeyin. Sınır yok.

---

*Kodlamada iyi eğlenceler! Herhangi bir sorunla karşılaşırsanız veya geliştirme fikirleriniz varsa, aşağıya yorum bırakın. Birlikte çözeriz.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}