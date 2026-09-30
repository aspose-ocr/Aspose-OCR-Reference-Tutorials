---
date: 2026-02-12
description: Узнайте, как распознавать текст на изображениях с выбором языка, используя
  Aspose.OCR для Java. Это пошаговое руководство охватывает извлечение текста в Java,
  коррекцию наклона OCR и многое другое.
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Как распознавать текст на изображении с указанием языка с помощью Aspose.OCR
url: /ru/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

 the PDF page to an image first (e.g., using Aspose.PDF) and then run OCR.

Translate each.

Next "## Conclusion" -> "## Заключение"

Paragraph translate.

Then line "---" keep.

Then "**Last Updated:** 2026-02-12" keep date.

"**Tested With:** Aspose.OCR 24.11 for Java" keep.

"**Author:** Aspose" keep.

Then closing shortcodes.

Then backtop button shortcode.

We must ensure we keep all shortcodes exactly.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как распознать текст на изображении с указанием языка с помощью Aspose.OCR

## Введение

Извлечение текста из файлов изображений — распространённая задача, будь то оцифровка отсканированных документов, обработка чеков или создание поисковых архивов. В этом руководстве мы пошагово рассмотрим полный пример, показывающий **как выполнять OCR текста на изображении** с указанием конкретного языка, чтобы вы могли уже сегодня интегрировать надёжный OCR в свои Java‑приложения. Вы также увидите, как работать с коррекцией наклона OCR и распознаванием по областям для достижения оптимальной точности.

## Быстрые ответы
- **Какая библиотека обрабатывает OCR в Java?** Aspose.OCR for Java  
- **Какая настройка выбирает язык?** `settings.setLanguage(Language.Eng)` (или любой поддерживаемый язык)  
- **Нужна ли лицензия для разработки?** Бесплатная оценочная лицензия подходит для тестирования; коммерческая лицензия требуется для продакшн.  
- **Можно ли ограничить OCR областью изображения?** Да, используйте `RecognitionSettings.setRecognitionAreas()` с прямоугольниками.  
- **Каково типичное время выполнения?** Несколько секунд на страницу на обычном ноутбуке, в зависимости от размера изображения и сложности языка.

## Как выполнить OCR текста на изображении с выбором языка
В этом разделе мы отвечаем на основной вопрос **как выполнить OCR** изображения, когда известен язык текста. Выбор правильного языка значительно повышает точность распознавания, поскольку движок OCR может применять языково‑специфичные словари и модели символов.

### Почему это важно
- **Более высокая точность** – языково‑специфичные модели снижают количество ошибок распознавания.  
- **Увеличение производительности** – движок пропускает ненужные проверки других языков.  
- **Лучшее распознавание диакритических знаков** – французский, испанский, немецкий и т.д. распознаются корректно при использовании соответствующего enum `Language`.

## Что такое «извлечение текста из изображения»?
OCR (оптическое распознавание символов) преобразует визуальное представление символов в машинно‑читаемые строки. Это позволяет реализовать поиск, аналитику и автоматическую обработку данных, которые иначе потребовали бы ручного ввода.

## Почему использовать Aspose.OCR с выбором языка?
- **Поддержка нескольких языков** – выберите точный язык(и), присутствующий(ие) на изображении, чтобы повысить точность.  
- **Тонкая настройка** – корректируйте наклон, задавайте области распознавания и управляйте автоматическим исправлением наклона.  
- **Чистый Java API** – без нативных зависимостей, легко интегрировать в любой Java‑проект.  
- **Богатый набор результатов** – получайте простой текст, JSON, координаты ограничивающих прямоугольников и предупреждения одним вызовом.

## Предварительные требования

Перед началом убедитесь, что у вас есть:

- **Java Development Kit (JDK)** установлен (JDK 8 или новее).  
- **Aspose.OCR for Java** library – скачайте её с официального сайта [здесь](https://reference.aspose.com/ocr/java/).  
- Файл изображения, содержащий нужный вам текст, например `p3.png`.

## Импорт пакетов

В вашем Java‑файле включите необходимые классы Aspose.OCR и стандартные утилиты Java:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Пошаговое руководство

### Шаг 1: Настройте каталог документов

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Замените `"Your Document Directory"` на абсолютный путь, где находится `p3.png`.

### Шаг 2: Определите путь к изображению

```java
// The image path
String file = dataDir + "p3.png";
```

Убедитесь, что переменная `file` указывает на точный файл изображения, который вы собираетесь обработать.

### Шаг 3: Создайте экземпляр Aspose.OCR API

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

Объект `AsposeOCR` предоставляет доступ ко всем операциям OCR.

### Шаг 4: Установите параметры распознавания (выбор языка)

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Здесь мы:

1. Отключаем автоматический корректор наклона, так как задаём значение наклона вручную.  
2. Определяем прямоугольную область (`RecognitionAreas`), чтобы ограничить OCR только той частью изображения, где действительно есть текст.  
3. Устанавливаем **language** на английский (`Language.Eng`). При необходимости замените на `Language.Fra`, `Language.Spa` и т.д., в зависимости от исходного изображения.

### Шаг 5: Выполните OCR и получите результаты

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Вызов `RecognizePage` запускает движок OCR, используя изображение и заданные настройки. Результат сохраняется в объект `RecognitionResult`.

### Шаг 6: Выведите и используйте результаты

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

Консольный вывод показывает:

- Полный извлечённый текст (`recognitionText`).  
- Текст для каждого заданного прямоугольника (`recognitionAreasText`).  
- Координаты ограничивающих прямоугольников.  
- Представление в формате JSON для удобной дальнейшей обработки.  
- Обнаруженный угол наклона и любые предупреждения.

Теперь вы можете передать `result.recognitionText` в свою бизнес‑логику — сохранить, проиндексировать или передать другому сервису.

## Распространённые проблемы и решения

| Проблема | Причина | Решение |
|----------|---------|---------|
| **Неправильные символы** | Выбран неверный язык | Установите правильный enum `Language` (например, `Language.Fra` для французского). |
| **Текст не возвращается** | Область распознавания не охватывает текст | Отрегулируйте координаты `Rectangle` или удалите `RecognitionAreas`, чтобы обрабатывать всё изображение. |
| **Низкая производительность** | Очень большое изображение или высокое разрешение | Уменьшите размер изображения перед OCR или увеличьте выделение памяти для JVM. |
| **Предупреждения о неподдерживаемом формате** | Формат изображения не распознан | Конвертируйте изображение в PNG, JPEG или TIFF перед обработкой. |

## FAQ

**Q: Можно ли распознавать несколько языков в одном вызове OCR?**  
A: Да. Используйте `settings.setLanguage(Language.Eng | Language.Fra)`, чтобы включить многоязычное распознавание.

**Q: Какие форматы изображений поддерживает Aspose.OCR?**  
A: PNG, JPEG, BMP, TIFF, GIF и несколько других. Просто укажите правильный путь к файлу.

**Q: Есть ли ограничение по размеру изображения?**  
A: Жёсткого ограничения нет, но очень большие изображения увеличивают расход памяти и время обработки. Рассмотрите возможность уменьшения размеров больших файлов.

**Q: Как получить производственную лицензию?**  
A: Приобретите лицензию на сайте Aspose и примените её через класс `License`, как показано в документации Aspose.

**Q: Можно ли извлечь текст напрямую со страницы PDF?**  
A: Не напрямую с помощью Aspose.OCR. Сначала преобразуйте страницу PDF в изображение (например, с помощью Aspose.PDF), а затем выполните OCR.

## Заключение

Теперь вы знаете, **как извлекать текст из изображения** с помощью Aspose.OCR для Java, выбирая соответствующий язык и ограничивая распознавание конкретными областями. Такой подход обеспечивает точный, высокопроизводительный OCR, который можно встроить в любой Java‑ориентированный рабочий процесс — от систем управления документами до конвейеров захвата данных. Готовы продолжить? Попробуйте изменить enum языка, поэкспериментируйте с различными областями распознавания и интегрируйте результаты в свою собственную бизнес‑логику.

---

**Last Updated:** 2026-02-12  
**Tested With:** Aspose.OCR 24.11 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}