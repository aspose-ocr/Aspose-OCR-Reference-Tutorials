---
category: general
date: 2026-04-04
description: OCR'yi hızlı ve güvenli bir şekilde nasıl kullanılır. Görüntüden metin
  çıkarmayı, DJVU'yu metne dönüştürmeyi ve Aspose.OCR ile OCR için görüntü yüklemeyi
  öğrenin.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert djvu to text
- load image for OCR
- extract text from djvu
language: tr
og_description: C#'ta OCR kullanarak görüntü dosyalarından ve DJVU belgelerinden metin
  çıkarmak. Tam kodlu adım adım öğretici.
og_title: C#'da OCR Nasıl Kullanılır – Tam Kılavuz
tags:
- OCR
- C#
- Aspose
title: C#'ta OCR Nasıl Kullanılır – Görüntülerden ve DJVU Dosyalarından Metin Çıkarma
url: /tr/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-and-djvu-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta OCR Nasıl Kullanılır – Görüntülerden ve DJVU Dosyalarından Metin Çıkarma

Hiç **OCR nasıl kullanılır** sorusunu, taranmış bir sayfadan kelimeleri manuel olarak yazmadan çıkarmak için merak ettiniz mi? Tek başınıza değilsiniz. Birçok projede—eski kitapları dijitalleştiriyor ya da makbuzlardan veri çekiyor olun—görüntüden metin elde etmek günlük bir sıkıntıdır. İyi haber? Aspose.OCR ile bunu sadece birkaç satırda yapabilirsiniz, hatta kaynak bir DJVU dosyası olsa bile.

Bu rehberde **görüntüden metin çıkarma**, **OCR için görüntü yükleme** ve hatta C# kullanarak **DJVU'yu metne dönüştürme** konularında ihtiyacınız olan her şeyi adım adım ele alacağız. Sonunda tanınan metni doğrudan konsola yazdıran, çalıştırmaya hazır bir konsol uygulamanız olacak. Gizem yok, ekstra bağımlılık yok, sadece saf C# ve Aspose.

## Öğrenecekleriniz

- Aspose.OCR kütüphanesini nasıl kurup referans göstereceğinizi.
- **OCR için görüntü yükleme** için gereken tam kodu, ister PNG, JPEG ister DJVU sayfası olsun.
- Motoru nasıl çağırıp sonucu alacağınızı.
- Büyük belgelerle çalışırken ipuçları ve yaygın tuzaklar.
- Visual Studio'ya kopyalayıp yapıştırabileceğiniz tam, çalıştırılabilir bir örnek.

> **Önkoşul:** .NET 6.0 veya daha yeni bir sürüm ve geçerli bir Aspose.OCR lisansı (veya ücretsiz deneme). Kütüphane henüz yoksa, `dotnet add package Aspose.OCR` komutuyla NuGet'ten edinebilirsiniz.

---

## C#'ta Aspose ile OCR Nasıl Kullanılır

Bu, **OCR nasıl kullanılır** sorusuna C# projesinde yanıt verdiğimiz temel adımdır. Aşağıdaki kod tam bir programdır; yeni bir konsol uygulamasına yapıştırıp F5 tuşuna basabilirsiniz.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create the OCR engine instance.
            var ocrEngine = new OcrEngine();

            // Step 2: Load the image (or DJVU page) you want to analyze.
            // Replace the path with your own file location.
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book-page.djvu");

            // Step 3: Run the recognition process.
            OcrResult ocrResult = ocrEngine.Recognize();

            // Step 4: Output the extracted text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Neden bu çalışır:**  
- `OcrEngine` giriş noktasıdır; görüntü ön işleme, dil algılama ve karakter sınıflandırmasının ağır işini soyutlar.  
- `ImageStream.FromFile` birçok formatı, DJVU dahil, işleyebilir; bu sayede ekstra bir dönüşüm adımına gerek kalmadan **DJVU'yu metne dönüştürebilirsiniz**.  
- `Recognize()` bir `OcrResult` nesnesi döndürür; bu nesne düz metin çıktısını, güven skorlarını ve gerekirse daha sonra kullanabileceğiniz sınırlama kutularını içerir.

Programı çalıştırdığınızda aşağıdakine benzer bir çıktı alırsınız:

```
=== OCR Result ===
In the beginning God created the heavens and the earth.
```

Bu kadar—ilk başarılı **DJVU'dan metin çıkarma** işleminiz.

![OCR nasıl kullanılır örneği](/images/ocr-demo.png "C# konsol uygulamasında OCR nasıl kullanılacağını gösteren ekran görüntüsü")

*Alt metin: “OCR nasıl kullanılır” konsol çıktısı ekran görüntüsü.*

---

## OCR için Görüntü Yükleme

Motor bir şey okuyabilmeden önce **OCR için görüntüyü doğru şekilde yüklemelisiniz**. Aspose, çoğu raster formatını kutudan çıkar çıkmaz destekler, ancak tanıma sürecini sorunsuzlaştıracak birkaç ipucu vardır:

- **Büyük görüntüleri yeniden boyutlandırın**; en uzun kenarı en fazla 2000 px olmalı. Aşırı büyük dosyalar bellek kullanımını artırır ve motoru yavaşlatabilir.  
- **Renkli görüntüleri gri tonlamaya çevirin** eğer gürültülü arka planlar fark ederseniz. `ocrEngine.Image = ImageStream.FromFile(path).ConvertToGrayscale();` kodunu kullanın.  
- **DPI'yi manuel olarak ayarlayın** düşük çözünürlüklü taramalar için (`ocrEngine.Image.DpiX = 300; ocrEngine.Image.DpiY = 300;`).

Bu ayarlamalar isteğe bağlıdır ancak taranmış makbuzlar gibi **görüntüden metin çıkarma** işlemlerinde doğruluğu genellikle artırır.

---

## Görüntüden Metin Çıkarma – En İyi Uygulamalar

Tipik görüntü formatları (PNG, JPEG, BMP) ile çalışırken adımlar aynı kalır, ancak motoru ince ayar yapabilirsiniz:

```csharp
ocrEngine.Image = ImageStream.FromFile("sample.png");

// Optional: enable language packs for better accuracy.
ocrEngine.Language = Language.English;

// Optional: set recognition mode to auto.
ocrEngine.RecognitionMode = RecognitionMode.Auto;
```

- **Dil seçimi** önemlidir. Çok dilli belgeler işliyorsanız `ocrEngine.Language = Language.Multilingual;` ayarlayın.  
- **RecognitionMode** `Auto`, `Fast` veya `Accurate` olabilir. `Accurate` daha yüksek kalite sunar ancak hızı düşürür—arşivleme görevleri için tercih edin.

---

## DJVU'yu Metne Dönüştürme – Çok Sayfalı Dosyaları İşleme

DJVU dosyaları genellikle birden fazla sayfa içerir. Aspose her sayfayı ayrı bir görüntü akışı olarak ele alır, bu yüzden döngüyle işleyebilirsiniz:

```csharp
using Aspose.OCR;
using System.Collections.Generic;

var ocrEngine = new OcrEngine();
List<string> allPagesText = new List<string>();

int pageCount = ImageStream.GetPageCount("book.djvu");
for (int i = 1; i <= pageCount; i++)
{
    ocrEngine.Image = ImageStream.FromFile("book.djvu", i); // Load page i
    OcrResult result = ocrEngine.Recognize();
    allPagesText.Add(result.Text);
}

// Combine all pages into a single string.
string fullText = string.Join("\n--- Page Break ---\n", allPagesText);
Console.WriteLine(fullText);
```

**Neden döngü?**  
DJVU dosyaları temelde bir görüntü yığınıdır. Her sayfayı teker teker işleyerek **DJVU'dan metin çıkarma** işlemini sırasıyla yaparsınız ve orijinal belge akışını korumuş olursunuz.

---

## Yaygın Tuzaklar ve Profesyonel İpuçları

| Sorun | Neden Oluşur | Çözüm |
|------|----------------|-----|
| **Garbage characters** | Düşük DPI veya yüksek sıkıştırma | Görüntüyü büyüt, `ocrEngine.Image.DpiX/Y = 300` ayarla |
| **Slow processing** | Büyük dosyalarda `Accurate` modunu kullanmak | Toplu işler için `Fast` moda geç |
| **Missing language support** | Varsayılan dil sadece İngilizce | Ek dil paketleri yükle (`ocrEngine.Language = Language.Spanish;`) |
| **Out‑of‑memory errors** | Birçok yüksek çözünürlüklü sayfayı aynı anda yüklemek | Sayfaları tek tek işleyip kaynakları serbest bırak (`ocrEngine.Dispose();`) |

Hızlı bir **pro ipucu**: bir sayfayı işledikten sonra her zaman `ocrEngine.Dispose()` çağırın. Bu, yerel kaynakları serbest bırakır ve uzun süre çalışan hizmetlerin çökmesine neden olabilecek ince bellek sızıntılarını önler.

---

## OCR İş Akışınızı Test Etme

Her şeyin sorunsuz çalıştığını doğrulamak için şu basit kontrolleri deneyin:

1. Tanınan dize **uzunluğunu yazdırın**: `Console.WriteLine($"Characters recognized: {ocrResult.Text.Length}");`  
2. Eğer bir referans metniniz varsa, basit bir diff kütüphanesi kullanarak **bilinen metinle karşılaştırın**.  
3. **Güven skorlarını kaydedin** (`ocrResult.Confidence`) ve düşük kaliteli sayfaları otomatik olarak tespit edin.

Güven skoru sürekli 0.7’nin altında ise, önceki bölümde bahsedilen görüntü ön işleme adımlarını yeniden gözden geçirin.

---

## Sonraki Adımlar

Artık **OCR nasıl kullanılır** bildiğinize göre iş akışınızı genişletmeyi düşünün:

- **Toplu işleme**: Büyük koleksiyonları hızlandırmak için döngüyü bir `Parallel.ForEach` içinde sarın.  
- **PDF'ye dışa aktar**: Aspose.PDF kullanarak tanınan metni aranabilir PDF'ler için gizli bir katman olarak gömün.  
- **AI ile bütünleştir**: Çıkarılan dizeleri özetleme veya varlık çıkarımı için bir dil modeline besleyin.

Tüm bu adımlar, az önce kurduğunuz temelin üzerine inşa edilir ve her adım, ele aldığımız **görüntüden metin çıkarma** prensiplerinden yararlanır.

---

## Sonuç

**OCR nasıl kullanılır** sorusunu C# ve Aspose ile derinlemesine inceledik; görüntü yüklemeden **görüntüden metin çıkarma**, **DJVU** dosyalarını işleme ve yaygın sorunları giderme konularını kapsadık. Yukarıdaki tam, çalıştırılabilir örnek size sağlam bir başlangıç noktası sunar ve metin içinde dağıtılan ipuçları, çözümü gerçek dünya projelerine uyarlamanıza yardımcı olur.

Deneyin, ayarları kendi belgelerinize göre ince ayarlayın ve taranmış sayfaları kısa sürede aranabilir metne dönüştürün. Sorularınız veya işbirliği etmeyen zor bir dosyanız varsa yorum bırakın—mutlu kodlamalar!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}