---
category: general
date: 2026-01-04
description: C#'ta OCR kullanarak formları nasıl etkinleştireceğinizi ve görüntülerden
  tabloları nasıl çıkaracağınızı öğrenin. Bu adım adım öğretici ayrıca OCR görüntüsünü
  nasıl çalıştıracağınızı ve tabloları OCR ile nasıl tespit edeceğinizi gösterir.
draft: false
keywords:
- how to enable forms
- how to extract tables
- run OCR image
- use OCR C#
- detect tables OCR
language: tr
og_description: Formları etkinleştirme, tabloları çıkarma, OCR görüntüsü çalıştırma
  ve C# kullanarak tablo OCR'sini algılama konusunda adım adım rehber.
og_title: C#'da Formları Etkinleştirme ve OCR ile Tabloları Çıkarma
tags:
- OCR
- C#
- Computer Vision
title: C#'ta Formları Etkinleştirme ve OCR ile Tabloları Çıkarma – Tam Kılavuz
url: /tr/net/image-and-drawing-recognition/how-to-enable-forms-and-extract-tables-with-ocr-in-c-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#’ta Formları Etkinleştirme ve OCR ile Tabloları Çıkarma – Tam Kılavuz

Faturalar, makbuzlar veya herhangi bir yapılandırılmış belgeyi tararken **formları nasıl etkinleştirirsiniz** diye hiç merak ettiniz mi? Tek başınıza değilsiniz. Gerçek dünyadaki birçok projede en büyük sürtünme noktası, OCR’nin hem form alanlarını **hem** tabloları bir milyon satır özel ayrıştırma olmadan anlayabilmesidir.  

Bu öğreticide, **formları nasıl etkinleştirirsiniz**, **tabloları nasıl çıkarırsınız** ve hatta **OCR görüntü** işleme tek bir C# programında nasıl çalıştırılır gösteren pratik, uçtan uca bir çözüm üzerinden ilerleyeceğiz. Sonunda, OCR tarzı tablo algılayan, anahtar‑değer çiftlerini çıkaran ve bunları konsola yazdıran hazır bir kod parçacığına sahip olacaksınız.

> **Önkoşullar** – .NET 6+ (veya .NET Framework 4.7+), kullandığınız OCR SDK’sına bir referans (örnek, genel bir `OcrEngine` sınıfı varsayar), ve içinde tablo veya form bulunan bir görüntü dosyası (`invoice_table.png`). Başka harici kütüphane gerekmez.

![formları OCR ile etkinleştirme C#](image.png)

## Bu Öğreticide Neler Ele Alınıyor

- **Form tanıma** etkinleştirilerek “Fatura Numarası” veya “Tarih” gibi alanların otomatik olarak tanımlanması.  
- Tarama belgelerinden **tabloların çıkarılması**, satır/sütun sayısı ve hücre içeriklerinin elde edilmesi.  
- Tek bir çağrı ile **OCR görüntü** işleme çalıştırılması ve sonucun programatik olarak ele alınması.  
- **detect tables OCR** kenar durumları için ipuçları, örneğin birleştirilmiş hücreler veya eksik kenarlıklar.  

Haydi başlayalım.

## Adım 1: OCR Motorunu Kurun – formları nasıl etkinleştirirsiniz

Herhangi bir tanıma gerçekleşmeden önce bir OCR motoru örneğine ihtiyacınız var. Çoğu SDK basit bir kurucu sunar; daha sonra yapılandırma seçeneklerini nerede ayarlayabileceğinizi de göstereceğiz.

```csharp
using System;
using System.Linq;

// Assume the OCR SDK namespace is OcrSdk
using OcrSdk;

public class OcrDemo
{
    public static void Main()
    {
        // Create the OCR engine – this is where “how to enable forms” starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that contains a table or form.
        // Replace the path with the actual location of your PNG/JPEG/TIFF file.
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");
```

**Neden Önemli:** Motorun örneklenmesi iç kaynakları (dil modelleri gibi) ayırır. Bu adımı atlayıp `Recognize` çağrısı yaparsanız `NullReferenceException` alırsınız.

## Adım 2: Yapılandırılmış Çıkarma Özelliğini Açın – tabloları nasıl çıkarırsınız & detect tables OCR

Şimdi iki temel özelliği etkinleştiriyoruz: tablo tanıma ve form alanı çıkarma. Modern OCR motorlarının çoğu boolean bayrakları ya da daha ayrıntılı bir `Config` nesnesi sunar.

```csharp
        // Enable structured extraction features.
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms
```

**Pro ipucu:** Yalnızca bir özelliğe ihtiyacınız varsa, diğerini devre dışı bırakmak performansı %20’ye kadar artırabilir.  

## Adım 3: OCR Görüntüyü Çalıştırın ve Sonucu Alın – run OCR image

Motor yapılandırıldıktan sonra tek bir metod çağrısı tüm işi yapar. Dönen `OcrResult` tablo ve form alanları için koleksiyonlar içerir.

```csharp
        // Run OCR – this is the “run OCR image” step.
        OcrResult ocrResult = ocrEngine.Recognize();

        // -----------------------------------------------------------------
        // Step 4: Process Detected Tables – how to extract tables
        // -----------------------------------------------------------------
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");

            // Show the first row for a quick sanity check.
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // -----------------------------------------------------------------
        // Step 5: Process Detected Form Fields – how to enable forms
        // -----------------------------------------------------------------
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```

### Beklenen Konsol Çıktısı

```
Table 1: 5 rows, 4 columns
Item | Qty | Price | Total
InvoiceNumber: INV-2025-001
Date: 2025-12-31
Customer: Acme Corp.
```

Tam sayılar kaynak görüntünüze göre değişecektir, ancak her tablo için bir özet satırı, ardından ilk satırın hücre değerleri ve form alanları için anahtar‑değer çiftleri listesi görmelisiniz.

## Adım 4: Detect Tables OCR’da Kenar Durumlarını Ele Alma

`EnableTableRecognition = true` olsa bile OCR şu durumlarda zorlanabilir:

| Sorun | Neden Oluşur | Hızlı Çözüm |
|-------|--------------|-------------|
| **Birleştirilmiş hücreler** | Motor birleştirilmiş alanı tek bir hücre olarak görür. | Satırları sonradan işle: aşırı geniş hücreleri boşluklara göre böl. |
| **Eksik kenarlıklar** | Tablo çizgileri soluk ya da kırık. | Motorun ön işlemine (`ocrEngine.PreprocessImage`) gitmeden önce görüntü kontrastını artır. |
| **Döndürülmüş tablolar** | Belge açıyla taranmış. | `ocrEngine.Config.AutoRotate = true` (varsa) kullan. |

**İpucu:** `table.Rows.Count` ve `table.Columns.Count` değerlerini indekslere erişmeden önce her zaman kontrol edin; aksi takdirde `IndexOutOfRangeException` alırsınız.

## Adım 5: Hepsini Bir Araya Getirin – Tam, Çalıştırılabilir Örnek

Aşağıda yeni bir konsol projesine kopyalayıp yapıştırabileceğiniz tam program yer alıyor. `using` yönergeleri, motor kurulumu ve önceki adımlarda gösterilen işleme mantığını içerir.

```csharp
using System;
using System.Linq;
using OcrSdk;   // Replace with your actual OCR SDK namespace

public class OcrDemo
{
    public static void Main()
    {
        // 1️⃣ Create OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the target image
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");

        // 3️⃣ Enable structured extraction (forms + tables)
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms

        // 4️⃣ Run OCR – “run OCR image”
        OcrResult ocrResult = ocrEngine.Recognize();

        // 5️⃣ Process tables – “how to extract tables”
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // 6️⃣ Process form fields – “how to enable forms”
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```

Programı çalıştırın (`dotnet run` ya da Visual Studio’da `Ctrl+F5`) ve önceki bölümde tarif edilen konsol çıktısını göreceksiniz.

## Sıkça Sorulan Sorular (SSS)

**S: PDF girişiyle çalışır mı?**  
C: Çoğu OCR SDK’sı PDF’leri dahili olarak her sayfayı rasterleştirerek kabul eder. `LoadImage` yerine `ocrEngine.LoadPdf("file.pdf")` çağırmanız yeterlidir.

**S: Görüntümde hem bir tablo *hem* bir imza varsa ne olur?**  
C: İmza ayrı bir görüntü bölgesi olarak ortaya çıkar. Düşük güvenilirlikli metinleri kontrol ederek `ocrResult.Images` içinde görmezden gelebilirsiniz.

**S: Tabloları CSV’ye dışa aktarabilir miyim?**  
C: Kesinlikle. `table.Rows` üzerinde dönerken her `cell.Text` değerini virgülle ayrılmış bir `StringBuilder`’a yazın, ardından oluşan dizgeyi `.csv` dosyasına kaydedin.

## Sonuç

Artık **formları nasıl etkinleştirirsiniz**, **tabloları nasıl çıkarırsınız** ve C# kullanarak **OCR görüntü** işleme adımlarını tam olarak biliyorsunuz. Örnek, motor oluşturulmasından yapılandırmaya, sonuçların ele alınmasına kadar tam iş akışını gösteriyor; böylece kodu doğrudan projelerinize kopyalayabilirsiniz.  

Şimdi örnek görüntüyü çok sayfalı bir fatura PDF’iyle değiştirin, `ocrEngine.Config.AutoRotate` ile deney yapın veya çıkarılan verileri bir veritabanına aktarın. Bu eklemeler, **detect tables OCR** ve **use OCR C#** konularında üretim senaryolarında uzmanlaşmanızı sağlayacak.

Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakmaktan çekinmeyin. İyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}