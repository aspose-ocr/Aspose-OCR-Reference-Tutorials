---
date: 2026-06-19
description: Узнайте, как преобразовать изображение в текст на Java, извлекать абзацы
  из изображения и получать прямоугольники областей текста с помощью библиотеки Aspose
  OCR Java.
keywords:
- image to text java
- convert scanned image text
- extract paragraphs from image
- aspose ocr java tutorial
linktitle: Image to Text Java – Распознавание текста с изображения и получение прямоугольников
  областей текста
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  headline: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  type: TechArticle
- description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  name: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  steps:
  - name: Set Up Your Project
    text: Create a new Java project (or add to an existing one) and place the Aspose.OCR
      JAR on the classpath. If you use Maven, add the dependency as described in the
      download package.
  - name: Define Document Directory and Image Path
    text: 'Specify where your sample image resides:'
  - name: Create AsposeOCR Instance
    text: '`AsposeOCR` is the main class that provides OCR functionality. Instantiate
      the OCR engine:'
  - name: Recognize Text in the Image
    text: Load your image and call `RecognizePage` to convert the picture into plain
      text. This single method call performs image preprocessing, character segmentation,
      and language‑specific recognition in one step.
  - name: Get Rectangles with Text Areas
    text: Retrieve the bounding rectangles for each paragraph (or other area types).
      This step returns a collection of `Rectangle` objects that precisely enclose
      the detected text blocks, enabling you to highlight or further process individual
      sections. CODE_BLOCK_PLACEHOLDER_5_END
  type: HowTo
- questions:
  - answer: Yes, Aspose.OCR works with Java 11 and later versions.
    question: Is Aspose.OCR compatible with Java 11?
  - answer: Yes, you can use it in any type of project. For licensing details, visit
      [here](https://purchase.aspose.com/buy).
    question: Can I use Aspose.OCR for both personal and commercial projects?
  - answer: You can obtain a temporary license [here](https://purchase.aspose.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: For support and discussions, visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).
    question: Where can I find community support or official assistance?
  - answer: Yes, the library is thread‑safe and can be used in concurrent environments
      for better performance.
    question: Does Aspose.OCR support multithreading?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Image to Text Java – Преобразование изображения в текст и получение прямоугольников
  областей текста
url: /ru/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Изображение в Текст Java – Преобразование изображения в текст и получение прямоугольников областей текста

## Введение

Если вам необходимо **convert image to text** в Java‑приложении, Aspose.OCR for Java предоставляет быстрое и точное решение. В этом руководстве мы пошагово пройдем процесс извлечения абзацев из изображения, получения ограничивающих прямоугольников для каждой области текста и вывода этих координат в консоль. К концу вы поймёте, почему этот подход работает, как интегрировать библиотеку и где её можно расширить для ваших собственных сценариев использования.

## Быстрые ответы
`AreasType` — это перечисление, которое указывает уровень сегментации текста (слова, строки, абзацы).

- **Что означает «recognize text from image»?** Это преобразование визуальных символов на изображении в редактируемые строковые данные.  
- **Какая библиотека обеспечивает это в Java?** Aspose.OCR for Java.  
- **Нужна ли лицензия для разработки?** Доступна временная лицензия для тестирования; полная лицензия требуется для продакшн.  
- **Могу ли я извлекать абзацы вместо отдельных слов?** Да — используйте `AreasType.PARAGRAPHS` для получения прямоугольников уровня абзаца.  
- **Совместим ли код с Java 11+?** Абсолютно, API работает с Java 11 и более новыми версиями.

## Что такое «convert image to text» в Aspose.OCR?

`convert image to text` относится к процессу анализа растрового изображения, применения OCR‑алгоритмов и возврата распознанных символов в виде строки. Метод `RecognizePage` библиотеки Aspose.OCR выполняет это преобразование, при необходимости предоставляя точные координаты `Rectangle` для каждого обнаруженного блока текста.

## Почему использовать эту **java ocr library**?

Aspose.OCR поддерживает **30+ языков** и может обрабатывать изображения размером до **50 MB** без загрузки всего файла в память, обеспечивая время отклика менее секунды на типичном серверном оборудовании. Библиотека потокобезопасна, требует только один JAR и предлагает гибкие форматы вывода — включая чистый текст, HTML и точные прямоугольники областей текста — что делает её идеальной для высокопроизводительных корпоративных сценариев.

## Требования

- **Java Development Kit** (JDK 11 или новее), установленный на вашем компьютере.  
- **Aspose.OCR for Java** — загрузите библиотеку с официального сайта [здесь](https://releases.aspose.com/ocr/java/).  
- IDE или система сборки (Maven/Gradle) для управления зависимостями JAR.

## Импорт пакетов

В вашем Java‑проекте импортируйте необходимые классы:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Пошаговое руководство

### Шаг 1: Настройте ваш проект
Создайте новый Java‑проект (или добавьте в существующий) и разместите JAR‑файл Aspose.OCR в classpath. Если вы используете Maven, добавьте зависимость, как описано в пакете загрузки.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Шаг 2: Определите каталог документа и путь к изображению
Укажите, где находится ваше образцовое изображение:

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### Шаг 3: Создайте экземпляр AsposeOCR
`AsposeOCR` — основной класс, предоставляющий OCR‑функциональность.

Создайте экземпляр OCR‑движка:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Шаг 4: Распознать текст на изображении
Загрузите изображение и вызовите `RecognizePage` для преобразования картинки в обычный текст. Этот один вызов метода выполняет предобработку изображения, сегментацию символов и распознавание, специфичное для языка, за один шаг.

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

### Шаг 5: Получить прямоугольники с областями текста
Получите ограничивающие прямоугольники для каждого абзаца (или других типов областей). Этот шаг возвращает коллекцию объектов `Rectangle`, точно охватывающих обнаруженные блоки текста, позволяя выделять или дополнительно обрабатывать отдельные секции.

CODE_BLOCK_PLACEHOLDER_5_END

## Распространённые проблемы и устранение неполадок

| Симптом | Вероятная причина | Решение |
|---------|-------------------|---------|
| `IOException` при `RecognizePage` | Неправильный путь к файлу или отсутствие прав на чтение | Убедитесь, что `imagePath` указывает на существующий PNG/JPG и приложение имеет доступ к файловой системе. |
| Пустая строка результата | Низкокачественное изображение или неподдерживаемый язык | Предобработайте изображение (увеличьте контраст, бинаризуйте) или укажите правильный язык с помощью `api.setLanguage("eng")`. |
| Прямоугольники не возвращаются | Используется неверный `AreasType` (например, `WORDS`, когда ожидаются абзацы) | Переключитесь на `AreasType.PARAGRAPHS` или `AreasType.LINES` при необходимости. |

## Часто задаваемые вопросы

**Q:** Совместим ли Aspose.OCR с Java 11?  
**A:** Да, Aspose.OCR работает с Java 11 и более новыми версиями.

**Q:** Могу ли я использовать Aspose.OCR в личных и коммерческих проектах?  
**A:** Да, вы можете использовать её в любом типе проекта. Для деталей лицензирования посетите [здесь](https://purchase.aspose.com/buy).

**Q:** Как получить временную лицензию для оценки?  
**A:** Вы можете получить временную лицензию [здесь](https://purchase.aspose.com/temporary-license/).

**Q:** Где можно найти поддержку сообщества или официальную помощь?  
**A:** Для поддержки и обсуждений посетите [форум Aspose.OCR](https://forum.aspose.com/c/ocr/16).

**Q:** Поддерживает ли Aspose.OCR многопоточность?  
**A:** Да, библиотека потокобезопасна и может использоваться в конкурентных средах для повышения производительности.

## Заключение

В этом **aspose ocr java tutorial** вы узнали, как **convert image to text** с помощью Aspose.OCR for Java, извлекать абзацы и получать точные прямоугольники, окружающие каждый блок текста. Эти возможности позволяют создавать поисковые PDF, выделять текст в наложениях UI или передавать структурированные данные в последующие процессы. Изучайте API дальше, чтобы настраивать параметры языка, обрабатывать различные форматы изображений или интегрировать с облачным хранилищем.

---

**Последнее обновление:** 2026-06-19  
**Тестировано с:** Aspose.OCR 23.10 for Java  
**Автор:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Связанные руководства

- [Извлечение текста из изображений – Основы OCR с Aspose.OCR for Java](/ocr/java/ocr-basics/)
- [Извлечение текста из изображения Java с Aspose.OCR Detect Areas Mode](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Преобразование изображения в текст в Java с использованием Aspose.OCR BufferedImage](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}