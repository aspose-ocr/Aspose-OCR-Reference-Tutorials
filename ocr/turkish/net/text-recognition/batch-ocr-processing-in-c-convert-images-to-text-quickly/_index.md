---
category: general
date: 2026-06-25
description: Toplu OCR işleme öğreticisi, Aspose.OCR kullanarak C#'ta görüntüleri
  metne dönüştürmeyi ve görüntülerden metin çıkarmayı gösterir. Adım adım uygulamayı
  öğrenin.
draft: false
keywords:
- batch ocr processing
- convert images to text
- how to extract text from images
language: tr
og_description: C#'ta toplu OCR işleme, görüntüleri hızlıca metne dönüştürmenizi sağlar.
  Aspose.OCR ile görüntülerden metin çıkarmayı öğrenmek için bu kılavuzu izleyin.
og_title: C#'de Toplu OCR İşleme – Görüntüleri Metne Dönüştür
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Batch OCR processing tutorial shows how to convert images to text and
    extract text from images using Aspose.OCR in C#. Learn step‑by‑step implementation.
  headline: Batch OCR Processing in C# – Convert Images to Text Quickly
  type: TechArticle
- description: Batch OCR processing tutorial shows how to convert images to text and
    extract text from images using Aspose.OCR in C#. Learn step‑by‑step implementation.
  name: Batch OCR Processing in C# – Convert Images to Text Quickly
  steps:
  - name: Expected Output
    text: 'When you run `dotnet run`, you’ll see something like:'
  - name: What image formats are supported?
    text: Aspose.OCR handles JPEG, PNG, TIFF, BMP, and GIF out of the box. If you
      encounter a format like WebP, convert it first or use a third‑party decoder.
  - name: Can I limit the OCR language to English only?
    text: 'Yes. Set the `Language` property on the `BatchRecognizer` before calling
      `Recognize`:'
  - name: How do I process thousands of files without blowing up memory?
    text: Break the list into smaller batches (e.g., 500 files each) and run the above
      routine in a loop. This keeps the in‑memory dictionary manageable and lets you
      log progress per batch.
  - name: What if I need the OCR results in a database instead of files?
    text: 'Replace the `File.WriteAllText` call with your preferred data‑access code.
      For example, using Dapper:'
  type: HowTo
tags:
- OCR
- Aspose
- C#
title: C#'ta Toplu OCR İşleme – Görüntüleri Hızlıca Metne Dönüştür
url: /tr/net/text-recognition/batch-ocr-processing-in-c-convert-images-to-text-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Toplu OCR İşleme – Görüntüleri Hızlıca Metne Dönüştürme

Hiç **toplu OCR işleme** ile her dosya için ayrı bir döngü yazmadan bir klasördeki tüm taramaları nasıl işleyebileceğinizi merak ettiniz mi? Tek başınıza değilsiniz. Birçok projede—fatura otomasyonu, eski belgelerin arşivlenmesi ya da basit bir kişisel fotoğraf‑metin aracını düşünün—**görüntüleri toplu olarak metne dönüştürmeniz** gerekir.  

İyi haber? Aspose.OCR ile bunu sadece birkaç satırda yapabilirsiniz. Bu rehber, **görüntülerden metin nasıl çıkarılır** sorusunu toplu OCR işleme kullanarak gösteren tam, çalıştırmaya hazır bir örnek üzerinden adım adım ilerlemenizi sağlar, her parçanın neden önemli olduğunu açıklar ve yaygın hatalardan kaçınmanız için ipuçları verir.

## Öğrenecekleriniz

- Aspose.OCR'ı toplu işlemler için kurma
- Büyük işler için paralellik ayarlama
- OCR sonuçlarını otomatik olarak ayrı `.txt` dosyalarına yazma
- İlerleme olaylarını yakalama, böylece her zaman neler olduğunu bilirsiniz
- Kodu özel hata yönetimi veya farklı çıktı formatları için genişletme

Aspose ile daha önce çalışmış olmanız gerekmez; sadece temel bir C# bilgisi ve .NET 6 (veya daha yenisi) yüklü olması yeterlidir.

---

## Adım 1: Toplu OCR İşleme İçin Projenizi Hazırlayın

Koda geçmeden önce Aspose.OCR NuGet paketinin yüklü olduğundan emin olun. Proje klasörünüzde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** En yeni kararlı sürümü (Haziran 2026 itibarıyla 23.9) kullanın; böylece performans iyileştirmeleri ve en yeni dil desteğinden yararlanırsınız.

Henüz bir konsol uygulamanız yoksa yeni bir tane oluşturun:

```bash
dotnet new console -n BatchOcrApp
cd BatchOcrApp
```

Artık gerçek toplu OCR işleme mantığını yazmaya hazırsınız.

## Adım 2: Dönüştürmek İstediğiniz Görüntü Dosyalarını Tanımlayın

**Toplu OCR işleme**nin ilk adımı, tanıyıcıya hangi dosyaları işleyeceğini söylemektir. Listeyi sabit kodlayabilir, bir dizinden okuyabilir ya da veritabanından çekebilirsiniz. Açıklık olması açısından statik bir liste kullanalım:

```csharp
// Step 2: List of image files to be processed
var imageFiles = new List<string>
{
    @"C:\Images\invoice1.jpg",
    @"C:\Images\receipt2.png",
    @"C:\Images\scan3.tif"
};
```

> **Neden önemli:** Bir koleksiyon geçirerek `BatchRecognizer` içsel olarak işi birden çok iş parçacığına dağıtabilir; bu da **görüntüleri metne dönüştürme** işlemlerinin temel hızlandırıcısıdır.

## Adım 3: BatchRecognizer'ı Oluşturun ve Yapılandırın

Şimdi öğreticinin kalbi devreye giriyor. `BatchRecognizer` sınıfı iş parçacığı detaylarını sizin yerinize soyutlar. `Parallelism` özelliğini CPU çekirdek sayınıza ya da diğer işler için çekirdek bırakmak istiyorsanız özel bir değere göre ayarlayabilirsiniz.

```csharp
// Step 3: Initialise the BatchRecognizer with optional settings
var ocrBatch = new BatchRecognizer
{
    // Number of concurrent threads (default = Environment.ProcessorCount)
    Parallelism = 4,

    // Optional: Hook into progress events for real‑time feedback
    ProgressChanged = (s, e) =>
        Console.WriteLine($"Processed {e.Completed}/{e.Total} – {e.CurrentFile}")
};
```

> **Açıklama:** `Parallelism = 4` ayarı, kütüphanenin aynı anda dört OCR işi çalıştırmasını söyler. Tipik bir quad‑core dizüstü bilgisayarda bu, sistemi aşırı yüklemeden güzel bir hız artışı sağlar. Daha çok çekirdeğe sahip bir sunucuda bu sayıyı artırabilirsiniz.

> **Köşe durumu:** Çok büyük görüntüler işliyorsanız bellek sınırına takılabilirsiniz. Bu durumda paralelliği düşürün ya da dosyaları daha küçük parçalar halinde işleyin.

## Adım 4: OCR'ı Çalıştırın ve Sonuçları Yakalayın

`BatchRecognizer` üzerindeki `Recognize` çağrısı, anahtarının orijinal dosya yolu, değerinin ise çıkarılan metin, güven skorları vb. bilgileri içeren bir `OcrResult` olduğu bir sözlük döndürür.

```csharp
// Step 4: Execute batch OCR – returns a map of file → OcrResult
IDictionary<string, OcrResult> ocrResults = ocrBatch.Recognize(imageFiles);
```

> **Ne elde edersiniz:** Her görüntü için `OcrResult.Text` düz metin temsili içerir. Bu, **görüntülerden metin nasıl çıkarılır** sorusunun programatik yanıtıdır.

## Adım 5: Her Sonucu Bir .txt Dosyasına Kaydedin

Gerçek dünya senaryolarının çoğu OCR çıktısını daha sonra işlemek üzere saklamayı gerektirir—örneğin bir arama indeksine beslemek ya da bir veritabanı kaydına eklemek. Aşağıdaki döngü, her kaynak görüntünün yanına aynı dosya adını koruyarak bir `.txt` dosyası yazar.

```csharp
// Step 5: Write each OCR result to a corresponding .txt file
foreach (var entry in ocrResults)
{
    string txtPath = Path.ChangeExtension(entry.Key, ".txt");
    File.WriteAllText(txtPath, entry.Value.Text);
    Console.WriteLine($"Saved OCR text to {txtPath}");
}
```

> **İpucu:** Farklı bir format (JSON, CSV vb.) isterseniz `entry.Value`'yu istediğiniz gibi serileştirin. `OcrResult` nesnesi ayrıca `Confidence` ve `PageCount` gibi metrikleri de sunar; bunlar sizin için faydalı olabilir.

## Adım 6: Tamamlanmayı Bildirin ve Hataları Zarifçe Ele Alın

Temiz bir bitiş, aracınızın daha profesyonel görünmesini sağlar. Örnek kod zaten bir son satır yazdırıyor, ancak beklenmedik istisnaları (eksik dosyalar, desteklenmeyen formatlar vb.) yakalamak için bir try‑catch bloğu ekleyelim.

```csharp
try
{
    // (All steps 2‑5 go here)
    Console.WriteLine("Batch OCR processing finished successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR processing: {ex.Message}");
}
```

> **Neden sarmalısınız:** Büyük bir klasörde programı çalıştırdığınızda tek bir bozuk görüntü tüm işi durdurabilir. Doğru hata yönetimiyle sorunu kaydedip kalan dosyalarla devam edebilirsiniz.

## Tam, Çalıştırmaya Hazır Örnek

Aşağıda `Program.cs` dosyasına kopyalayıp yapıştırabileceğiniz tam program yer alıyor. Görüntü yollarının makinenizdeki gerçek dosyalara işaret ettiğinden emin olun.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchExample
{
    static void Main()
    {
        try
        {
            // Step 2: Define the image files to be processed
            var imageFiles = new List<string>
            {
                @"C:\Images\invoice1.jpg",
                @"C:\Images\receipt2.png",
                @"C:\Images\scan3.tif"
            };

            // Step 3: Create a BatchRecognizer and configure optional settings
            var ocrBatch = new BatchRecognizer
            {
                // Set the degree of parallelism (default = Environment.ProcessorCount)
                Parallelism = 4,

                // Hook into progress events to monitor processing
                ProgressChanged = (s, e) =>
                    Console.WriteLine($"Processed {e.Completed}/{e.Total} – {e.CurrentFile}")
            };

            // Step 4: Run OCR on the batch of images (returns file → OcrResult)
            IDictionary<string, OcrResult> ocrResults = ocrBatch.Recognize(imageFiles);

            // Step 5: Write each OCR result to a corresponding .txt file
            foreach (var entry in ocrResults)
            {
                string txtPath = Path.ChangeExtension(entry.Key, ".txt");
                File.WriteAllText(txtPath, entry.Value.Text);
                Console.WriteLine($"Saved OCR text to {txtPath}");
            }

            // Step 6: Indicate that batch processing has completed
            Console.WriteLine("Batch OCR processing finished successfully.");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during batch OCR processing: {ex.Message}");
        }
    }
}
```

### Beklenen Çıktı

`dotnet run` komutunu çalıştırdığınızda şu benzeri bir çıktı göreceksiniz:

```
Processed 1/3 – C:\Images\invoice1.jpg
Saved OCR text to C:\Images\invoice1.txt
Processed 2/3 – C:\Images\receipt2.png
Saved OCR text to C:\Images\receipt2.txt
Processed 3/3 – C:\Images\scan3.tif
Saved OCR text to C:\Images\scan3.txt
Batch OCR processing finished successfully.
```

Her `.txt` dosyası artık karşılık gelen görüntünün düz metin versiyonunu içeriyor—tam da **görüntüleri metne dönüştürme** ihtiyacınızı karşılayacak şekilde ölçekli.

---

## Sık Sorulan Sorular & Köşe Durumları

### Hangi görüntü formatları destekleniyor?

Aspose.OCR JPEG, PNG, TIFF, BMP ve GIF formatlarını kutudan çıkar çıkmaz destekler. WebP gibi bir formatla karşılaşırsanız önce dönüştürün ya da üçüncü‑taraf bir çözücü kullanın.

### OCR dilini sadece İngilizce ile sınırlayabilir miyim?

Evet. `BatchRecognizer` üzerindeki `Language` özelliğini `Recognize` çağrısından önce ayarlayın:

```csharp
ocrBatch.Language = "en";
```

Dili sınırlamak, özellikle sadece **görüntülerden metin nasıl çıkarılır** sorusuna tek bir dilde yanıt arıyorsanız doğruluğu ve hızı artırabilir.

### Belleği tüketmeden binlerce dosyayı nasıl işlerim?

Listeyi daha küçük partilere (örneğin 500 dosya) bölün ve yukarıdaki rutini bir döngü içinde çalıştırın. Böylece bellek içinde tutulan sözlük yönetilebilir kalır ve her parti için ilerleme kaydı tutabilirsiniz.

### OCR sonuçlarını dosyalar yerine bir veritabanına kaydetmem gerekirse?

`File.WriteAllText` çağrısını tercih ettiğiniz veri erişim kodu ile değiştirin. Örneğin Dapper kullanarak:

```csharp
connection.Execute(
    "INSERT INTO OcrResults (FilePath, Text) VALUES (@Path, @Text)",
    new { Path = entry.Key, Text = entry.Value.Text });
```

---

## Sonuç

Aspose.OCR ile **C#'ta toplu OCR işleme**yi, **görüntüleri metne dönüştürme**yi ustaca yapmayı, ve **görüntülerden metin nasıl çıkarılır** sorusuna verimli bir yanıt üretmeyi öğrendiniz. Tüm iş akışı—dosya yollarını toplama, bir `BatchRecognizer` yapılandırma, OCR çalıştırma ve sonuçları kalıcı hale getirme—tek, okunması kolay bir programda bir araya geliyor.

Sırada ne var? Çok çekirdekli bir sunucuda `Parallelism` değerini artırın, dil paketleriyle deney yapın ya da çıktı sonrası imla denetimi ekleyin. Ayrıca çıkarılan metni Azure Cognitive Search'e göndererek taranmış belgelerinizi saniyeler içinde aranabilir hâle getirebilirsiniz.

PDF OCR'ı ya da çok sayfalı TIFF'ler gibi bir varyasyonunuz varsa yorumlarda paylaşın; sohbeti sürdürelim. Mutlu kodlamalar!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Klasörlerde OCR İşlemi Kullanarak Görüntülerden Metin Çıkarma](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Aspose.OCR for .NET ile Listede Toplu OCR Görüntü İşleme](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Aspose.OCR for .NET ile ZIP Arşivlerinden Metin Çıkarma](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}