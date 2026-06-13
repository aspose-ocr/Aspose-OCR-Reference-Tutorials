---
category: general
date: 2026-02-13
description: Aspose OCR kullanarak fişi hızlıca nasıl okuyup, regex ile tutarı nasıl
  çıkarabilirsiniz. OCR ile fiş işleme adım adım öğrenin.
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: tr
og_description: C#'ta Aspose OCR ve regex kullanarak fişi nasıl okuyabilirsiniz. Bu
  rehber, fişi OCR ile işleme ve toplam tutarı çıkarmayı gösterir.
og_title: C#'ta Makbuz Nasıl Okunur – Tam OCR ve Regex Öğreticisi
tags:
- OCR
- C#
- Regex
- Aspose
title: C#'ta Makbuz Okuma – OCR + Regex Rehberi
url: /tr/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

final backtop button shortcode.

Let's produce final content.

Be careful to keep all placeholders unchanged.

Let's write translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Makbuz Okuma – OCR + Regex Rehberi

Her zaman **makbuz nasıl okunur** görsellerini elle her satırı yazmadan okuyabilir miyim diye merak ettiniz mi? Birçok küçük işletme uygulamasında bir makbuz fotoğrafından toplam tutarı çekmeniz gerekir ve bunu elle yapmak otomasyonun amacını ortadan kaldırır. İyi haber? Aspose OCR ile motorun işi yapmasını sağlayabilir, ardından basit bir regular expression toplamı bulur. Bu öğreticide **OCR ile makbuz işleme** sürecini adım adım inceleyecek, tutarı regex ile çıkaracağız ve kullanıma hazır bir toplam değer elde edeceğiz.

Tam, çalıştırılabilir bir örnek göreceksiniz, makbuz dil modelinin neden önemli olduğunu keşfedecek ve farklı para birimi sembolleri ya da eksik “Total” etiketleri gibi kenar durumlarını nasıl ele alacağınıza dair ipuçları alacaksınız. Harici dokümanlara gerek yok—gereken her şey burada.

## Öğrenecekleriniz

- Aspose OCR'ı makbuz‑özel tanıma için nasıl kuracağınızı öğrenin (`Receipt` dil modeli görüntüyü otomatik olarak düzeltir ve gürültüyü azaltır).  
- Çoğu ABD‑stili makbuzda çalışan **regex ile tutarı çıkar** desenlerini uygulamayı öğrenin.  
- “TOTAL”, “Total:” veya “Grand Total – $12.34” gibi yaygın varyasyonları nasıl yöneteceğinizi öğrenin.  
- Sonucu güvenli bir şekilde nasıl çıktılayacağınızı ve desen bulunamadığında ne yapmanız gerektiğini öğrenin.  

**Önkoşullar**: .NET 6+ (veya .NET Framework 4.7+), geçerli bir Aspose OCR lisansı veya deneme sürümü ve yerel olarak kaydedilmiş bir makbuz görüntüsü. Hepsi bu kadar—Aspose.OCR dışındaki ekstra NuGet paketlerine gerek yok.

---

## 1. Adım – Aspose OCR'ı Yükleyin ve Projeyi Hazırlayın

### Bunun önemi

Aspose OCR, kırışık kağıdı düzeltmeyi ve arka plan gürültüsünü yok etmeyi bilen özel bir **OCR ile makbuz işleme** modeli sunar. Genel metin modeli, özellikle düşük çözünürlüklü taramalarda daha fazla hata üretir.

### Kod

```csharp
// Install the package via NuGet first:
//   dotnet add package Aspose.OCR
using Aspose.OCR;
using Aspose.OCR.Enums;
using System.Text.RegularExpressions;

// If you have a license file, load it now (optional but removes trial watermark)
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

> **Pro ipucu:** Lisans dosyasını kaynak kontrol klasörünüzün dışına koyun; böylece yanlışlıkla commit edilmesini önlersiniz.

---

## 2. Adım – OCR Motorunu Makbuz Tanıma İçin Yapılandırın

### Bunun önemi

`Receipt` dil modeli, yerleşik olarak eğikliği düzeltir ve gürültüyü azaltır; bu da katlanmış veya buruşmuş gerçek dünya makbuzlarında doğruluğu büyük ölçüde artırır.

### Kod

```csharp
// Step 2: Create and configure the OCR engine for receipt processing
var ocrEngine = new OcrEngine
{
    // Receipt model is optimized for invoices, grocery receipts, etc.
    Language = OcrLanguage.Receipt
};
```

---

## 3. Adım – Makbuz Görüntüsünden Metni Tanıyın

### Bunun önemi

Herhangi bir regex uygulamadan önce ham metne ihtiyacınız var. `RecognizeImage` metodu, tam dizeyi, güven skorlarını ve gerektiğinde daha fazlasını içeren bir `OcrResult` döndürür.

### Kod

```csharp
// Step 3: Recognize text from the receipt image
// Replace the path with the actual location of your receipt file.
string receiptPath = @"C:\Receipts\sample-receipt.jpg";

OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

// Quick sanity check – print the whole OCR output (helps debugging)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(receiptResult.Text);
Console.WriteLine("===================\n");
```

**Beklenen OCR çıktısı (örnek)**  
```
Walmart Supercenter
123 Main St.
Anytown, USA
Date: 02/12/2026
Item A   $3.45
Item B   $7.89
Subtotal $11.34
Tax      $0.91
Total:   $12.25
Thank you!
```

---

## 4. Adım – **Regex ile Tutarı Çıkar** İçin Bir Regex Oluşturun

### Bunun önemi

Makbuzlar birçok formatta olabilir, ancak “Total” (veya benzeri) kelimesinin ardından gelen dolar tutarı güvenilir bir referans noktasıdır. Aşağıdaki desen, isteğe bağlı boşlukları, iki nokta üst üste ve tireleri ve opsiyonel `$` işaretini toleranslı bir şekilde kabul eder.

### Kod

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**Desenin Açıklaması**

| Parça | Anlam |
|------|---------|
| `Total` | “Total” kelimesini (büyük/küçük harf duyarsız) arar. |
| `\s*[:\-]?` | İsteğe bağlı boşlukları, ardından opsiyonel iki nokta üst üste veya tireyi kabul eder. |
| `\s*\$?` | İsteğe bağlı boşluk ve opsiyonel dolar işareti. |
| `(\d+(\.\d{2})?)` | Bir veya daha fazla rakamı, isteğe bağlı olarak ondalık ve iki basamaklı cent'i yakalar. |

---

## 5. Adım – Çıkarılan Toplamı Çıktıla veya Eksik Veri Durumunu Yönet

### Bunun önemi

En iyi OCR bile bulanık makbuzlarda bir kelimeyi kaçırabilir. Zarif bir geri dönüş sağlamak çöküşleri önler ve özel mantık (ör. kullanıcıdan onay isteme) eklemenize olanak tanır.

### Kod

```csharp
// Step 5: Output the extracted total, or indicate it wasn't found
if (totalMatch.Success)
{
    string amount = totalMatch.Groups[1].Value;
    Console.WriteLine($"Total: ${amount}");
}
else
{
    Console.WriteLine("Total amount not found. Consider reviewing the OCR output manually.");
}
```

**Örnek konsol çıktısı**

```
Total: $12.25
```

---

## Tam Çalışan Örnek – Tüm Adımlar Tek Dosyada

Aşağıda, bir konsol projesine kopyalayıp yapıştırabileceğiniz tek dosyalı, kendine yeten bir program bulunuyor. Açıklamalar, hata yönetimi ve opsiyonel lisans yükleme içerir.

```csharp
// ---------------------------------------------------------------
// How to Read Receipt in C# – OCR + Regex (Complete Example)
// ---------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 0️⃣ Optional: Load your Aspose OCR license (remove trial watermark)
        try
        {
            var license = new Aspose.OCR.License();
            license.SetLicense("Aspose.OCR.lic"); // path to .lic file
        }
        catch (Exception ex)
        {
            Console.WriteLine("License not found – running in trial mode.");
        }

        // 1️⃣ Configure the OCR engine for receipt processing
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Receipt // receipt model = de‑skew + de‑noise
        };

        // 2️⃣ Path to the receipt image (change to your file)
        string receiptPath = @"YOUR_DIRECTORY/receipt.jpg";

        // 3️⃣ Perform OCR
        OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

        // 4️⃣ Debug: show full OCR text (helps when regex fails)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(receiptResult.Text);
        Console.WriteLine("===================\n");

        // 5️⃣ Regex to **extract amount using regex** (find the total)
        string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
        Match totalMatch = Regex.Match(receiptResult.Text, pattern,
                                        RegexOptions.IgnoreCase);

        // 6️⃣ Output
        if (totalMatch.Success)
        {
            string amount = totalMatch.Groups[1].Value;
            Console.WriteLine($"Total: ${amount}");
        }
        else
        {
            Console.WriteLine("Total amount not found. You might need to adjust the regex or improve image quality.");
        }
    }
}
```

**Programı Çalıştırma**

1. Yeni bir konsol projesi oluşturun (`dotnet new console -n ReceiptReader`).  
2. Aspose.OCR NuGet paketini ekleyin (`dotnet add package Aspose.OCR`).  
3. `YOUR_DIRECTORY/receipt.jpg` kısmını gerçek makbuz görüntüsü yolunuzla değiştirin.  
4. Derleyin ve çalıştırın (`dotnet run`).  

Her şey doğruysa OCR dökümü ardından `Total: $xx.xx` satırını görmelisiniz.

---

## Kenar Durumları ve Yaygın Varyasyonlar

### 1. Farklı Para Birimi Sembolleri

Euro (€) veya pound (£) gibi para birimleriyle çalışıyorsanız deseni genişletin:

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. Eksik “Total” Etiketi

Bazı makbuzlarda sadece “Grand Total” bulunur. Alternatif ekleyin:

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. Birden Fazla Toplam (ör. “Subtotal” ve “Total”)

Regex ilk eşleşmeyi bulursa, **son** eşleşmeyi almak isteyebilirsiniz:

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. Düşük Çözünürlüklü Görüntüler

- Tarama yaparken DPI'yi artırın (`300 DPI` ideal bir seviyedir).  
- Görüntüyü Aspose'a göndermeden önce basit bir bulanıklık‑azaltma filtresiyle ön‑işlem yapın (bu kılavuzun kapsamı dışında, ancak keşfetmeye değer).

---

## Gerçek Dünya Projeleri İçin Pro İpuçları

- Birden fazla alan (vergi, ürünler vb.) çıkarmanız gerekiyorsa **OCR sonucunu önbelleğe alın** – OCR maliyetini sadece bir kez ödersiniz.  
- Ham OCR metnini bir veritabanına **loglayın**; bu, itiraz edilen harcamalar için değerli bir denetim izi olur.  
- Bir web API geliştirirken **OCR'ı arka plan çalışanında çalıştırın**; birkaç yüz milisaniye sürebilir, bu asenkron olarak uygundur ancak senkron bir istek için ideal değildir.  
- **Çıkarılan tutarı iş kurallarına göre doğrulayın** (ör. tutar > 0 olmalı) veritabanına kaydetmeden önce.

---

## Sonuç

Aspose OCR kullanarak C#'ta **makbuz nasıl okunur** sorusunu yanıtladık, ardından **regex ile tutarı çıkar** yöntemiyle toplam satırını güvenilir bir şekilde bulduk. `Receipt` dil modeli sayesinde eğikliği düzeltilmiş ve gürültüsü azaltılmış metin elde ediyor, kısa bir regular expression ise çoğu format farklılığını hallediyor. Yukarıdaki tam kod parçacığı, herhangi bir .NET konsol ya da servis projesine kolayca eklenebilir; ek kenar‑durum önerileri ise üretim ortamı için sağlam bir temel sunar.

Bir sonraki adıma hazır mısınız? Çözümü, tek tek satır öğelerini çekmek, vergiyi otomatik hesaplamak ya da bir harcama‑takip API'siyle bütünleştirmek için genişletin. Deseni kıran bir makbuzla karşılaşırsanız, **regex ile toplam bul** yaklaşımının sadece bir başlangıç olduğunu unutmayın—lokalinize göre deseni istediğiniz gibi ayarlayabilirsiniz.

İyi kodlamalar, ve makbuz‑işlemenizin hızlı, doğru ve tamamen otomatik olmasını dileriz!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}