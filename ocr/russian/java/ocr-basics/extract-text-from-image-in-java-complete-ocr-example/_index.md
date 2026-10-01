---
category: general
date: 2026-01-12
description: Извлекать текст из изображения с помощью Aspose OCR в Java. Узнайте,
  как извлечь текст из изображения счета с примером OCR на Java и получить полученный
  OCR‑текст.
draft: false
keywords:
- extract text from image
- how to extract text
- java ocr example
- process invoice image
- output ocr text
language: ru
og_description: Извлечение текста из изображения с помощью Aspose OCR в Java. Это
  руководство показывает, как извлечь текст из изображения счета, включает пример
  OCR на Java и выводит OCR‑текст.
og_title: Извлечение текста из изображения в Java — полный пример OCR
tags:
- OCR
- Java
- Aspose
title: Извлечение текста из изображения в Java – Полный пример OCR
url: /ru/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения в Java – Полный пример OCR

Когда‑нибудь задумывались, как **извлечь текст из изображения** без потери волос? Возможно, у вас есть стопка отсканированных счетов, и вам нужны цифры быстро. По моему опыту, самый простой способ – позволить специализированной OCR‑библиотеке выполнить всю тяжелую работу. Этот учебник показывает, *как извлечь текст* из типичного изображения счета с помощью Aspose OCR for Java, и даже демонстрирует **java ocr example**, который выводит OCR‑текст, который вы можете передать в вашу downstream‑систему.

Мы пройдем всё, что нужно знать: от настройки проекта, определения области интереса (ROI), сосредоточенной на заголовке и общей сумме, до финального вывода извлечённого текста. К концу вы сможете **обрабатывать изображения счетов** автоматически и получать чистый, поисковый текст.

> **Что вы получите:** готовую к запуску программу на Java, понятные объяснения каждого шага и практические советы по работе с реальными счетами.

---

## Prerequisites

Прежде чем погрузиться в детали, убедитесь, что у вас есть следующее:

- Java Development Kit (JDK) 8 или новее.
- Maven или Gradle для управления зависимостями (приведен пример для Maven).
- Лицензия Aspose OCR for Java (бесплатная trial‑версия подходит для тестов).
- Изображение счета (`invoice.png`), размещённое в известном каталоге.

Если что‑то из этого вам незнакомо, не переживайте — большинство можно просто скачать, а код всё равно скомпилируется с community‑edition.

---

## Step 1: Set Up Your Maven Project

Сначала создайте новый Maven‑проект (или добавьте в существующий). В ваш `pom.xml` добавьте зависимость Aspose OCR:

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest version available -->
    </dependency>
</dependencies>
```

> **Pro tip:** Держите номер версии актуальным; новые релизы часто повышают точность для сложных шрифтов, встречающихся в счетах.

После сохранения файла выполните `mvn clean install`, чтобы загрузить библиотеку в локальный репозиторий.

---

## Step 2: Load the Invoice Image

Теперь, когда библиотека готова, напишем небольшой класс на Java. Первое, что мы делаем — создаём экземпляр `OcrEngine` и указываем ему изображение, которое нужно прочитать.

```java
import com.aspose.ocr.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png"); // <-- replace with your path
```

Почему мы создаём движок **до** загрузки изображения? Движок хранит конфигурацию, такую как язык, DPI и ROI. Установка изображения заранее гарантирует, что эти настройки применятся к именно тому файлу, который вы собираетесь обработать.

---

## Step 3: Define Regions of Interest (ROI)

Счета часто содержат много шума — таблицы, логотипы, мелкий шрифт. Сужая OCR только до заголовка и общей суммы, вы существенно повышаете и скорость, и точность. Aspose позволяет описать эти зоны прямоугольниками.

```java
        // Step 3: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Apply ROI to the engine
        engine.setRegion(region);
```

Координаты задаются в пикселях (`x`, `y`, `width`, `height`). Если размеры ваших счетов различаются, вы можете вычислять эти значения динамически — например, сначала проверив размеры изображения. Это хорошее расширение, если вам нужен **process invoice image**‑решение, работающие пакетно.

---

## Step 4: Run OCR on the Specified Regions

С установленным ROI OCR‑движок может сосредоточить внимание там, где это действительно важно. Метод `recognize()` возвращает `OcrResult`, содержащий извлечённый текст.

```java
        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();
```

За кулисами Aspose выполняет несколько предобработок: бинаризацию, удаление шума и сегментацию символов. Вызывать их вручную не нужно — просто дайте `recognize()` сделать свою работу.

---

## Step 5: Output the Extracted Text

Наконец, выводим текст в консоль. В реальном приложении вы, вероятно, сохраните его в базе данных, передадите в downstream‑аналитический конвейер или даже сгенерируете поисковый PDF.

```java
        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

При запуске программы вы должны увидеть что‑то вроде:

```
ROI text:
Acme Corp.
Invoice #12345
Date: 2025-12-31
Total Amount: $1,250.00
```

Если вывод выглядит искажённым, проверьте координаты прямоугольника или увеличьте разрешение изображения. OCR‑движки любят чёткие сканы с высоким DPI.

---

## Full Working Example

Ниже полное, самодостаточное Java‑файл, который можно скопировать в `src/main/java/RoiExample.java`. Никаких внешних фрагментов не требуется — всё, что нужно, уже здесь.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.region.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png");

        // Step 2: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Step 3: Apply the ROI configuration to the engine
        engine.setRegion(region);

        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

> **Note:** Замените `YOUR_DIRECTORY` на абсолютный путь к вашему изображению счета. Если используете относительный путь, убедитесь, что рабочий каталог совпадает с тем, откуда вы запускаете команду `java`.

---

## Common Questions & Edge Cases

### What if the invoice size changes?

Вы можете вычислять ROI динамически:

```java
int imgWidth = engine.getImage().getWidth();
int imgHeight = engine.getImage().getHeight();

int headerHeight = imgHeight / 10;
int totalHeight = imgHeight / 8;

OcrRegion region = OcrRegion.builder()
        .addRectangle(0, 0, imgWidth, headerHeight)
        .addRectangle(0, imgHeight - totalHeight, imgWidth, totalHeight)
        .build();
```

### How do I handle multiple languages?

Aspose OCR поддерживает языковые пакеты. Просто задайте язык перед вызовом `recognize()`:

```java
engine.setLanguage(OcrLanguage.Spanish); // or OcrLanguage.English, etc.
```

### What if the OCR returns empty strings?

Типичные причины:

- Низкое разрешение изображения (< 300 DPI). Увеличьте масштаб или запросите сканы более высокого качества.
- Слишком тёмный или светлый фон. Примените простой фильтр повышения контраста перед OCR.
- Неправильные координаты ROI, которые полностью пропускают текст.

---

## Tips for Production‑Ready OCR

1. **Batch Processing:** Оберните логику в цикл, проходящий по каталогу файлов счетов. Логируйте каждый результат для аудита.
2. **Error Handling:** Перехватывайте `OcrException`, чтобы gracefully пропускать повреждённые изображения без остановки всей задачи.
3. **Performance:** Переиспользуйте один экземпляр `OcrEngine` для нескольких изображений; создание нового движка для каждого файла добавляет лишние накладные расходы.
4. **Validation:** После извлечения выполните проверку регулярным выражением для общей суммы (`\$\d{1,3}(,\d{3})*(\.\d{2})?`), чтобы убедиться, что число выглядит правдоподобно.

Реализовав эти рекомендации, вы превратите простой **java ocr example** в надёжное, масштабируемое решение для любой компании, которой нужно **process invoice image** файлы каждую ночь.

---

## Conclusion

Мы только что рассмотрели, как **извлечь текст из изображения** в Java с помощью Aspose OCR, сосредоточившись на практическом сценарии обработки счетов. Определив область интереса, запустив OCR‑движок и выведя **output OCR text**, вы получили прочную основу для построения автоматических конвейеров захвата данных.

Следующие шаги? Попробуйте расширить ROI, включив таблицы позиций, поэкспериментируйте с различными языковыми настройками или передайте извлечённые строки в библиотеку генерации PDF для поисковых документов. Возможности безграничны, когда OCR сочетается с современными инструментами Java.

Есть вопросы о **how to extract text** из других типов документов или нужна помощь с настройкой ROI для необычных макетов? Оставляйте комментарий ниже — happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}