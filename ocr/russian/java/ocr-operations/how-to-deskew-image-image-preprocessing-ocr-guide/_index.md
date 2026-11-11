---
category: general
date: 2026-06-22
description: 'Как исправить наклон изображения для OCR: изучите этапы предобработки
  изображений, удалите шум «соль‑перец» и повысите точность.'
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: ru
og_description: Как выпрямить изображение для OCR, удалить шум «соль‑перец» и применить
  техники предварительной обработки изображений для OCR в полном примере на Java.
og_title: Как выпрямить изображение – Руководство по предобработке изображений для
  OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: Как выпрямить изображение — Руководство по предобработке изображений для OCR
url: /ru/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как исправить наклон изображения – Руководство по предобработке изображений для OCR

Когда‑нибудь задавались вопросом **how to deskew image**, чтобы ваш OCR‑движок действительно читал текст? Вы не одиноки. Наклонённый скан может превратить идеальный документ в неразборчивый беспорядок, и большинство разработчиков сталкиваются с этим хотя бы раз.

В этом руководстве мы пройдём полный конвейер **image preprocessing OCR**, который не только исправляет вращение, но и **remove[s] salt pepper** артефакты и повышает контраст — по‑сути всё, что нужно для **preprocess images OCR**‑стиля перед передачей в движок. К концу вы получите готовый к запуску фрагмент Java и чёткое представление о том, почему каждый шаг важен.

## Как исправить наклон изображения – построение конвейера предобработки

Сердцем любого OCR‑дружественного рабочего процесса является объект **preprocess options**, который соединяет последовательность фильтров. Представьте его как конвейер: каждый фильтр выполняет одну задачу, затем передаёт изображение следующему. Ниже приведён минимальный, но полный пример с гипотетической OCR‑библиотекой, содержащей `DeskewFilter`, `DenoiseFilter` и `ContrastBoostFilter`.

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### Почему это работает

* **DeskewFilter** анализирует доминирующие строки текста на изображении, оценивает угол и вращает bitmap обратно в горизонтальное положение. Большинство библиотек ограничивают коррекцию ±15°, потому что большие углы обычно указывают на плохо отсканированную страницу, требующую ручного вмешательства.
* **DenoiseFilter** нацелен на классический шаблон *salt‑and‑pepper* — отдельные чёрные или белые пиксели, похожие на статическое изображение на телевизоре. Их удаление предотвращает ошибочное распознавание шума как символов OCR‑движком.
* **ContrastBoostFilter** растягивает гистограмму, делая слабые штрихи более заметными. Коэффициент `1.5f` является безопасным значением по умолчанию; его можно увеличить, если ваши сканы особенно блеклые.

> **Pro tip:** Если вы знаете, что ваши документы никогда не наклоняются более чем на 10°, передайте этот меньший предел в `DeskewFilter` — алгоритм будет работать быстрее и с меньшей вероятностью пере‑корректирует.

## Предобработка изображений OCR: добавление фильтров в правильном порядке

Порядок имеет значение. Представьте, что вы удаляете шум *до* исправления наклона; шум может сбить определение угла, что приведёт к неверному выравниванию. И наоборот, применение повышения контраста *после* исправления наклона гарантирует, что вращение не внесёт новых артефактов.

Ниже представлен быстрый чек‑лист, который вы можете скопировать и вставить в любой проект:

| Шаг | Фильтр | Причина |
|------|--------|--------|
| 1 | `DeskewFilter` | Выравнивает базовую линию текста |
| 2 | `DenoiseFilter` | Удаляет изолированный пиксельный шум |
| 3 | `ContrastBoostFilter` | Повышает читаемость для OCR |

Если вам нужно добавить дополнительные шаги — например, фильтр **binarization** для бинарного OCR — разместите его **после** повышения контраста, потому что чистое, высококонтрастное изображение бинаризуется точнее.

## Удаление шума «соль‑перец» с помощью DenoiseFilter

Шум «соль‑перец» печально известен в сканах низкого качества, особенно полученных с дешевых камер телефонов. `DenoiseFilter` в нашей библиотеке реализует ядро медианного фильтра, которое заменяет каждый пиксель медианой его окружения. Эффект? Эти пятна исчезают без размытия настоящих символов.

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*When to increase the kernel size?* Если ваши исходные изображения покрыты большими пятнами, более крупное ядро их очистит, но будьте осторожны: слишком большое ядро может начать стирать тонкие штрихи в крошечных шрифтах.

## Предобработка изображений OCR — применение конвейера

После того как вы собрали цепочку фильтров, её привязка к движку осуществляется одной строкой (`engine.setPreprocessOptions`). С этого момента каждый вызов `recognizeText` автоматически проходит через конвейер. Нет необходимости вручную вызывать каждый фильтр — ваш код остаётся аккуратным, а будущие изменения (добавление нового фильтра, настройка параметров) централизованы.

Вот как выглядит успешный запуск с примером скана, изначально имеющего наклон 12° и заметный шум «перец»:

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Обратите внимание, как текст чистый, правильно ориентирован и свободен от посторонних символов, которые иначе могли бы выглядеть как “I n v o i c e” или “$‑‑‑”.

## Пограничные случаи и распространённые подводные камни

| Ситуация | На что обратить внимание | Рекомендуемое решение |
|-----------|-------------------|---------------|
| Rotation > 15° | DeskewFilter может прекратить работу | Выполнить предварительное вращение вручную или использовать фильтр более широкого диапазона |
| Extremely low resolution ( < 100 dpi ) | Повышение контраста не может восстановить детали | Сначала пересэмплировать изображение (например, `ResampleFilter`) |
| Mixed noise (Gaussian + salt‑pepper) | Одного `DenoiseFilter` недостаточно | Подключить `GaussianBlurFilter` перед `DenoiseFilter` |
| Color scans with colored text | Требуется преобразование в градации серого | Вставить `GrayscaleFilter` перед повышением контраста |

Предвидя эти сценарии, вы экономите часы отладки в дальнейшем.

## Полный рабочий пример (все в одном)

Ниже представлен автономный класс Java, который вы можете добавить в любой проект Maven или Gradle, включающий зависимость `com.example.ocr`. Он демонстрирует **how to deskew image**, **remove salt pepper** шум и **preprocess images OCR**‑стиль.

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**Expected output** (при условии, что `scanned-document.png` содержит чёткий счёт):

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

Если заменить изображение на уже идеально выровненное, вы заметите, что конвейер всё равно работает — ничего не ломается, и точность OCR остаётся высокой.

## Заключение

Теперь у вас есть прочное понимание **how to deskew image** и того, почему каждый шаг предобработки — **image preprocessing OCR**, **remove salt pepper**, и **preprocess images OCR** — играет решающую роль в получении чистого, пригодного для поиска текста. Приведённый выше пример является полным,

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Calculate Skew Angle for OCR Image Preprocessing](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}