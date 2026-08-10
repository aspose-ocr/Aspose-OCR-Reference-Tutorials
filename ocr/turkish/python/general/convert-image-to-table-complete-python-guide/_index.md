---
category: general
date: 2026-03-26
description: Python ile OCR ve AI kullanarak görüntüyü tabloya dönüştürün. Görüntüden
  tablo çıkarmayı, OCR doğruluğunu artırmayı ve hızlı bir şekilde yapılandırılmış
  sonuçlar elde etmeyi öğrenin.
draft: false
keywords:
- convert image to table
- extract table from image
- extract tabular data image
- enhance OCR accuracy
language: tr
og_description: Python'da görüntüyü tabloya dönüştürün. Bu rehber, görüntüden tablo
  çıkarmayı, OCR doğruluğunu artırmayı ve yapılandırılmış verilerle çalışmayı gösterir.
og_title: Görüntüyü tabloya dönüştür – Adım adım Python öğreticisi
tags:
- OCR
- Python
- AI post‑processing
title: Görüntüyü tabloya dönüştür – Tam Python Rehberi
url: /tr/python/general/convert-image-to-table-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüyü tabloya dönüştür – Tam Python Rehberi

Hiç **görüntüyü tabloya dönüştür**mek isterken bulanık bir ekran görüntüsüne bakıp takıldıysanız? Tek başınıza değilsiniz. Veri odaklı birçok projede, sayısal verileri bir veri çerçevesine (dataframe) en hızlı şekilde aktarmanın yolu, basılı bir tablonun fotoğrafını çekmek ve bir betiğin işi halletmesini sağlamaktır. İyi haber? Modern bir OCR motoru ve küçük bir AI post‑işlemcisiyle, neredeyse her görüntüden temiz, yapılandırılmış bir tablo çıkarabilirsiniz.

Bu öğreticide, **tablo içeren bir görüntüyü çıkaran gerçek‑dünya bir örnek** üzerinden ilerleyecek, veriyi temizleyecek ve her satırı düz metin olarak yazdıracağız. Sonunda **OCR doğruluğunu artırma**, yaygın tuzakları ele alma ve kodu kendi akışlarınıza uyarlama konularını anlayacaksınız. Sihir yok, sadece Python, birkaç kütüphane ve biraz mantık.

> **İhtiyacınız olanlar**  
> * Python 3.9+  
> * `OutputFormat.Structured` destekleyen bir OCR kütüphanesi (ör. `myocr`)  
> * İsteğe bağlı bir AI post‑işlemci (hafif bir transformer veya kural‑tabanlı bir fonksiyon olabilir)  
> * Basit bir tablo içeren örnek görüntü dosyası (`table.png`)

---

## Adım 1: Görüntüyü tabloya dönüştür – Yapılandırılmış çıktı ile görüntüyü tanıma

İlk olarak resmi OCR motoruna veriyoruz ve **yapılandırılmış** bir sonuç istiyoruz. Yapılandırılmış çıktı, motorun satır, sütun ve hücre sınırlarını düz bir metin yerine tahmin ettiği anlamına gelir.

```python
import myocr as ocr          # Hypothetical OCR package
import myengine as engine    # Wrapper around the OCR engine
import myai as ai            # Simple AI post‑processor

def recognize_image(path: str):
    """
    Sends the image to the OCR engine and asks for a tabular
    (structured) representation.
    """
    # Step 1: Recognize the image and request a structured (tabular) result
    structured_result = engine.recognize_image(
        path,
        output_format=ocr.OutputFormat.Structured
    )
    return structured_result
```

**Neden önemli:**  
OCR’dan düz metin istediğinizde, satır ya da sütun kavramı olmadan karışık karakterler elde edersiniz. Yapılandırılmış bir format talep ederek, motor satır tespiti, sütun hizalama ve temel hücre birleştirmesini sizin yerinize yapar. Bu, daha sonra yapmanız gereken manuel ayrıştırma işini büyük ölçüde azaltır.

> **İpucu:** Görüntünün iyi kontrastlı ve minimum eğimli olduğundan emin olun. 300 dpi tarama genellikle en iyi sonuçları verir.

---

## Adım 2: OCR doğruluğunu artır – Ham yapıyı post‑işlemle

OCR mükemmel değildir—özellikle kaynak görüntü zayıf çizgilere ya da alışılmadık yazı tiplerine sahipse. İşte burada hafif bir AI (veya kural‑tabanlı bir betik) çıktıyı temizleyebilir, yaygın hataları düzeltebilir ve eksik bağlamı ekleyebilir.

```python
def enhance_structure(structured_result):
    """
    Runs a post‑processor that fixes typical OCR errors
    (e.g., 'O' vs '0', merged cells) and adds semantic context.
    """
    # Step 2: Enhance the raw OCR structure with AI (adds context, corrects errors)
    enhanced_structure = ai.run_postprocessor(structured_result)
    return enhanced_structure
```

**Neden önemli:**  
Ham OCR tablosu başlığı “Q1 2022” olarak tanımlarken “1”i “l” olarak okuyabilir. AI katmanı bu kalıpları küçük bir eğitim setinden öğrenerek daha temiz bir tablo üretir. Basit bir sezgi (ör. yalnızca rakamlarla çevrili izole “l” karakterini “1” ile değiştirme) **OCR doğruluğunu artırma** konusunda büyük bir fark yaratabilir.

> **Yaygın kenar durumu:** Tablo birleşik hücreler içeriyorsa, OCR içeriği sütunlar arasında çoğaltabilir. Post‑işlemci aynı komşu hücreleri tespit edip birleştirmelidir.

---

## Adım 3: Tablo içeren görüntüyü çıkar – Satırları dolaş ve hücre metnini göster

Artık düzenli bir yapımız olduğuna göre, veriyi çıkarmak çok basit. İlk tespit edilen tabloyu dolaşacağız ve her satırı hücre değerlerinin bir listesi olarak yazdıracağız.

```python
def print_table(enhanced_structure):
    """
    Prints each row of the first detected table.
    """
    # Step 3: Iterate over the rows of the first detected table and display cell text
    for row in enhanced_structure.tables[0].rows:
        print([cell.text for cell in row.cells])

if __name__ == "__main__":
    # Path to your image file
    image_path = "YOUR_DIRECTORY/table.png"

    # Run the pipeline
    raw = recognize_image(image_path)
    cleaned = enhance_structure(raw)
    print_table(cleaned)
```

**Gördükleriniz:**  
`table.png` basit bir 3 × 2 ızgara içeriyorsa, çıktı şu şekilde görünebilir:

```
['Product', 'Price']
['Apple', '$1.20']
['Banana', '$0.80']
```

Eğer OCR bir başlığı kaçırdıysa, AI post‑işlemci çevresel bağlamdan yola çıkarak muhtemelen ekleyecek, böylece son tablo pandas ya da herhangi bir sonraki analiz için hazır olur.

> **Dikkat:** Tablonun sonunda boş satırlar olabilir. Bazı OCR motorları boşlukla karşılaştıklarında boş bir satır ekler. `if any(cell.text for cell in row.cells):` gibi bir kontrol bu satırları filtreleyebilir.

---

## Bonus: Daha ileri – Tabloyu CSV’ye ya da DataFrame’e kaydet

Çoğu gerçek‑dünya iş akışı veriyi bir CSV dosyası ya da pandas DataFrame olarak ister. İşte yazdırılan satırları Python sürecinden çıkmadan bir CSV’ye dönüştüren küçük bir snippet.

```python
import csv
import pandas as pd

def save_to_csv(enhanced_structure, output_path="output.csv"):
    rows = [
        [cell.text for cell in row.cells]
        for row in enhanced_structure.tables[0].rows
        if any(cell.text for cell in row.cells)  # Skip empty rows
    ]
    # Write CSV
    with open(output_path, "w", newline="", encoding="utf-8") as f:
        writer = csv.writer(f)
        writer.writerows(rows)

    # Also return a DataFrame for immediate use
    return pd.DataFrame(rows[1:], columns=rows[0])  # Assume first row is header

# Example usage:
df = save_to_csv(cleaned, "my_table.csv")
print(df.head())
```

Artık kullanıma hazır bir DataFrame’iniz var; analiz, görselleştirme ya da bir makine‑öğrenme modeline besleme için mükemmel.

---

## Sıkça Sorulan Sorular (SSS)

**S: Tarama yapılmış tablolar içeren PDF’lerle çalışır mı?**  
C: Kesinlikle—her PDF sayfasını bir görüntüye (ör. `pdf2image` kullanarak) dönüştürün ve elde edilen PNG’leri aynı boru hattına besleyin.

**S: Tablomda birleştirilmiş başlık hücreleri var; AI bunu düzeltebilir mi?**  
C: İyi eğitilmiş bir post‑işlemci hücre kapsamlarını kontrol ederek birleşik hücreleri tespit edebilir. Kural‑tabanlı bir yaklaşım kullanıyorsanız, yan yana aynı metni içeren hücreleri bulup birleştirin.

**S: OCR birden fazla tablo döndürürse ne yapmalıyım?**  
C: `enhanced_structure.tables` bir listedir. Üzerinde dönebilir ya da en çok satır/sütun içeren tabloyu seçebilirsiniz—beklentilerinize en uygun olanı.

**S: AI post‑işlemciyi basit bir regex temizliğiyle değiştirebilir miyim?**  
C: Evet. Birçok projede birkaç regex değişimi (ör. “O” → “0” düzeltmesi) yeterli olur. Önemli olan OCR’dan sonra *bir şey* çalıştırarak **OCR doğruluğunu artırma** sağlamaktır.

---

## Sonuç

Python’da **görüntüyü tabloya dönüştür**meyi, ham OCR tanımasından AI‑geliştirilmiş, kullanıma hazır bir veri yapısına kadar gösterdik. Tanıma, geliştirme, çıkarma adımlarından oluşan üç aşamalı boru hattı, **görüntüden tablo çıkarma**nin temel zorluklarını kapsar ve **OCR doğruluğunu artırma** için pratik yollar sunar.

Herhangi bir elektronik tablo ekran görüntüsü alın, betiği ona yönlendirin ve saniyeler içinde bir CSV ya da DataFrame elde edin. Bundan sonra daha ileri teknikler keşfedebilirsiniz: çok sayfalı PDF’ler, el yazısı tablolar ya da gerçek‑zaman kamera akışları.

Bir sonraki meydan okumaya hazır mısınız? Boru hattını canlı video kareleriyle besleyin ya da eksik sütun adlarını tahmin edebilen dil‑modeli‑tabanlı post‑işlemciler deneyin. Ufuklar geniş, ve artık üzerine inşa edebileceğiniz sağlam bir temele sahipsiniz.

İyi kodlamalar! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}