---
category: general
date: 2026-05-31
description: Aspose OCR kullanarak C#'ta görüntüden tabloları çıkarın. Görüntüyü tabloya
  dönüştürmeyi, tablo algılamayı etkinleştirmeyi ve sonuçları verimli bir şekilde
  çıkarmayı öğrenin.
draft: false
keywords:
- extract tables from image
- convert image to table
- OCR table extraction
- Aspose OCR C#
- image to spreadsheet conversion
- table detection in OCR
language: tr
og_description: Aspose OCR ile görüntüden tabloları çıkarın. Bu rehber, görüntüyü
  tabloya dönüştürmeyi, tablo algılamayı etkinleştirmeyi ve sonuçları C#'ta nasıl
  ele alacağınızı gösterir.
og_title: Görüntüden Tabloları Çıkar – Adım Adım C# Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  headline: Extract Tables from Image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  name: Extract Tables from Image with Aspose OCR – Complete C# Guide
  steps:
  - name: Expected Output
    text: 'Assuming the source image contains a 3 × 4 table of invoice line items,
      you might see something like:'
  - name: Low‑Resolution Images
    text: 'When your source picture is under 150 dpi, the table detection algorithm
      may miss cell boundaries. A quick fix is to upscale the image using `System.Drawing`
      before feeding it to Aspose:'
  - name: Skewed Tables
    text: 'If the table is rotated even a few degrees, enable auto‑deskew:'
  - name: Multiple Tables on One Page
    text: Aspose OCR returns each table as a separate object in `result.Tables`. You
      can treat them individually, or merge them into a single DataTable if you need
      a unified view.
  - name: Exporting to Excel
    text: 'Once you have a `DataTable`, exporting to an `.xlsx` file is a breeze with
      `ClosedXML`:'
  type: HowTo
- questions:
  - answer: Yes. Convert each PDF page to an image first (`PdfRenderer` or `Ghostscript`),
      then feed the bitmap to Aspose OCR.
    question: Does this work with PDFs?
  - answer: Absolutely. The `ImageStream.FromFile` method accepts JPEG, PNG, BMP,
      and TIFF out of the box.
    question: Can I extract tables from a JPG?
  - answer: Aspose OCR treats merged cells as separate logical cells; you may need
      to post‑process the output to combine them based on confidence or content patterns.
    question: What if my table has merged cells?
  - answer: Practically, the engine handles tables up to several hundred rows. Performance
      degrades linearly, so consider chunking very large scans.
    question: Is there a limit on table size?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- Data Extraction
title: Aspose OCR ile Görüntüden Tablo Çıkarma – Tam C# Rehberi
url: /tr/net/image-and-drawing-recognition/extract-tables-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Tabloları Çıkarma – Tam C# Rehberi

Hiç **extract tables from image** ihtiyacınız oldu mu ama nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz; birçok geliştirici taranmış faturaları veya makbuzları kullanılabilir verilere dönüştürmeye çalışırken bu engelle karşılaşıyor. İyi haber? Aspose OCR ile sadece birkaç C# satırıyla **convert image to table** yapabilirsiniz.

Bu öğreticide gerçek bir örnek üzerinden ilerleyeceğiz: bir tablo içeren PNG'yi yüklemek, görsel yerleşimi yapılandırılmış bir ızgaraya dönüştürmek ve her hücrenin içeriğini güven puanlarıyla yazdırmak. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz tam çalışan bir kod parçacığına ve kenar durumlarını ele alma ve çözümü ölçeklendirme ipuçlarına sahip olacaksınız.

## İhtiyacınız Olanlar

- **.NET 6.0** veya daha yenisi (kod .NET Framework 4.6+ ile de çalışır)
- **Aspose.OCR** NuGet paketi (`Install-Package Aspose.OCR`)
- Gerçek bir tablo içeren bir görüntü dosyası (ör. `invoice_with_table.png`)
- Temel bir C# IDE (Visual Studio, Rider veya C# uzantılı VS Code)

Hepsi bu—ekstra OCR motorları yok, ağır bağımlılıklar yok. Hazır mısınız? Hadi başlayalım.

## Adım 1: OCR Motorunu **Extract Tables from Image** için Başlatma

İlk olarak bir `OcrEngine` örneği oluşturup kaynak görüntümüze işaret ediyoruz. Motoru, her pikseli okuyup yerleşimi anlamaya çalışan bir beyin olarak düşünün.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Initialize the OCR engine with the input image
OcrEngine engine = new OcrEngine
{
    // ImageStream.FromFile loads the image from disk
    Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
};
```

> **Neden bu önemli:** Motoru doğru şekilde başlatmazsanız OCR motorunun analiz edecek bir şeyi olmaz ve görüntüden hiçbir tablo elde edemezsiniz. `ImageStream.FromFile` çağrısı ayrıca yaygın format sorunlarını (PNG, JPEG, BMP) halleder, böylece ekstra dönüşüm adımlarına ihtiyaç duymazsınız.

## Adım 2: Tablo Algılamayı Etkinleştirme – **Convert Image to Table** için Anahtar

Aspose OCR bir görüntüden düz metin okuyabilir, ancak tablo aramasını söylemezseniz satır ve sütunları sihirli bir şekilde anlayamaz. İşte `DetectTables` bayrağının devreye girdiği yer.

```csharp
// Turn on table detection in the OCR options
engine.Options = new OcrOptions
{
    DetectTables = true   // This activates the table extraction algorithm
};
```

> **Pro ipucu:** Yalnızca ham metne ihtiyacınız varsa `DetectTables` değerini `false` bırakın. Etkinleştirmek küçük bir ek yük getirir, ancak karşılığı, doğrudan bir elektronik tabloya veya veritabanına aktarabileceğiniz temiz, yapılandırılmış bir sonuçtur.

## Adım 3: OCR Tanımasını Gerçekleştirme – Gerçek An

Şimdi motoru görüntüyü gerçekten okumaya çağırıyoruz. `Recognize` metodu, düz metin ve algılanan tabloları içeren bir `OcrResult` nesnesi döndürür.

```csharp
// Execute the OCR process
OcrResult result = engine.Recognize();
```

> **Arka planda ne oluyor?** Aspose, sinir‑ağ‑tabanlı metin tanıma motorunu uygulamadan önce bir dizi görüntü ön işleme adımı (eğrilik düzeltme, ikilileştirme) gerçekleştirir. `DetectTables` true olduğunda, karakterleri satır ve sütunlara gruplayan bir yerleşim analizi aşaması da çalıştırır.

## Adım 4: Algılanan Tabloları Döngüyle İşleme – **Extract Tables from Image** Uygulamada

Motor herhangi bir tablo bulursa, bunlar `result.Tables` içinde görünecek. Her tabloyu, ardından her satırı ve sütunu döngüyle gezerek hücre metnini ve güven yüzdesini yazdıracağız.

```csharp
// Loop over every detected table
foreach (var table in result.Tables)
{
    Console.WriteLine("Table found:");
    for (int r = 0; r < table.Rows; r++)
    {
        for (int c = 0; c < table.Columns; c++)
        {
            var cell = table[r, c];
            // Show cell text and its confidence level
            Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
        }
        Console.WriteLine(); // New line after each row
    }
}
```

> **Neden güveni kontrol edelim?** OCR mükemmel değildir, özellikle düşük çözünürlüklü taramalarda. `Confidence` değeri (0‑100), hücreyi olduğu gibi kabul edip etmeyeceğinize veya manuel inceleme için işaretleyeceğinize karar vermenizi sağlar. Kritik veriler için tipik bir eşik %80’dir.

### Beklenen Çıktı

Kaynak görüntünün 3 × 4 bir fatura satırı tablosu içerdiğini varsayarsak, aşağıdaki gibi bir şey görebilirsiniz:

```
Table found:
Item (conf:96%)   Qty (conf:94%)   Price (conf:97%)   Total (conf:95%)
Pen (conf:99%)    10 (conf:98%)    1.20 (conf:97%)    12.00 (conf:96%)
Notebook (conf:95%) 5 (conf:93%)  3.50 (conf:94%)    17.50 (conf:92%)
...
```

Eğer hiçbir tablo algılanmazsa, `result.Tables` boş olacaktır—yazdırılacak bir şey yok, ancak program sorunsuz bir şekilde sonlanacaktır.

## Adım 5: Kenar Durumlarını ve Yaygın Tuzakları Ele Alma

### Düşük Çözünürlüklü Görüntüler

Kaynak resminiz 150 dpi’nin altında olduğunda, tablo algılama algoritması hücre sınırlarını kaçırabilir. Hızlı bir çözüm, görüntüyü Aspose’a göndermeden önce `System.Drawing` kullanarak ölçeklendirmektir:

```csharp
using System.Drawing;
using System.Drawing.Imaging;

// Load and upscale
Bitmap bmp = new Bitmap(@"YOUR_DIRECTORY/invoice_with_table.png");
Bitmap resized = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
engine.Image = ImageStream.FromBitmap(resized);
```

### Eğik Tablolar

Tablo birkaç derece bile döndürülmüşse, otomatik eğrilik düzeltmeyi etkinleştirin:

```csharp
engine.Options.Deskew = true; // Turns on automatic deskewing
```

### Tek Sayfada Birden Çok Tablo

Aspose OCR, her tabloyu `result.Tables` içinde ayrı bir nesne olarak döndürür. Bunları ayrı ayrı işleyebilir veya birleşik bir görünüm için tek bir DataTable’a birleştirebilirsiniz.

```csharp
// Example: Merge all tables into one DataTable
var merged = new System.Data.DataTable();
foreach (var tbl in result.Tables)
{
    // Simple merge logic – assumes same column count
    // Add rows from each table
    for (int r = 0; r < tbl.Rows; r++)
    {
        var row = merged.NewRow();
        for (int c = 0; c < tbl.Columns; c++)
        {
            row[c] = tbl[r, c].Text;
        }
        merged.Rows.Add(row);
    }
}
```

### Excel’e Aktarma

Bir `DataTable` elde ettiğinizde, `ClosedXML` ile bir `.xlsx` dosyasına aktarmak çok kolaydır:

```csharp
using ClosedXML.Excel;

var workbook = new XLWorkbook();
var worksheet = workbook.Worksheets.Add(merged, "ExtractedTable");
workbook.SaveAs("ExtractedTable.xlsx");
```

Artık gerçekten **converted image to table** yaptınız ve elektronik tabloyu sonraki süreçlere teslim edebilirsiniz.

## Tam Çalışan Örnek – Baştan Sona

Aşağıda her şeyi bir araya getiren, tam ve çalıştırmaya hazır program bulunmaktadır. Yeni bir konsol projesine yapıştırın, dosya yolunu değiştirin ve **F5** tuşuna basın.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;
using System.Data;
using ClosedXML.Excel;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine with the image
        OcrEngine engine = new OcrEngine
        {
            Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
        };

        // 2️⃣ Enable table detection (key to convert image to table)
        engine.Options = new OcrOptions
        {
            DetectTables = true,
            Deskew = true // Helps with slightly rotated scans
        };

        // 3️⃣ Perform recognition
        OcrResult result = engine.Recognize();

        // 4️⃣ Process each detected table
        DataTable merged = new DataTable();
        bool firstTable = true;

        foreach (var table in result.Tables)
        {
            Console.WriteLine("Table found:");
            for (int r = 0; r < table.Rows; r++)
            {
                // Ensure DataTable has enough columns
                if (firstTable && merged.Columns.Count < table.Columns)
                {
                    for (int i = merged.Columns.Count; i < table.Columns; i++)
                        merged.Columns.Add($"Col{i + 1}");
                }

                DataRow dr = merged.NewRow();
                for (int c = 0; c < table.Columns; c++)
                {
                    var cell = table[r, c];
                    Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
                    dr[c] = cell.Text; // Populate DataTable for Excel export
                }
                Console.WriteLine();
                merged.Rows.Add(dr);
            }
            firstTable = false;
            Console.WriteLine(); // Blank line between tables
        }

        // 5️⃣ Optional: Export merged result to Excel
        if (merged.Rows.Count > 0)
        {
            using var wb = new XLWorkbook();
            wb.Worksheets.Add(merged, "ExtractedTables");
            wb.SaveAs("ExtractedTables.xlsx");
            Console.WriteLine("\nExcel file 'ExtractedTables.xlsx' created successfully.");
        }
        else
        {
            Console.WriteLine("\nNo tables were detected in the image.");
        }
    }
}
```

**Akışın Açıklaması**

1. **Engine setup** – Görüntüyü yükler ve Aspose’a tabloları aramasını söyler.
2. **Options tuning** – `DetectTables` ağır işi yapar; `Deskew` eğimli taramalarda doğruluğu artırır.
3. **Recognition** – Hem düz metni hem de bir `Table` nesnesi koleksiyonunu döndürür.
4. **Iteration** – Her hücreyi güvenle birlikte yazdırır, aynı zamanda sonraki dışa aktarma için bir `DataTable` oluşturur.
5. **Export** – `ClosedXML` (hafif, interop gerektirmeyen bir kütüphane) kullanarak bir `.xlsx` dosyası yazar—sonraki analizler veya raporlamalar için mükemmeldir.

## Sıkça Sorulan Sorular

- **Does this work with PDFs?**  
  Evet. Önce her PDF sayfasını bir görüntüye dönüştürün (`PdfRenderer` veya `Ghostscript`), ardından bitmap'i Aspose OCR’a verin.

- **Can I extract tables from a JPG?**  
  Kesinlikle. `ImageStream.FromFile` metodu JPEG, PNG, BMP ve TIFF formatlarını doğrudan kabul eder.

- **What if my table has merged cells?**  
  Aspose OCR birleştirilmiş hücreleri ayrı mantıksal hücreler olarak ele alır; çıktıyı güvene veya içerik desenlerine göre birleştirmeniz gerekebilir.

- **Is there a limit on table size?**  
  Pratikte, motor birkaç yüz satıra kadar tabloyu işleyebilir. Performans doğrusal olarak düşer, bu yüzden çok büyük taramaları bölmeyi düşünün.

## Sonuç

Size sadece nasıl yapılacağını gösterdik

## Sonra Ne Öğrenmelisiniz?

- [Aspose.OCR for .NET kullanarak görüntüden tablo nasıl çıkarılır](/ocr/english/net/text-recognition/recognize-table/)
- [Görüntüden Metin Çıkarma – Aspose.OCR for .NET ile OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)
- [OCR’da Dikdörtgen Hazırlayarak Görüntüden Metin Nasıl Çıkarılır](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}