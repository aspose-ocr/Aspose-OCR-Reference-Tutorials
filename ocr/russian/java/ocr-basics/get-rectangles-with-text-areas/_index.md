---
date: 2026-02-09
description: Узнайте, как преобразовать изображение в текст и извлечь прямоугольники
  областей текста с помощью библиотеки Aspose OCR Java. Пошаговое руководство с примерами
  кода.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: Преобразовать изображение в текст – распознать текст на изображении и получить
  прямоугольники областей текста
url: /ru/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование изображения в текст – Распознавание текста на изображении и получение прямоугольников областей текста

## Введение

Если вам нужно **convert image to text** и **recognize text from image** файлы в Java‑приложении, Aspose.OCR for Java предоставляет быстрый и точный способ сделать это. В этом руководстве мы пройдём по точным шагам, необходимым для извлечения абзацев из изображения, получения ограничивающих прямоугольников для каждой области текста и вывода этих координат в консоль. К концу вы поймёте, почему этот подход работает, как интегрировать библиотеку и где её можно расширить для ваших собственных сценариев использования.

## Краткие ответы
- **What does “recognize text from image” mean?** Это означает преобразование визуальных символов на изображении в редактируемые строковые данные.  
- **Which library handles this in Java?** Aspose.OCR for Java.  
- **Do I need a license for development?** Временная лицензия доступна для тестирования; полная лицензия требуется для продакшна.  
- **Can I extract paragraphs instead of single words?** Да — используйте `AreasType.PARAGRAPHS`, чтобы получить прямоугольники уровня абзаца.  
- **Is the code compatible with Java 11+?** Абсолютно, API работает с Java 11 и новее.

## Что такое “convert image to text” в Aspose.OCR?

Метод `RecognizePage` Aspose.OCR анализирует растровое изображение, применяет OCR‑алгоритмы и возвращает распознанную строку. Когда вы запрашиваете области текста, библиотека также вычисляет точные координаты `Rectangle` для каждого блока текста, что упрощает выделение или последующую обработку конкретных секций.

## Почему использовать эту **java ocr library**?

- **High accuracy** – поддерживает несколько языков и сложные шрифты.  
- **Easy integration** – один JAR добавляет полные возможности OCR.  
- **Flexible output** – вы можете получить необработанный текст, отформатированный HTML или точные прямоугольники областей текста.  
- **Thread‑safe** – подходит для серверных сред с высокой пропускной способностью.

## Требования

- **Java Development Kit** (JDK 11 или новее), установленный на вашем компьютере.  
- **Aspose.OCR for Java** library – скачайте её с официального сайта [here](https://releases.aspose.com/ocr/java/).  
- IDE или система сборки (Maven/Gradle) для управления зависимостью JAR.

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

### Step 1: Set Up Your Project
Создайте новый Java‑проект (или добавьте в существующий) и разместите JAR Aspose.OCR в classpath. Если вы используете Maven, добавьте зависимость, как описано в пакете загрузки.

### Step 2: Define Document Directory and Image Path
Укажите, где находится ваш пример изображения:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Step 3: Create Aspose.OCR Instance
Создайте экземпляр OCR‑движка:

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### Step 4: Recognize Text in the Image
Вызовите `RecognizePage`, чтобы преобразовать изображение в обычный текст. Этот шаг демонстрирует основную возможность **recognize text image java**:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Step 5: Get Rectangles with Text Areas
Теперь получите ограничивающие прямоугольники для каждого абзаца (или других типов областей). Здесь вы **extract paragraphs from image** и получаете их координаты:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Распространённые проблемы и устранение неполадок

| Симптом | Вероятная причина | Решение |
|---------|-------------------|---------|
| `IOException` on `RecognizePage` | Неправильный путь к файлу или отсутствие прав на чтение | Убедитесь, что `imagePath` указывает на существующий PNG/JPG и приложение имеет доступ к файловой системе. |
| Empty result string | Изображение низкого качества или неподдерживаемый язык | Предобработайте изображение (увеличьте контраст, бинаризуйте) или укажите правильный язык с помощью `api.setLanguage("eng")`. |
| No rectangles returned | Используется неверный `AreasType` (например, `WORDS`, когда ожидаются абзацы) | Переключитесь на `AreasType.PARAGRAPHS` или `AreasType.LINES` при необходимости. |

## Часто задаваемые вопросы

**Q: Совместим ли Aspose.OCR с Java 11?**  
A: Да, Aspose.OCR работает с Java 11 и более новыми версиями.

**Q: Могу ли я использовать Aspose.OCR в личных и коммерческих проектах?**  
A: Да, вы можете использовать её в любом типе проекта. Подробности о лицензировании см. [here](https://purchase.aspose.com/buy).

**Q: Как получить временную лицензию для оценки?**  
A: Вы можете получить временную лицензию [here](https://purchase.aspose.com/temporary-license/).

**Q: Где я могу найти поддержку сообщества или официальную помощь?**  
A: Для поддержки и обсуждений посетите [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).

**Q: Поддерживает ли Aspose.OCR многопоточность?**  
A: Да, библиотека thread‑safe и может использоваться в конкурентных средах для повышения производительности.

## Заключение

В этом **aspose ocr java tutorial** вы узнали, как **convert image to text** с помощью Aspose.OCR for Java, извлекать абзацы и получать точные прямоугольники, окружающие каждый блок текста. Эти возможности позволяют создавать поисковые PDF, выделять текст в UI‑оверлеях или передавать структурированные данные в последующие процессы. Изучайте API дальше, чтобы настраивать параметры языка, обрабатывать разные форматы изображений или интегрировать с облачным хранилищем.

---

**Последнее обновление:** 2026-02-09  
**Тестировано с:** Aspose.OCR 23.10 for Java  
**Автор:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}