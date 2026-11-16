---
category: general
date: 2026-03-07
description: Запустите OCR на изображении с помощью Java. Узнайте, как распознавать
  текст из PNG, извлекать текст из чека и загружать изображение для OCR с полным примером
  Java OCR.
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: ru
og_description: Запустите OCR на изображении с помощью Java. Это руководство показывает,
  как распознавать текст из PNG, извлекать текст из чека и загружать изображение для
  OCR, используя полный пример OCR на Java.
og_title: Запустите OCR на изображении с помощью Java – извлечение текста с использованием
  GPU
tags:
- OCR
- Java
- GPU
- Image Processing
title: Запуск OCR на изображении с помощью Java – извлечение текста с использованием
  GPU
url: /ru/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Запуск OCR на изображении с Java – ускоренное извлечение текста с помощью GPU

Когда‑то вам нужно было **запустить OCR на изображении**, но вы не знали, с чего начать в Java? Вы не одиноки — многие разработчики сталкиваются с тем же самым, когда впервые пытаются извлечь текст из отсканированного чека или скриншота PNG.  

В этом руководстве мы пройдёмся по **полному примеру OCR на Java**, который не только **распознаёт текст из PNG**‑файлов, но и показывает, как **извлекать текст из изображений чеков**, используя ускорение GPU для повышения скорости. К концу вы получите готовую к запуску программу, которая загружает изображение для OCR, обрабатывает его и выводит результат в виде простого текста.

## Что вы узнаете

- Как **загрузить изображение для OCR** с помощью простого `ImageInputStream`.
- Как включить поддержку GPU, чтобы движок работал быстрее на современном оборудовании.
- Точные шаги для **распознавания текста из PNG** и получения полезных строк из чека.
- Распространённые подводные камни (например, неверный ID GPU‑устройства) и рекомендации по лучшим практикам.
- Полный, готовый к запуску фрагмент кода, который можно скопировать и вставить в свою IDE.

**Требования**

- Java 17 или новее (в коде используется ключевое слово `var` для краткости, но вы можете заменить его на явные типы, если используете Java 8).
- OCR‑библиотека, предоставляющая классы `OcrEngine`, `ImageInputStream` и `OcrResult` (например, вымышленный SDK *FastOCR*; замените на реальную библиотеку, которую используете).
- Машина с поддержкой GPU, если вы хотите получить ускорение производительности (необязательно, но рекомендуется).

---

## Шаг 1: Запуск OCR на изображении – включение ускорения GPU

Первое, что нужно сделать, — создать OCR‑движок и указать ему использовать GPU. Этот шаг критически важен, потому что без поддержки GPU движок переходит на CPU, что может заметно замедлить обработку изображений высокого разрешения, например чеков.

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**Почему это важно:**  
Ускорение GPU разгружает тяжёлые матричные вычисления, которые выполняют OCR‑движки. Если у вас несколько GPU, вы можете выбрать тот, у которого больше памяти, изменив значение `setGpuDeviceId`. Забвение включить GPU — частая причина жалоб «почему мой OCR такой медленный?».

> **Совет:** Если в вашей машине нет совместимого GPU, вызов `setUseGpu(true)` просто будет проигнорирован — не произойдёт сбоя, просто обработка будет медленнее.

---

## Шаг 2: Загрузка изображения для OCR

Теперь, когда движок готов, нам нужно передать ему изображение. Пример ниже показывает, как загрузить PNG‑чек, хранящийся на диске. Вы можете заменить путь на любой другой формат, поддерживаемый вашей OCR‑библиотекой.

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**Пограничный случай:**  
Если файл не существует или путь указан неверно, `ImageInputStream` бросит `IOException`. Оберните вызов в блок `try‑catch` и выведите полезное сообщение в лог:

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## Шаг 3: Распознавание текста из PNG

После загрузки изображения OCR‑движок может приступить к работе. Этот шаг действительно **распознаёт текст из PNG** (или любого другого поддерживаемого формата) и возвращает объект `OcrResult`.

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**Что происходит «под капотом»?**  
Движок выполняет предварительную обработку (выравнивание, бинаризацию), запускает нейронную сеть для обнаружения символов и затем собирает их в строки текста. Поскольку мы включили GPU ранее, вычисления нейронной сети происходят на видеокарте, экономя секунды общего времени выполнения.

---

## Шаг 4: Извлечение текста из чека

После распознавания обычно требуется получить «чистый» текст. Класс `OcrResult`, как правило, предоставляет метод `getText()`, который возвращает один `String`. Затем вы можете выполнить пост‑обработку (например, регулярные выражения для извлечения сумм, дат и т.д.).

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Типичный вывод чека:**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Теперь вы можете передать эту строку в собственный парсер, чтобы извлечь общую сумму, позиции товаров или информацию о налогах.

---

## Шаг 5: Полный пример OCR на Java – готов к запуску

Объединив всё вместе, получаем **полный пример OCR на Java**, который можно поместить в файл `Main.java`. Убедитесь, что OCR‑библиотека находится в classpath.

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Ожидаемый вывод в консоль** (при условии, что используется пример чека выше):

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Если вывод выглядит «мусорным», проверьте, что изображение чёткое (высокое DPI) и что языковой пакет OCR соответствует языку вашего чека.

---

## Часто задаваемые вопросы и подводные камни

| Вопрос | Ответ |
|----------|--------|
| *Что делать, если мой GPU не обнаружен?* | Движок автоматически переключится на CPU. Проверьте драйверы и убедитесь, что `setGpuDeviceId` указывает на существующее устройство (`nvidia-smi` в Linux может помочь). |
| *Можно ли обрабатывать JPEG или TIFF файлы?* | Да — просто измените расширение файла в `ImageInputStream`. OCR‑библиотека обычно автоматически определяет формат. |
| *Есть ли способ пакетно обрабатывать множество чеков?* | Оберните код распознавания в цикл и переиспользуйте один экземпляр `OcrEngine`; повторная инициализация для каждого изображения тратит GPU‑память. |
| *Как улучшить точность при низком контрасте чеков?* | Предобработайте изображение (увеличьте контраст, переведите в градации серого) перед передачей в OCR‑движок. Некоторые библиотеки предоставляют API `preprocess`. |

---

## Заключение

Теперь вы знаете, **как запускать OCR на изображениях** в Java, от загрузки картинки до извлечения чистого текста из чека. Руководство охватило **распознавание текста из PNG**, **извлечение текста из чека** и показало **пример OCR на Java**, который можно адаптировать под любой проект.  

Что дальше? Попробуйте отключить флаг GPU, чтобы увидеть разницу в производительности, поэкспериментируйте с различными разрешениями изображений или интегрируйте парсер на основе регулярных выражений для автоматического извлечения сумм. Если интересуют более продвинутые темы, изучите **пост‑обработку OCR**, **коррекцию с помощью языковых моделей** или **пакетные конвейеры обработки**.

Счастливого кодинга, и пусть ваши чеки всегда читаются!  

![run OCR on image example](/images/run-ocr-on-image.png "run OCR on image – Java example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}