---
category: general
date: 2026-05-25
description: Minimal bir ASP.NET Core API ile görüntüden metin çıkarma yöntemini öğrenin.
  Görüntüyü POST ile yükleyin, çok parçalı form verilerini okuyun ve görüntü üzerinde
  OCR gerçekleştirin.
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: tr
og_description: Minimal bir ASP.NET Core API kullanarak görüntüden metin çıkarın.
  Bu kılavuz, görüntüyü POST ile nasıl yükleyeceğinizi, multipart form verilerini
  nasıl okuyacağınızı ve görüntü üzerinde OCR nasıl yapılacağını gösterir.
og_title: ASP.NET Core'da Görüntüden Metin Çıkarma – Adım Adım
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  headline: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  type: TechArticle
- description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  name: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  steps:
  - name: Breaking Down the Logic
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **ReadFormAsync** | Parses the incoming *multipart/form-data* request. | Without
      this, you can’t access the uploaded files. | | **form.Files["image"]** | Retrieves
      the file whose form‑field name is `image`. | Guarant'
  - name: 1. Large Files
    text: 'The default request body limit is 30 MB. For larger scans you might need
      to adjust:'
  - name: 2. Asynchronous OCR
    text: Some OCR libraries expose async methods (`RecognizeAsync`). If yours does,
      replace `ocr.Recognize(img)` with `await ocr.RecognizeAsync(img)` and mark the
      lambda as `async`.
  - name: 3. Security Considerations
    text: '- **Validate file size** before loading it into memory. - **Sanitize the
      filename** if you ever write it to disk. - **Rate‑limit** the endpoint to avoid
      denial‑of‑service attacks.'
  - name: 4. GPU Acceleration
    text: If you uncomment the `engine.GpuDevice = new GpuDevice(0);` line and your
      hardware supports CUDA or DirectML, you’ll see a noticeable speed boost, especially
      on high‑resolution images.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Minimal API
title: ASP.NET Core Minimal API'de Görüntüden Metin Çıkarma – Tam Kılavuz
url: /tr/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ASP.NET Core Minimal API ile Görüntüden Metin Çıkarma – Tam Kılavuz

Hiç **görüntüden metin çıkarma** işlemini ağır çerçevelerle uğraşmadan yapmayı düşündünüz mü? Yalnız değilsiniz. Birçok geliştirici, kullanıcıların bir fotoğraf bırakıp ham karakterleri alabilmesi için hızlı bir yol arıyor; ister fiş tarama, el yazısı notları dijitalleştirme, isterse bir arama indeksini besleme olsun.

Bu eğitimde, **POST ile görüntü yükleme** yapan, *multipart/form‑data* yükünü ayrıştıran ve ardından tek bir `OcrEngine` örneği kullanarak **görüntüde OCR gerçekleştirme** yapan minik bir ASP.NET Core Minimal API oluşturacağız. Sonunda, herhangi bir .NET 8 projesine ekleyebileceğiniz ve hemen görüntüden metin çıkarabileceğiniz tamamen çalışır bir uygulamanız olacak.

## Ne Yapacaksınız

- `/ocr` yolunda dinleyen minimal bir web uygulaması.
- `multipart/form-data` POST isteğiyle gönderilen bir görüntü dosyasını kabul eden bir uç nokta.
- Yüklenen dosyayı okuyan, OCR motoruna besleyen ve düz metin sonuçlarını döndüren mantık.
- Uyumlu bir kartı olanlar için (yorum satırı olarak) GPU hızlandırma örneği.

**Önkoşullar**  
- .NET 8 SDK (veya daha yeni).  
- C# ve komut satırı konusunda temel bilgi.  
- `OcrEngine` sınıfını sunan bir OCR kütüphanesi (örnek, varsayımsal bir NuGet paketi varsayar).  

Bu koşullara sahipseniz, başlayalım.

## Adım 1: Projeyi Kurun ve OCR Paketini Ekleyin

İlk olarak yeni bir web projesi oluşturun ve OCR kütüphanesini ekleyin.

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **Pro ipucu:** Bağımlılıklarınızı güncel tutun. Yeni sürümler genellikle performans artışı getirir, özellikle GPU‑hızlandırmalı çıkarım için.

## Adım 2: Tek Bir OCR Motoru (Singleton) Kaydedin

Uygulama boyunca tek bir `OcrEngine` örneği istiyoruz—her istek için yeni bir motor başlatmaya gerek yok. Bunu builder’ın servis konteynerine kaydedin.

```csharp
using Awesome.Ocr;               // <-- the OCR library namespace
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using System.Drawing;            // System.Drawing.Common for Image handling

var builder = WebApplication.CreateBuilder(args);

// Register a singleton OCR engine (English language)
// Uncomment the GPU line if you have a compatible GPU and the library supports it.
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU acceleration
    return engine;
});
```

**Neden singleton?**  
Bir OCR motoru oluşturmak maliyetli olabilir—nöral ağ ağırlıklarını belleğe yüklemek gibi. Aynı örneği yeniden kullanarak CPU döngülerinden ve RAM’den tasarruf eder, bu da her `/ocr` çağrısında daha hızlı yanıt süreleri sağlar.

## Adım 3: Uygulamayı Oluşturun

Şimdi `WebApplication` nesnesini somutlaştırıyoruz.

```csharp
var app = builder.Build();
```

Bu satır neredeyse sihirli görünebilir, ancak altında yönlendirme, ara katman (middleware) ve az önce yapılandırdığımız DI konteyneri bağlanır.

## Adım 4: POST Uç Noktasını Tanımlayın – “POST ile Görüntü Yükleme”

İşte eğitimin kalbi: **POST ile görüntü yükleme**, multipart yükünü okuyan ve veriyi OCR motoruna veren bir uç nokta.

```csharp
app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    // Step 5: Read multipart form data and extract the uploaded image
    var form = await request.ReadFormAsync();               // <-- read multipart/form-data
    var file = form.Files["image"];                         // expects a field named "image"

    if (file is null || file.Length == 0)
    {
        return Results.BadRequest("No image file provided.");
    }

    // Guard against unsupported content types
    if (!file.ContentType.StartsWith("image/"))
    {
        return Results.BadRequest("Uploaded file is not an image.");
    }

    // Load the image into a System.Drawing.Image
    using var img = Image.FromStream(file.OpenReadStream());

    // Step 6: Perform OCR on the image
    string text = ocr.Recognize(img);                       // <-- perform OCR on image

    // Step 7: Return the extracted text as plain‑text
    return Results.Text(text);
});
```

### Mantığın Açıklaması

| Adım | Ne Olur | Neden Önemli |
|------|----------|--------------|
| **ReadFormAsync** | Gelen *multipart/form-data* isteğini ayrıştırır. | Dosyalara erişim olmadan yüklenen görüntülere ulaşamazsınız. |
| **form.Files["image"]** | Form alanı adı `image` olan dosyayı alır. | Çağırıcılar için öngörülebilir bir sözleşme sağlar. |
| **Content‑type kontrolü** | Dosyanın bir görüntü olduğunu doğrular (örn. `image/png`). | OCR motorunun görüntü dışı verilerle takılmasını önler. |
| **Image.FromStream** | Ham akışı `System.Drawing.Image` nesnesine dönüştürür. | OCR kütüphanesi bir `Image` nesnesi bekler, ham bayt dizisi değil. |
| **ocr.Recognize(img)** | OCR motorunu **görüntüden metin tanıma** için çalıştırır. | Bu, **görüntüde OCR gerçekleştirme** adımının çekirdeğidir. |
| **Results.Text** | Düz metin yanıtını gönderir. | Sonraki hizmetler için basit, tüketilebilir bir format. |

## Adım 5: API’yi Çalıştırın

Son olarak web sunucusunu başlatın.

```csharp
app.Run();
```

`dotnet run` komutunu çalıştırdığınızda API, `http://localhost:5000` (veya seçtiğiniz bir port) üzerinden dinleyecek. `curl` ile test edebilirsiniz:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**Beklenen çıktı:** Konsol, tanınan karakterleri yazdırır, örneğin:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

Görüntü bulanıksa veya dil desteklenmiyorsa, OCR motoru boş bir dize ya da hata mesajı dönecektir—bu durumları üretim kodunda ele alın.

## Köşe Durumları ve En İyi Uygulamalar

### 1. Büyük Dosyalar

Varsayılan istek gövdesi sınırı 30 MB’tir. Daha büyük taramalar için ayarlamanız gerekebilir:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. Asenkron OCR

Bazı OCR kütüphaneleri async metodlar (`RecognizeAsync`) sunar. Eğer sizinkinde varsa, `ocr.Recognize(img)` yerine `await ocr.RecognizeAsync(img)` kullanın ve lambda’yı `async` olarak işaretleyin.

### 3. Güvenlik Hususları

- **Dosya boyutunu** belleğe yüklemeden önce doğrulayın.  
- **Dosya adını** diske yazacaksanız temizleyin.  
- **Rate‑limit** uygulayarak hizmet reddi saldırılarını önleyin.

### 4. GPU Hızlandırma

`engine.GpuDevice = new GpuDevice(0);` satırının yorumunu kaldırıp donanımınız CUDA ya da DirectML destekliyorsa, özellikle yüksek çözünürlüklü görüntülerde belirgin bir hız artışı göreceksiniz.

## Tam Çalışan Örnek

Aşağıda, yeni bir Minimal API projesine kopyalayıp yapıştırabileceğiniz tam `Program.cs` dosyası yer alıyor.

```csharp
using Awesome.Ocr;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Http.Features;
using System.Drawing;

var builder = WebApplication.CreateBuilder(args);

// Optional: increase multipart limit for big images
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});

// Register the OCR engine as a singleton
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU if available
    return engine;
});

var app = builder.Build();

app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    var form = await request.ReadFormAsync();
    var file = form.Files["image"];

    if (file is null || file.Length == 0)
        return Results.BadRequest("No image file provided.");

    if (!file.ContentType.StartsWith("image/"))
        return Results.BadRequest("Uploaded file is not an image.");

    using var img = Image.FromStream(file.OpenReadStream());

    // Core OCR operation
    string text = ocr.Recognize(img);

    return Results.Text(text);
});

app.Run();
```

Kaydedin, `dotnet run` komutunu çalıştırın ve **görüntüden metin çıkarma** işlevine anında sahip olun.

## Sonuç

ASP.NET Core Minimal API kullanarak **görüntüden metin çıkarma** için **tam, uçtan uca bir çözüm** üzerinden geçtik. Proje iskeletini oluşturduktan, **singleton OCR motoru kaydettikten**, **POST ile görüntü yükleme** uç noktasını kurarak **multipart form verisini okuduk** ve sonunda **görüntüde OCR gerçekleştirme** yaparak temiz düz metin döndürdük.

Bundan sonra şunları yapabilirsiniz:

- Daha zengin yanıtlar için JSON sarmalayıcılar ekleyin.  
- Çıkarılan metni saklamak için bir veritabanı bağlayın.  
- Birden fazla dili desteklemek için (`OcrLanguage.Spanish` vb.) genişletin.  

Bu desen, aynı uç noktayı daha büyük bir mikroservise ekleyerek ya da bir API geçidi arkasına koyarak sorunsuzca ölçeklenebilir.

PDF işleme, toplu işlem veya GPU ayarları hakkında sorularınız mı var? Yorum bırakın, iyi kodlamalar!

## İlgili Eğitimler

- [Aspose.OCR .NET ile Görüntüden Metin Çıkarma](/ocr/english/net/image-and-drawing-recognition/)
- [Aspose.OCR .NET için OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)
- [Aspose.OCR ile Dil Seçimi Kullanarak C#’ta Görüntü Metni Çıkarma](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}