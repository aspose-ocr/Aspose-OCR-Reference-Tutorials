---
category: general
date: 2026-02-17
description: Узнайте, как распознавать текст с изображения и загружать изображение
  для OCR с помощью библиотеки Aspose OCR Java. Пошаговое руководство со спелл‑корректором.
draft: false
keywords:
- recognize text from image
- load image for OCR
- Aspose OCR Java
- spell corrector OCR
- OCR engine setup
language: ru
og_description: Распознавать текст с изображения с помощью Aspose OCR Java. Этот учебник
  показывает, как загрузить изображение для OCR, включить исправление орфографии и
  вывести чистый текст.
og_title: распознавание текста с изображения – Полное руководство по Aspose OCR на
  Java
tags:
- Java
- OCR
- Aspose
title: Распознавание текста с изображения с помощью Aspose OCR – учебник Java
url: /ru/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-tutorial/
---

translate.

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# распознавание текста с изображения с помощью Aspose OCR – Java Tutorial

Когда‑то вам нужно было **распознать текст с изображения**, но вы не знали, какую библиотеку выбрать? Вы не одиноки. Во многих реальных проектах — сканирование счетов, оцифровка рукописных заметок или извлечение подписей из скриншотов — точные результаты OCR имеют решающее значение.  

В этом руководстве мы пройдем процесс загрузки изображения для OCR, включения встроенного корректора орфографии Aspose OCR и вывода очищенного текста. К концу вы получите готовую к запуску Java‑программу, которая **распознает текст с изображения** всего несколькими строками кода.

## Что покрывает этот учебник

- Как применить вашу лицензию Aspose OCR (чтобы демо‑версия работала без водяных знаков)  
- Создание экземпляра `OcrEngine` и выбор английского языка распознавания  
- **Load image for OCR** с помощью `OcrInput` и указание PNG‑файла, содержащего ошибки в написании слов  
- Включение корректора орфографии, при желании указание собственного словаря  
- Запуск распознавания и вывод исправленного результата  

Никаких внешних сервисов, никаких скрытых файлов конфигурации — только чистый Java и JAR Aspose OCR.

> **Pro tip:** Если вы новичок в Aspose, получите бесплатную 30‑дневную пробную лицензию на сайте Aspose и поместите файл `.lic` в папку, доступную из вашего кода.

## Предварительные требования

- Java 8 или новее (код также компилируется с JDK 11)  
- Aspose.OCR for Java JAR в вашем classpath  
- Действительный файл `Aspose.OCR.lic` (или можно работать в режиме оценки, но демо будет содержать водяной знак)  
- Файл изображения (`misspelled.png`), содержащий текст с намеренными орфографическими ошибками — идеально подходит для демонстрации работы корректора  

Все готово? Отлично — приступаем.

## Шаг 1: Примените вашу лицензию Aspose OCR

Прежде чем движок начнёт работу, он должен знать, что у вас есть лицензия. Иначе в выводе появится баннер «Trial version».

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – replace the path with where you stored your .lic file
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

*Почему это важно:* Лицензирование отключает водяной знак пробной версии и открывает полный словарь корректора орфографии. Пропустить этот шаг можно, но вывод будет загрязнён текстом «Aspose OCR Demo».

## Шаг 2: Создайте и настройте OCR‑движок

Теперь мы инициализируем движок и указываем, какой язык использовать. Английский — самый распространённый, но Aspose поддерживает десятки языков.

```java
        // Step 2: Instantiate the OCR engine
        OcrEngine engine = new OcrEngine();

        // Choose English for recognition – you could pick French, German, etc.
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);
```

*Почему мы задаём язык:* Языковая модель определяет набор символов и влияет на предложения корректора орфографии. Выбор неправильного языка может резко снизить точность.

## Шаг 3: Включите коррекцию орфографии и (при желании) укажите собственный словарь

Aspose OCR поставляется со встроенным английским словарём, но вы можете задать свой, если у вас есть термины специфической области (например, медицинская терминология или коды продуктов).

```java
        // Step 3: Turn on the spell corrector
        engine.getSpellCorrector().setEnable(true); // activate spell‑checking

        // Optional: use a custom dictionary folder
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english");
```

*Что делает корректор:* Когда OCR‑движок встречает слово, отсутствующее в словаре, он пытается заменить его на самое близкое совпадение. Поэтому демо может автоматически превратить «recieve» в «receive».

## Шаг 4: Загрузите изображение для OCR

Это часть, которая напрямую отвечает на **load image for OCR**. Мы создаём объект `OcrInput` и добавляем наш PNG‑файл.

```java
        // Step 4: Prepare the image input
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // path to the image you want to process
```

*Почему мы используем `OcrInput`:* Он абстрагирует логику чтения файлов и позволяет позже добавить несколько страниц, если понадобится обработать многостраничный PDF или набор изображений.

## Шаг 5: Запустите распознавание и получите исправленный текст

Теперь движок выполняет основную работу — распознаёт символы, применяет языковую модель и в конце корректирует орфографию.

```java
        // Step 5: Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Step 6: Output the corrected text to the console
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

*Ожидаемый вывод:* Предположим, `misspelled.png` содержит фразу «Ths is a smple test», консоль выведет:

```
Corrected text:
This is a simple test
```

Обратите внимание, как ошибочные слова (`Ths`, `smple`) автоматически исправлены.

## Полный готовый к запуску пример

Ниже представлен весь код программы в одном блоке. Скопируйте, поправьте пути и нажмите **Run**.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose.OCR license (replace with your license file)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Select the language for recognition (e.g., English)
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);

        // Enable the built‑in spell corrector and optionally set a custom dictionary
        engine.getSpellCorrector().setEnable(true);                     // activate spell‑checking
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english"); // optional

        // Prepare the input image containing the text to be recognized
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // load image for OCR

        // Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Output the corrected text
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

**Подсказка:** Если хотите обработать JPEG или BMP вместо PNG, просто измените расширение файла — Aspose OCR поддерживает все распространённые растровые форматы.

## Часто задаваемые вопросы и особые случаи

- **Что делать, если изображение низкого разрешения?**  
  Увеличьте DPI перед передачей в Aspose, пересчитав изображение с помощью библиотеки вроде `java.awt.Image`. Большее DPI даёт движку больше пикселей, что обычно повышает точность.

- **Можно ли распознавать несколько языков в одном изображении?**  
  Да. Вызовите `engine.getLanguage().setLanguage(OcrLanguage.MULTI_LANGUAGE);` и при желании добавьте список языков через `engine.getLanguage().addLanguage(OcrLanguage.SPANISH);`.

- **Мой собственный словарь не используется — почему?**  
  Убедитесь, что папка содержит обычные текстовые файлы с одним словом на строку и что путь указан абсолютный или правильно относительный к рабочей директории.

- **Как извлечь оценки уверенности?**  
  `result.getConfidence()` возвращает `float` от 0 до 1 для всей страницы. Для уверенности по отдельным символам изучите `result.getWordList()`.

## Заключение

Теперь вы знаете, как **распознавать текст с изображения** с помощью Aspose OCR для Java, как **загружать изображение для OCR** и как включить корректор орфографии для исправления типичных опечаток. Полный пример выше готов к интеграции в любой Maven‑ или Gradle‑проект, а с небольшими изменениями его можно масштабировать для пакетной обработки папок, подключить к веб‑сервису или интегрировать в систему управления документами.

Готовы к следующему шагу? Попробуйте обработать многостраничный PDF, поэкспериментируйте с собственным словарём для отраслевой терминологии или передайте результат в API перевода. Возможности безграничны, а основной шаблон — лицензия → движок → язык → корректор → ввод → распознавание → вывод — остаётся неизменным.

Счастливого кодинга, и пусть ваши результаты OCR всегда будут безупречными!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}