---
date: 2026-05-24
description: Узнайте, как использовать OCR с Aspose.OCR для Java, извлекать текст
  из изображений, задавать разрешённые символы и применять временную лицензию за считанные
  минуты.
keywords:
- how to use OCR
- extract text from images
- how to apply license
- how to set characters
linktitle: Указание разрешённых символов в Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-05-24'
  description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  headline: How to Use OCR – Extract Text from Images with Aspose.OCR
  type: TechArticle
- description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  name: How to Use OCR – Extract Text from Images with Aspose.OCR
  steps:
  - name: Set Your Document Directory
    text: Choose a folder where OCR results and temporary files will be stored. This
      path is later used to locate the image you want to process.
  - name: Specify the Image Path
    text: Provide the full file system path or a class‑path resource location that
      points to the image you wish to analyse.
  - name: Create an Aspose.OCR Instance
    text: '`AsposeOCR` is the core engine that performs optical character recognition.
      Instantiate it with either a temporary or permanent license string.'
  - name: Perform OCR Recognition
    text: '`RecognizeLine` extracts a single line of text from the supplied image
      and returns it as a plain Java `String`. You can call this method repeatedly
      for multi‑line documents. > **Pro tip:** If you need to restrict the output
      to digits only (e.g., for invoice numbers), call `setAllowedCharacters("0123'
  type: HowTo
- questions:
  - answer: Visit the [temporary license page](https://purchase.aspose.com/temporary-license/)
      to request a trial key that removes evaluation watermarks.
    question: How can I obtain a temporary license for Aspose.OCR?
  - answer: Join the community at the [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16)
      for help and discussions.
    question: Where can I find support for Aspose.OCR?
  - answer: Yes, use the `setAllowedCharacters` API to define a custom whitelist of
      characters. This is ideal for numeric‑only fields.
    question: Can I specify allowed characters in Aspose.OCR?
  - answer: Absolutely—Aspose.OCR is regularly updated to stay compatible with the
      newest Java releases.
    question: Is Aspose.OCR compatible with the latest JDK versions?
  - answer: The library also supports block, paragraph, and full‑page recognition,
      language packs, and advanced image preprocessing.
    question: Are there additional OCR features beyond line recognition?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Как использовать OCR – извлечение текста из изображений с помощью Aspose.OCR
url: /ru/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR – извлечение текста из изображений с помощью Aspose.OCR

В современных Java‑приложениях вопрос **how to use OCR** часто задаётся, особенно когда необходимо преобразовать отсканированные счета, чеки или печатные формы в поисковый текст. Этот учебник проведёт вас через полный пример **Aspose.OCR for Java**: извлечение текста из изображений, ограничение вывода пользовательским набором символов и применение временной лицензии для быстрой оценки.

## Быстрые ответы
- **Что делает Aspose.OCR?** Он извлекает текст из изображений с высокой точностью и позволяет ограничивать распознаваемые символы.  
- **Нужна ли мне лицензия?** Временная или постоянная лицензия требуется для использования в продакшене; временный ключ удаляет водяные знаки.  
- **Какая версия JDK поддерживается?** Библиотека работает с последними версиями JDK (JDK 17, 19, 21).  
- **Могу ли я ограничить распознаваемые символы?** Да — используйте метод `setAllowedCharacters` для ограничения вывода.  
- **Сколько времени занимает настройка?** Около 10‑15 минут для базовой реализации от начала до конца.

## Что такое «извлечение текста из изображений»?
Извлечение текста из изображений, также известное как оптическое распознавание символов (OCR), преобразует визуальные символы — будь то печатные, рукописные или набранные — в машинно‑читаемые строки. Это преобразование позволяет приложениям выполнять поиск, индексацию, редактирование и анализ содержимого программно, поддерживая такие рабочие процессы, как обработка счетов, архивирование документов и автоматизация ввода данных.

## Почему использовать Aspose.OCR для Java?
Aspose.OCR поддерживает **60+ языков**, может обрабатывать изображения размером до **10 МБ** без загрузки всего файла в память и обеспечивает **>95 % точности** на чистых сканах. Библиотека автономна, не требует внешних OCR‑движков, что упрощает развертывание и снижает затраты на лицензирование.

## Предварительные требования

### Java Development Kit (JDK)

Убедитесь, что у вас установлена последняя версия Java Development Kit. Вы можете скачать её [здесь](https://www.oracle.com/java/technologies/javase-downloads.html).

### Библиотека Aspose.OCR для Java

Скачайте и установите библиотеку Aspose.OCR для Java по [ссылке для загрузки](https://releases.aspose.com/ocr/java/).

### Лицензия Aspose.OCR

Чтобы разблокировать полный функционал, получите лицензию. Вы можете приобрести её [здесь](https://purchase.aspose.com/buy) или запросить [временную лицензию](https://purchase.aspose.com/temporary-license/) для пробного использования.

## Как использовать OCR с Aspose.OCR для Java?

Загрузите изображение, настройте OCR‑движок и вызовите метод распознавания — всё это в нескольких простых строках. Этот абзац с прямым ответом подскажет, что именно нужно сделать: создать экземпляр `AsposeOCR` с вашей строкой лицензии, задать разрешённые символы и вызвать `RecognizeLine` для целевого изображения, чтобы получить извлечённый текст. API обрабатывает предобработку изображения внутри, поэтому вы получаете чистый результат без дополнительного кода.

### Импорт пакетов

Класс `AsposeOCR` находится в пакете `com.aspose.ocr`. Импортируйте необходимые классы перед началом кодирования.

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Пошаговое руководство

### Шаг 1: Установите каталог документов

Выберите папку, где будут сохраняться результаты OCR и временные файлы. Этот путь позже используется для поиска изображения, которое нужно обработать.

```java
String dataDir = "Your Document Directory";
```

### Шаг 2: Укажите путь к изображению

Укажите полный путь в файловой системе или расположение ресурса в class‑path, указывающее на изображение, которое вы хотите проанализировать.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Шаг 3: Создайте экземпляр Aspose.OCR

`AsposeOCR` — это основной движок, выполняющий оптическое распознавание символов. Создайте его экземпляр, передав строку временной или постоянной лицензии.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Шаг 4: Выполните OCR‑распознавание

`RecognizeLine` извлекает одну строку текста из предоставленного изображения и возвращает её как обычный Java `String`. Вы можете вызывать этот метод многократно для многострочных документов.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Совет:** Если вам нужно ограничить вывод только цифрами (например, для номеров счетов), вызовите `setAllowedCharacters("0123456789")` у экземпляра `AsposeOCR` перед вызовом `RecognizeLine`. Это заставит движок игнорировать любые нечисловые символы.  
> `setAllowedCharacters` — это метод `AsposeOCR`, который ограничивает вывод OCR указанным белым списком символов.

## Распространённые проблемы и решения

| Проблема | Причина | Решение |
|----------|---------|---------|
| **Нет вывода или пустая строка** | Неправильный путь к изображению или неподдерживаемый формат | Проверьте `imagePath` и используйте поддерживаемый формат (JPEG, PNG, BMP) |
| **Ошибки распознавания** | Низкое разрешение изображения или шумный фон | Предобработайте изображение (увеличьте контраст, бинаризуйте) перед OCR |
| **Лицензия не применена** | Отсутствует или недействительный ключ лицензии | Убедитесь, что строка лицензии правильна и передана конструктору `AsposeOCR` |

## Часто задаваемые вопросы

**В: Как я могу получить временную лицензию для Aspose.OCR?**  
A: Посетите страницу [temporary license page](https://purchase.aspose.com/temporary-license/), чтобы запросить пробный ключ, который удаляет водяные знаки оценки.

**В: Где я могу найти поддержку для Aspose.OCR?**  
A: Присоединяйтесь к сообществу на [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16) для получения помощи и обсуждений.

**В: Могу ли я указать разрешённые символы в Aspose.OCR?**  
A: Да, используйте API `setAllowedCharacters` для определения пользовательского белого списка символов. Это идеально для полей, содержащих только цифры.

**В: Совместим ли Aspose.OCR с последними версиями JDK?**  
A: Абсолютно — Aspose.OCR регулярно обновляется, чтобы оставаться совместимым с новейшими версиями Java.

**В: Есть ли дополнительные возможности OCR помимо распознавания строк?**  
A: Библиотека также поддерживает распознавание блоков, абзацев и полной страницы, языковые пакеты и продвинутую предобработку изображений.

## Заключение

Следуя этому **уроку Aspose OCR Java**, вы теперь знаете **how to use OCR** для извлечения текста из изображений, ограничения набора символов и применения временной лицензии для быстрой проверки. Более подробно изучите полную [документацию](https://reference.aspose.com/ocr/java/), чтобы исследовать поддержку нескольких языков, пакетную обработку и пользовательские конвейеры предобработки.

---

**Последнее обновление:** 2026-05-24  
**Тестировано с:** Aspose.OCR for Java 24.11  
**Автор:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Связанные руководства

- [Как установить лицензию и проверить лицензию Aspose.OCR в Java](/ocr/java/ocr-basics/set-license/)
- [Преобразовать изображение в текст в Java с использованием Aspose.OCR BufferedImage](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Пример Aspose OCR Java — распознавание строк на изображениях](/ocr/java/advanced-ocr-techniques/recognize-lines/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}