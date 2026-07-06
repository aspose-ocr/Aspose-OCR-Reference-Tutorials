---
category: general
date: 2026-06-16
description: C#'ta toplu OCR işleme, görüntüleri hızlı bir şekilde metne dönüştürmenizi
  sağlar. Aspose.OCR kullanarak görüntülerden metin çıkarmayı adım adım kodla öğrenin.
draft: false
keywords:
- batch OCR processing
- extract text from images
- convert images to text
language: tr
og_description: C#'ta toplu OCR işleme, görüntüleri metne dönüştürür. Aspose.OCR kullanarak
  görüntülerden metin çıkarmak için bu kılavuzu izleyin.
og_title: C#'ta Toplu OCR İşleme – Görüntülerden Metin Çıkarma
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Batch OCR processing in C# lets you convert images to text quickly.
    Learn how to extract text from images using Aspose.OCR with step‑by‑step code.
  headline: Batch OCR Processing in C# – Complete Guide to Extract Text from Images
  type: TechArticle
- description: Batch OCR processing in C# lets you convert images to text quickly.
    Learn how to extract text from images using Aspose.OCR with step‑by‑step code.
  name: Batch OCR Processing in C# – Complete Guide to Extract Text from Images
  steps:
  - name: Expected Output
    text: 'Assuming you have three images (`invoice1.png`, `receipt2.jpg`, `form3.tif`)
      in the input folder, the output folder will contain:'
  - name: What if some images fail to process?
    text: '`OcrBatchProcessor` logs errors to the console by default and continues
      with the next file. For production use, you can subscribe to the `OnError` event
      to collect failed filenames and retry later.'
  - name: Can I process PDFs directly?
    text: Yes. Aspose.OCR treats each page of a PDF as an image internally. Just point
      `InputFolder` to a directory containing PDFs, and the processor will extract
      text from every page—effectively **convert images to text** even when the source
      is a PDF.
  - name: How do I handle multi‑language documents?
    text: Set `Language` to `OcrLanguage.Multilingual` or specify a list of languages
      if the library version supports it. The engine will attempt to recognize characters
      from all provided languages, which is handy for international invoices.
  - name: What about memory consumption?
    text: The batch processor streams each image, so memory usage stays low even with
      thousands of files. However, enabling a high `MaxDegreeOfParallelism` on a memory‑constrained
      machine could cause spikes. Monitor your RAM and adjust the thread count accordingly.
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: C#'ta Toplu OCR İşleme – Görsellerden Metin Çıkarma İçin Tam Rehber
url: /tr/net/text-recognition/batch-ocr-processing-in-c-complete-guide-to-extract-text-fro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Toplu OCR İşleme – Görsellerden Metin Çıkarma Tam Kılavuzu

Her bir resim için ayrı bir döngü yazmadan **toplu OCR işleme**yi C#’ta nasıl yapabileceğinizi hiç merak ettiniz mi? Tek başınıza değilsiniz. Onlarca—hatta yüzlerce—taralı fiş, fatura ya da el yazısı notunuz olduğunda, her dosyayı manuel olarak OCR motoruna beslemek kısa sürede bir kabusa dönüşür.  

İyi haber? Aspose.OCR ile *görselleri metne dönüştürme*yi tek, düzenli bir işlemde gerçekleştirebilirsiniz. Bu öğreticide, kütüphaneyi kurmaktan üretim‑hazır bir toplu işi çalıştırmaya kadar tüm süreci adım adım ele alacağız; **görsellerden metin çıkarma** ve sonuçları ihtiyacınız olan formatta kaydetme konularını göstereceğiz.

> **Neler elde edeceksiniz:** Tüm klasörü işleyen, orijinal dosyaların yanına düz‑metin (veya JSON, XML, HTML, PDF) dosyaları yazan hazır bir konsol uygulaması ve maksimum verimlilik için paralellik ayarlarını nasıl yapacağınızı gösteren bir rehber.

## Ön Koşullar

- .NET 6.0 SDK veya daha yenisi (kod .NET Core ve .NET Framework’te de çalışır)
- Visual Studio 2022, VS Code veya tercih ettiğiniz herhangi bir C# editörü
- Aspose.OCR NuGet lisansı (değerlendirme için ücretsiz deneme sürümü yeterli)
- **Görselleri metne dönüştürmek** istediğiniz bir resim klasörü (`.png`, `.jpg`, `.tif`, vb.)

Bu maddeleri işaretlediyseniz, başlayalım.

![Diagram illustrating batch OCR processing flow](batch-ocr-workflow.png "Batch OCR processing flow")

## Adım 1: Aspose.OCR’yi NuGet üzerinden kurun

İlk olarak Aspose.OCR paketini projenize ekleyin. Proje dizininde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

Ya da Visual Studio içinde, *Dependencies → Manage NuGet Packages* üzerine sağ‑tıklayın, **Aspose.OCR**’u aratın ve *Install*’a tıklayın. Bu tek satır, **toplu OCR işleme** için ihtiyacınız olan her şeyi getirir.

> **Pro ipucu:** Paket sürümünü güncel tutun; Haziran 2026 itibarıyla en yeni sürüm yeni görüntü formatlarını destekliyor ve çok‑dilli doğruluğu artırıyor.

## Adım 2: Konsol Taslağını Oluşturun

Henüz oluşturmadıysanız yeni bir C# konsol uygulaması yaratın ve oluşturulan `Program.cs` dosyasını aşağıdaki taslakla değiştirin. En üstteki `using Aspose.OCR;` yönergesine dikkat edin – bu, `OcrBatchProcessor` sınıfını bize sağlayan ad alanıdır.

```csharp
using Aspose.OCR;
using System;

class BatchDemo
{
    static void Main()
    {
        // We'll fill this in later.
    }
}
```

Şu an dosya sadece bir yer tutucu, ancak **toplu OCR işleme** mantığımız için temiz bir başlangıç noktası.

## Adım 3: OcrBatchProcessor’ı Başlatın

`OcrBatchProcessor`, bir klasörü tarayan, her desteklenen görselde OCR çalıştıran ve çıktıyı yazan iş gücüdür. Oluşturması çok basittir:

```csharp
// Step 3: Create an OCR batch processor instance
var ocrBatchProcessor = new OcrBatchProcessor();
```

Neden tek‑resim API’si yerine toplu işlemci kullanıyorsunuz? Toplu sınıf dosya listelemesini, hata kaydını ve hatta paralel yürütmeyi otomatik olarak halleder; bu sayede döngü kodlamaya daha az, doğruluk ayarına daha çok zaman harcarsınız.

## Adım 4: Giriş ve Çıkış Klasörlerini Belirtin

İşlemcinin görselleri nereden okuyacağını ve sonuçları nereye bırakacağını söyleyin. Yer tutucu yolları makinenizdeki gerçek dizinlerle değiştirin.

```csharp
// Step 4: Configure the input folder containing images to process
ocrBatchProcessor.InputFolder = @"C:\MyProjects\OCRDemo\Images\Batch";

// Step 5: Set the folder where OCR results will be saved
ocrBatchProcessor.OutputFolder = @"C:\MyProjects\OCRDemo\Results\Batch";
```

Her iki klasör de uygulamayı çalıştırmadan önce var olmalıdır; aksi takdirde `DirectoryNotFoundException` alırsınız. Programatik olarak oluşturmak mümkün, ancak açıklık açısından örneği basit tuttuk.

## Adım 5: Çıktı Formatını Seçin

Aspose.OCR düz metin, JSON, XML, HTML ya da PDF üretebilir. Çoğu **görsellerden metin çıkarma** senaryosu için düz metin yeterli olur, ancak ihtiyacınıza göre değiştirebilirsiniz.

```csharp
// Step 6: Choose the desired output format (e.g., plain text)
ocrBatchProcessor.OutputFormat = ResultFormat.Text;   // alternatives: Json, Xml, Html, Pdf, etc.
```

Eğer sonraki aşamalarda yapılandırılmış veri gerekiyorsa, `ResultFormat.Json` sağlam bir tercihtir. Kütüphane, her sayfanın metnini bir JSON nesnesi içinde otomatik olarak paketler ve düzen bilgilerini korur.

## Adım 6: Dil ve Paralellik Ayarlarını Yapın

OCR doğruluğu doğru dil modeline bağlıdır. İngilizce çoğu Batı belgesi için yeterli, ancak desteklenen herhangi bir dili (Arapça, Çince vb.) seçebilirsiniz. Ayrıca işlemcinin kaç iş parçacığı kullanacağını belirtebilirsiniz—varsayılan olarak dört adete kadar.

```csharp
// Step 7: Specify the language for OCR recognition
ocrBatchProcessor.Language = OcrLanguage.English;

// Step 8: Define the level of parallelism (up to 4 concurrent threads)
ocrBatchProcessor.MaxDegreeOfParallelism = 4;
```

**Paralelliğin önemi:** Quad‑core bir CPU’ya sahipseniz, `MaxDegreeOfParallelism` değerini `4` yapmanız işlem süresini yaklaşık %75 azaltabilir. İki çekirdekli bir dizüstü bilgisayarda ise `2` daha güvenli bir seçimdir. Donanımınıza en uygun ayarı bulmak için deneme yapın.

## Adım 7: Toplu İşi Çalıştırın

Şimdi asıl iş burada gerçekleşiyor. Tek bir satır tüm hattı başlatır, giriş klasöründeki her görseli işler ve sonuçları çıkış klasörüne yazar.

```csharp
// Step 9: Execute the batch processing of all supported image files
ocrBatchProcessor.Execute();

Console.WriteLine("Batch OCR completed.");
```

Konsol *Batch OCR completed.* mesajını verdiğinde, her orijinal görselin yanına seçtiğiniz formatta bir `.txt` (veya başka) dosya bulacaksınız. Dosya adları kaynakla aynı olduğundan OCR çıktısını görselle eşleştirmek çok kolaydır.

## Tam Çalışan Örnek

Hepsini bir araya getirdiğimizde, `Program.cs` içine kopyalayıp hemen çalıştırabileceğiniz tam program aşağıdadır:

```csharp
using Aspose.OCR;
using System;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create an OCR batch processor instance
        var ocrBatchProcessor = new OcrBatchProcessor();

        // Step 2: Configure the input folder containing images to process
        ocrBatchProcessor.InputFolder = @"C:\MyProjects\OCRDemo\Images\Batch";

        // Step 3: Set the folder where OCR results will be saved
        ocrBatchProcessor.OutputFolder = @"C:\MyProjects\OCRDemo\Results\Batch";

        // Step 4: Choose the desired output format (plain text is default)
        ocrBatchProcessor.OutputFormat = ResultFormat.Text; // alternatives: Json, Xml, Html, Pdf, etc.

        // Step 5: Specify the language for OCR recognition
        ocrBatchProcessor.Language = OcrLanguage.English;

        // Step 6: Define the level of parallelism (up to 4 concurrent threads)
        ocrBatchProcessor.MaxDegreeOfParallelism = 4;

        // Step 7: Execute the batch processing of all supported image files
        ocrBatchProcessor.Execute();

        Console.WriteLine("Batch OCR completed.");
    }
}
```

### Beklenen Çıktı

Giriş klasöründe üç resim (`invoice1.png`, `receipt2.jpg`, `form3.tif`) olduğunu varsayalım; çıkış klasörü şu dosyaları içerecek:

```
invoice1.txt
receipt2.txt
form3.txt
```

Her `.txt` dosyası, ilgili görselden çıkarılan ham karakterleri barındırır. Notepad ile açtığınızda, taramanın düz‑metin temsilini göreceksiniz.

## Yaygın Sorular & Kenar Durumlar

### Bazı görseller işlenemezse ne olur?

`OcrBatchProcessor` hataları varsayılan olarak konsola yazar ve bir sonraki dosyaya geçer. Üretim ortamında `OnError` olayına abone olarak başarısız dosya adlarını toplayabilir ve daha sonra yeniden deneyebilirsiniz.

```csharp
ocrBatchProcessor.OnError += (sender, args) =>
{
    Console.WriteLine($"Failed on {args.FileName}: {args.Exception.Message}");
};
```

### PDF’leri doğrudan işleyebilir miyim?

Evet. Aspose.OCR, bir PDF’nin her sayfasını dahili olarak bir görsel gibi ele alır. `InputFolder`’ı PDF içeren bir dizine yönlendirin; işlemci her sayfadan metin çıkarır—kaynak bir PDF olsa bile **görselleri metne dönüştürme** gerçekleşir.

### Çok‑dilli belgeler nasıl ele alınır?

`Language` değerini `OcrLanguage.Multilingual` olarak ayarlayın veya kütüphane sürümü destekliyorsa bir dil listesi belirtin. Motor, sağlanan tüm dillerdeki karakterleri tanımaya çalışır; bu, uluslararası faturalar için çok kullanışlıdır.

### Bellek tüketimi nasıl?

Toplu işlemci her görseli akış (stream) olarak okur, bu yüzden binlerce dosya olsa da bellek kullanımı düşük kalır. Ancak bellek kısıtlı bir makinede yüksek `MaxDegreeOfParallelism` değeri ani bellek artışına yol açabilir. RAM’inizi izleyin ve iş parçacığı sayısını buna göre ayarlayın.

## Daha İyi Doğruluk İçin İpuçları

- **Görselleri ön‑işleyin:** Gürültüyü temizleyin, eğikliği düzeltin ve gri tonlamaya çevirin. Aspose.OCR, `ImagePreprocessOptions` aracılığıyla `ocrBatchProcessor`a eklenebilen seçenekler sunar.
- **Doğru formatı seçin:** Düzen korunması gerekiyorsa, `ResultFormat.Html` ya da `Pdf` satır sonlarını ve temel stil bilgilerini tutar.
- **Sonuçları doğrulayın:** Boş çıktı dosyalarını kontrol eden basit bir post‑processing adımı ekleyin—boş dosyalar genellikle tanıma hatasını gösterir.

## Sonraki Adımlar

Artık **toplu OCR işleme**yi **görsellerden metin çıkarma** amacıyla ustaca kullandığınıza göre, aşağıdaki konuları keşfetmek isteyebilirsiniz:

- **Veritabanı entegrasyonu** – her OCR sonucunu meta veriyle birlikte depolayarak arama imkanı sağlayın.
- **Kullanıcı arayüzü ekleyin** – klasörleri sürükle‑bırak yapabilen küçük bir WPF ya da WinForms ön‑uç oluşturun.
- **Ölçeklendirme** – toplu işi Azure Functions veya AWS Lambda’da çalıştırarak bulut‑yerel işleme geçiş yapın.

Bu konular, burada ele aldığımız temel kavramlar üzerine inşa edildiği için çözümünüzü kolayca genişletebilirsiniz.

---

**Kodlamanın tadını çıkarın!** Bir sorunla karşılaşırsanız ya da geliştirme önerileriniz varsa, aşağıya yorum bırakın. Konuşmayı sürdürelim ve OCR otomasyonunu daha da sorunsuz hâle getirelim.


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}