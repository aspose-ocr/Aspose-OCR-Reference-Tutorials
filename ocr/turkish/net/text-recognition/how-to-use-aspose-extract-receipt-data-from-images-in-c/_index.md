---
category: general
date: 2026-04-04
description: Aspose'ı kullanarak fiş verilerini çıkarmayı, fiş görüntüsünü yüklemeyi
  ve tam bir C# örneğiyle fiş görüntüsünü OCR ile işlemeyi öğrenin. Geliştiriciler
  için adım adım rehber.
draft: false
keywords:
- how to use aspose
- extract receipt data
- how to extract receipt
- load receipt image
- ocr receipt image
language: tr
og_description: Aspose kullanarak taranmış bir fiş görüntüsünden fiş verilerini nasıl
  çıkarabilirsiniz. Tam C# kodu, açıklamalar ve OCR fiş görüntüsü işleme ipuçları.
og_title: Aspose Nasıl Kullanılır – Görüntülerden Makbuz Verilerini Çıkarma
tags:
- Aspose
- OCR
- C#
- Receipt Processing
title: Aspose Nasıl Kullanılır – Görsellerden Makbuz Verilerini C# ile Çıkarma
url: /tr/net/text-recognition/how-to-use-aspose-extract-receipt-data-from-images-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Nasıl Kullanılır – C#'ta Görsellerden Makbuz Verilerini Çıkarma

Hiç **Aspose nasıl kullanılır** sorusunu bir makbuz fotoğrafından yapılandırılmış bilgi çekmek için düşündünüz mü? Tek başınıza değilsiniz. İster bir gider‑takip uygulaması geliştiriyor olun ister fatura girişini otomatikleştiriyor olun, sorun aynı: elinizde bir PNG ya da JPEG var ve satıcı adı, tarih ve toplam tutarı manuel olarak yazmadan elde etmeniz gerekiyor.

Şöyle ki—Aspose.OCR bu tüm süreci çocuk oyuncağı haline getiriyor. Bu öğreticide bir makbuz görselini yüklemeyi, OCR çalıştırmayı ve sonunda birkaç C# satırıyla makbuz verilerini çıkarmayı adım adım göstereceğiz. Sonunda satıcı, tarih ve toplam tutarı doğrudan konsola yazdıran çalıştırılabilir bir konsol programına sahip olacaksınız.

> **Hızlı kazanç:** Sadece koda ihtiyacınız varsa, alttaki “Tam Çalışan Örnek” bölümüne atlayın ve kopyalayıp yapıştırın.

## Gereksinimler

- **.NET 6.0 veya üzeri** (API .NET Core ve .NET Framework ile çalışır)
- **Aspose.OCR for .NET** NuGet paketi (`Install-Package Aspose.OCR`)
- Yerel olarak kaydedilmiş bir örnek makbuz görseli (PNG, JPG veya BMP)
- Visual Studio 2022 veya C# projelerini destekleyen herhangi bir editör

Başka üçüncü‑taraf kütüphane gerekmez. Tek ön koşul, C# konsol uygulamaları hakkında temel bir anlayışa sahip olmaktır—eğer “Hello World” yazdıysanız, hazırsınız.

## Adım 1 – Aspose.OCR'yi Yükleyin ve Referans Verin

Aspose'ı **nasıl kullanacağınızı** öğrenmek için önce projeye kütüphaneyi eklemeniz gerekir. Package Manager Console'ı açın ve şu komutu çalıştırın:

```powershell
Install-Package Aspose.OCR
```

Alternatif olarak, NuGet UI'ı kullanıp “Aspose.OCR”ı arayın. Kurulduktan sonra, dosyanızın en üstüne gerekli ad alanlarını ekleyin:

```csharp
using Aspose.OCR;
using Aspose.OCR.Structured;
```

> **Pro ipucu:** NuGet paketlerinizi güncel tutun. Bugün (Nisan 2026) itibarıyla en son stabil sürüm 23.11.0'dır ve yüksek çözünürlüklü makbuzlarda OCR performans iyileştirmeleri içerir.

## Adım 2 – Makbuz Görselini Yükleyin

Makbuz görsellerini **yüklerken**, iki yaygın kaynağınız vardır: yerel bir yol ya da bir web isteğinden gelen akış. Bu öğreticide basit tutup diskteki dosyayı okuyacağız:

```csharp
// Step 2: Load the receipt image to be processed
var ocrEngine = new OcrEngine
{
    Language = Language.English // set language for better accuracy
};

ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.png");
```

`YOUR_DIRECTORY/receipt.png` ifadesini makbuz dosyanızın gerçek yolu ile değiştirin. Kullanıcı yüklemeleriyle çalışıyorsanız, bir `MemoryStream`'i `ImageStream.FromStream`'e besleyebilirsiniz.

> **Neden önemli:** Dil (İngilizce) belirtmek, OCR motoruna hangi karakter setini bekleyeceğini söyler ve yanlış tanıma oranını düşürür—özellikle sayılar ve semboller içeren bir **ocr receipt image** (makbuz görseli OCR) yaparken çok önemlidir.

## Adım 3 – OCR'ı Çalıştırın ve Düzen Bilgilerini Yakalayın

OCR adımı sadece ham metni çıkarmakla kalmaz; aynı zamanda düzeni de yakalar, bu da daha sonraki yapılandırılmış çıkarım için kritik öneme sahiptir.

```csharp
// Step 3: Run OCR to generate text and layout information (required for structured extraction)
ocrEngine.Recognize();
```

`Recognize()` tamamlandıktan sonra, `ocrEngine` hem düz metni hem de her kelimenin konumsal verilerini tutar. Bu, bir sonraki adımda Aspose'tan “**how to extract receipt**” alanlarını otomatik olarak istemek için temel oluşturur.

## Adım 4 – Layout Recognizer'ı Başlatın

Aspose, makbuzların tipik olarak nasıl düzenlendiğini bilen bir `LayoutRecognizer` sınıfı sunar (satıcı üstte, tarih satırı, toplam alt kısma yakın). Sadece yapılandırılmış OCR motorunu bu sınıfa geçirmeniz yeterlidir:

```csharp
// Step 4: Initialize the layout recognizer with the OCR engine
var layoutRecognizer = new LayoutRecognizer(ocrEngine);
```

Arka planda, tanıyıcı para birimi sembolleri veya tarih desenleri gibi bir dizi sezgisel kural uygular ve ham metni anlamsal alanlara eşler.

## Adım 5 – Yapılandırılmış Makbuz Verilerini Çıkarın

Şimdi tatlı kısım geliyor: **extract receipt data**. Tek bir metod çağrısı tüm işi yapar:

```csharp
// Step 5: Extract structured receipt data (merchant, date, total amount)
var receiptData = layoutRecognizer.ExtractReceiptData();
```

`receiptData`, `Aspose.OCR.Structured` içinde tanımlı `ReceiptData` tipinde bir nesnedir. Üç ana özelliği vardır:

- `Merchant` – mağazanın adı
- `Date` – satın alma tarihi (`DateTime` olarak, tespit edilirse)
- `TotalAmount` – toplam tutar (`decimal` tipinde)

Motor belirli bir alanı bulamazsa, özellik `null` ya da `0` olur. Gerekirse geri dönüş mantığı ekleyebilirsiniz (ör. kullanıcıdan onay istemek).

## Adım 6 – Çıkarılan Bilgileri Görüntüleyin

Son olarak, sonuçları konsola yazdırın. İşinizin meyvelerini burada göreceksiniz:

```csharp
// Step 6: Display the extracted information
Console.WriteLine($"Merchant: {receiptData.Merchant}");
Console.WriteLine($"Date:     {receiptData.Date:d}");
Console.WriteLine($"Total:    {receiptData.TotalAmount:C}");
```

Biçim dizeleri (`:d` ve `:C`) sırasıyla kısa tarih ve para birimi dizesi üretir, böylece çıktı insan tarafından okunabilir olur.

### Beklenen Çıktı

Makbuzun “Coffee Corner” adlı mağazaya ait olduğunu, tarihinin 2025‑12‑01 ve toplam tutarın $4.75 olduğunu varsayarsak, konsol şu şekilde gösterir:

```
Merchant: Coffee Corner
Date:     12/1/2025
Total:    $4.75
```

Herhangi bir alan eksikse, boş bir satır ya da varsayılan bir değer görürsünüz—hata ayıklama için mükemmel.

## Kenar Durumları ve Yaygın Tuzaklar

### 1. Düşük Çözünürlüklü Görseller
Makbuz görseli bulanıktıysa ya da 150 dpi'nin altındaysa, OCR doğruluğu büyük ölçüde düşer. Görseli Aspose'a beslemeden önce basit bir bilineer filtre ile büyütmek sonuçları iyileştirebilir.

```csharp
ocrEngine.Image = ImageStream.FromFile("receipt.png")
    .Resize(2.0, InterpolationMode.Bilinear);
```

### 2. İngilizce Olmayan Makbuzlar
Ana örnek `Language.English` kullanır. Çok dilli makbuzlar için `Language`'ı uygun enum ile ayarlayın (ör. `Language.French`) ya da emin değilseniz `Language.AutoDetect` kullanın.

### 3. Tek Görselde Birden Fazla Makbuz
Aspose'ın layout tanıyıcısı her görselde tek bir makbuz bekler. Yan yana birden fazla makbuz fotoğrafınız varsa, OCR çalıştırmadan önce görüntüyü ön işleme almanız gerekir—her makbuzu ayrı bir dosyaya kırpın.

### 4. Para Birimi Sembolünün Eksik Olması
Bazen toplam tutar `$` işareti olmadan gösterilir. Tanıyıcı yine de sayıları yakalar, ancak doğru ondalık konumunu sağlamak için dizeyi sonradan işlemek gerekebilir.

```csharp
if (receiptData.TotalAmount == 0 && rawText.Contains("Total"))
{
    // fallback parsing logic here
}
```

## Üretim İçin Pro İpuçları

- **OCR motorunu önbelleğe alın**; bir toplu işlemde birden çok makbuz işliyorsanız aynı örneği yeniden kullanmak tahsis yükünü azaltır.
- **Ham OCR metnini kaydedin** (`ocrEngine.Text`) denetim izleri için. Bir alan çıkarılamadığında faydalıdır.
- **Tüm akışı try/catch içinde sarın** ve kullanıcı dostu bir hata mesajı gösterin (ör. “Makbuz okunamadı, lütfen daha net bir görsel yükleyin”).

## Tam Çalışan Örnek

Aşağıda, olduğu gibi derleyip çalıştırabileceğiniz bağımsız bir konsol uygulaması bulunmaktadır. Sadece görsel yolunu değiştirin ve hazırsınız.

```csharp
// ------------------------------------------------------------
// How to Use Aspose – Extract Receipt Data from Images (C#)
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Structured;

namespace ReceiptExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create and configure the OCR engine for English language
            var ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the receipt image you want to process
            // 👉 Make sure the file exists; otherwise an exception will be thrown.
            const string imagePath = "YOUR_DIRECTORY/receipt.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Run OCR – this also captures layout information
            ocrEngine.Recognize();

            // 4️⃣ Initialize the layout recognizer with the OCR engine
            var layoutRecognizer = new LayoutRecognizer(ocrEngine);

            // 5️⃣ Extract structured receipt data (merchant, date, total amount)
            var receiptData = layoutRecognizer.ExtractReceiptData();

            // 6️⃣ Display the extracted information
            Console.WriteLine($"Merchant: {receiptData.Merchant ?? "Not detected"}");
            Console.WriteLine($"Date:     {(receiptData.Date == DateTime.MinValue ? "Not detected" : receiptData.Date.ToShortDateString())}");
            Console.WriteLine($"Total:    {(receiptData.TotalAmount == 0 ? "Not detected" : receiptData.TotalAmount.ToString("C"))}");

            // Keep the console window open when debugging
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Kodu Çalıştırma**

1. Yeni bir .NET konsol projesi oluşturun (`dotnet new console -n ReceiptExtractor`).
2. Aspose.OCR paketini ekleyin (`dotnet add package Aspose.OCR`).
3. Oluşturulan `Program.cs` dosyasını yukarıdaki kod parçacığıyla değiştirin.
4. Belirttiğiniz yola bir makbuz görseli koyun.
5. Derleyin ve çalıştırın (`dotnet run`).

Satıcı, tarih ve toplamın, daha önce gösterildiği gibi tam olarak yazdırıldığını görmelisiniz.

## Sonuç

Bu rehberde **Aspose nasıl kullanılır** konusunu, **makbuz görselini yükleme**, **ocr receipt image** çalıştırma ve sonunda **extract receipt data** yapma adımlarını birkaç satırla ele aldık. Ana çıkarım, Aspose.OCR'nun ağır işi yaptığıdır—OCR motorunu yapılandırdıktan sonra `LayoutRecognizer` ham metni güvenebileceğiniz yapılandırılmış bir nesneye dönüştürür.

Sonraki adımlar? Çıkarılan değerleri bir veritabanına kaydetmeyi, PDF makbuz özeti oluşturmayı ya da harcama sınıflandırması için bir makine‑öğrenme modeline beslemeyi deneyin. Ayrıca faturalar veya gönderi etiketleri gibi diğer yapılandırılmış belge türleriyle de deney yapabilirsiniz—Aspose'ın `ExtractInvoiceData` işlevi çok benzer şekilde çalışır.

Kenar durumlarıyla ilgili sorularınız mı var ya da çok sayfalı PDF'leri nasıl ele alacağınızı görmek mi istiyorsunuz? Yorum bırakın ya da gelişmiş senaryolar için resmi Aspose.OCR dokümantasyonuna göz atın. Kodlamanın tadını çıkarın ve makbuz otomasyonu için **how to use Aspose**'ın sadeliğinden keyif alın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}