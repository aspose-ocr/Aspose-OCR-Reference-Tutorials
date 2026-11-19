---
category: general
date: 2026-05-21
description: Aspose OCR GPU, metin görüntülerini hızlı bir şekilde tanımanıza olanak
  tanır. OCR için görüntüyü nasıl yükleyeceğinizi, TIFF'ten metin çıkarmayı ve performansı
  artırmayı öğrenin.
draft: false
keywords:
- aspose ocr gpu
- recognize text image
- ocr tiff image
- load image for ocr
- extract text from tiff
language: tr
og_description: Aspose OCR GPU, metin çıkarımını hızlandırır. Bu kılavuz, OCR için
  görüntünün nasıl yükleneceğini, metin görüntüsünün nasıl tanınacağını ve TIFF'ten
  metnin nasıl verimli bir şekilde çıkarılacağını gösterir.
og_title: Aspose OCR GPU – C# ile TIFF'ten Metin Görüntüsü Tanıma
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Aspose OCR GPU lets you recognize text image quickly. Learn how to
    load image for OCR, extract text from TIFF and boost performance.
  headline: 'Aspose OCR GPU: Recognize Text Image from TIFF with C#'
  type: TechArticle
- description: Aspose OCR GPU lets you recognize text image quickly. Learn how to
    load image for OCR, extract text from TIFF and boost performance.
  name: 'Aspose OCR GPU: Recognize Text Image from TIFF with C#'
  steps:
  - name: Enables GPU acceleration (optional, with automatic CPU fallback).
    text: Enables GPU acceleration (optional, with automatic CPU fallback).
  - name: Creates an `OcrEngine` configured for English.
    text: Creates an `OcrEngine` configured for English.
  - name: Loads a large **OCR TIFF image** from disk.
    text: Loads a large **OCR TIFF image** from disk.
  - name: Runs the recognition and prints the result.
    text: Runs the recognition and prints the result.
  type: HowTo
tags:
- aspose
- ocr
- csharp
title: 'Aspose OCR GPU: C# ile TIFF''ten Metin Görüntüsünü Tanıma'
url: /tr/net/ocr-optimization/aspose-ocr-gpu-recognize-text-image-from-tiff-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR GPU: TIFF'ten C# ile Metin Görüntüsü Tanıma

Büyük bir TIFF dosyasından **metin görüntüsü** tanımayı, CPU'nuzu durma noktasına getirmeden nasıl yapabileceğinizi hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok belge‑işleme hattında darboğaz OCR adımıdır, özellikle gigabaytlarca taranmış sayfayı sade bir motorla işlediğinizde.  

İyi haber? **Aspose OCR GPU** süreci turbo‑şarj yapabilir ve aşağıdaki kod örneği **OCR için resmi yükleme**, **TIFF'ten metin çıkarma** ve GPU mevcut değilse sorunsuz bir şekilde geri dönüş yapma konusunda tam olarak nasıl yapılacağını gösteriyor. Hadi başlayalım.

## Bu Eğitimde Neler Kapsanıyor

1. GPU hızlandırmayı etkinleştirir (isteğe bağlı, otomatik CPU geri dönüşü ile).  
2. `OcrEngine`'i İngilizce için yapılandırır.  
3. Diskten büyük bir **OCR TIFF görüntüsü** yükler.  
4. Tanıma işlemini çalıştırır ve sonucu yazdırır.  

Sonunda her adımın **neden** önemli olduğunu, yaygın kenar durumlarını nasıl ele alacağınızı anlayacak ve PDF'lere, çok sayfalı TIFF'lere ya da gerçek zamanlı kamera akışlarına uyarlayabileceğiniz çalıştırılabilir bir örnek elde edeceksiniz.

> **Önkoşullar** – .NET 6+ (veya .NET Framework 4.7+), Aspose.OCR NuGet paketi ve hızı artırmak istiyorsanız GPU‑destekli bir makine. Özel bir donanım gerekmez; GPU algılanmadığında kod sadece CPU'yu kullanır.

---

![Aspose OCR GPU processing diagram showing CPU fallback](/images/aspose-ocr-gpu-diagram.png){: .align-center alt="aspose ocr gpu"}

## Adım 1: GPU Hızlandırmayı Etkinleştir (İsteğe Bağlı)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // adds GPU support

// Enable GPU if a compatible device is present.
// The call is safe – if no GPU is found Aspose falls back to CPU.
OcrEngine.EnableGpu(true);
```

**Neden Önemli:**  
GPU çekirdekleri, görüntü ön işleme (ikiliye çevirme, gürültü giderme) ve sinir ağı çıkarımı için gereken büyük paralellikte mükemmeldir. `EnableGpu(true)`'ı etkinleştirerek motorun bu görevleri dışarı aktarabilmesi için yeşil ışığı yakarsınız. Makinede CUDA uyumlu bir kart yoksa, Aspose sessizce CPU'ya geri döner, böylece sert bir çökme yaşamazsınız.

**İpucu:**  
Windows'ta en yeni NVIDIA sürücüsüne ve CUDA araç setine ihtiyacınız olabilir. Linux'ta ise `nvidia‑driver` ve `libcuda.so`'nun kütüphane yolunuzda olduğundan emin olun.

## Adım 2: OCR Motorunu Oluştur ve Yapılandır

```csharp
// Step 2: Instantiate the OCR engine and set the language.
var ocrEngine = new OcrEngine
{
    // English works for most scanned docs; you can pick other languages here.
    Language = OcrLanguage.English
};
```

**Neden Önemli:**  
`OcrEngine`, **Aspose OCR GPU**'nin kalbidir. `Language` ayarı, temel sinir modeline hangi karakter setinin beklendiğini söyler ve doğruluğu büyük ölçüde artırır. Zor belgeler için `Resolution`, `PreprocessOptions` veya `RecognitionMode` ayarlarını da değiştirebilirsiniz.

## Adım 3: OCR İçin Görüntüyü Yükle

```csharp
// Step 3: Load a large TIFF image from disk.
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/large_doc.tif");
```

**Neden Önemli:**  
Bir TIFF birden fazla sayfa, yüksek çözünürlük ve kayıpsız sıkıştırma içerebilir—arşiv taramaları için mükemmel ama bellek açısından ağırdır. `ImageStream.FromFile` dosyayı akış olarak okur, çok büyük görüntüler için tam bellek yüklemesinden kaçınır.

**Kenar Durumu:**  
Çok sayfalı bir TIFF işlemek istiyorsanız, bir döngü içinde `ocrEngine.Image = ImageStream.FromFile(path, pageIndex);` çağrısı yapın ve `pageIndex`'i `ocrEngine.Image.IsNull` `true` döndürene kadar artırın.

## Adım 4: Tanıma İşlemini Gerçekleştir

```csharp
// Step 4: Run the OCR process.
ocrEngine.Recognize();
```

**Neden Önemli:**  
`Recognize()` tüm ağır işleri yapar: ön işleme, düzen analizi, karakter segmentasyonu ve sonunda sinir ağı çıkarımı. GPU aktif olduğunda, çıkarım adımı GPU'da çalışır ve büyük TIFF'lerde işlem süresinin %50‑80'ini azaltabilir.

## Adım 5: Sonuçları Çıktıla

```csharp
// Step 5: Show how many characters were extracted and how long it took.
Console.WriteLine($"Recognized {ocrEngine.Text.Length} characters in {ocrEngine.ProcessingTime} ms");

// Optional: print the extracted text (be careful with huge strings!)
Console.WriteLine("--- Extracted Text Start ---");
Console.WriteLine(ocrEngine.Text);
Console.WriteLine("--- Extracted Text End ---");
```

**Neden Önemli:**  
`ocrEngine.Text`, görüntüden elde edilen tam birleştirilmiş dizeyi tutar, `ProcessingTime` ise CPU vs. GPU çalıştırmalarını karşılaştırmak için hızlı bir ölçüm sağlar. Konsol çıktısı hızlı hata ayıklama için kullanışlıdır; üretimde muhtemelen metni bir veritabanına ya da dosyaya yazarsınız.

**Beklenen çıktı (2 sayfalı bir fatura örneği):**

```
Recognized 1342 characters in 842 ms
--- Extracted Text Start ---
Invoice #12345
Date: 2026‑04‑30
...
Total: $1,234.56
--- Extracted Text End ---
```

GPU mevcut değilse, aynı donanımda süre ~1800 ms'ye çıkabilir ve **aspose ocr gpu**'nun faydasını açıkça gösterir.

---

## Yaygın Tuzakları Ele Alma

| Durum | Dikkat Edilmesi Gereken | Nasıl Düzeltilir |
|-----------|-------------------|------------|
| **GPU algılanmadı** | `EnableGpu(true)` sessizce geri döner, ancak hâlâ GPU kullandığını düşünebilirsiniz. | Çağrıdan sonra `OcrEngine.IsGpuEnabled`'ı kontrol edin; sonucu kaydedin. |
| **Büyük TIFF'te bellek yetersizliği** | 10 000 × 10 000 piksel bir görüntüyü yüklemek RAM'i aşabilir. | Yükleme sırasında örnekleme yapmak için `ImageStream.FromFile(path, pageIndex, maxResolution: 300)` kullanın. |
| **Yanlış dil** | Fransızca bir belgede İngilizce model bozuk çıktı verir. | `Language = OcrLanguage.French` olarak ayarlayın veya çok dilli modu etkinleştirin. |
| **Çok sayfalı TIFF** | Sadece ilk sayfa işleniyor. | `ImageStream.FromFile(path, pageNumber)` kullanarak sayfalar üzerinde döngü yapın. |

## Tam Çalışan Örnek

Aşağıda bir konsol uygulamasına ekleyebileceğiniz tam program yer alıyor. Hata yönetimi, GPU durum kaydı ve kendi ölçümleriniz için basit bir zamanlayıcı içerir.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // adds GPU support

namespace AsposeOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Enable GPU acceleration (if available)
            OcrEngine.EnableGpu(true);
            Console.WriteLine($"GPU enabled: {OcrEngine.IsGpuEnabled}");

            // 2️⃣ Create the OCR engine and set language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 3️⃣ Load the TIFF image (replace with your actual path)
            string imagePath = @"YOUR_DIRECTORY\large_doc.tif";
            try
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Failed to load image: {ex.Message}");
                return;
            }

            // 4️⃣ Perform recognition
            try
            {
                ocrEngine.Recognize();
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Recognition error: {ex.Message}");
                return;
            }

            // 5️⃣ Output results
            Console.WriteLine($"Recognized {ocrEngine.Text.Length} characters in {ocrEngine.ProcessingTime} ms");
            Console.WriteLine("--- Extracted Text Start ---");
            Console.WriteLine(ocrEngine.Text);
            Console.WriteLine("--- Extracted Text End ---");
        }
    }
}
```

Kopyalayıp yapıştırın, **F5** tuşuna basın ve konsolun karakter sayısını ve çıkarılan metni göstermesini izleyin. `OcrLanguage.English`'i Aspose tarafından desteklenen başka bir dil ile değiştirin; böylece İspanyolca, Almanca vb. dillerde **metin görüntüsü tanıma** yapabilirsiniz.

## Özet ve Sonraki Adımlar

Şimdi **aspose ocr gpu** kullanarak **OCR TIFF görüntüsünden metin görüntüsü tanıma**, **OCR için görüntü yükleme** ve **TIFF'ten metin çıkarma** konularını ele aldık. Temel fikirler—GPU'yu etkinleştirme, dili yapılandırma, TIFF'i akış olarak okuma ve sonucu okuma—JPEG veya PNG gibi diğer dosya formatlarına da taşınabilir.

### Sonraki Denemeler

- **Toplu işleme**: Bir klasördeki TIFF'ler üzerinde döngü oluşturun, her bir `ocrEngine.Text`'i bir `.txt` dosyasına yazın.  
- **Çok sayfalı işleme**: Çok sayfalı bir belgede her sayfayı işlemek için `while` döngüsü içinde `ImageStream.FromFile(path, pageIndex)` kullanın.  
- **Özel ön işleme**: Gürültülü taramalar için `ocrEngine.PreprocessOptions` (ör. `Denoise`, `Deskew`) ayarlarını değiştirin.  
- **GPU performans ölçümü**: Aynı makinede `EnableGpu(true)` ile ve olmadan `ProcessingTime` kaydedin, hız artışını ölçün.

Deney yapmaktan çekinmeyin—GPU hızlandırma yüksek çözünürlüklü, çok sayfalı TIFF'lerde en çok farkı gösterir, ancak mütevazı bir 1080 Ti bile tanıma süresini büyük ölçüde kısaltır.

Belirli bir belge türü hakkında sorularınız mı var ya da çıktıyı bir veritabanına entegre etme konusunda yardıma mı ihtiyacınız var? Aşağıya yorum bırakın, iyi kodlamalar!

## İlgili Eğitimler

- [Görüntüden Metin Çıkarma – Aspose.OCR ile .NET için OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)
- [OCR'da Dikdörtgen Hazırlayarak Görüntüden Metin Çıkarma](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Görüntüden Metin Çıkarma – Aspose.OCR ile Satır Tanıma](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}