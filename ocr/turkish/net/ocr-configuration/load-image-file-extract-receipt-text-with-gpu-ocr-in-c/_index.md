---
category: general
date: 2026-02-14
description: Görüntü dosyasını yükleyin ve Aspose OCR GPU motorunu kullanarak makbuzdan
  metin çıkarın. Maksimum GPU belleğini ayarlamayı, GPU belleğini yapılandırmayı ve
  görüntü üzerinde OCR'ı verimli bir şekilde çalıştırmayı öğrenin.
draft: false
keywords:
- load image file
- extract text from receipt
- set max gpu memory
- run OCR on image
- configure gpu memory
language: tr
og_description: Görüntü dosyasını yükleyin ve Aspose OCR GPU motoru kullanarak makbuzdan
  metni çıkarın. Bu kılavuz, maksimum GPU belleğini ayarlamayı ve C#'ta görüntü üzerinde
  OCR çalıştırmayı gösterir.
og_title: Resim Dosyasını Yükle ve GPU OCR ile C#'ta Makbuz Metnini Çıkar
tags:
- C#
- OCR
- Aspose
- GPU
title: Resim Dosyasını Yükle ve C#'ta GPU OCR ile Makbuz Metnini Çıkar
url: /tr/net/ocr-configuration/load-image-file-extract-receipt-text-with-gpu-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntü Dosyasını Yükle ve GPU OCR ile Fiş Metnini Çıkar C#'ta

Hiç **görüntü dosyasını yükleyip** bir fişten tam metni almak istediğinizde OCR adımında takıldıysanız yalnız değilsiniz. Gerçek dünyadaki birçok uygulamada—gider takipçileri, envanter sistemleri ya da basit fiş tarama botları—bir fiş görüntüsünü hızlıca okuyabilmek oyunun kurallarını değiştirebilir.  

İyi haber? Aspose.OCR’nun GPU‑hızlandırmalı motoru sayesinde **görüntü dosyasını yükleyebilir**, **maksimum GPU belleğini ayarlayabilir** ve **görüntü üzerinde OCR çalıştırabilirsiniz** sadece birkaç satır C# koduyla. Aşağıda GPU’yu yapılandırmaktan çıkarılan düz metni yazdırmaya kadar tüm süreci adım adım göstereceğiz.

## Öğrenecekleriniz

Bu öğreticide şunları keşfedeceksiniz:

* **Görüntü dosyasını** Aspose’un `ImageStream`iyle diskinizden **yükleme**.
* **GPU belleğini** yapılandırarak motorun izin verdiğinizden fazla RAM tüketmemesini sağlama.
* **Görüntü üzerinde OCR çalıştırma** ve bir fişteki tüm karakterleri çıkarma.
* Bellek yetersizliği hataları ya da bulanık taramalar gibi yaygın sorunları ele alma.
* Çıktıyı doğrulama ve doğruluğu artırmak için ayarları ince ayar yapma.

Harici hizmetler yok, karmaşık hileler yok—sadece .NET 6+ projenize ekleyebileceğiniz saf C# kodu.

---

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* .NET 6 SDK veya daha yeni bir sürüm.
* Geçerli bir Aspose.OCR lisansı (ya da ücretsiz değerlendirme modunu kullanabilirsiniz).
* Projenize eklenmiş `Aspose.OCR` ve `Aspose.OCR.Gpu` NuGet paketleri.
* Diskte hazır bir örnek fiş görüntüsü (`receipt.png`).

Eğer bunlardan biri size yabancı geliyorsa, bir an durun ve paketleri kurun:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Hepsi bu—GPU desteği NuGet paketine yerleşik olduğu için ekstra yerel kütüphanelere gerek yok.

---

## Görüntü Dosyasını Yükle ve GPU Motorunu Hazırla

İlk yapmanız gereken **görüntü dosyasını** bir `ImageStream`e **yüklemek**. Bu nesne dosya sistemi detaylarını soyutlayarak OCR motoruna temiz bir bellek içi temsil sunar.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Step 1️⃣: Initialize the GPU‑accelerated engine.
var gpuEngine = new GpuEngine
{
    // Step 2️⃣: Set a safety net for GPU RAM usage.
    // Here we limit the engine to 1024 MB (1 GB). Adjust as needed.
    MaxDeviceMemory = 1024 // MB
};

// Step 3️⃣: Load the receipt image from disk.
var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

// At this point the image is ready for OCR.
```

**Neden önemli:**  
`ImageStream.FromFile` ile *görüntü dosyasını* yüklemek, motorun tam piksel verisini görmesini, DPI ve renk derinliğini korumasını sağlar. Bu adımı atlamak ya da bozuk bir akış vermek, OCR’nin karakterleri kaçırmasına veya istisna fırlatmasına yol açar.

> **İpucu:** Kullanıcı‑yüklediği dosyalarla çalışıyorsanız, `FromFile` çağrısını bir try‑catch bloğuna sarın ve önce dosya boyutunu doğrulayın. Büyük görüntüler, **GPU belleği yapılandırması** doğru yapılmazsa GPU belleğini zorlayabilir.

---

## Optimum Performans İçin Maksimum GPU Belleğini Ayarla

GPU kaynakları özellikle paylaşımlı sunucularda ya da sınırlı VRAM’e sahip dizüstü bilgisayarlarda kıymetlidir. `MaxDeviceMemory` özelliği, Aspose’a GPU’nun ne kadar belleğini güvenli bir şekilde tahsis edebileceğini söyler.

```csharp
// Example: Restrict to 512 MB for low‑end GPUs.
gpuEngine.MaxDeviceMemory = 512; // MB
```

**Maksimum GPU belleğini** ayarladığınızda, motor isteği karşılayamazsa otomatik olarak CPU işleme geri döner—çöküşleri önler. Bu, cihaz‑spesifik limitleri sabit kodlamadan **GPU belleğini yapılandırmanın** en güvenli yoludur.

**Ne zaman ayarlamalısınız:**  
* Yoğun toplu işleme sırasında `OutOfMemoryException` görürseniz, limiti düşürün.  
* Fișleriniz yüksek çözünürlükte (300 DPI+) ise, hızı yüksek tutmak için 2 GB’a yükseltin.

---

## Görüntü Üzerinde OCR Çalıştırarak Fiș Metnini Çıkar

Şimdi eğlenceli kısım—gerçekten **görüntü üzerinde OCR çalıştırma** ve fișin metnini çıkarma. `Recognize` metodu, düz metin çıktısını içeren bir `Text` özelliği taşıyan bir `OcrResult` nesnesi döndürür.

```csharp
// Step 4️⃣: Perform OCR.
OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

// Step 5️⃣: Output the extracted text.
Console.WriteLine("=== Receipt Text ===");
Console.WriteLine(ocrResult.Text);
```

Konsol aşağıdakine benzer bir şey gösterecek:

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

**Neden işe yarıyor:**  
GPU motoru, çeşitli belge düzenleri üzerinde eğitilmiş bir derin‑öğrenme modeli çalıştırır. Temiz ve doğru yüklenmiş bir görüntü besleyerek, modelin **fișten metin çıkarma** konusunda en iyi şansa sahip olmasını sağlarsınız.

---

## Çıktıyı Doğrula ve Yaygın Tuzaklar

Güçlü bir motor olsa da OCR sihirli değildir. Dikkat etmeniz gereken birkaç nokta:

| Sorun | Sebep | Çözüm |
|-------|-------|-----|
| Bozuk karakterler | Düşük kontrast veya bulanık görüntü | Aspose’un `ImageProcessor`ı ile kontrastı artırarak ön‑işleme yapın |
| Kaçan satırlar | Görüntü çok sıkı kırpılmış | Fișin tam olarak görüntü sınırları içinde olduğundan emin olun |
| Bellek yetersizliği hataları | `MaxDeviceMemory` görüntü boyutu için çok düşük | `MaxDeviceMemory`ı artırın ya da önce görüntüyü küçültün |
| Yanlış dil | Fiș İngilizce dışı bir dilde | `gpuEngine.Language = OcrLanguage.Spanish;` (veya uygun dil) şeklinde ayarlayın |

Bunlarla karşılaşırsanız, hızlı çözüm en uzun kenarı 2000 px’nin altında olacak şekilde görüntüyü yeniden boyutlandırmaktır—bu, çoğu fiş için okunabilirliği kaybetmeden GPU baskısını büyük ölçüde azaltır.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, derlenmeye hazır tüm program yer alıyor. Dosya yolunu kendi fiş konumunuzla değiştirin.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class ReceiptOcrDemo
{
    static void Main()
    {
        // 1️⃣ Create GPU‑accelerated engine with a safe memory cap.
        var gpuEngine = new GpuEngine
        {
            MaxDeviceMemory = 1024 // MB – adjust for your hardware
        };

        // 2️⃣ Load the receipt image from disk.
        //    Make sure the path points to a valid PNG/JPEG file.
        var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

        // 3️⃣ Run OCR – this will automatically use the GPU if available.
        OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

        // 4️⃣ Print the extracted text.
        Console.WriteLine("=== Receipt Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Beklenen konsol çıktısı** (fişiniz elbette farklı olacaktır):

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

Programı `dotnet run` ile çalıştırın. Metin ekrana basıldıysa, **görüntü dosyasını yükleme**, **maksimum GPU belleğini ayarlama** ve **görüntü üzerinde OCR çalıştırma** adımlarını başarıyla tamamlamış oldunuz ve **fişten metin çıkarma** işlemini gerçekleştirdiniz.

---

## Sık Sorulan Sorular

**S: Ayrı bir GPU’su olmayan makinelerde çalışır mı?**  
C: Evet. Aspose.OCR, uyumlu bir GPU tespit edemezse sorunsuz bir şekilde CPU moduna geçer. **Görüntü dosyasını yükleme** ve **görüntü üzerinde OCR çalıştırma** hâlâ mümkün, sadece biraz daha yavaş olur.

**S: Birden fazla fişi toplu olarak işleyebilir miyim?**  
C: Kesinlikle. Tanıma kodunu bir `foreach` döngüsüne sarın, ancak aynı `GpuEngine` örneğini yeniden kullanın—bu, her dosya için GPU kaynaklarını yeniden başlatmayı önler.

**S: Fișim İngilizce dışı bir dilde ise ne yapmalıyım?**  
C: `Recognize` çağrısından önce dili ayarlayın:

```csharp
gpuEngine.Language = OcrLanguage.French;
```

Motor o zaman uygun karakter setini uygular.

---

## Sonraki Adımlar & İlgili Konular

Temelleri kavradığınıza göre şu konuları keşfetmeyi düşünün:

* **OCR doğruluğunu ince ayar yapma** – `gpuEngine.RecognitionOptions` içinde `EnableDeskew` veya `ContrastEnhancement` gibi seçenekleri deneyin.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}