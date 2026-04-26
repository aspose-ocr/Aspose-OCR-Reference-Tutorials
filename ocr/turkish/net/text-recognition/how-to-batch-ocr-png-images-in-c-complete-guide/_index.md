---
category: general
date: 2026-04-26
description: PNG görüntülerini hızlı bir şekilde toplu OCR ile işleme. PNG'den metin
  çıkarmayı, görüntüleri metne dönüştürmeyi, tanınan metni yazmayı ve Aspose OCR ile
  PNG dizinini okumayı öğrenin.
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: tr
og_description: C# ile Aspose OCR kullanarak PNG görüntülerini toplu OCR nasıl yapılır.
  Bu kılavuz, PNG'den metin çıkarma, görüntüleri metne dönüştürme ve tanınan metni
  verimli bir şekilde yazma yöntemlerini gösterir.
og_title: C#'ta PNG Görüntülerini Toplu OCR Yapma – Adım Adım
tags:
- OCR
- C#
- Aspose
title: C#'ta PNG Görsellerini Toplu OCR İşlemi Nasıl Yapılır – Tam Rehber
url: /tr/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Batch OCR PNG Images in C# – Complete Guide

Hiç **bir klasördeki tüm PNG dosyalarını ayrı ayrı program yazmadan toplu OCR** yapmanın yolunu merak ettiniz mi? Sadece siz değil, onlarca ekran görüntüsü, taranmış fiş ya da metne dönüştürülmesi gereken grafikle uğraşan birçok kişi var. Bu öğreticide **PNG’den metin çıkarma**, **görüntüleri metne çevirme** ve **tanınan metni ayrı dosyalara yazma** işlemlerini otomatik olarak PNG dizinini okuyarak nasıl yapacağınızı adım adım göstereceğiz.

Bu rehberin sonunda, tek seferde istediğiniz sayıda görüntüyü işleyen, çalıştırmaya hazır bir C# konsol uygulamanız olacak. Ek scriptlere, manuel kopyala‑yapıştır işlemlerine gerek yok – sadece sizin için işi yapan saf kod.

## What You’ll Need

- **.NET 6.0** veya daha yeni bir sürüm (kod .NET Framework’te de çalışır).  
- **Aspose.OCR for .NET** NuGet paketi (deneme sürümü test için yeterli).  
- OCR yapmak istediğiniz birkaç *.png* dosyasının bulunduğu bir klasör.  
- Visual Studio 2022 ya da tercih ettiğiniz herhangi bir C# IDE.

Bu gereksinimlere sahipseniz, doğrudan uygulamaya geçebiliriz.

## Step 1 – Prepare Your Input and Output Folders *(Read PNG Directory)*

İlk adım, programı görüntülerin bulunduğu klasöre yönlendirmek ve ortaya çıkan *.txt* dosyalarının nereye kaydedileceğini belirlemek. `Directory.GetFiles` kullanarak dizindeki tüm PNG dosyalarını temiz bir şekilde enumerable olarak alıyoruz.

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**Neden önemli:**  
- `*.png` gibi bir joker karakter kullanmak, yalnızca görüntü dosyalarını işlediğimizden emin olur, rastgele belgeleri göz ardı eder.  
- Çıktı klasörünü anında oluşturmak, ileride `DirectoryNotFoundException` hatasını önler.

> **Pro tip:** Başka formatları (JPEG, BMP) da desteklemek isterseniz, arama desenini genişletin ya da `Directory.EnumerateFiles` metodunu birden fazla uzantıyla çağırın.

## Step 2 – Initialise the OCR Engine *(Convert Images to Text)*

Aspose.OCR iki motor tipi sunar: CPU‑tabanlı `OcrEngine` ve GPU‑hızlandırmalı `GpuOcrEngine`. Çoğu toplu iş için CPU motoru yeterlidir, ancak güçlü bir GPU’nuz varsa sınıf adını değiştirerek GPU motorunu kullanabilirsiniz.

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**Neden önemli:**  
- Dilin belirtilmesi, motorun hangi karakter setini bekleyeceğini bilmesi sayesinde doğruluğu büyük ölçüde artırır.  
- Performans darboğazı yaşadığınızda `GpuOcrEngine`e geçmek sadece bir satır değişiklikle mümkün.

## Step 3 – Create a Batch Recogniser

Aspose, dosya yolu enumerable’ını kabul eden ve sonuçları tek tek akıtan kullanışlı bir `BatchRecognizer` sağlar. Bu, tüm görüntülerin aynı anda belleğe yüklenmesini engeller – büyük klasörler için kritik bir detaydır.

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**Neden önemli:**  
- Toplu tanıyıcı, döngü mantığını kapsüller; böylece her bir sonuçla ne yapacağımıza odaklanırız, güvenli bir şekilde nasıl yineleyeceğimizi düşünmek zorunda kalmayız.

## Step 4 – Run OCR on All Images and Write the Output *(Write Recognized Text)*

Şimdi OCR işlemini gerçekleştiriyoruz. `Recognize` metodu, her bir sonuçta çıkarılan metin ve diğer meta verileri içeren bir `IEnumerable<RecognitionResult>` döndürür.

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**Neden önemli:**  
- `File.WriteAllText` kullanmak, metnin varsayılan olarak UTF‑8 kodlamasıyla kaydedilmesini sağlar ve özel karakterleri korur.  
- Artımlı adlandırma (`out_0.txt`, `out_1.txt`) işleme sırasını yansıttığı için hata ayıklamayı kolaylaştırır.

> **Köşe durum:** Bir görüntü OCR’da başarısız olursa (ör. bozuk dosya), `RecognitionResult.Text` boş olur. Döngü içinde basit bir kontrol ekleyerek hataları kaydedebilirsiniz:

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## Step 5 – Put It All Together – Full Working Example

Aşağıda yeni bir konsol projesine kopyalayıp yapıştırabileceğiniz tam program yer alıyor. `using` yönergeleri, klasör doğrulaması ve toplu işlemin ne zaman bittiğini gösteren küçük bir konsol UI’si içerir.

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**Beklenen çıktı:**  
Programı çalıştırdığınızda aşağıdakine benzer bir çıktı alırsınız:

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

Ve çıktı klasöründe `out_0.txt` … `out_11.txt` dosyalarını göreceksiniz; her biri ilgili görüntünün düz metin versiyonunu içerir.

## Common Questions & Tips

| Question | Answer |
|----------|--------|
| *Can I OCR sub‑folders as well?* | Evet—`Directory.GetFiles` yerine `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)` kullanın. |
| *What if I need a different language?* | `ocrEngine.Language = Language.Spanish;` (veya desteklenen herhangi bir enum) şeklinde ayarlayın. |
| *How do I handle huge batches (thousands of files)?* | Bellek tükenmesini önlemek için parçalar halinde işleyin ya da `Parallel.ForEach` ile sınırlı bir paralellik derecesi kullanın. |
| *Is the output always UTF‑8?* | `File.WriteAllText` varsayılan olarak BOM’suz UTF‑8 yazar; bu çoğu Latin temelli dil için yeterlidir. Asya dilleri için `Encoding.UTF8`’i açıkça belirtebilirsiniz. |
| *Can I get confidence scores?* | `RecognitionResult` içinde `Confidence` bulunur; kalite kontrolü için metinle birlikte kaydedebilirsiniz. |

## Visual Overview *(How to Batch OCR – Diagram)*

![PNG klasöründen OCR motoruna → toplu tanıyıcıya → çıktı txt dosyalarına iş akışını gösteren toplu OCR diyagramı](https://example.com/diagram-how-to-batch-ocr.png "Toplu OCR nasıl yapılır")

*Alt metin, SEO gereksinimlerini karşılamak için ana anahtar kelimeyi içerir.*

## Wrapping Up

Aspose.OCR kullanarak bir PNG klasörünü toplu OCR yapma, PNG dizinini okuma ve tanınan metni her dosyaya yazma sürecini adım adım ele aldık. Çözüm tamamen bağımsız, modern .NET runtime’larında çalışır ve GPU hızlandırma, çok‑dilli destek ya da paralel işleme gibi ihtiyaçlarınıza göre genişletilebilir.

Bir sonraki adıma hazır mısınız? `Language.Latin` yerine başka bir dil seçin ya da çıktıyı bir arama indeksine entegre ederek belgelerinizin anında aranabilir olmasını sağlayın. Toplu OCR’u bir kez kavradığınızda, sınır yoktur.

Kodlamanın tadını çıkarın ve yorumlarda takıldığınız bir nokta olursa bize bildirin!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}