---
category: general
date: 2026-02-19
description: Узнайте, как исправлять наклон изображения и удалять шум для OCR. В этом
  руководстве показано, как распознавать текст на изображении, корректировать вращение
  изображения и предварительно обрабатывать изображение для OCR с помощью Aspose OCR.
draft: false
keywords:
- how to deskew image
- recognize text image
- how to remove noise
- correct image rotation
- preprocess image ocr
language: ru
og_description: Как исправить наклон изображения и удалить шум, чтобы быстро распознавать
  текст на изображении. Следуйте этому руководству, чтобы скорректировать вращение
  изображения и предобработать его для OCR с помощью Aspose.
og_title: Как выпрямить изображение — Полный учебник по предобработке OCR
tags:
- OCR
- Java
- Image Processing
title: Как выпрямить изображение — пошаговое руководство по предобработке OCR
url: /ru/java/ocr-operations/how-to-deskew-image-step-by-step-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как исправить наклон изображения — Полный учебник по предобработке OCR

Когда‑нибудь задумывались **как исправить наклон изображения** перед передачей его в OCR‑движок? Возможно, вы отсканировали партию чеков, и страницы выглядят слегка наклонёнными, или скан содержит случайные точки. Это распространённая проблема — наклонные, шумные картинки мешают распознаванию текста.  

Хорошие новости? Вы можете выпрямить (correct image rotation) и избавиться от шума (how to remove noise) всего в несколько строк Java с помощью Aspose.OCR. В этом руководстве мы пройдём весь процесс: от загрузки шумного‑наклонного PNG, применения deskew + median denoise, до **recognize text image** и вывода результата. К концу у вас будет переиспользуемый фрагмент кода, который можно вставить в любой Java‑проект.

## Что понадобится

- **Java 17** или новее (код компилируется и в более старых версиях, но 17 — оптимальный вариант).  
- **Aspose.OCR for Java** — скачайте последнюю JAR‑ку из Maven Central (`com.aspose:aspose-ocr`).  
- Файл изображения, который одновременно наклонён и зашумлён (например, `noisy-rotated.png`).  
- Любая удобная IDE (IntelliJ, Eclipse или даже VS Code).  

Никаких сложных систем сборки не требуется; простая команда `javac` + `java` работает отлично.

---

## Шаг 1 — Создание экземпляра OCR‑движка  

Первое, что нужно сделать, — создать `OcrEngine`. Это как мозг, который позже будет читать символы за вас.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Совет:** Делайте движок синглтоном, если обрабатываете много изображений; он переиспользует внутренние буферы и ускоряет работу.

## Шаг 2 — Включение Deskew и Median Denoise (Как удалить шум)

Теперь мы говорим движку **correct image rotation** и **how to remove noise**. Оба фильтра необязательны, но вместе они значительно повышают точность.

```java
        // Turn on preprocessing filters
        ocrEngine.getPreprocessing().setDeskew(true);          // fixes rotation
        ocrEngine.getPreprocessing().setMedianDenoise(true);   // smooths out speckles
```

Почему median denoise? Он сохраняет границы (линии, определяющие символы), одновременно удаляя одиночные пиксели — именно то, что нужно для чистого OCR.

## Шаг 3 — Загрузка изображения для обработки  

Здесь мы указываем движку файл, который нуждается в очистке. `ImageStream.fromFile` читает PNG в память.

```java
        // Load the noisy‑rotated image
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/noisy-rotated.png"));
```

Если ваше изображение находится на удалённом сервере, просто передайте `InputStream` — Aspose обработает его без проблем.

## Шаг 4 — Запуск OCR и получение распознанного текста  

С включённой предобработкой движок теперь читает выпрямленное изображение. Вызов `recognize()` возвращает `RecognitionResult`, содержащий извлечённую строку.

```java
        // Perform OCR – the engine automatically applies deskew & denoise first
        String recognizedText = ocrEngine.recognize().getText();

        // Show the output
        System.out.println("=== Recognized Text ===");
        System.out.println(recognizedText);
    }
}
```

В консоли вы должны увидеть чистый, читаемый текст, даже если исходное изображение было наклонённым и зернистым.

## Шаг 5 — Проверка результата (Что ожидать)

Когда всё работает, консоль выводит что‑то вроде:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑02‑15
Total: $1,234.56
```

Если вывод всё ещё содержит искажённые символы, проверьте:

- Разрешение изображения (≥ 300 dpi — идеально).  
- Правильность пути к файлу.  
- Может, помогут дополнительные фильтры (например, `setContrastStretch`).

---

## Необязательно: визуальная проверка на примере изображения  

Ниже небольшая превью‑версия наклонённого, шумного чека. Обратите внимание на наклон — наш код выпрямит его для вас.

![пример исправления наклона изображения](deskew-demo.png "пример исправления наклона изображения")

*Alt text: пример исправления наклона изображения — до и после обработки.*

---

## Часто задаваемые вопросы

### Работает ли это с PDF или только с PNG/JPEG?  
Aspose.OCR умеет читать PDF напрямую; просто замените `ImageStream.fromFile` на `ImageStream.fromPdf`. Те же флаги предобработки применяются, так что вы всё равно получаете **how to deskew image** и **how to remove noise**.

### Что если мне нужно сохранить оригинальную ориентацию для последующих шагов?  
Можно клонировать изображение перед предобработкой:

```java
Image original = ocrEngine.getImage().clone();
ocrEngine.getPreprocessing().apply(); // modifies the internal copy
// Use original later if needed
```

### Можно ли задать угол deskew вручную?  
Да — `setDeskewAngle(double degrees)` позволяет переопределить алгоритм автоопределения. Полезно, когда автоопределение не справляется с экстремальными наклонами.

### Чем отличается median denoise от Gaussian blur?  
Median‑фильтры заменяют каждый пиксель медианой соседних, сохраняя границы. Gaussian blur размывает всё, что может размыть штрихи символов — поэтому median считается более безопасным выбором для OCR.

---

## Подведение итогов  

В этом учебнике мы рассмотрели **how to deskew image**, продемонстрировали **how to remove noise** и показали, как **recognize text image** с помощью встроенной предобработки Aspose OCR. Включив `setDeskew(true)` и `setMedianDenoise(true)`, вы автоматически **correct image rotation** и убираете пятна, превращая грязный скан в чистую строку текста.  

Экспериментируйте: пробуйте разные стратегии шумоподавления, обрабатывайте PDF или объединяйте несколько изображений в цикле. Один и тот же шаблон — engine → preprocess → recognize — подойдёт для любой задачи, делая эту основу надёжной для любой OCR‑конвейера.

**Следующие шаги**, которые стоит изучить:

- **Пакетная обработка** — итерация по папке изображений и запись каждого результата в файл `.txt`.  
- **Языковые пакеты** — загрузка словаря конкретного языка для повышения точности распознавания неанглийского текста.  
- **Продвинутые фильтры** — например, `setContrastStretch` или `setBinarization` для сканов с низким контрастом.  

Есть вопросы? Оставляйте комментарий, и удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}