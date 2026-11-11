---
category: general
date: 2026-09-10
description: выполнить OCR на изображении с помощью Aspose OCR Java. Узнайте, как
  распознавать текст из JPEG, извлекать текст из изображения и эффективно преобразовывать
  изображение в текст.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- recognize text from JPEG
- extract text from image
- convert image to text
- load image for OCR
language: ru
lastmod: 2026-09-10
og_description: Выполните OCR изображения с помощью Aspose OCR Java. Этот учебник
  показывает, как распознать текст из JPEG, извлечь текст из изображения и преобразовать
  изображение в текст за несколько строк кода.
og_image_alt: Screenshot of Java code that performs OCR on an image using Aspose OCR
og_title: Выполнить OCR изображения с помощью Aspose OCR – руководство по Java
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  headline: How to perform OCR on image with Aspose OCR in Java
  type: TechArticle
- description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  name: How to perform OCR on image with Aspose OCR in Java
  steps:
  - name: Prerequisites
    text: '* Java Development Kit (JDK) 8 or later. * Maven or Gradle to manage dependencies
      (the example uses Maven). * A valid Aspose OCR for Java license (or a temporary
      evaluation key). * An image file named `sample.jpg` placed in a known directory.'
  - name: Load image for OCR
    text: '```java // Step 1: Load the image you want to process String imagePath
      = "YOUR_DIRECTORY/sample.jpg"; ImageStream imageStream = ImageStream.fromFile(imagePath);
      ```'
  - name: Create and configure the OCR engine
    text: '```java // Step 2: Create an OCR engine instance OcrEngine engine = new
      OcrEngine();'
  - name: Recognize text from JPEG
    text: '```java // Step 3: Attach the image to the engine engine.setImage(imageStream);'
  - name: Extract text from image and output
    text: '```java // Step 5: Output the recognized text System.out.println("=== Recognized
      Text ==="); System.out.println(result.getText()); ```'
  - name: Expected output
    text: 'Assuming `sample.jpg` contains the text “Hello World”, the console will
      display:'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: Как выполнить OCR изображения с помощью Aspose OCR в Java
url: /ru/java/ocr-operations/how-to-perform-ocr-on-image-with-aspose-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR на изображении с помощью Aspose OCR в Java

Если вам нужно **выполнять OCR на изображении** файлов в Java‑приложении, это руководство предоставляет полное, готовое к запуску решение. Вы увидите, как **распознавать текст из JPEG** файлов, **извлекать текст из изображения** и **преобразовывать изображение в текст** с помощью современного API Aspose OCR.

Учебник пошагово проходит каждый необходимый этап — от загрузки изображения до вывода распознанного текста — чтобы вы могли интегрировать функциональность OCR без поиска дополнительных ресурсов. Ниже не требуется никаких внешних инструментов, кроме библиотеки Aspose OCR for Java.

## Что вы достигнете

* **Загрузить изображение для OCR** напрямую из файловой системы.  
* Включить предобработку Aspose OCR (например, удаление шума) для повышения точности.  
* **Распознавать текст из JPEG** и других растровых форматов.  
* **Извлекать текст из изображения** и выводить его в консоль.  
* Понять, как **преобразовать изображение в текст** в готовом к производству примере кода.

### Предварительные требования

* Java Development Kit (JDK) 8 или новее.  
* Maven или Gradle для управления зависимостями (пример использует Maven).  
* Действующая лицензия Aspose OCR for Java (или временный оценочный ключ).  
* Файл изображения с именем `sample.jpg`, размещённый в известном каталоге.

> **Pro tip:** Используйте JPEG высокого разрешения (300 dpi и выше) для лучшей точности распознавания.  

## Шаг 1: Добавьте Aspose OCR в ваш проект

Если вы управляете зависимостями с помощью Maven, вставьте следующий фрагмент в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version>
</dependency>
```

Для Gradle добавьте:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Эти координаты подтягивают последнюю стабильную библиотеку Aspose OCR, которая включает функции предобработки, используемые позже.

## Выполнение OCR на изображении – пошагово

Следующие разделы разбивают полную программу. Каждый блок — самодостаточная часть, которую можно скопировать, вставить и запустить.

### Загрузка изображения для OCR

```java
// Step 1: Load the image you want to process
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ImageStream imageStream = ImageStream.fromFile(imagePath);
```

*Почему это важно:*  
`ImageStream.fromFile` считывает необработанные байты JPEG и подготавливает их для OCR‑движка. Метод работает с любым растровым форматом, поддерживаемым Aspose OCR, поэтому вы можете заменить JPEG на PNG или BMP без изменения кода.

### Создание и настройка OCR‑движка

```java
// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();

// Enable preprocessing to improve accuracy (e.g., denoising)
engine.getPreprocessing().setDenoise(true);
```

*Почему это важно:*  
Создание экземпляра `OcrEngine` выделяет основной движок распознавания. Включение флага **denoise** удаляет визуальный шум, который часто мешает обнаружению символов, особенно в отсканированных JPEG‑файлах.

### Распознавание текста из JPEG

```java
// Step 3: Attach the image to the engine
engine.setImage(imageStream);

// Step 4: Perform OCR recognition
OcrResult result = engine.recognize();
```

*Почему это важно:*  
`engine.setImage` привязывает данные изображения к OCR‑конвейеру. `engine.recognize()` запускает полный процесс распознавания, возвращая `OcrResult`, содержащий извлечённый текст и метрики уверенности.

### Извлечение текста из изображения и вывод

```java
// Step 5: Output the recognized text
System.out.println("=== Recognized Text ===");
System.out.println(result.getText());
```

*Почему это важно:*  
`result.getText()` предоставляет простое текстовое представление содержимого изображения. Вывод его в консоль демонстрирует, что **преобразовать изображение в текст** удалось, и вы можете перенаправить эту строку в файлы, базы данных или последующие сервисы.

## Полный, исполняемый пример

Ниже представлен полный Java‑класс, включающий все шаги. Замените `YOUR_DIRECTORY` абсолютным путём к вашему JPEG‑файлу.

```java
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the image for OCR
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ImageStream imageStream = ImageStream.fromFile(imagePath);

        // Create and configure the OCR engine
        OcrEngine engine = new OcrEngine();
        engine.getPreprocessing().setDenoise(true); // improve accuracy

        // Attach the image and run recognition
        engine.setImage(imageStream);
        OcrResult result = engine.recognize();

        // Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### Ожидаемый вывод

При условии, что `sample.jpg` содержит текст «Hello World», консоль отобразит:

```
=== Recognized Text ===
Hello World
```

Если изображение содержит несколько строк, каждая строка появится в отдельной строке вывода.

## Распространённые варианты и граничные случаи

| Ситуация                                 | Рекомендуемая настройка |
|------------------------------------------|--------------------------|
| **JPEG низкого разрешения** (≤150 dpi)   | Увеличьте `engine.getPreprocessing().setUpsample(true);`, чтобы Aspose масштабировал изображение перед распознаванием. |
| **Цветной фон** (например, отсканированные формы) | Включите `engine.getPreprocessing().setBinarize(true);` для преобразования изображения в чёрно‑белое. |
| **Нелатинский скрипт** (например, кириллица) | Установите язык: `engine.getLanguage().setLanguage(OcrLanguage.RUSSIAN);`. |
| **Обработка больших пакетов**            | Переиспользуйте один экземпляр `OcrEngine` для нескольких изображений, чтобы снизить накладные расходы на запуск. |
| **Требуются оценки уверенности**         | Обратитесь к `result.getConfidence()` для получения значений уверенности по каждому символу. |

Эти настройки показывают, как вы можете **загрузить изображение для OCR** в разных условиях, оставаясь при этом надёжным в **выполнении OCR на изображении**.

## Соображения по производительности

* **Memory usage:** Каждый `ImageStream` хранит всё изображение в памяти. Для очень больших файлов (например, >10 MB) рассмотрите потоковую передачу изображения частями с помощью `ImageStream.fromByteArray`.  
* **Thread safety:** `OcrEngine` *не* является потокобезопасным. Создавайте отдельный экземпляр на каждый поток, если планируете параллельную обработку OCR‑задач.  
* **License mode:** Оценочный режим ограничивает количество страниц, обрабатываемых за одну сессию. Разверните лицензированную версию для производственных нагрузок.

## Заключение

Теперь вы знаете, как **выполнять OCR на изображении** файлов в Java с использованием Aspose OCR. Учебник охватил загрузку изображения, включение предобработки, распознавание текста из JPEG, извлечение текста и преобразование изображения в текст — все в одном лаконичном приложении.  

Отсюда вы можете изучать связанные темы, такие как **распознавать текст из JPEG** пакетно, интегрировать вывод в поисковый индекс или сочетать OCR с обработкой естественного языка для более умных конвейеров документов. Экспериментируйте с параметрами предобработки, чтобы достичь наилучшей точности для ваших конкретных источников изображений.

--- 

*Изображение, иллюстрирующее вывод кода*  
![perform OCR on image Java example](image-placeholder.png){alt="perform OCR on image using Aspose OCR Java"}

## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Preprocess Image OCR in Java with Aspose OCR – Boost Accuracy & Extract Text](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}