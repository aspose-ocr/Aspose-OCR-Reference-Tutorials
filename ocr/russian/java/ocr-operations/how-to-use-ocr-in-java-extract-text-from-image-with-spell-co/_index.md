---
category: general
date: 2026-05-06
description: Как использовать OCR для извлечения текста из изображения в Java. Узнайте
  о преобразовании изображения в текст с помощью OCR, исправлении ошибок OCR и загрузке
  изображения для OCR с помощью Aspose OCR.
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: ru
og_description: Как использовать OCR в Java для извлечения текста из изображения,
  исправления ошибок OCR и загрузки изображения для OCR с помощью Aspose OCR.
og_title: Как использовать OCR в Java – Полное руководство
tags:
- OCR
- Java
- Aspose
title: Как использовать OCR в Java — извлечение текста из изображения с исправлением
  орфографии
url: /ru/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR в Java – извлечение текста из изображения с исправлением орфографии

Когда‑нибудь задумывались **как использовать OCR**, чтобы превратить размытое фото чека в чистый, индексируемый текст? Вы не одиноки. Во многих проектах — приложениях для учёта расходов, конвейерах оцифровки счетов или даже в быстром скрипте для заметок — получение надёжного текста из изображения является первой преградой.  

Этот учебник покажет вам точно, как использовать OCR в Java, охватывая всё от загрузки изображения для OCR до исправления ошибок OCR, чтобы результат выглядел так, как будто его набрал человек. К концу вы сможете **извлекать текст из изображения**, выполнять преобразование **OCR image to text** и автоматически исправлять распространённые ошибки распознавания.

## Что вы построите

Мы создадим небольшую консольную программу на Java, которая:

1. Загружает PNG (или любой поддерживаемый формат) в движок Aspose OCR.  
2. Включает встроенную функцию исправления орфографии для **коррекции ошибок OCR**.  
3. Запускает процесс распознавания и выводит очищенный текст.  

Никаких внешних сервисов, никаких тяжёлых фреймворков — только один JAR‑файл и несколько строк кода.

### Предварительные требования

- Java Development Kit (JDK) 8 или новее.  
- Maven (или любой другой инструмент сборки) для получения библиотеки Aspose OCR.  
- Файл изображения (например, `receipt.png`), который вы хотите проанализировать.  

Если у вас нет JAR‑файла Aspose OCR, добавьте эту зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **Pro tip:** Бесплатная оценочная версия подходит для тестирования, но лицензия убирает водяной знак оценки.

## Шаг 1 – Initialise the OCR Engine (Primary Keyword in Action)

Первое, что нужно сделать, — создать экземпляр `OcrEngine`. Считайте его мозгом, который будет читать пиксели и превращать их в символы.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*Почему это важно:* Инициализация движка подготавливает внутренние ресурсы (языковые модели, словари и т.д.). Пропуск этого шага приведёт к `NullPointerException` позже, когда вы попытаетесь загрузить изображение.

## Шаг 2 – Load Image for OCR

Теперь мы действительно **загружаем изображение для OCR**. Aspose предоставляет удобный помощник `ImageStream.fromFile`, но вы также можете передать `byte[]`, если предпочитаете.

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*Распространённая ошибка:* Путь к файлу должен быть абсолютным или относительным к рабочей директории. Если изображение не найдено, движок бросит `IOException`. Проверьте путь, особенно при запуске из IDE versus упакованного JAR‑файла.

## Шаг 3 – Enable Spell Correction to **Correct OCR Errors**

Стандартный OCR может быть шумным — представьте «l0ve» вместо «love» или «0» вместо «O». Включение исправления орфографии заставляет движок выполнить пост‑обработку, исправляющую типичные ошибки.

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*Зачем это нужно:* Без исправления орфографии вам придётся вручную чистить вывод, что сводит автоматизацию к нулю. Встроенный словарь хорошо работает для английского и нескольких других языков.

## Шаг 4 – Perform the Recognition (**OCR Image to Text**)

С изображением, загруженным и включённым исправлением орфографии, мы наконец можем попросить движок распознать текст.

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*Пограничный случай:* Если изображение имеет низкий контраст или сильно искажено, результат всё равно может содержать мусор. Рассмотрите предобработку (например, бинаризацию, выравнивание) перед передачей в движок.

## Шаг 5 – Output the Cleaned‑Up Text

Последний шаг — просто вывести результат. В реальном приложении вы, вероятно, запишете его в базу данных или файл, но для этой демонстрации достаточно `System.out`.

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Ожидаемый вывод

Предположим, `receipt.png` содержит чёткий список товаров, вы можете увидеть что‑то вроде:

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

Обратите внимание, как «Qty» и «Price» написаны правильно, даже если исходный скан имел ошибку «Qy».

## Полный рабочий пример

Ниже полная программа, которую можно скопировать в файл с именем `SpellCorrectDemo.java`. Убедитесь, что JAR‑файл Aspose OCR находится в вашем classpath.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

Запустите её с помощью:

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

Теперь вы должны увидеть очищенный текст, напечатанный в консоли.

## Bonus: Tweaking Settings for Better Accuracy

Хотя конфигурация по умолчанию подходит для большинства печатных документов, в специализированных сценариях может потребоваться настроить несколько параметров:

| Параметр | Что делает | Когда менять |
|----------|------------|--------------|
| `setLanguage(OcrLanguage.English)` | Принудительно использует английский словарь (снижает количество ложных срабатываний) | Если изображение содержит только английский текст. |
| `setResolution(300)` | Указывает движку DPI исходного изображения | Для сканов высокого разрешения. |
| `setEnableAutoSkewCorrection(true)` | Автоматически вращает слегка наклонённые страницы | Когда изображения сняты с телефона. |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## Часто задаваемые вопросы

**Q: Работает ли это с PDF?**  
A: Да. Преобразуйте каждую страницу PDF в изображение (например, с помощью Aspose PDF) и передайте изображение в OCR‑движок.

**Q: Что если моё изображение в формате BMP?**  
A: `ImageStream.fromFile` поддерживает PNG, JPEG, BMP, TIFF и GIF «из коробки». Просто измените расширение файла.

**Q: Можно ли отключить исправление орфографии?**  
A: Конечно — установите `setEnableSpellCorrection(false)`, если вам нужен «сырой» вывод OCR для последующей обработки.

## Заключение

Теперь вы знаете **как использовать OCR** в Java для **извлечения текста из изображения**, автоматической **коррекции ошибок OCR** и правильной **загрузки изображения для OCR** с помощью Aspose OCR. Пятишаговый процесс — инициализация, загрузка, включение исправления орфографии, распознавание и вывод — покрывает большинство повседневных задач OCR.  

Далее вы можете связать эту логику с записью в базу данных, REST‑эндпоинтом или пакетным процессором, чтобы обрабатывать десятки чеков одновременно. Поэкспериментируйте с таблицей дополнительных настроек выше, чтобы выжать из OCR каждый последний символ точности.

Счастливого кодинга, и пусть результаты вашего OCR всегда чище, чем ваши кофе‑запятнанные чеки! 

![диаграмма как использовать OCR, показывающая поток изображение → OCR engine → исправленный текст flow]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}