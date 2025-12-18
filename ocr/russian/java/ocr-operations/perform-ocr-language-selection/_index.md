---
date: 2025-12-13
description: Узнайте, как извлекать текст из изображения с помощью Aspose.OCR для
  Java с выбором языка. Этот пошаговый учебник по Aspose OCR для Java демонстрирует
  точную настройку OCR.
linktitle: How to Extract Text from Image with Language Selection Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Как извлечь текст из изображения с выбором языка с помощью Aspose.OCR
url: /ru/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как извлечь текст из изображения с выбором языка с помощью Aspose.OCR

## Введение

Извлечение текста из файлов изображений — распространённая задача, будь то оцифровка отсканированных документов, обработка чеков или создание поисковых архивов. Aspose.OCR for Java делает эту задачу простой и предоставляет тонкую настройку выбора языка, коррекции наклона и областей распознавания. В этом руководстве мы пошагово рассмотрим полный пример, показывающий **как извлечь текст из изображения** с заданным языком, чтобы вы могли уже сегодня интегрировать надёжный OCR в свои Java‑приложения.

## Быстрые ответы
- **Какой библиотекой осуществляется OCR в Java?** Aspose.OCR for Java  
- **Какой параметр выбирает язык?** `settings.setLanguage(Language.Eng)` (или любой поддерживаемый язык)  
- **Нужна ли лицензия для разработки?** Бесплатная оценочная лицензия подходит для тестирования; для продакшна требуется коммерческая лицензия.  
- **Можно ли ограничить OCR областью изображения?** Да, используйте `RecognitionSettings.setRecognitionAreas()` с прямоугольниками.  
- **Каково типичное время выполнения?** Несколько секунд на страницу на обычном ноутбуке, в зависимости от размера изображения и сложности языка.

## Что такое «извлечение текста из изображения»?
Извлечение текста из изображения (OCR) преобразует визуальное представление символов в машинно‑читаемые строки. Это позволяет реализовать поиск, аналитику и потоки извлечения данных, которые иначе потребовали бы ручного ввода.

## Почему стоит использовать Aspose.OCR с выбором языка?
- **Многоязычная поддержка** – Выберите точный язык(и), присутствующие на изображении, чтобы повысить точность.  
- **Тонкая настройка** – Регулируйте наклон, определяйте области распознавания и задавайте поведение авто‑наклона.  
- **Чистый Java API** – Без нативных зависимостей, легко интегрировать в любой Java‑проект.  
- **Богатые данные результата** – Получайте простой текст, JSON, ограничивающие прямоугольники и предупреждения одним вызовом.

## Предварительные требования

Перед началом убедитесь, что у вас есть:

- **Установлен Java Development Kit (JDK)** (JDK 8 или новее).  
- **Библиотека Aspose.OCR for Java** – скачайте её с официального сайта [здесь](https://reference.aspose.com/ocr/java/).  
- Файл изображения, содержащий текст, который нужно извлечь, например, `p3.png`.

## Импорт пакетов

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

Убедитесь, что переменная `file` указывает на точное изображение, которое вы собираетесь обработать.

### Шаг 3: Создайте экземпляр API Aspose.OCR

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
1. Отключаем авто‑наклон, так как задаём значение наклона вручную.  
2. Определяем прямоугольную область (`RecognitionAreas`), чтобы ограничить OCR частью изображения, содержащей текст.  
3. Устанавливаем **язык** на английский (`Language.Eng`). Измените на `Language.Fra`, `Language.Spa` и т.д., в зависимости от исходного изображения.

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

Вызов `RecognizePage` запускает OCR‑движок с использованием изображения и заданных параметров. Результат сохраняется в объект `RecognitionResult`.

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
- Текст для каждого определённого прямоугольника (`recognitionAreasText`).  
- Координаты ограничивающего прямоугольника.  
- JSON‑представление для удобной последующей обработки.  
- Обнаруженный угол наклона и любые предупреждения.

Теперь вы можете передать `result.recognitionText` в вашу бизнес‑логику — сохранить, проиндексировать или передать в другой сервис.

## Распространённые проблемы и решения

| Проблема | Причина | Решение |
|----------|---------|----------|
| **Непонятные символы** | Выбран неправильный язык | Установите правильный enum `Language` (например, `Language.Fra` для французского). |
| **Текст не возвращается** | Область распознавания не охватывает текст | Отрегулируйте координаты `Rectangle` или удалите `RecognitionAreas`, чтобы обработать всё изображение. |
| **Низкая производительность** | Очень большое изображение или высокое разрешение | Уменьшите размер изображения перед OCR или увеличьте выделение памяти для JVM. |
| **Предупреждения о неподдерживаемом формате** | Формат изображения не распознан | Конвертируйте изображение в PNG, JPEG или TIFF перед обработкой. |

## Часто задаваемые вопросы

**Q: Можно ли распознавать несколько языков в одном вызове OCR?**  
A: Да. Используйте `settings.setLanguage(Language.Eng | Language.Fra)`, чтобы включить многоязычное распознавание.

**Q: Какие форматы изображений поддерживает Aspose.OCR?**  
A: PNG, JPEG, BMP, TIFF, GIF и несколько других. Просто укажите правильный путь к файлу.

**Q: Есть ли ограничение по размеру изображения?**  
A: Жёсткого ограничения нет, но очень большие изображения увеличивают расход памяти и время обработки. Рекомендуется уменьшать размер больших файлов.

**Q: Как получить производственную лицензию?**  
A: Приобретите лицензию на сайте Aspose и примените её через класс `License`, как показано в документации Aspose.

**Q: Можно ли извлечь текст напрямую со страницы PDF?**  
A: Не напрямую с помощью Aspose.OCR. Сначала преобразуйте страницу PDF в изображение (например, с помощью Aspose.PDF), а затем выполните OCR.

## Заключение

Вы теперь знаете, как **извлечь текст из изображения** с помощью Aspose.OCR for Java, выбирая нужный язык и ограничивая распознавание конкретными областями. Этот подход обеспечивает точный и высокопроизводительный OCR, который можно встроить в любой Java‑ориентированный рабочий процесс — от систем управления документами до конвейеров захвата данных.

---

**Last Updated:** 2025-12-13  
**Tested With:** Aspose.OCR 24.11 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}