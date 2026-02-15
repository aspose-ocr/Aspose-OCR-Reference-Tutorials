---
category: general
date: 2026-02-14
description: Извлеките текст из изображения с помощью Aspose OCR. Узнайте, как загрузить
  изображение для OCR, считать текст из прямоугольника и пройти этот учебник Aspose
  OCR за несколько минут.
draft: false
keywords:
- extract text from image
- load image for ocr
- read text from rectangle
- aspose ocr tutorial
language: ru
og_description: Извлекайте текст из изображения мгновенно. Это руководство показывает,
  как загрузить изображение для OCR, считать текст из прямоугольника и завершить учебник
  по Aspose OCR.
og_title: Извлечение текста из изображения с помощью Aspose OCR – Быстрое руководство
tags:
- Aspose
- OCR
- Java
title: Извлечение текста из изображения с помощью Aspose OCR – пошаговый демонстрационный
  пример
url: /ru/java/ocr-operations/extract-text-from-image-with-aspose-ocr-step-by-step-demo/
---

remain unchanged.

Now produce final markdown.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения с помощью Aspose OCR – пошаговая демонстрация

Когда‑нибудь вам нужно было **извлечь текст из изображения**, но вы не знали, с чего начать? Вы не одиноки — многие разработчики сталкиваются с этим, когда впервые берутся за сканирование чеков или проверку удостоверений личности. Хорошая новость? С Aspose OCR вы можете загрузить изображение, определить точный регион, где находится текст, и извлечь символы всего в несколько строк.

В этом **aspose ocr tutorial** мы пройдем всё, что вам нужно: загрузку изображения для OCR, установку прямоугольника, указывающего движку, где искать, и, наконец, чтение извлечённого текста. К концу у вас будет исполняемая Java‑программа, выводящая текст ROI в консоль — без загадок, только чёткое рабочее решение.

## Что понадобится

Прежде чем погрузиться, убедитесь, что у вас есть всё необходимое:

| Требования | Почему это важно |
|--------------|----------------|
| **Java JDK 8+** | Aspose OCR поставляется как Java‑библиотека; любой современный JDK подойдёт. |
| **Aspose.OCR for Java** (скачайте с сайта Aspose или добавьте через Maven) | Предоставляет `OcrEngine`, `ImageStream` и связанные классы. |
| **An image file** (например, `receipt.jpg`), содержащий печатаемый текст | Мы укажем движку прямоугольник внутри этого файла. |
| **IDE or editor** (IntelliJ, Eclipse, VS Code…) | Помогает быстро компилировать и запускать пример. |

Если вы используете Maven, добавьте эту зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check Aspose for the latest version -->
</dependency>
```

> **Совет:** Номер версии выше актуален на февраль 2026 года. Обновление до последней версии гарантирует получение исправлений ошибок и улучшений производительности.

## Шаг 1 – Инициализация OCR‑движка

Первое, что нужно: создать экземпляр `OcrEngine`. Считайте его мозгом, который будет анализировать пиксели.

```java
// Step 1: Create the OCR engine object
OcrEngine ocrEngine = new OcrEngine();
```

Зачем создавать его так? Aspose разделяет движок (который хранит конфигурацию) и данные изображения, предоставляя гибкость повторного использования одного и того же движка для нескольких изображений, если это необходимо.

## Шаг 2 – Загрузка изображения для OCR

Теперь мы действительно **загружаем изображение для OCR**. Вспомогательная функция `ImageStream.fromFile` считывает файл в поток, понятный Aspose.

```java
// Step 2: Load the target image (replace with your own path)
String imagePath = "YOUR_DIRECTORY/receipt.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

Если файл не найден, движок бросает исключение, поэтому в продакшн‑коде стоит обернуть это в блок try‑catch. Для этой демонстрации мы позволяем исключению подняться — пример остаётся лаконичным.

## Шаг 3 – Определение прямоугольника (Чтение текста из прямоугольника)

Здесь проявляется часть **read text from rectangle**. Вы указываете движку точно, где искать, что ускоряет обработку и уменьшает количество ложных срабатываний.

```java
// Step 3: Create a rectangle that covers the area with the receipt total
// Parameters: x, y, width, height (all in pixels)
Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);
```

> **Почему прямоугольник?**  
> Большинство документов имеют предсказуемую структуру — например, в чеке сумма всегда находится в нижней части. Сфокусировавшись на этом участке, OCR‑движок игнорирует нерелевантную графику и повышает точность.

**Особый случай:** Если прямоугольник выходит за границы изображения, Aspose тихо обрезает его, но вы потеряете данные. Быстрая проверка может предотвратить это:

```java
if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
    regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
    throw new IllegalArgumentException("ROI exceeds image dimensions.");
}
```

## Шаг 4 – Обработка изображения

Когда всё готово, мы просим движок выполнить своё волшебство.

```java
// Step 4: Run OCR on the defined ROI
OcrResult ocrResult = ocrEngine.process();
```

Вызов `process()` возвращает объект `OcrResult`, содержащий извлечённый текст, оценки уверенности и даже ограничивающие рамки для каждого слова, если они понадобятся позже.

## Шаг 5 – Вывод извлечённого текста

Наконец, выведите результат. В реальном приложении вы можете сохранить его в базе данных или передать другому сервису, но для этого урока достаточно вывода в консоль.

```java
// Step 5: Display the recognized text
System.out.println("ROI text:");
System.out.println(ocrResult.getText());
```

**Ожидаемый вывод** (при условии, что прямоугольник захватил общую сумму в чеке):

```
ROI text:
$12.34
```

Если ROI пустой или изображение размыто, вы увидите пустую строку или искажённые символы. Отрегулируйте прямоугольник, улучшите качество изображения или включите параметры предобработки Aspose (например, `setAutoSkewCorrection(true)`).

## Полный рабочий пример

Ниже представлен полный готовый к запуску код. Скопируйте его в файл с именем `RoiDemo.java`, поправьте путь к изображению и выполните `javac RoiDemo.java && java RoiDemo`.

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

/**
 * Demo: Extract text from a specific rectangle (ROI) in an image using Aspose OCR.
 * Adjust the rectangle coordinates to match the area you want to read.
 */
public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.jpg"));

        // Step 3: Define the region of interest where text is expected
        // (x, y, width, height) in pixels
        Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
        ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);

        // Optional sanity check – ensures ROI fits inside the image
        if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
            regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
            throw new IllegalArgumentException("ROI exceeds image dimensions.");
        }

        // Step 4: Perform OCR on the defined ROI
        OcrResult ocrResult = ocrEngine.process();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

> **Проверка результата:** После выполнения сравните вывод консоли с реальным текстом внутри прямоугольника. Если они совпадают, вы успешно **extract text from image** с помощью Aspose OCR.

## Часто задаваемые вопросы и советы

### Что если нужно обработать несколько ROI в одном изображении?

Создайте новый `Rectangle` для каждой области, снова вызовите `setRegionOfInterest` и повторно запустите `process()`. Движок переиспользует те же данные изображения, поэтому производительность остаётся высокой.

### Как Aspose обрабатывает разные языки или шрифты?

Вы можете переключить языковую модель через `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.English)`. Для нелатинских скриптов загрузите соответствующий языковой пакет (доступен на странице загрузки Aspose).

### Поддерживает ли библиотека ввод PDF?

Да — Aspose OCR может принимать PDF‑потоки напрямую. Просто замените `ImageStream.fromFile` на `ImageStream.fromPdfFile("doc.pdf")` и при необходимости укажите номер страницы.

### Как улучшить точность при сканах низкого качества?

Включите предобработку:

```java
ocrEngine.getEngineOptions().setAutoSkewCorrection(true);
ocrEngine.getEngineOptions().setBinarizationMethod(BinarizationMethod.Otsu);
```

## Заключение

Мы только что прошли полный **aspose ocr tutorial**, демонстрирующий, как **extract text from image**, **load image for OCR** и **read text from rectangle** с помощью Java. Ключевые шаги: инициализация движка, загрузка изображения, определение региона интереса, обработка и, наконец, вывод результата.

Отсюда вы можете исследовать:

* **Batch processing** – перебрать папку с чеками и сохранить каждую сумму в базе данных.  
* **Dynamic ROI detection** – использовать библиотеки обработки изображений (OpenCV) для автоматического обнаружения текстовых блоков.  
* **Post‑processing** – применять регулярные выражения или нечёткое сопоставление для очистки артефактов OCR.

Попробуйте эти идеи, подкорректируйте прямоугольник под свои документы, и у вас будет надёжный конвейер извлечения текста в кратчайшие сроки. Счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}