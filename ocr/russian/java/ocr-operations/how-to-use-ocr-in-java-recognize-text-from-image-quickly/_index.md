---
category: general
date: 2026-02-17
description: Узнайте, как использовать OCR в Java для распознавания текста из файлов
  изображений, извлечения текста из PNG‑чеков и преобразования чека в JSON с помощью
  Aspose OCR.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: ru
og_description: Пошаговое руководство по использованию OCR в Java для распознавания
  текста на изображении, извлечения текста из PNG‑чеков и преобразования чека в JSON.
og_title: Как использовать OCR в Java — распознавать текст с изображения
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Как использовать OCR в Java — быстро распознавать текст на изображении
url: /ru/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

of a photo ...". Translate.

We need to keep **bold** formatting.

Proceed.

Will need to translate bullet list under "What You’ll Need". Keep bold parts.

Translate blockquote >.

Translate step headings.

Translate code block placeholders unchanged.

Translate other text.

Make sure to keep markdown syntax.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR в Java – Быстро распознавать текст на изображении

Когда‑то задумывались **как использовать OCR**, чтобы извлечь текст из фотографии чека? Возможно, вы пробовали несколько онлайн‑инструментов, но получали искажённые символы или формат, который невозможно разобрать. Хорошая новость: несколько строк кода на Java позволяют **распознавать текст на изображении**, **извлекать текст из PNG** чеков и даже **преобразовать чек в JSON** для дальнейшей обработки.  

В этом руководстве мы пройдём полный рабочий процесс — от лицензирования библиотеки Aspose OCR до получения чистого JSON‑payload, который можно загрузить в базу данных или передать модели машинного обучения. Без лишних слов, только практический, готовый к запуску пример, который можно скопировать и вставить в IDE. К концу вы получите автономную программу, принимающую `receipt.png` и выдающую готовую строку JSON.

## Что понадобится

- **Java Development Kit (JDK) 8+** — подойдёт любая современная версия.  
- **Aspose OCR for Java** — Maven‑артефакт `com.aspose:aspose-ocr`.  
- **Действительный файл лицензии Aspose OCR** (`Aspose.OCR.lic`). Бесплатная trial‑версия подходит для тестов, но полноценная лицензия снимает ограничения оценки.  
- Файл изображения (PNG, JPEG и т.д.), содержащий нужный вам текст — назовём его `receipt.png` и разместим в известной папке.  
- Любая любимая IDE (IntelliJ IDEA, Eclipse, VS Code…) — выбор за вами.

> **Pro tip:** Храните файл лицензии вне папки с исходным кодом и указывайте его через абсолютный или относительный путь, чтобы случайно не закоммитить в систему контроля версий.

Теперь, когда требования ясны, приступим к коду.

## Как использовать OCR — основные шаги

Ниже представлена высокоуровневая схема действий:

1. **Загрузить библиотеку Aspose OCR** и применить лицензию.  
2. **Создать экземпляр `OcrEngine`** — это движок, который делает всю тяжёлую работу.  
3. **Подготовить объект `OcrInput`**, указывающий на изображение, которое нужно обработать.  
4. **Вызвать `recognize` с `ResultFormat.JSON`**, чтобы получить JSON‑представление извлечённого текста.  
5. **Обработать JSON‑вывод** — напечатать, записать в файл или дальше распарсить.

Каждый шаг подробно описан в последующих разделах.

## Шаг 1 — Установить Aspose OCR и применить лицензию

Сначала добавьте зависимость Aspose OCR в ваш `pom.xml`, если используете Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Теперь в Java‑коде загрузите лицензию. Этот шаг обязателен; без него библиотека работает в режиме оценки и может добавлять водяные знаки в результат.

```java
import com.aspose.ocr.*;

public class OcrSetup {
    public static void applyLicense() throws Exception {
        // Replace the path with the actual location of your Aspose.OCR.lic file
        License ocrLicense = new License();
        ocrLicense.setLicense("C:/licenses/Aspose.OCR.lic");
    }
}
```

> **Почему это важно:** Объект `License` сообщает OCR‑движку, что вы уполномочены использовать полный набор функций, включая высокоточное распознавание и экспорт в JSON. Пропуск этого шага всё равно позволит **распознавать текст на изображении**, но результаты могут быть ограничены.

## Шаг 2 — Создать экземпляр OCR‑движка

Класс `OcrEngine` — точка входа для всех OCR‑операций. Считайте его «мозгом», который читает пиксели и определяет, какие символы они представляют.

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

Позже вы можете настроить движок (например, задать язык, включить исправление наклона), если ваши чеки содержат нелатинские скрипты или отсканированы под углом. Для большинства чеков из США значения по умолчанию работают отлично.

## Шаг 3 — Загрузить изображение для обработки

Теперь укажем OCR‑движку файл с чеком. Класс `OcrInput` может принимать несколько изображений, но в этом руководстве мы ограничимся одним PNG.

```java
import com.aspose.ocr.*;

public class ImageLoader {
    public static OcrInput loadImage(String imagePath) {
        OcrInput input = new OcrInput();
        // Add the PNG receipt – this is where we **extract text from PNG**
        input.add(imagePath);
        return input;
    }
}
```

Если понадобится **извлекать текст из PNG** файлов пакетно, просто вызывайте `input.add()` многократно или передайте список путей к файлам.

## Шаг 4 — Распознать текст и преобразовать чек в JSON

Это сердце руководства. Мы просим движок распознать текст и вернуть результат в формате JSON. Флаг `ResultFormat.JSON` делает всю тяжёлую работу за нас.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonRecognizer {
    public static String recognizeToJson(OcrEngine engine, OcrInput input) throws Exception {
        // Perform OCR and request JSON output
        OcrResult result = engine.recognize(input, ResultFormat.JSON);
        // Retrieve the JSON string
        return result.getJson();
    }
}
```

JSON‑payload содержит каждую распознанную строку, её ограничивающий прямоугольник, коэффициент уверенности и сам текст. Такая структура упрощает **преобразование чека в JSON** и последующую передачу в любой downstream‑API.

## Шаг 5 — Собрать всё вместе и запустить программу

Ниже полная, готовая к запуску Java‑класс, объединяющий всё вышеописанное. Сохраните её как `JsonExportDemo.java` (или под другим именем) и запустите из IDE или из командной строки.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonExportDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license (replace with your actual license file)
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.lic"); // <-- adjust path if needed

        // 2️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Prepare the input image that contains the text to be recognized
        OcrInput ocrInput = new OcrInput();
        // Replace with the absolute or relative path to your receipt PNG
        ocrInput.add("YOUR_DIRECTORY/receipt.png"); // <-- **extract text from PNG** here

        // 4️⃣ Perform recognition and request the result in JSON format
        OcrResult ocrResult = ocrEngine.recognize(ocrInput, ResultFormat.JSON);

        // 5️⃣ Retrieve the JSON string from the result
        String jsonResult = ocrResult.getJson();

        // 6️⃣ Output the JSON (or save it to a file for further processing)
        System.out.println(jsonResult);
    }
}
```

### Ожидаемый вывод

При запуске программа выводит строку JSON, похожую на следующую (точное содержание зависит от вашего чека):

```json
{
  "pages": [
    {
      "lines": [
        {
          "text": "Store Name",
          "confidence": 0.99,
          "boundingBox": [12, 34, 200, 45]
        },
        {
          "text": "Date: 2024-02-15",
          "confidence": 0.98,
          "boundingBox": [12, 60, 180, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.97,
          "boundingBox": [12, 120, 150, 45]
        }
      ]
    }
  ]
}
```

Теперь вы можете передать этот JSON в базу данных, REST‑endpoint или конвейер анализа данных. Шаг **преобразования чека в JSON** уже выполнен.

## Часто задаваемые вопросы и особые случаи

### Что делать, если изображение повернуто?

Aspose OCR автоматически обнаруживает и исправляет небольшие повороты. Для сильно наклонённых изображений вызовите `engine.getImagePreprocessingOptions().setDeskew(true)` перед распознаванием.

### Как работать с несколькими языками?

Используйте `engine.getLanguage()` для установки нужного языка, например `engine.setLanguage(Language.FRENCH)`. Это удобно, когда нужно **распознавать текст на изображении**, содержащем многоязычные чеки.

### Можно ли вывести обычный текст вместо JSON?

Конечно. Замените `ResultFormat.JSON` на `ResultFormat.TEXT` и вызовите `result.getText()`.

### Как ограничить OCR конкретной областью?

Да — используйте `ocrInput.add(imagePath, new Rectangle(x, y, width, height))`, чтобы сфокусироваться на области чека; это может повысить скорость и точность.

## Pro Tips для production‑готового OCR

- **Кешировать объект лицензии**, если обрабатываете много файлов в цикле; повторное создание добавляет накладные расходы.  
- **Пакетная обработка**: загрузите все пути к чекам в один `OcrInput` и вызовите `recognize` один раз. JSON будет содержать массив страниц, каждая со своими строками.  
- **Валидация JSON**: после получения строки распарсите её библиотекой вроде Jackson, чтобы убедиться в корректности перед сохранением.  
- **Контроль уверенности**: в JSON присутствует поле `confidence` для каждой строки. Фильтруйте строки ниже порога (например, 0.85), чтобы избавиться от «мусорных» данных.  
- **Защита лицензии**: храните `Aspose.OCR.lic` в безопасном хранилище или переменной окружения, особенно при развертывании в облаке.

## Заключение

Мы рассмотрели **как использовать OCR** в Java для **распознавания текста на изображении**, **извлечения текста из PNG** чеков и **преобразования чека в JSON** — всё в компактном, сквозном примере. Шаги просты, код полностью исполняем, а JSON‑вывод даёт структурированное представление, готовое для любой downstream‑системы.

Дальше вы можете исследовать более продвинутые сценарии: отправлять JSON в Apache Kafka для обработки в реальном времени, применять regex‑шаблоны для извлечения сумм позиций, или интегрировать облачный OCR‑сервис для масштабируемости. Что бы вы ни выбрали, фундаментальные принципы останутся теми же.

Есть вопросы или возникли трудности при выполнении? Оставьте комментарий ниже, и мы разберёмся вместе. Приятного кодинга и удачной трансформации ваших «грязных» изображений чеков в чистые, поисковые данные!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}