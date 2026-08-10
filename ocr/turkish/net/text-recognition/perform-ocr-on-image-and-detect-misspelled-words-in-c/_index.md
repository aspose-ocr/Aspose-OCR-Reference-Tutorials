---
category: general
date: 2026-06-03
description: Aspose.OCR kullanarak görüntüde OCR gerçekleştirip metni çıkarın. Tek
  bir C# demosunda yanlış yazılmış kelimeleri nasıl tespit edeceğinizi ve yazım önerilerini
  nasıl alacağınızı öğrenin.
draft: false
keywords:
- perform OCR on image
- extract text from image
- detect misspelled words
- get spelling suggestions
- how to extract text
language: tr
og_description: Görüntüdeki metni çıkarmak için OCR yapın, ardından hatalı yazılmış
  kelimeleri tespit edin ve Aspose.OCR ile C#’ta yazım önerileri alın.
og_title: Resimde OCR Yap ve C#'ta Yazım Hatalı Kelimeleri Tespit Et
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Perform OCR on image and extract text from image using Aspose.OCR.
    Learn how to detect misspelled words and get spelling suggestions in a single
    C# demo.
  headline: Perform OCR on Image and Detect Misspelled Words in C#
  type: TechArticle
tags:
- Aspose OCR
- C#
- Spell Checking
title: Görüntüde OCR Yap ve C#'ta Yanlış Yazılmış Kelimeleri Tespit Et
url: /tr/net/text-recognition/perform-ocr-on-image-and-detect-misspelled-words-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntü Üzerinde OCR Yapma ve C#'ta Yazım Hatalı Kelimeleri Tespit Etme

Saçınızı yolmak zorunda kalmadan **perform OCR on image** dosyalarının nasıl yapılacağını hiç merak ettiniz mi? Tek başınıza değilsiniz. İster eski mektupları dijitalleştiriyor olun, faturaları tarıyor olun ya da akıllı bir belge iş akışı oluşturuyor olun, resimlerden temiz metin çıkarmak ilk engeldir. İyi haber? Aspose.OCR ile dakikalar içinde bir çözüm oluşturabilirsiniz ve ek olarak aynı çalıştırmada **detect misspelled words** ve **get spelling suggestions** da yapabilirsiniz.

Bu öğreticide, **extracts text from image** yapan, bir İngilizce yazım denetleyicisi çalıştıran ve her hatayı kullanışlı düzeltme önerileriyle yazdıran tam, çalıştırmaya hazır bir C# konsol uygulamasını adım adım inceleyeceğiz. Sonuna geldiğinizde **how to extract text**'i tam olarak bilecek, spell‑check API'sini nasıl bağlayacağınızı ve beklenen konsol çıktısının nasıl göründüğünü öğreneceksiniz.

## Oluşturacağınız Şey

- Tipografik hatalar içeren bir bitmap (veya PNG) yükleyin.  
- Aspose.OCR'yi **perform OCR on image** yapmak ve ham dize verisi elde etmek için çalıştırın.  
- Yerleşik İngilizce yazım denetleyiciyi başlatın.  
- **Detect misspelled words** ve her biri için **get spelling suggestions** alın.  
- Konsola düzenli bir rapor yazdırın.

Harici hizmetler yok, uğraştırıcı HTTP çağrıları yok—sadece tek bir NuGet paketi ve birkaç satır kod.

## Önkoşullar

- .NET 6.0 SDK veya daha yenisi (kod .NET Framework 4.7+ üzerinde de çalışır).  
- Visual Studio 2022 (veya istediğiniz herhangi bir editör).  
- .NET için Aspose.OCR NuGet paketi (`Aspose.OCR`).  
- Projeden referans alabileceğiniz bir yerde bulunan bir görüntü dosyası (`letter_with_typos.png`).

Aspose'u daha önce hiç kullanmadıysanız endişelenmeyin—paketi kurmak şu komutu çalıştırmak kadar kolay:

```bash
dotnet add package Aspose.OCR
```

Şimdi uygulamaya dalalım.

## Adım 1: Projeyi Kurun ve Aspose.OCR'yi Yükleyin

Yeni bir konsol projesi oluşturun ve OCR kütüphanesini ekleyin:

```bash
dotnet new console -n OcrSpellDemo
cd OcrSpellDemo
dotnet add package Aspose.OCR
```

Geri yükleme tamamlandıktan sonra `Program.cs` dosyasını açın. Varsayılan içeriği daha sonra tam demo kodu ile değiştireceğiz, ama önce her bir ad alanının neden önemli olduğundan bahsedelim.

- `Aspose.OCR` – Çekirdek OCR motoru ve görüntü işleme.  
- `Aspose.OCR.SpellCheck` – Kütüphane ile gelen yazım denetleme yardımcı programları.  
- `System` – Standart .NET temel sınıfları (ör. `Console`).

## Adım 2: Görüntüyü Yükleyin ve Görüntü Üzerinde OCR Yapın

İlk gerçek iş, görüntüyü OCR motoruna beslemektir. Aspose.OCR birçok formatı (PNG, JPEG, TIFF) okur. İşte işi yapan kod parçacığı:

```csharp
// Step 2: Load the image that contains the text to be recognized
var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

// Step 3: Perform OCR to extract the raw text from the image
var ocrEngine = new OcrEngine();
var ocrResult = ocrEngine.Recognize(image);
```

> **Neden önemli:** `OcrImage.FromFile` piksel‑seviyesindeki detayları soyutlar, `OcrEngine.Recognize` ise görsel glifleri Unicode karakterlerine çeviren eğitilmiş sinir modelini çalıştırır. `ocrResult.Text` özelliği artık ham dizeyi tutar—tam da **extract text from image**'e ihtiyacınız olan şey.  
> **Pro ipucu:** Görüntünüz birden fazla dil içeriyorsa, `Recognize`'ı çağırmadan önce `ocrEngine.Language = OcrLanguage.Multilingual;` ayarlayabilirsiniz.

## Adım 3: İngilizce Yazım Denetleyiciyi Başlatın

Aspose.OCR, kutudan çıkar çıkmaz İngilizceyi anlayan yerleşik bir yazım denetleme motoru ile birlikte gelir. Onu başlatmak tek satırdır:

```csharp
// Step 4: Initialise the English spell‑checker
var spellChecker = new SpellChecker(OcrLanguage.English);
```

> **Bu adımın önemi:** OCR çıktısı hatalı tanınmış karakterler (ör. “l” vs “1”) veya kaynak belgeden gelen gerçek yazım hataları içerebilir. Yazım denetleyici dizeyi tarar, şüpheli tokenları bulur ve alternatifler önerir.

## Adım 4: Yazım Hatalı Kelimeleri Tespit Edin ve Yazım Önerileri Alın

Şimdi OCR metnini denetleyiciye besliyoruz:

```csharp
// Step 5: Check the recognized text for misspelled words and obtain suggestions
var misspellings = spellChecker.Check(ocrResult.Text);
```

`misspellings`, her bir girişin hatalı kelimeyi ve olası düzeltmelerin bir dizisini içerdiği bir koleksiyondur.

## Adım 5: Sonuçları Çıktılayın

Son olarak, koleksiyon üzerinde döngü kurup insan tarafından okunabilir bir rapor yazdırıyoruz:

```csharp
// Step 6: Output each misspelled word together with its suggested corrections
foreach (var entry in misspellings)
{
    Console.WriteLine($"Misspelled: {entry.Word}");
    Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
}
```

### Beklenen Konsol Çıktısı

`letter_with_typos.png` dosyasının şu cümleyi içerdiğini varsayalım:

```
Ths is an exampel of a lettter with som misspelled wrds.
```

Demo çalıştırıldığında aşağıdakine benzer bir çıktı üretir:

```
Misspelled: Ths
  Suggestions: This, Thus, The
Misspelled: exampel
  Suggestions: example, exemplar, exampell
Misspelled: lettter
  Suggestions: letter, litter, lett
Misspelled: som
  Suggestions: some, sum, son
Misspelled: wrds
  Suggestions: words, wards, wryds
```

Her bir yazım hatasının bir dizi makul düzeltme ile eşleştiğine dikkat edin—kullanıcı dostu bir düzeltme arayüzü oluştururken tam da ihtiyacınız olan şey.

## Tam Çalışan Örnek

Aşağıda **tam, kopyala‑yapıştır‑hazır** program bulunmaktadır. `YOUR_DIRECTORY` ifadesini görüntü dosyanızın gerçek yolu ile değiştirin.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Load the image that contains the text to be recognized
        var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

        // Step 2: Perform OCR to extract the raw text from the image
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(image);

        // Step 3: Initialise the English spell‑checker
        var spellChecker = new SpellChecker(OcrLanguage.English);

        // Step 4: Check the recognized text for misspelled words and obtain suggestions
        var misspellings = spellChecker.Check(ocrResult.Text);

        // Step 5: Output each misspelled word together with its suggested corrections
        foreach (var entry in misspellings)
        {
            Console.WriteLine($"Misspelled: {entry.Word}");
            Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
        }

        // Optional: Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

> **Dikkate Alınması Gereken Kenar Durumları**  
> - **Boş Görüntü:** OCR motoru boş bir dize döndürürse, `spellChecker.Check` sadece boş bir koleksiyon döndürür—çökme olmaz.  
> - **İngilizce Olmayan Metin:** `OcrLanguage.English` yerine `OcrLanguage.French` (veya desteklenen herhangi bir dil) kullanarak **detect misspelled words**'i diğer yerel ayarlarda yapabilirsiniz.  
> - **Büyük Belgeler:** Çok sayfalı PDF'lerde, her sayfada OCR çalıştırıp sonuçları birleştirerek yazım denetlemesinden önce toplarsınız.

## Görsel Genel Bakış (Resim Alt Metni)

![Görüntü üzerinde OCR yapma, görüntüden metin çıkarma ve ardından yazım hatalı kelimeleri yazım önerileriyle tespit etme akışını gösteren diyagram](perform-ocr-on-image-flow.png)

*Yukarıdaki diyagram uçtan uca akışı gösterir: görüntü → OCR motoru → ham metin → yazım denetleyici → öneriler.*

## Sık Sorulan Sorular & Pro İpuçları

| Question | Answer |
|----------|--------|
| **İnternet bağlantısına ihtiyacım var mı?** | Hayır. Aspose.OCR tamamen yerel olarak çalışır; çevrim dışı veya güvenli ortamlar için mükemmeldir. |
| **Yazım denetleyici ne kadar doğru?** | Yaklaşık 150k İngilizce kelime içeren bir sözlük ve bulanık eşleşme kullanır, bu yüzden çoğu yaygın yazım hatası yakalanır. |
| **Sözlüğü özelleştirebilir miyim?** | Evet. `SpellChecker.AddUserDictionary("custom.txt")` domain‑spesifik terimleri (ör. ürün adları) yüklemenizi sağlar. |
| **Görüntü eğik olursa ne olur?** | OCR motoru yönelimi otomatik algılar, ancak inatçı durumlar için `ocrEngine.ImagePreprocessing.Rotate(angle)` metodunu manuel olarak çağırabilirsiniz. |
| **Önerileri UI'da vurgulamanın bir yolu var mı?** | `misspellings` koleksiyonuna sahip olduktan sonra, her bir `entry.Word`'i `ocrResult.Text` içindeki konumuna eşleyebilir ve RichTextBox ya da web görünümünde altını çizebilirsiniz. |

## Sonuç

Sizlere **how to perform OCR on image**, **extract text from image** ve ardından **detect misspelled words** yaparken **getting spelling suggestions** almayı gösterdik—hepsi kısa bir C# konsol uygulamasıyla. Temel fikir basit: karakter tanıma işini Aspose.OCR'ye bırakın, ardından yerleşik yazım denetleyicisi çıktıyı temizlesin. Buradan demo'yu tam bir belge işleme servisine genişletebilir, bir web API ile entegre edebilir veya bir masaüstü editörüne bağlayabilirsiniz.

Bir sonraki adıma hazır mısınız? Dili İspanyolcaya değiştirin, çok sayfalı bir PDF besleyin veya kullanıcıların bir kelimeye tıklayarak öneriyi kabul etmesini sağlayan küçük bir WPF ön yüzü oluşturun. Yapı taşları zaten yerinde—denemeye devam edin.

Herhangi bir sorunla karşılaşırsanız veya genişletme fikirleriniz varsa, aşağıya bir yorum bırakın. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.OCR kullanarak dil seçimiyle Görüntü Metni Çıkarma C#](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Aspose.OCR .NET ile Görüntüden Metin Çıkarma](/ocr/english/net/image-and-drawing-recognition/)
- [Görüntüden Metin Çıkarma – Aspose.OCR for .NET ile OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}