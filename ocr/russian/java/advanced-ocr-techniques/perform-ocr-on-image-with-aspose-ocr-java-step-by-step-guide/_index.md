---
category: general
date: 2026-02-14
description: Узнайте, как выполнять OCR на изображении и извлекать текст из изображения
  с помощью Aspose OCR в Java. Включает загрузку изображения для OCR, пользовательский
  словарь и исправление орфографии.
draft: false
keywords:
- perform OCR on image
- extract text from image
- load image for OCR
- Aspose OCR Java
- spell correction OCR
language: ru
og_description: Выполните OCR изображения в Java с помощью Aspose OCR. Это руководство
  показывает, как загрузить изображение для OCR, извлечь текст из изображения и включить
  исправление орфографии.
og_title: Выполнить OCR на изображении — Полный учебник по Java
tags:
- OCR
- Java
- Aspose
title: Выполните OCR изображения с помощью Aspose OCR – пошаговое руководство на Java
url: /ru/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

? It's not a class name. I'd translate to "пользовательский словарь". But keep code references unchanged.

We'll translate naturally.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполнять OCR на изображении – Полный Java‑урок

Когда‑нибудь вам нужно было **выполнять OCR на изображении**, но вы не знали, с чего начать? Вы не одиноки; многие разработчики сталкиваются с тем же самым, когда впервые пытаются извлечь текст из графических данных. Хорошая новость в том, что с Aspose OCR for Java вы можете получить надёжные результаты всего в несколько строк кода — плюс вы можете повысить точность с помощью пользовательского словаря и проверки орфографии.

В этом руководстве мы пройдёмся по всему, что вам нужно знать: от загрузки изображения для OCR, до включения исправления орфографии и, наконец, вывода очищенного текста. К концу вы сможете **выполнять OCR на изображении** в своих Java‑проектах, а также узнаете, как **извлекать текст из изображения** даже из шумных сканов.

## Что вам понадобится

Прежде чем погрузиться в детали, убедитесь, что у вас есть следующее:

- **Java Development Kit (JDK) 8+** – код использует стандартные Java API.
- **Aspose OCR for Java** библиотека (можно скачать последнюю JAR‑файл с сайта Aspose или из Maven Central).
- Файл изображения (например, `invoice.png`), который вы хотите обработать.
- (Опционально) Текстовый файл `custom_dict.txt`, содержащий специфичные для домена слова, по одному на строку.

И всё — без тяжёлых фреймворков, без внешних сервисов. Просто чистый Java и JAR‑файл Aspose OCR.

## Шаг 1: Создайте проект и подключите зависимости

Сначала создайте новый Maven (или Gradle) проект и добавьте зависимость Aspose OCR. Если вы используете Maven, ваш `pom.xml` должен содержать:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

Если вы предпочитаете скачать JAR вручную, поместите её в папку `libs` и добавьте в classpath.

> **Pro tip:** Всегда проверяйте номер версии на момент написания; более новые релизы могут добавлять дополнительные возможности, такие как языковые пакеты.

## Шаг 2: Загрузите изображение для OCR

Первый реальный шаг кода — указать OCR‑движку, какое изображение анализировать. Aspose OCR использует обёртку `ImageStream`, которая может читать из файла, массива байтов или даже URL.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you wish to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

Обратите внимание, как мы **загружаем изображение для OCR** одним вызовом метода — без лишних манипуляций с `BufferedImage`. Если ваше изображение находится в ресурсах, просто замените путь на `getClass().getResourceAsStream(...)`.

## Шаг 3: Включите исправление орфографии (опционально, но мощно)

Aspose OCR может автоматически исправлять типичные ошибки OCR (например, «l» vs «1»). Включить эту функцию так же просто, как переключить флаг:

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

Зачем это нужно? Представьте, что вы сканируете печатный счёт, где шрифт крошечный, а сканер добавляет случайные пятна. Исправление орфографии часто превращает «Inv0ice» обратно в «Invoice» без дополнительной работы с вашей стороны.

## Шаг 4: Предоставьте пользовательский словарь (адаптируйте движок)

Если вы работаете с отраслевой терминологией — будь то медицинские коды, юридический жаргон или артикулы товаров — пользовательский словарь может значительно повысить точность. Словарь — это просто текстовый файл, где каждое слово находится на отдельной строке.

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

Убедитесь, что файл сохранён в кодировке UTF‑8; иначе вы можете увидеть «кракозябры» для не‑ASCII символов.

## Шаг 5: Запустите процесс OCR

Теперь мы наконец позволяем движку выполнить свою магию. Вызов `process()` возвращает объект `OcrResult`, содержащий распознанный текст, оценки уверенности и даже макет, если он понадобится позже.

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

Если вам интересно, бросает ли движок исключение, оберните вызов в `try‑catch` и проверьте `ocrResult.getErrorMessage()` для получения деталей.

## Шаг 6: Выведите распознанный (и исправленный) текст

Последний шаг — отобразить или сохранить извлечённую строку. Для быстрой демонстрации просто выведем её в консоль:

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

Запуск программы должен вывести что‑то вроде:

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

Если вы видите посторонние символы, проверьте пользовательский словарь и попробуйте улучшить качество изображения (например, увеличить контраст перед передачей в движок).

### Полный рабочий пример

Собрав всё вместе, получаем полностью готовый к запуску класс:

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you wish to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));

        // Step 3: Enable spell‑checking for the OCR result
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);

        // Step 4: Provide a custom dictionary (one word per line)
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));

        // Step 5: Run the OCR process
        OcrResult ocrResult = ocrEngine.process();

        // Step 6: Output the recognized (and corrected) text
        System.out.println(ocrResult.getText());
    }
}
```

Сохраните файл как `SpellCorrectDemo.java`, поправьте пути, скомпилируйте командой `javac`, а затем запустите `java SpellCorrectDemo`. Теперь вы сможете **выполнять OCR на изображении** и увидеть извлечённый текст в консоли.

## Часто задаваемые вопросы и особые случаи

### Что делать, если изображение в другом формате (PDF, TIFF и т.д.)?

Aspose OCR поддерживает многие растровые форматы «из коробки». Для PDF‑файлов сначала нужно извлечь каждую страницу как изображение — Aspose PDF for Java делает это удобно. После получения `BufferedImage` или байтового потока тот же вызов `setImage` работает.

### Как обрабатывать многостраничные документы?

Итерируйте каждую страницу‑изображение, запускайте шаги OCR и конкатенируйте результаты. Не забудьте сбрасывать или создавать новый `OcrEngine` для каждой страницы, если требуется независимый контекст проверки орфографии.

### Можно ли ограничить язык или набор символов?

Да. Используйте `ocrEngine.getEngineOptions().setLanguage(Language.English);` (или любой другой поддерживаемый язык), чтобы уменьшить количество ложных срабатываний и ускорить обработку.

### Какова производительность при больших партиях?

Aspose OCR потокобезопасен для операций только чтения. Вы можете создать пул потоков и обрабатывать изображения параллельно — только не делитесь одним экземпляром `OcrEngine` между потоками.

## Советы для повышения точности

- **Предобрабатывайте изображение**: увеличьте контраст, удалите фоновой шум или переведите в градации серого.
- **Используйте скан высокого разрешения** (300 dpi и выше). При низком разрешении часто получаются «кракозябры».
- **Держите пользовательский словарь компактным**: слишком много нерелевантных слов может запутать проверку орфографии.
- **Проверяйте вывод**: если известен ожидаемый формат (например, даты, числа), выполните пост‑обработку с помощью регулярных выражений, чтобы отловить аномалии.

## Следующие шаги

Теперь, когда вы умеете **выполнять OCR на изображении** и **извлекать текст из изображения** с помощью Aspose OCR, вы можете исследовать следующие темы:

- **Сохранение результата OCR в PDF** с поисковыми текстовыми слоями.
- **Интеграция с базой данных** для автоматического хранения извлечённых данных из счетов.
- **Применение машинного обучения** для пост‑обработки и ещё более высокой точности рукописных заметок.
- **Использование флага `load image for OCR`** в веб‑службе, принимающей загруженные пользователями фотографии.

Все эти темы опираются на базовые шаги, рассмотренные выше, так что переход будет плавным.

---

*Счастливого кодинга! Если возникнут трудности, оставляйте комментарий — ничто не заменит обучение на реальных примерах.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}