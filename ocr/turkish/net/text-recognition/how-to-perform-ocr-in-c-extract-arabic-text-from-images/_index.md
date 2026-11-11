---
category: general
date: 2026-03-17
description: C#'ta OCR yaparak Arapça metin çıkarmayı, görüntüden metin tanımayı ve
  görüntüyü metne dönüştürmeyi tam bir kod örneğiyle öğrenin.
draft: false
keywords:
- how to perform OCR
- extract arabic text
- recognize text from image
- convert image to text
- extract text from image
language: tr
og_description: C#'ta OCR nasıl yapılır? Bu rehber, Arapça metni nasıl çıkaracağınızı,
  görüntüden metni nasıl tanıyacağınızı ve görüntüyü metne nasıl dönüştüreceğinizi
  sadece birkaç adımda gösterir.
og_title: C#'ta OCR Nasıl Yapılır – Arapça Metin Çıkarma
tags:
- OCR
- C#
- Arabic
- ImageProcessing
title: C#'ta OCR Nasıl Yapılır – Görüntülerden Arapça Metin Çıkarma
url: /tr/net/text-recognition/how-to-perform-ocr-in-c-extract-arabic-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile OCR Nasıl Yapılır – Görsellerden Arapça Metin Çıkarma

Bir Arapça fatura ya da taranmış bir belgede **OCR nasıl yapılır** diye hiç merak ettiniz mi? Tek başınıza değilsiniz—birçok geliştirici bitmap’ten Arapça karakterleri çıkarmaya çalışırken takılıp kalıyor. İyi haber şu ki, sadece birkaç C# satırıyla görüntü dosyalarından metin tanıyabilir, görüntüyü metne dönüştürebilir ve nihayetinde **Arapça metin çıkarabilirsiniz**.

Bu öğreticide, OCR nasıl yapılır, her adımın önemi ve sağ‑to‑sol (RTL) betiklerle çalışırken nelere dikkat edilmesi gerektiğini gösteren tam, çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz. Sonunda **görüntüden metin çıkarma** işlemini Arapça, Urdu, Kürtçe ya da OCR motorunun desteklediği herhangi bir dilde yapabilecek durumdasınız.

## Önkoşullar

- .NET 6.0 veya üzeri (kod .NET Core ile de derlenebilir)  
- `OcrEngine` sağlayan OCR kütüphanesine referans (ör. `MyOcrSdk.dll`).  
- `invoice_arabic.png` gibi Arapça metin içeren bir görüntü dosyası.  
- C# konsol uygulamalarıyla temel aşinalık.

> **Pro ipucu:** Eğer bir OCR SDK’nız yoksa, *MyOcrSdk*’nin ücretsiz topluluk sürümü test için yeterli ve kullanacağımız dilleri destekliyor.

---

## 1. Adım – Projeyi Oluşturun ve OCR Namespace’ini İçe Aktarın

**görüntüden metin tanıma** yapabilmek için bir proje iskeleti ve doğru `using` yönergeleri gerekir.

```csharp
using System;
using MyOcrSdk;          // <-- Replace with the actual namespace of your OCR library
using MyOcrSdk.IO;       // For ImageStream helper class

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the OCR workflow will go here
        }
    }
}
```

*Neden önemli:* Doğru namespace’leri içe aktarmak, `OcrEngine`, `Language` ve `ImageStream` gibi sınıflara erişmenizi sağlar. Bu adımı atlamak, yeni başlayanlar için hayal kırıklığı yaratabilecek derleme hatalarına yol açar.

---

## 2. Adım – OCR Motoru Örneği Oluşturun (Anahtar Kelime Dahil)

Şimdi motoru örnekleyerek **OCR gerçekleştiriyoruz**.

```csharp
// Step 2: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

`OcrEngine` nesnesi işlemin kalbidir; yapılandırmayı tutar, ağır işi yapar ve çıkarılan dizeyi içeren sonuç nesnesini döndürür. Bunu, **görüntüyü metne dönüştüren** “beyin” olarak düşünebilirsiniz.

---

## 3. Adım – Tanıma İçin Dili Seçin

Arapça, Urdu, Kürtçe… hepsi aynı yazı sistemi ailesini paylaşır, bu yüzden motorun hangi dili bekleyeceğini belirtmeliyiz. Bu, doğruluğu büyük ölçüde artırır.

```csharp
// Step 3: Choose the language for recognition (Arabic, Urdu, Kurdish, etc.)
ocrEngine.Config.Language = Language.Arabic;   // You can switch to Language.Urdu, etc.
```

*Neden önemli:* OCR motorları dil modellerine dayanır. Doğru modeli seçmek, özellikle sağ‑to‑sol betiklerde benzer görünen karakterlerin hatalı tanınmasını azaltır.

---

## 4. Adım – Metni İçeren Görüntüyü Yükleyin

Motorun analiz edebileceği bir bitmap’e ihtiyacımız var. Yardımcı `ImageStream.FromFile` dosya‑IO detaylarını soyutlar.

```csharp
// Step 4: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_arabic.png");
```

Yolun **geçerli bir görüntü**ye işaret ettiğinden emin olun. Dosya eksik ya da bozuksa, motor bir istisna fırlatır ve **görüntüden metin çıkarma** işlemini başarılı bir şekilde gerçekleştiremezsiniz.

---

## 5. Adım – OCR Sürecini Çalıştırın ve Sonucu Alın

Son olarak `Recognize()` metodunu çağırıp çıkarılan dizeyi gösteriyoruz.

```csharp
// Step 5: Perform the OCR operation
var ocrResult = ocrEngine.Recognize();

// Step 6: Display the extracted text
Console.WriteLine("=== Extracted Arabic Text ===");
Console.WriteLine(ocrResult.Text);
```

`ocrResult.Text` özelliği, motorun okuyabildiği her şeyin düz metin temsilini tutar. Çoğu durumda Arapça karakterler ve sayılar karışımı görürsünüz; bu, veritabanı ekleme ya da çeviri gibi sonraki işlemler için idealdir.

### Beklenen Çıktı

```
=== Extracted Arabic Text ===
فاتورة رقم: 12345
التاريخ: 2026/03/15
المبلغ: 2500.00 ريال
...
```

Eğer bozuk karakterler görürseniz, dil ayarını tekrar kontrol edin ve görüntünün yüksek çözünürlüklü (300 dpi veya üzeri) olduğundan emin olun.

---

## Tam Çalışan Örnek

Aşağıda **tam, bağımsız program** yer alıyor; yeni bir konsol projesine kopyalayıp hemen çalıştırabilirsiniz.

```csharp
// Full OCR demo – extracts Arabic text from an image
using System;
using MyOcrSdk;
using MyOcrSdk.IO;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Set language – Arabic (change to Urdu or Kurdish if needed)
            ocrEngine.Config.Language = Language.Arabic;

            // 3️⃣ Load the source image
            // Replace YOUR_DIRECTORY with the folder that holds your PNG/JPG
            string imagePath = @"YOUR_DIRECTORY/invoice_arabic.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            try
            {
                // 4️⃣ Run OCR
                var result = ocrEngine.Recognize();

                // 5️⃣ Output the text
                Console.WriteLine("=== Extracted Arabic Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – useful when you need to **extract text from image** in batch jobs
                Console.Error.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

> **Not:** OCR SDK’nız lisans gerektiriyorsa, 1. adımdan önce lisansı başlatın (ör. `OcrEngine.SetLicense("YOUR_LICENSE_KEY");`). Bu satır burada kısalık nedeniyle çıkarılmıştır.

---

## Yaygın Kenar Durumlarını Ele Alma

| Durum | Neden Oluşur | Hızlı Çözüm |
|-----------|----------------|-----------|
| **Bulanık veya düşük çözünürlüklü görüntü** | OCR doğruluğu %70’in altına düşer | 300 dpi’de tarayın ya da motorun önüne bicubic algoritmasıyla ölçeklendirin. |
| **Karışık diller (Arapça + İngilizce)** | Motor ilk dil bloğundan sonra durabilir | Çok‑dilli modu etkinleştirin: `ocrEngine.Config.Language = Language.Arabic \| Language.English;` |
| **Sağ‑to‑sol gösterim sorunları** | Konsol karakterleri soldan sağa yazar, Arapça ters görünür | `Console.OutputEncoding = System.Text.Encoding.UTF8;` ve RTL betikleri destekleyen bir terminal kullanın. |
| **Büyük PDF’ler birçok sayfaya bölünmüş** | Bellek tüketimi artar | Sayfa sayfa işleyin: her sayfayı ayrı bir görüntü olarak yükleyin ve OCR akışını tekrarlayın. |
| **Özel semboller (para birimi, tarih)** | Bazı OCR modelleri bunları gürültü olarak algılar | `ocrResult.Text` üzerinde regex kullanarak bilinen desenleri normalleştirin. |

---

## Çözümü Genişletmek – OCR’dan Veri Çıkarımına

Artık **OCR nasıl yapılır** bildiğinize göre, çıkarılan Arapça metinle ne yapabilirsiniz? İşte doğal olarak akla gelen birkaç fikir:

1. **Faturaları ayrıştırın** – Düzenli ifadelerle fatura numaraları, tarih ve tutarları çekin.  
2. **Çeviri API’sine gönderin** – Arapça dizeyi Azure Translator ya da Google Cloud Translate’e gönderin.  
3. **Veritabanına kaydedin** – Temizlenmiş metni bir SQL tablosuna ekleyerek raporlama yapın.  
4. **İş akışlarını tetikleyin** – RabbitMQ gibi bir mesaj kuyruğu ile sonraki işlemleri başlatın.

Tüm bu senaryolar aynı temel işlemi içerir: **görüntüyü metne dönüştür**, ardından sonucu manipüle et.

---

## Sonuç

**C# ile OCR nasıl yapılır** ve **görüntüden Arapça metin çıkarma** konularında ihtiyacınız olan her şeyi ele aldık. Proje kurulumundan `OcrEngine` örneği oluşturma, dili yapılandırma, bitmap yükleme, tanıma çalıştırma ve sonucu yazdırmaya kadar adımları gösterdik. Ayrıca yaygın tuzakları tartıştık ve temel akışı gerçek‑dünya hat hatlarına nasıl genişletebileceğinizi gösterdik.

Deneyin—görüntü yolunu değiştirin, dili Urdu’ya ayarlayın ya da çıktıyı bir veritabanına bağlayın. **görüntüden metin tanıma** ve **görüntüyü metne dönüştürme** işlemini güvenilir bir şekilde yapabildiğinizde, olanaklar sınırsızdır.

---

### Keşfedebileceğiniz İlgili Konular

- **Tesseract OCR** (açık kaynak alternatif) ile **görüntüden metin çıkarma**  
- Binlerce taranmış PDF için **toplu OCR işleme**  
- Görüntü ön‑işleme (eşikleme, gürültü kaldırma) ile **OCR doğruluğunu artırma**  
- .NET UI çerçevelerinde (WPF, WinForms) **sağ‑to‑sol betiklerin işlenmesi**

Herhangi bir sorunla karşılaşırsanız yorum bırakın ya da bu deseni kendi projelerinizde nasıl uyarladığınızı paylaşın. İyi kodlamalar!  

![görüntüden OCR örneği](images/ocr_flow.png "görüntüden OCR örneği")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}