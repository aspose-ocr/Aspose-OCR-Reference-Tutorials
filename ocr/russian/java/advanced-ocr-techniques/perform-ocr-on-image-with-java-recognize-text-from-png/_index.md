---
category: general
date: 2026-03-28
description: Выполните OCR изображения с помощью Aspose OCR в Java. Узнайте, как распознавать
  текст из PNG и улучшать точность OCR с помощью встроенной коррекции орфографии.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- read image text
- improve OCR accuracy
- Aspose OCR Java
- spell correction OCR
language: ru
og_description: Выполните OCR изображения с помощью Aspose OCR для Java. Это руководство
  показывает, как распознавать текст из PNG и улучшать точность OCR за считанные минуты.
og_title: Выполнить OCR изображения с помощью Java – Полное руководство
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Выполнить OCR на изображении с помощью Java – распознать текст из PNG
url: /ru/java/advanced-ocr-techniques/perform-ocr-on-image-with-java-recognize-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполнение OCR на изображении с Java – Распознавание текста из PNG

Когда‑нибудь вам нужно было **выполнять OCR на изображении** файлов, но вы постоянно получали искажённые результаты? Вы не одиноки — шумные сканы, PNG с низким контрастом и странные шрифты могут превратить чистый документ в набор символов.  

В этом руководстве мы пройдёмся по полному, готовому к запуску примеру на Java, который **распознаёт текст из PNG** с использованием Aspose OCR, а также покажем, как **повысить точность OCR** с помощью функции исправления орфографии библиотеки. К концу вы сможете **чтать текст с изображения** надёжно, даже если исходный файл не идеален.

## Что вы узнаете

- Как настроить Aspose OCR для Java в Maven‑проекте.  
- Точные шаги для **выполнения OCR на изображении** данных, от загрузки файла до извлечения чистого текста.  
- Почему включение исправления орфографии может значительно повысить качество вывода.  
- Распространённые подводные камни (отсутствующие файлы, неподдерживаемые форматы) и как с ними справиться.  
- Полный пример кода, готовый к копированию и запуску, который вы можете выполнить сегодня.

### Требования

- Установленный Java 8 или новее.  
- Maven для управления зависимостями (подойдёт любой IDE с поддержкой Maven).  
- PNG‑изображение, содержащее читаемый текст — желательно слегка шумное, чтобы увидеть преимущества исправления орфографии.

> **Совет:** Если у вас нет PNG‑файла под рукой, возьмите любой скриншот документа или фото вывески. Чем «шумнее» выглядит изображение, тем лучше вы оцените повышение точности.

---

## Шаг 1: Добавьте зависимость Aspose OCR

Для начала добавьте библиотеку Aspose OCR в ваш `pom.xml`. Эта одна строка подтягивает последнюю версию (по состоянию на март 2026) и разрешает все транзитивные зависимости.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

> **Почему это важно:** Без библиотеки вы не сможете создать `OcrEngine`, и весь процесс **выполнения OCR на изображении** сломается во время выполнения.

---

## Шаг 2: Инициализируйте OCR‑движок

Создание движка простое, но есть тонкая причина держать инициализацию отдельно от вызова распознавания: это даёт возможность настроить параметры, такие как язык, DPI или, что для нас самое важное, исправление орфографии.

```java
import com.aspose.ocr.*;

public class SpellCorrectExample {

    public static void main(String[] args) {
        try {
            // Step 2: Initialize the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Pro tip: you can set the language here if you need something other than English
            // ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.FRENCH);
```

Обратите внимание на комментарий — установка языка может спасти ситуацию, когда ваш PNG содержит символы не на английском.

---

## Шаг 3: Включите исправление орфографии для **повышения точности OCR**

Aspose OCR поставляется со встроенным модулем исправления орфографии, который работает как лёгкий словарь. Включить его можно одной строкой, однако влияние на конечный результат может быть огромным, особенно для шумных изображений.

```java
            // Step 3: Enable spell correction to improve OCR accuracy on noisy text
            ocrEngine.getRecognitionSettings().setEnableSpellCorrection(true);
```

> **Что если он вам не нужен?** Вы можете просто установить флаг в `false`. Отключение может быть полезным для специализированных текстов, где словарь помечал бы корректные термины как ошибки.

---

## Шаг 4: Загрузите и распознайте PNG

Теперь мы действительно **читаем текст с изображения** из файла. Метод `recognizeImage` принимает строку пути, но вы также можете передать ему `java.io.InputStream`, если получаете изображение из базы данных или из интернета.

```java
            // Step 4: Perform OCR on the input image
            String imagePath = "YOUR_DIRECTORY/noisy-image.png"; // replace with your actual path
            OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

Если файл не найден, Aspose бросает описательное исключение — нет необходимости вручную проверять `File.exists()`. Тем не менее, обёртывание вызова в `try/catch` (как мы делаем) даёт пользователю чистое сообщение об ошибке.

---

## Шаг 5: Выведите исправленный текст

Наконец, выведите результат в консоль. В реальном приложении вы, вероятно, запишете его в базу данных или в downstream‑сервис, но консоль идеально подходит для быстрой демонстрации.

```java
            // Step 5: Output the corrected text
            System.out.println("Corrected text:\\n" + ocrResult.getText());
        } catch (Exception e) {
            System.err.println("Error during OCR processing: " + e.getMessage());
        }
    }
}
```

**Ожидаемый вывод** (при условии, что PNG содержит фразу «Aspose OCR library» с некоторым шумом):

```
Corrected text:
Aspose OCR library
```

Если отключить исправление орфографии, вы можете увидеть что‑то вроде «Asp0se OCR libr@ry» — именно поэтому **повышение точности OCR** имеет значение.

---

## Шаг 6: Проверьте результат — действительно ли он **чтёт текст с изображения**?

Соблазнительно слепо доверять выводу в консоль, но быстрая проверка может сэкономить часы позже. Вот несколько способов проверить извлечённый текст:

1. **Проверка длины** — сравните `ocrResult.getText().length()` с ожидаемым количеством символов.  
2. **Поиск ключевого слова** — используйте `String.contains("Aspose")`, чтобы убедиться, что ключевые термины присутствуют.  
3. **Юнит‑тест** — если вы интегрируете это в большую систему, напишите JUnit‑тест, который проверяет, что вывод соответствует известному правильному значению.

```java
// Example sanity check
if (ocrResult.getText().contains("Aspose")) {
    System.out.println("✅ Text successfully read from image.");
} else {
    System.out.println("⚠️ Unexpected OCR result – consider tweaking settings.");
}
```

---

## Распространённые граничные случаи и как с ними справиться

| Ситуация | Почему происходит | Быстрое решение |
|-----------|----------------|-----------|
| **Файл не найден** | Неправильный путь или отсутствие прав | Проверьте `imagePath` и используйте `Files.isReadable(Paths.get(imagePath))` перед вызовом `recognizeImage`. |
| **Неподдерживаемый формат** | Aspose OCR поддерживает PNG, JPEG, BMP, TIFF и т.д. | Сначала преобразуйте изображение в PNG (например, с помощью ImageIO) или используйте `ocrEngine.recognizeImage(InputStream)`. |
| **Очень низкое DPI** | OCR‑движкам требуется минимум ~300 DPI для приемлемой точности | Увеличьте масштаб изображения с помощью `BufferedImage` и `Graphics2D` перед передачей его в движок. |
| **Специфический жаргон** | Исправление орфографии может заменить корректные термины словами из словаря | Отключите исправление орфографии (`setEnableSpellCorrection(false)`) или предоставьте собственный словарь через `ocrEngine.getRecognitionSettings().setCustomDictionary(...)`. |

---

## Полный рабочий пример (готовый к копированию)

Ниже приведён весь исходный файл, готовый к компиляции и запуску. Замените `YOUR_DIRECTORY/noisy-image.png` на реальный путь к вашему тестовому изображению.

```java
import com.aspose.ocr.*;

public class SpellCorrectExample {
    public static void main(String[] args) {
        try {
            // Initialize the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Enable spell correction to improve OCR accuracy on noisy text
            ocrEngine.getRecognitionSettings().setEnableSpellCorrection(true);

            // Path to the PNG you want to process
            String imagePath = "YOUR_DIRECTORY/noisy-image.png";

            // Perform OCR on the input image
            OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

            // Output the corrected text
            System.out.println("Corrected text:\\n" + ocrResult.getText());

            // Simple verification that we actually read image text
            if (ocrResult.getText().toLowerCase().contains("aspose")) {
                System.out.println("✅ OCR succeeded – key term found.");
            } else {
                System.out.println("⚠️ OCR may need tweaking – key term missing.");
            }
        } catch (Exception e) {
            System.err.println("Error during OCR processing: " + e.getMessage());
        }
    }
}
```

Запустите его с помощью:

```bash
mvn compile exec:java -Dexec.mainClass=SpellCorrectExample
```

Вы должны увидеть напечатанный **исправленный текст**, подтверждающий, что вы успешно **выполнили OCR на изображении**.

---

## Визуальное резюме

![Пример выполнения OCR на изображении](/images/ocr-example.png){alt="выполнение OCR на изображении – до и после исправления орфографии"}

Скриншот иллюстрирует шумный PNG слева и чистый, исправленный орфографией вывод справа.

---

## Заключение

Мы только что прошли полный сквозной процесс решения, как **выполнять OCR на изображении** файлов с использованием Aspose OCR для Java. Включив встроенный флаг исправления орфографии, вы можете **повысить 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}