---
category: general
date: 2026-02-17
description: 'görüntüden metne java öğreticisi: Aspose OCR kullanarak bir görüntüden
  Urdu metnini nasıl çıkaracağınızı öğrenin. Tam java OCR örneği dahil.'
draft: false
keywords:
- image to text java
- how to extract text
- extract urdu text
- java ocr example
- load image ocr
language: tr
og_description: Görüntüden metne Java öğreticisi, Aspose OCR kullanarak bir görüntüden
  Urdu metnini nasıl çıkaracağını gösterir. Tam Java OCR örneğini adım adım izleyin.
og_title: 'görüntüden metne java: Aspose OCR ile Urdu Metnini Çıkar'
tags:
- OCR
- Java
- Aspose
title: 'görüntüden metne java: Aspose OCR ile Urdu Metnini Çıkar'
url: /tr/java/ocr-operations/image-to-text-java-extract-urdu-text-with-aspose-ocr/
---

/products/products-backtop-button >}}

All preserved.

Now produce final output with translated content. Ensure no extra explanations.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# image to text java: Aspose OCR ile Urdu Metnini Çıkarın

Urdu belgeleri için **image to text java** dönüşümüne ihtiyacınız varsa, doğru yerdesiniz. *Metni nasıl çıkaracağınızı* bir el yazısı notunun ya da taranmış bir gazete sayfasının fotoğrafından merak ettiniz mi? Bu rehber, Aspose OCR kullanarak bir görüntüden doğrudan Urdu karakterlerini çeken bir **java ocr example** üzerinden size yol gösterecek.

Kütüphaneyi lisanslamaktan sonuçları konsola yazdırmaya kadar her şeyi ele alacağız. Sonunda **load image ocr** dosyalarını yükleyebilecek, dili Urdu olarak ayarlayabilecek ve temiz Unicode çıktısı elde edebileceksiniz—ekstra araçlara gerek kalmayacak.  

## Gereksinimler

- **Java Development Kit (JDK) 8+** – kod, herhangi bir yeni JDK'da çalışır.
- **Aspose.OCR for Java** JAR (Aspose web sitesinden indirin).  
- Geçerli bir **Aspose OCR license** dosyası (`Aspose.OCR.lic`).  
- Urdu metin içeren bir görüntü, ör. `urdu-sample.png`.  

Bu temel öğelere sahip olmak, eksik bağımlılıkları aramadan doğrudan koda atlamanızı sağlar.

## image to text java – Aspose OCR Kurulumu

İlk olarak, Aspose'a bir lisansımız olduğunu söylememiz gerekir. Lisans olmadan kütüphane değerlendirme modunda çalışır ve çıktıya filigran ekler.

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**Neden önemli:** Lisanslama, 5 saniyelik işleme sınırını kaldırır ve 2025‑Q3'te eklenen tam Urdu dil paketinin kilidini açar. Bu adımı atlayırsanız, OCR motoru hâlâ çalışır, ancak sonuçlarda küçük bir “Evaluation” etiketi görürsünüz.

## Metni Çıkarma – OCR Motorunu Başlatma

Şimdi motoru oluşturuyor ve açıkça Urdu ile ilgilendiğimizi belirtiyoruz. `OcrLanguage.URDU` sabiti doğru karakter kümesini ve segmentasyon kurallarını etkinleştirir.

```java
        // Step 2: Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3
```

**İpucu:** Tek bir çalıştırmada birden fazla dili işlemek isterseniz, virgülle ayrılmış bir liste geçirebilirsiniz, ör. `OcrLanguage.ENGLISH, OcrLanguage.URDU`. Motor her bölgeyi otomatik algılayacaktır.

## Load Image OCR – Girdiyi Hazırlama

Aspose, bir veya birden fazla görüntüyü tutabilen bir `OcrInput` nesnesiyle çalışır. Burada yerel bir dosyadan **load image ocr** verisini yüklüyoruz.

```java
        // Step 3: Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");
```

> **Not:** `YOUR_DIRECTORY` ifadesini mutlak yol ya da proje kökünden göreceli bir yol ile değiştirin. Dosya bulunamazsa, Aspose bir `FileNotFoundException` fırlatır. `new File(path).exists()` ile hızlı bir kontrol, çokça hata ayıklama süresinden tasarruf sağlar.

## Metni Tanıma – OCR Sürecini Çalıştırma

Motor yapılandırıldı ve görüntü yüklendiğinde, sonunda `recognize` metodunu çağırıyoruz. Bu metod, çıkarılan dizeyi tutan bir `OcrResult` döndürür.

```java
        // Step 4: Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Arka planda ne oluyor?** OCR motoru görüntüyü satırlara, ardından karakterlere ayırır ve Urdu’ya özgü şekillendirme kurallarını (örneğin birleştirme formları) uygular. Bu yüzden dili erken ayarlamak çok önemlidir; aksi takdirde karışık Latin yer tutucular elde edersiniz.

## Tanınan Urdu Metnini Yazdırma

Son adım sadece sonucu yazdırmaktır. Urdu sağ‑dan‑sola bir yazı sistemi kullandığı için, konsolunuzun Unicode desteklediğinden emin olun (çoğu modern terminal bunu yapar).

```java
        // Step 5: Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

**Beklenen çıktı (örnek):**

```
Urdu text:
یہ ایک مثال کا متن ہے جو تصویر سے نکالا گیا ہے۔
```

Eğer soru işaretleri ya da boş dizeler görürseniz, konsol kodlamanızın UTF‑8 olarak ayarlandığını iki kez kontrol edin (`Windows`'ta `chcp 65001` ya da Java'yı `-Dfile.encoding=UTF-8` ile çalıştırın).

## Tam Çalışan Örnek – Tüm Adımlar Tek Bir Yerde

Aşağıda, tamamen kopyala‑yapıştır‑hazır program bulunmaktadır. Harici referans yok, sadece tek bir Java dosyası.

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3

        // Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");

        // Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

Şöyle çalıştırın:

```bash
javac -cp "aspose-ocr-23.10.jar" UrduDemo.java
java -cp ".:aspose-ocr-23.10.jar" UrduDemo
```

JAR sürümünü (`23.10`) indirdiğiniz sürümle değiştirin. Konsol, PNG dosyanızdan çıkarılan Urdu cümlesini göstermelidir.

## Yaygın Tuzaklar ve Kenar Durumları

| Sorun | Neden Oluşur | Nasıl Düzeltilir |
|-------|----------------|------------|
| **Boş çıktı** | Görüntü çok karanlık veya düşük çözünürlüktedir. | Aspose'a vermeden önce `BufferedImage` kullanarak görüntüyü ön işleme tabi tutun (kontrastı artırın, ikilileştirin). |
| **Bozuk karakterler** | Yanlış dil ayarı (varsayılan İngilizcedir). | `recognize` çağrılmadan önce `ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU);` çağrıldığından emin olun. |
| **Lisans bulunamadı** | Yol hatası ya da dosya eksik. | Mutlak bir yol kullanın veya `.lic` dosyasını sınıf yoluna koyun ve `license.setLicense("Aspose.OCR.lic");` çağırın. |
| **Büyük görüntülerde bellek yetersizliği** | Büyük PNG dosyaları heap'i tüketir. | İçeride küçültmek için `ocrEngine.setMaxImageSize(2000);` çağırın, ya da görüntüyü kendiniz yeniden boyutlandırın. |

## Demoyu Genişletme

- **Batch processing:** Bir klasörü döngüye al, her dosyayı aynı `OcrInput`a ekle ve sonuçları bir CSV'de topla.  
- **Different languages:** `OcrLanguage.URDU` yerine `OcrLanguage.ARABIC` kullan veya birden fazla dili birleştir.  
- **Saving to file:** `Files.write(Paths.get("output.txt"), ocrResult.getText().getBytes(StandardCharsets.UTF_8));` kullan.  

Bu fikirlerin tümü, az önce oluşturduğumuz **java ocr example** üzerine inşa edilmiştir ve çözümü gerçek‑dünya projelerine göre uyarlamanıza olanak tanır.

## Sonuç

Artık Aspose OCR kullanarak bir görüntüden Urdu karakterlerini çıkaran sağlam bir **image to text java** iş akışına sahipsiniz. Eğitim, lisanslamadan dil seçimine, görüntüyü yüklemeye ve sonucu yazdırmaya kadar her adımı kapsadı—böylece kodu herhangi bir Java projesine yapıştırıp çalışmasını izleyebilirsiniz.

Sonra, daha büyük PDF'lerle, farklı yazı sistemleriyle denemeler yapın ya da OCR adımını bir Spring Boot REST uç noktasına entegre etmeyi deneyin. Aynı prensipler—**how to extract text**, **load image o

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}