---
category: general
date: 2026-06-16
description: Учебник по ограничивающим рамкам OCR на Java демонстрирует, как извлекать
  текст из изображения, считывать текст с изображения и получать оценку уверенности
  OCR для JPG‑файлов.
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: ru
og_description: OCR‑ограничивающий прямоугольник в Java позволяет распознавать текст
  из JPG‑файлов, извлекать текст из изображения и просматривать оценки уверенности
  OCR — всё в простом примере кода.
og_title: Ограничивающая рамка OCR в Java – извлечение текста из изображения
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: Ограничивающий прямоугольник OCR в Java – извлечение текста из изображения
url: /ru/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Bounding Box в Java – Извлечение текста из изображения

Задумывались ли вы когда‑нибудь, как получить **ocr bounding box** для каждого фрагмента текста на изображении в Java? В этом руководстве мы покажем, как **extract text from image** файлы, **read text from image**, и даже увидеть **ocr confidence score**, пока вы **recognize text from jpg** файлы. Краткий ответ? Пара строк кода с использованием современной OCR‑библиотеки и небольшое объяснение, почему каждый вызов важен.

Ниже вы найдете полностью готовый к запуску пример, пошаговый разбор и несколько практических советов, которые вы можете сразу скопировать в свой проект. К концу вы сможете вывести что‑то вроде:

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## Что вам понадобится

- **Java 11** или новее (синтаксис ниже использует ключевое слово `var` для краткости, но вы можете опустить его для более старых JDK).  
- OCR‑библиотека, предоставляющая Java API – для этого руководства мы будем использовать **[Tesseract4J](https://github.com/nguyenq/tess4j)**, тонкую оболочку вокруг популярного движка Tesseract.  
- JPEG‑изображение (`.jpg`), содержащее чёткий печатный текст.  
- Ваш любимый IDE (IntelliJ IDEA, Eclipse, VS Code…) – любой подойдет.

Если у вас нет библиотеки, просто добавьте эту Maven‑зависимость:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

А теперь погрузимся.

![OCR bounding box example](ocr-bounding-box.png "OCR bounding box example")

## OCR Bounding Box: Настройка движка

Первое, что нужно сделать, — создать экземпляр OCR‑движка. Представьте это как включение сканера, который позже будет считывать пиксели.

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**Почему это важно:**  
Если не задать `datapath`, Tesseract не будет знать, где находятся языковые пакеты, и вы получите непонятную ошибку «Failed loading language». Вызов `setLanguage` необязателен, если вам нужен только пакет английского языка по умолчанию, но явное указание делает код понятнее для будущих читателей.

## Загрузка изображения для обработки

Далее передайте движку JPEG, который вы хотите проанализировать. Библиотека принимает `File` или `BufferedImage`; для простоты мы будем использовать `File`.

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**Pro tip:**  
Если ваше изображение находится в ресурсах (например, внутри JAR), используйте `getResourceAsStream` и оберните его в `ImageIO.read`. Так руководство будет работать как локально, так и в упакованном приложении.

## Выполнение OCR‑распознавания

Теперь мы действительно просим движок прочитать изображение. Результатом будет строка обычного текста, но нам также нужны **ocr confidence score** и **ocr bounding box** для каждой строки.

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**Почему мы используем `getWords` вместо простого `doOCR`:**  
`doOCR` возвращает сырую строку, но теряет пространственную информацию. Вызывая `getWords` с `RIL_WORD` (или `RIL_TEXTLINE`, если вам нужны коробки уровня строки), мы получаем список объектов `Word`, каждый из которых содержит текст, уверенность и ограничивающий прямоугольник. Это и есть ядро функции **ocr bounding box**.

## Понимание вывода

Запуск приведённого выше фрагмента кода на чистом JPEG даёт вывод, похожий на:

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – распознанные символы.  
- **Confidence** – значение с плавающей точкой от 0 до 1; чем выше, тем более уверенно движок.  
- **Box** – прямоугольник, охватывающий слово в пиксельных координатах (x, y, width, height).  

Теперь вы можете **read text from image** и также точно знать, где каждый фрагмент находится на холсте — идеально для подсветки, обрезки или передачи в последующие NLP‑конвейеры.

## Пограничные случаи и распространённые подводные камни

| Ситуация | На что обратить внимание | Исправление / Обходной путь |
|-----------|-------------------|-------------------|
| Изображение размытое или с низким контрастом | Уровень уверенности резко падает (часто ниже 0.6). | Предобработайте с помощью OpenCV: увеличьте контраст, примените пороговую обработку. |
| JPEG содержит повернутый текст | Ограничивающие рамки выглядят искривленными или отсутствуют. | Используйте `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)`, чтобы Tesseract автоматически определял ориентацию. |
| Большие изображения вызывают OutOfMemoryError | Куча Java заполняется при загрузке больших изображений. | Уменьшите масштаб изображения перед OCR (`ImageIO.read` → `BufferedImage.getScaledInstance`). |
| Нужны рамки уровня строки вместо уровня слова | `RIL_WORD` возвращает рамки для каждого слова. | Переключитесь на `ITesseract.PageIteratorLevel.RIL_TEXTLINE`. |
| Неанглийские символы отображаются как � | Языковые данные не загружены. | Скачайте соответствующий файл `.traineddata` и укажите его папку в `setDatapath`. |

Решение этих проблем на ранних этапах сэкономит вам часы отладки позже.

## Полный рабочий пример (Все шаги в одном файле)

Ниже представлен автономный Java‑класс, который вы можете скопировать‑вставить в папку `src/main/java` и запустить с помощью `mvn exec:java`. Он объединяет всё, о чём мы говорили.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Извлечение текста из изображения Java с Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Извлечение текста из изображений – основы OCR с Aspose.OCR для Java](/ocr/english/java/ocr-basics/)
- [Как выполнять OCR текста изображения с указанием языка, используя Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}