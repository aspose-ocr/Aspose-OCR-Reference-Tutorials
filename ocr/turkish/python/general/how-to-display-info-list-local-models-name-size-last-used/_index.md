---
category: general
date: 2026-01-12
description: AsposeAI'dan bilgi görüntülemeyi, yerel modelleri listeleyerek, model
  adını, boyutunu ve son kullanılan zaman damgasını net bir Python örneğiyle öğrenin.
draft: false
keywords:
- how to display info
- list local models
- display model name
- show model size
- show last used
language: tr
og_description: 'AsposeAI''dan bilgi nasıl görüntülenir: yerel modelleri listele,
  model adını, boyutunu ve son kullanım zaman damgasını tam bir Python rehberiyle
  göster.'
og_title: Bilgi Nasıl Görüntülenir – Yerel Modelleri, İsim, Boyut, Son Kullanılanı
  Listele
tags:
- AsposeAI
- Python
- Model Management
title: Bilgi Nasıl Görüntülenir – Yerel Modelleri, İsim, Boyut, Son Kullanılan
url: /tr/python/general/how-to-display-info-list-local-models-name-size-last-used/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bilgi Görüntüleme – Yerel Modelleri, İsim, Boyut, Son Kullanım Tarihini Listeleme

AsposeAI kurulumunuzdan **bilgi nasıl görüntülenir** diye hiç merak ettiniz mi? Günlük dosyalarına ya da arayüze bakmadan? Tek başınıza değilsiniz. Birçok veri‑bilim akışında ilk ihtiyaç, makinenizde hangi modellerin bulunduğunu, adlarını, boyutlarını ve en son ne zaman kullanıldığını hızlıca görebilmektir.

Tam da bunu ele alacağız: **yerel modelleri listeleyen** kısa, uçtan‑uca bir Python kodu, ardından **model adını gösteren**, **model boyutunu gösteren** ve **son kullanım zaman damgasını gösteren** bir örnek. Harici kütüphane yok, gizli sihir yok—sadece zaten sahip olduğunuz AsposeAI istemcisi.

Bu öğreticinin sonunda kodu herhangi bir betiğe ekleyebilir, çalıştırabilir ve yerel önbelleğe alınmış modellerinizin düzenli bir tablosunu anında alabilirsiniz. Ortamları doğrulamak, sağlık panoları oluşturmak ya da sadece diskte neler saklı merak etmek için mükemmeldir.

## Önkoşullar

- Python 3.8 ve üzeri (örnek f‑string kullanıyor, bu yüzden 3.6+ zorunlu)
- `asposeai` paketi kurulu (`pip install asposeai`)
- Çalışan bir AsposeAI lisansı ya da deneme anahtarı (istemci kimlik bilgilerini ortam değişkenlerinden ya da bir yapılandırma dosyasından alır)

Bu maddeleri zaten karşıladıysanız, harika—hadi başlayalım.

## Adım 1: Bilgi Görüntüleme – AsposeAI İstemcisini Başlatma

**Yerel modelleri listeleyebilmek** için AsposeAI çalışma zamanına bağlanan bir istemci nesnesine ihtiyacımız var. Bu adım temeldir; olmadan kod `NameError` verir.

```python
# Step 1: Create an instance of the AsposeAI client
# The client automatically reads credentials from the environment
aspose_ai = AsposeAI()
```

*Neden önemli*: İstemciyi başlatmak, yerel çıkarım motoru ile bir oturum oluşturur, gerekli yerel kütüphaneleri yükler. Ayrıca lisansınızın aktif olduğunu doğrular, modelleri sorgularken ortaya çıkabilecek belirsiz hataları önler.

> **İpucu**: Bunu bir CI sunucusunda çalıştırıyorsanız, `ASPOSEAI_LICENSE` ortam değişkenini ayarlayın; böylece istemci etkileşimli istemler olmadan başlayabilir.

## Adım 2: Yerel Modelleri Listeleme – Mevcut Modelleri Almak

İstemci hazır olduğuna göre, **yerel modelleri listeleyebilir**iz. `list_local()` metodu, `name`, `size_mb` ve `last_used` gibi özellikleri olan nesneler koleksiyonunu döndürür.

```python
# Step 2: Retrieve the list of locally available models
local_models = aspose_ai.list_local()
```

*Arka planda neler oluyor*: `list_local()` AsposeAI’nin model dosyalarını önbelleğe aldığı dizini (`~/.asposeai/models` varsayılan) tarar ve hafif meta veri nesneleri oluşturur. Model ağırlıklarını yüklemediği için hızlıdır; sadece küçük bir JSON manifestosunu okur.

Belirli bir modelin zaten önbellekte olup olmadığını merak ediyorsanız, bu çağrı en hızlı doğrulama yoludur.

## Adım 3: Model Adını Görüntüleme, Model Boyutunu Gösterme ve Son Kullanım Zamanını Görüntüleme

Modeller elinizde olduğuna göre, **bilgi görüntüleme**yi koleksiyon üzerinde döngü kurarak ve her özelliği yazdırarak gerçekleştiriyoruz. Bu adımda **model adını görüntüler**, **model boyutunu gösterir** ve **son kullanım zamanını** tek bir satırda sunarız.

```python
# Step 3: Print each model's name, size (in MB), and last‑used timestamp
print("Available local models:")
print("-" * 50)
for model_info in local_models:
    # Using an f‑string to format the output cleanly
    print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
```

**Beklenen çıktı** (zaman damgalarınız farklı olacaktır):

```
Available local models:
--------------------------------------------------
gpt‑tiny‑en – 120 MB – last used 2025-11-02 14:23:11
bert‑base‑fr – 420 MB – last used 2025-10-18 09:07:45
whisper‑large‑audio – 1580 MB – last used 2025-09-30 22:41:02
```

*Bu şekilde biçimlendirmemizin nedeni*: Tire (`–`) alanları okunabilir kılar, başlık satırı ise konsol çıktısını taramayı kolaylaştırır. Daha sonra makine‑okunur bir format (CSV, JSON) isterseniz, `print` çağrısını `writer.writerow` ya da `json.dump` ile değiştirebilirsiniz.

### Kenar Durumlarını Ele Alma

- **Önbellekte model yok** – `list_local()` boş bir liste döndürür. Döngü sadece başlığı gösterir ve sonlanır. Bir koruma eklemek isteyebilirsiniz:

  ```python
  if not local_models:
      print("No local models found. Use aspose_ai.download(...) to fetch one.")
  ```

- **Eksik özellikler** – Nadiren bir manifest bozulmuş olabilir. `model_info.last_used` erişimi `AttributeError` fırlatabilir. Böyle bir durum bekliyorsanız `try/except` ile `print`i sarmalayın.

- **Büyük model dizinleri** – Yüzlerce modeliniz varsa, çıktıyı sayfalara bölmeyi ya da konsola yazdırmak yerine bir dosyaya kaydetmeyi düşünün.

## Görsel Özet (İsteğe Bağlı)

Eğer hızlı bir görsel ipucu isterseniz, aşağıdaki diyagram istemci başlatmadan son görüntülemeye kadar akışı gösterir.  

![AsposeAI istemcisinden bilgi nasıl görüntülenir gösteren diyagram](/images/how-to-display-info.png "bilgi nasıl görüntülenir diyagramı")

*Alt metin*: **bilgi nasıl görüntülenir** – AsposeAI istemci başlatma, model listeleme ve bilgi gösterme şeması.

## Tam Çalışan Betik

Her şeyi bir araya getirdiğimizde, işte eksiksiz, çalıştırmaya hazır betik:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
How to display info from AsposeAI:
List local models and show each model's name, size, and last‑used timestamp.
"""

from asposeai import AsposeAI

def main():
    # Initialize client
    aspose_ai = AsposeAI()

    # Retrieve local models
    local_models = aspose_ai.list_local()

    # Header
    print("Available local models:")
    print("-" * 50)

    if not local_models:
        print("No local models found. Use aspose_ai.download(...) to fetch one.")
        return

    # Display each model's details
    for model_info in local_models:
        try:
            print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
        except AttributeError:
            # Fallback if any attribute is missing
            print(f"{model_info.name} – info incomplete")

if __name__ == "__main__":
    main()
```

Bunu `list_models.py` olarak kaydedin, çalıştırılabilir yapın (`chmod +x list_models.py`) ve çalıştırın:

```bash
./list_models.py
```

Daha önce gösterilen düzenli listeyi göreceksiniz.

## Sonuç

AsposeAI’den **bilgi nasıl görüntülenir** sorusunu **yerel modelleri listeleyerek**, ardından **model adını göstererek**, **model boyutunu göstererek** ve **son kullanım zaman damgalarını** göstererek yanıtladık. Yaklaşım hafif, sadece standart `asposeai` paketini gerektirir ve herhangi bir otomasyon hattına ya da hata ayıklama oturumuna kolayca eklenebilir.

Bundan sonra şunları yapabilirsiniz:

- Çıktıyı CSV’ye aktararak tablo analizleri yapın (`csv` modülü).
- Zaman damgalarını bir izleme panosuna besleyerek eski modeller için uyarı oluşturun.
- Bu betiği `aspose_ai.download()` ile birleştirerek uzun süredir kullanılmayan modelleri otomatik yenileyin.

Unutmayın, model envanterinizin net görünürlüğü zaman kazandırır, depolama şişkinliğini azaltır ve AI hizmetlerinizin sorunsuz çalışmasını sağlar. Betiği deneyin, biçimlendirmeyi zevkinize göre ayarlayın ve araç kutunuzun vazgeçilmez bir parçası haline getirin.

İyi kodlamalar, modelleriniz hep taze olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}