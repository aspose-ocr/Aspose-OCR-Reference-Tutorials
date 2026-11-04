---
category: general
date: 2026-02-14
description: 'Toplu görüntü OCR''si artık kolay: Java''da paralel işleme ile Aspose
  OCR kullanarak PNG dosyalarından metin çıkarmayı öğrenin.'
draft: false
keywords:
- batch image OCR
- extract text from png
- parallel OCR Java
- Aspose OCR async
- OCR batch processing
language: tr
og_description: Java'da Aspose OCR'un asenkron API'sini kullanarak PNG dosyalarından
  metin nasıl çıkarılacağını gösteren toplu görüntü OCR öğreticisi.
og_title: Java'da Toplu Görüntü OCR – Hızlı PNG Metin Çıkarma
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Java'da Toplu Görüntü OCR – PNG Dosyalarından Metni Hızlıca Çıkar
url: /tr/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Toplu Görüntü OCR – PNG Dosyalarından Metni Hızlıca Çıkar

Bir klasördeki PNG taramalarına **toplu görüntü OCR** çalıştırmanız ve hız konusunda endişelenmeniz hiç oldu mu? Yalnız değilsiniz. Gerçek dünyadaki birçok projede—fatura dijitalleştirme, taranmış kitapların arşivlenmesi veya makbuzların işlenmesi—geliştiricilerin **PNG'den metin çıkarması** hızlı ve güvenilir bir şekilde gerekir.  

İyi haber? Aspose OCR’un eşzamansız API'si sayesinde sadece birkaç Java satırıyla paralel bir OCR hattı oluşturabilirsiniz. Bu rehberde tam, çalıştırılabilir çözümü adım adım inceleyecek, her parçanın neden önemli olduğunu açıklayacak ve sonuçları nasıl doğrulayacağınızı göstereceğiz. Sonunda, tüm PNG dosyalarını paralel olarak işleyen, temiz ve imla kontrolü yapılmış metin çıktısı veren bağımsız bir programınız olacak.

## Öğrenecekleriniz

- Toplu işleme için PNG dosyalarını listeleme  
- Aspose `OcrEngine`'i İngilizce dil ve imla düzeltmesi için yapılandırma  
- `processAsync` ile eşzamansız OCR çalıştırma ve `Future` sonucunu işleme  
- Her görüntü için tanınan metni okuma ve gösterme  
- Ölçeklendirme, hata yönetimi ve performans ayarlamaları için ipuçları  

### Önkoşullar

- Java 8 veya daha yeni bir sürüm (kod standart `java.util.concurrent` paketini kullanıyor)  
- Aspose OCR for Java lisansı veya ücretsiz deneme sürümü (Aspose web sitesinden indirin)  
- Test etmek istediğiniz birkaç PNG ekran görüntüsü veya taranmış sayfa içeren bir klasör  

Şimdi başlayalım.

## Adım 1 – Toplu İşlem İçin PNG Dosyalarınızı Toplayın

OCR motorunun çalışabilmesi için önce hangi görüntüleri işleyeceğini bilmesi gerekir. En basit yol, mutlak ya da göreli dosya yollarından oluşan bir `List<String>` oluşturmak.

```java
// Step 1: Prepare a list of PNG files you want to run OCR on
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png",
        "YOUR_DIRECTORY/page4.png");
```

**Neden önemli:**  
Listeyi önceden oluşturmak, motorun her dosyayı bağımsız olarak zamanlamasını sağlar; bu da gerçek toplu işleme temelidir. Daha sonra klasörü dinamik olarak taramanız gerekirse, statik `Arrays.asList` yerine bir `Files.walk` akışı kullanarak değiştirebilirsiniz.

## Adım 2 – Aspose OCR Motorunu Başlatın ve Ayarlayın

Aspose’un `OcrEngine`i oldukça yapılandırılabilir. Burada dili İngilizce olarak ayarlıyor ve imla düzeltmesini açıyoruz—gürültülü PNG taramalarından çıkarılan metnin kalitesini büyük ölçüde artıran iki seçenek.

```java
// Step 2: Create and configure the OCR engine
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getEngineOptions()
         .setLanguage(OcrLanguage.ENGLISH)          // English language model
         .setSpellCorrectionEnabled(true);          // Enable spell‑checking
```

**Bu ayarların nedeni:**  
- **Dil seçimi** motorun hangi karakter seti ve sözlüğü kullanacağını belirler, yanlış tanıma olasılığını azaltır.  
- **İmla düzeltme** yaygın OCR hatalarını (ör. “1” ile “l” karışıklığı) otomatik olarak yakalar, çıktıyı sonradan işlemek zorunda kalmazsınız.

> **Pro ipucu:** Görüntüleriniz birden fazla dil içeriyorsa, `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.FRENCH)` gibi bir liste geçirebilirsiniz.

## Adım 3 – Eşzamansız Toplu İşlemeyi Başlatın

Ağır iş `processAsync` içinde gerçekleşir. Bu metod bir `Future<List<OcrResult>>` döndürür; böylece ana iş parçacığınız OCR arka planda çalışırken başka işler yapmaya devam edebilir.

```java
// Step 3: Start asynchronous processing of the image batch
Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

// (Optional) Do something useful while OCR runs, e.g., log progress, load UI, etc.
System.out.println("OCR started – you can perform other tasks now...");
```

**Neden eşzamansız:**  
OCR’u sıralı çalıştırmak son derece yavaş olabilir—her PNG bir saniye ya da daha fazla sürebilir. İşi bir iş parçacığı havuzuna devrederek birden çok CPU çekirdeğini kullanır ve toplam çalışma süresini büyük ölçüde azaltırsınız.

## Adım 4 – Sonuçlar Hazır Olduğunda Çekin

Çıktıyı tüketmeye hazır olduğunuzda, sadece `Future` üzerindeki `get()` metodunu çağırın. Bu çağrı yalnızca OCR tamamlanana kadar bloklanır, ardından giriş listesindeki sıraya göre `OcrResult` nesnelerinin bir listesini verir.

```java
// Step 4: Wait for all results and retrieve them
List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion
```

**Zaman aşımı yönetimi:**  
Sonsuz beklemeyi önlemek isterseniz `ocrFuture.get(60, TimeUnit.SECONDS)` kullanın ve bir `TimeoutException` yakalayarak geri dönüş stratejisi uygulayın.

## Adım 5 – Her PNG İçin Tanınan Metni Gösterin

Artık sonuçlar elinizde, bunları döngüye alıp çıkarılan metni orijinal dosya adıyla birlikte yazdırın. İşte **PNG dosyalarından metin çıkarma** işleminin son adımı.

```java
// Step 5: Show the OCR output for each image
for (int i = 0; i < ocrResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(ocrResults.get(i).getText());
    System.out.println("---");
}
```

**Beklenen çıktı örneği**

```
File: YOUR_DIRECTORY/page1.png
Invoice #12345
Date: 2024‑03‑01
Total: $1,250.00
---
File: YOUR_DIRECTORY/page2.png
...
```

OCR motoru bir sayfayı tanıyamazsa, ilgili `getText()` boş bir dize döndürür—üretim kodunda her zaman kontrol etmeye değer.

## Tam Çalışan Örnek

Aşağıda tüm parçaları bir araya getiren, çalıştırmaya hazır tam program yer alıyor. `ParallelOcrDemo.java` adlı bir dosyaya yapıştırın, `YOUR_DIRECTORY` kısmını PNG klasörünüzün yolu ile değiştirin ve `javac ParallelOcrDemo.java && java ParallelOcrDemo` komutlarıyla çalıştırın.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Prepare a list of image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png",
                "YOUR_DIRECTORY/page4.png");

        // Step 2: Create and configure the OCR engine (set language and enable spell‑checking)
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineOptions()
                 .setLanguage(OcrLanguage.ENGLISH)
                 .setSpellCorrectionEnabled(true);

        // Step 3: Start asynchronous processing of the image batch
        Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

        // (Optional) Perform other work here while OCR runs in the background...
        System.out.println("OCR processing started in background...");

        // Step 4: Wait for all results and retrieve them
        List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion

        // Step 5: Display the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### Demoyu Çalıştırma

1. **Derleme** – `javac -cp "aspose-ocr.jar" ParallelOcrDemo.java`  
2. **Çalıştırma** – `java -cp ".:aspose-ocr.jar" ParallelOcrDemo`  

Her PNG dosya adı ve ardından çıkarılan metin, tire işaretiyle ayrılmış olarak görüntülenmelidir.  

> **Not:** `LicenseException` alırsanız, motoru oluşturmadan önce Aspose lisansınızı yüklediğinizden emin olun:

```java
License lic = new License();
lic.setLicense("Aspose.OCR.Java.lic");
```

## Ölçeklendirme – Gerçek Dünya Toplu OCR İçin İpuçları

| Durum | Öneri |
|-----------|----------------|
| **Yüzlerce PNG** | `ocrEngine.setThreadPoolSize(8)` (veya CPU çekirdek sayısına göre daha yüksek) ile iş parçacığı havuzunu artırın. |
| **Bellek kısıtlamaları** | Dosyaları daha küçük parçalar halinde işleyin (ör. 50’şer batch) ve her batch sonrası `OcrResult` listesini serbest bırakın. |
| **Değişken görüntü kalitesi** | Tanımadan önce otomatik döndürme, eğikliği giderme veya kontrast artırma için `setPreprocessingOptions`ı etkinleştirin. |
| **Birden fazla dil** | `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.SPANISH)` çağırın ve isteğe bağlı olarak özel bir sözlük ayarlayın. |
| **Hata yönetimi** | `ocrFuture.get()` çağrısını `ExecutionException` için try‑catch bloğuna alın; başarısız dosyaları kaydedin ve tüm batch’i durdurmayın. |

Bu stratejiler, **toplu görüntü OCR** hattınızı giriş kümesi büyüdükçe bile sağlam tutar.

## Sık Sorulan Sorular

**S: JPEG veya TIFF dosyalarıyla da çalışır mı?**  
C: Kesinlikle. `processAsync` metodu Aspose OCR tarafından desteklenen (PNG, JPEG, TIFF, BMP vb.) tüm formatları kabul eder. Sadece listenizdeki dosya uzantılarını değiştirmeniz yeterlidir.

**S: Düzeni (tablolar, sütunlar) korumam gerekirse?**  
C: Aspose OCR, konumsal verileri döndüren bir `getLayoutResult()` metodu sağlar. Her kelimenin sınırlayıcı kutularını analiz ederek tabloları yeniden oluşturabilirsiniz.

**S: Bunu sunucusuz bir platformda çalıştırabilir miyim?**  
C: Evet—JAR dosyasını Aspose kütüphanesiyle paketleyip AWS Lambda, Azure Functions veya Google Cloud Functions üzerine dağıtabilirsiniz. OCR iş parçacığı havuzu için fonksiyonun bellek tahsisinin yeterli olduğundan emin olun.

## Sonuç

Artık Aspose OCR’un eşzamansız API’sini Java’da kullanarak **toplu görüntü OCR** çözümünü tamamen kendinizin içinde barındıran, **PNG dosyalarından metin çıkarma** işlemini verimli bir şekilde gerçekleştiren bir programınız var. Bu öğreticide dosya listesinin hazırlanmasından dil ve imla kontrolünün yapılandırılmasına, paralel işleme başlatmaya, sonuçları ele almaya ve üretim ortamları için hattı ölçeklendirmeye kadar her şeyi ele aldık.

Bir sonraki adım için hazır mısınız? Dili Fransızcaya değiştirin, özel sözlüklerle deney yapın ya da çıktıyı aranabilir bir ElasticSearch indeksine entegre edin. Hızlı toplu OCR ile modern Java eşzamanlılığını birleştirdiğinizde sınır yoktur.

İyi kodlamalar, metin çıkarımınız hızlı ve kusursuz olsun! 

![Diagram showing parallel OCR workers handling multiple PNG files](/images/batch-ocr-diagram.png){: .center alt="Paralel OCR çalışanlarının birden çok PNG dosyasını işlediği diyagram"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}