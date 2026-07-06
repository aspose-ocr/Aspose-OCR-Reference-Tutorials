---
category: general
date: 2026-02-17
description: Java'da OCR kullanarak PDF'den metin çıkarmak, PDF'yi görüntülere dönüştürmek
  ve Aspose.OCR kullanarak taranmış PDF dosyalarında OCR gerçekleştirmek nasıl yapılır?
draft: false
keywords:
- how to use OCR
- extract text from pdf
- convert pdf to images
- perform OCR on pdf
- recognize scanned pdf
language: tr
og_description: Java'da OCR kullanarak PDF dosyalarından metin nasıl çıkarılır. PDF'yi
  görüntülere dönüştürmeyi ve taranmış PDF'yi Aspose.OCR ile tanımayı öğrenin.
og_title: Java'da OCR Nasıl Kullanılır – Tam Kılavuz
tags:
- OCR
- Java
- Aspose
title: Java'da OCR Nasıl Kullanılır – Aspose.OCR ile PDF'den Metin Çıkarma
url: /tr/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-pdf-with-aspose-ocr/
---

.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da OCR Nasıl Kullanılır – Aspose.OCR ile PDF’ten Metin Çıkarma

Tarayıcıdan gelen bir PDF’i aranabilir metne **nasıl dönüştürebileceğinizi** hiç merak ettiniz mi? Tek başınıza değilsiniz. Çoğu geliştirici, PDF bir dizi görüntü olarak geldiğinde bir duvara çarpar ve geleneksel metin çıkarıcıları hiçbir şey döndürmez. İyi haber? Birkaç satır Java ve Aspose.OCR ile **PDF’ten metin çıkarabilir**, **PDF’i görüntülere dönüştürebilir** ve **tar scanned PDF’yi tanıyabilirsiniz** tek bir, zahmetsiz iş akışı içinde.

Bu öğreticide, kütüphaneyi lisanslamaktan son sonucu yazdırmaya kadar bilmeniz gereken her şeyi adım adım ele alacağız. Sonunda, taranmış rapor, fatura veya e‑kitaptan düz metin çıkaran, çalıştırmaya hazır bir programınız olacak. Harici hizmetler, sihir yok — sadece kontrol sizde olan saf Java kodu.

## Gereksinimler

- **Java Development Kit (JDK) 8+** – herhangi bir yeni sürüm yeterli.
- **Aspose.OCR for Java** JAR (Aspose web sitesinden indirin).  
- **Geçerli bir Aspose.OCR lisans dosyası** (`Aspose.OCR.lic`). Ücretsiz deneme çalışır, ancak lisans tam doğruluk sağlar.
- **Örnek bir taranmış PDF** (ör. `scanned-report.pdf`).  
- Bir IDE veya basit bir metin editörü ve bir terminal.

Hepsi bu. Maven, Gradle veya ekstra bağımlılıklar yok — sadece Aspose.OCR JAR’ı sınıf yolunuza ekleyin.

![OCR kullanma örneği](image-placeholder.png "OCR kullanma örneği")

## Adım 1 – Aspose.OCR Lisansınızı Yükleyin (Neden Önemli)

Motor tam hızda çalışabilmesi için lisans dosyanızın nerede olduğunu ona söylemeniz gerekir. Bu adımı atlamak, kütüphaneyi değerlendirme moduna sokar; bu da çıktıya filigran ekler ve doğruluğu sınırlayabilir.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – required for unrestricted OCR
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**Neden işe yarıyor:** `License` sınıfı `.lic` dosyasını okur ve global olarak kaydeder. Bir kez ayarlandığında, oluşturduğunuz her `OcrEngine` otomatik olarak lisanslı özellikleri kullanır.

## Adım 2 – OCR Motorunu Oluşturun (Sihirin Arkasındaki Motor)

`OcrEngine` örneği, görüntüleri tarayan ve metin üreten iş gücüdür. Piksel desenlerini yorumlayan beyin gibi düşünün.

```java
        // Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**İpucu:** Dil, güven eşiği gibi ayarları değiştirebilir veya motorun özellikleri aracılığıyla GPU hızlandırmasını etkinleştirebilirsiniz. Çoğu İngilizce PDF için varsayılanlar yeterlidir.

## Adım 3 – Girişi Hazırlayın: PDF’nizi Ekleyin (PDF’i Görüntülere Dönüştürme)

Aspose.OCR, bir PDF’in her sayfasını bir görüntü olarak ele alır. `addPdf` metodunu çağırdığınızda kütüphane sessizce her sayfayı rasterleştirir; bu da **PDF’i görüntülere dönüştürme** işlemini tanıma öncesinde yapmanızı sağlar.

```java
        // Prepare OCR input – each PDF page becomes an image internally
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");
```

**Ne oluyor:**  
- PDF açılıyor.  
- Her sayfa, karakter detayını korumak için 300 dpi (varsayılan) ile işleniyor.  
- Oluşturulan bitmap nesneleri `OcrInput` koleksiyonunda saklanıyor.

Eğer ham görüntülere (hata ayıklama veya özel ön işleme için) ihtiyacınız olursa, bu adımdan sonra `ocrInput.getPages()` metodunu çağırabilirsiniz.

## Adım 4 – OCR İşlemini Çalıştırın (PDF Üzerinde OCR Yapma)

Şimdi asıl iş başlıyor. `recognize` metodu her görüntü üzerinde döner, tanıma algoritmasını çalıştırır ve sonuçları bir `OcrResult` içinde toplar.

```java
        // Run OCR on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Neden önemli:** `OcrResult` sadece düz metni değil, aynı zamanda güven skorlarını, sınırlayıcı kutuları ve orijinal görüntü referansını da içerir. Çoğu senaryoda sadece `getText()` yeterlidir.

## Adım 5 – Çıkarılan Metni Alın ve Görüntüleyin

Son olarak, sonuçtan düz metin dizesini alın ve ekrana yazdırın. Ayrıca bir dosyaya kaydedebilir, bir arama indeksine besleyebilir veya sonraki bir NLP boru hattına aktarabilirsiniz.

```java
        // Output the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

### Beklenen Çıktı

`scanned-report.pdf` basit bir paragraf içeriyorsa, aşağıdakine benzer bir çıktı görürsünüz:

```
Extracted text:
Quarterly Sales Report
Region: North America
Total Revenue: $4,527,000
...
```

Tam formatlama, mümkün olduğunca orijinal düzeni korur; satır sonları da aynı kalır.

## Yaygın Kenar Durumlarını Ele Alma

### 1. Çok‑Dilli PDF’ler

Belgeniz Fransızca veya İspanyolca metin içeriyorsa, `recognize` çağırmadan önce dili ayarlayın:

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);
```

Motorun otomatik algılamasını sağlamak için bir dizi dil de verebilirsiniz.

### 2. Düşük Çözünürlüklü Taramalar

150 dpi taramalarla çalışıyorsanız, iç render DPI değerini artırın:

```java
ocrInput.addPdf("low-res.pdf", 600); // render at 600 dpi for better accuracy
```

Daha yüksek DPI karakter netliğini artırır ancak daha fazla bellek tüketir.

### 3. Büyük PDF’ler (Bellek Yönetimi)

Yüzlerce sayfalı PDF’ler için, sayfaları partiler halinde işleyin:

```java
int batchSize = 10;
for (int i = 0; i < ocrInput.getPages().size(); i += batchSize) {
    List<OcrPage> batch = ocrInput.getPages().subList(i, Math.min(i + batchSize, ocrInput.getPages().size()));
    OcrInput batchInput = new OcrInput();
    batchInput.getPages().addAll(batch);
    OcrResult batchResult = ocrEngine.recognize(batchInput);
    // Append batchResult.getText() to your final output
}
```

Bu yöntem, JVM yığınının aşırı büyümesini önler.

## Tam, Çalıştırmaya Hazır Örnek

Aşağıda, import’lar ve lisans yönetimi dahil tam program yer alıyor; kopyalayıp anında çalıştırabilirsiniz.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (required for full functionality)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Step 2: Create an OCR engine instance that will perform the recognition
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Prepare the OCR input by adding the PDF file.
        // Each page of the PDF is internally converted to an image.
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");

        // Step 4: Run the OCR process on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

Şu komutla çalıştırın:

```bash
javac -cp "path/to/aspose-ocr.jar" PdfOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" PdfOcrDemo
```

Çıkarılan metnin konsola yazdırıldığını göreceksiniz.

## Özet – Neler Öğrendik

- Java’da **OCR nasıl kullanılır** ve Aspose.OCR ile.  
- **PDF’ten metin çıkarma** iş akışı.  
- Kütüphane, karakterleri tanımadan önce **PDF’i görüntülere dönüştürür**.  
- **PDF üzerinde OCR** yaparken çoklu dil, düşük çözünürlük ve büyük belgeler için ipuçları.  
- Herhangi bir Java projesine ekleyebileceğiniz tam, çalıştırılabilir kod örneği.

## Sonraki Adımlar ve İlgili Konular

Artık **tar scanned PDF** tanıyabildiğinize göre, şu fikirleri değerlendirebilirsiniz:

- **Aranabilir PDF Oluşturma** – OCR metnini orijinal PDF üzerine bindirerek aranabilir bir belge yaratın.  
- **Toplu İşleme Servisi** – Kodu bir Spring Boot mikroservisine sararak PDF’leri REST üzerinden kabul edin.  
- **Elasticsearch Entegrasyonu** – Çıkarılan metni hızlı tam‑metin arama için indeksleyin.  
- **Görüntü Ön‑İşleme** – OpenCV kullanarak sayfaları eğriltme düzeltme veya gürültü azaltma yapın; böylece doğruluk daha da artar.

Bu konular, keşfettiğimiz temel kavramların üzerine inşa edilmiştir; deney yapmaktan çekinmeyin ve OCR motorunun ağır işini üstlenmesine izin verin.

---

*İyi kodlamalar! Lisans hataları ya da beklenmedik null sonuçları gibi sorunlarla karşılaşırsanız, aşağıya yorum bırakın. Her zaman bir hata ayıklama oturumuna hazırım.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}