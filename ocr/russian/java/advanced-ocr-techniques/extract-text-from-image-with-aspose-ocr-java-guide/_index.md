---
category: general
date: 2026-02-14
description: Извлекайте текст из изображения с помощью Aspose OCR на Java. Узнайте,
  как извлекать текст из полей формы с областями интереса для точных результатов.
draft: false
keywords:
- extract text from image
- extract text from form
language: ru
og_description: Извлечение текста из изображения с помощью Aspose OCR на Java. Этот
  учебник показывает, как извлекать текст из полей формы через области интереса.
og_title: Извлечение текста из изображения с помощью Aspose OCR – руководство по Java
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Извлечение текста из изображения с помощью Aspose OCR – руководство по Java
url: /ru/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/
---

keep line breaks.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения с помощью Aspose OCR – Руководство на Java

Когда‑нибудь вам нужно было **извлечь текст из изображения**, но вы в итоге парсили всю картинку, тратя процессорное время и получая шумные результаты? Вы не одиноки. Во многих реальных приложениях — например, сканерах счетов, считывателях паспортов или формах ввода данных — вам нужны лишь несколько полей, а не весь холст.  

Хорошая новость в том, что Aspose OCR позволяет **извлекать текст из изображения** *и* из конкретных областей формы, определяя полигоны. В этом руководстве вы увидите, как **извлекать текст из полей формы** с помощью Java, почему этот подход важен и что можно настроить, если что‑то пойдёт не так.

Ниже мы рассмотрим всё — от настройки библиотеки до обработки сложных граничных случаев, так что к концу у вас будет готовый к запуску фрагмент кода, который извлекает только нужные данные.

## Что понадобится

- Java 17 (или любой современный JDK) — более новые версии имеют лучшую поддержку Unicode.  
- Aspose.OCR for Java 23.10 (или последняя версия на момент чтения).  
- Пример изображения с именем `form.png`, содержащий чётко определённые поля.  
- IDE или простой текстовый редактор — IntelliJ IDEA, VS Code или даже Notepad подойдёт.

Для базовой демонстрации не требуется магия Maven/Gradle; просто добавьте JAR Aspose OCR в ваш classpath.

---

## Шаг 1 – Инициализация OCR‑движка и загрузка изображения

Первому, что нужен движку, — это bitmap для обработки. Мы укажем ему `form.png`, который находится в той же папке, что и исходный файл.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the source image – replace the path if your file lives elsewhere
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));
```

*Почему это важно:*  
Создание нового `OcrEngine` даёт чистый старт, гарантируя, что прежние настройки не повлияют на ваш запуск. Раннее загрузка изображения также проверяет существование файла, поэтому вы получаете полезное исключение до того, как потратите время на последующие шаги.

> **Совет:** Если ваше изображение огромное (более 5 МБ), рассмотрите возможность его предварительного масштабирования. Aspose OCR работает быстрее с изображениями размером менее 2000 px по любой из сторон.

---

## Шаг 2 – Определение полигонов для полей, которые нужно прочитать

*Region of Interest* (ROI) — это просто полигон, указывающий движку, где искать. Ниже мы создаём два прямоугольника — один для «First Name» и другой для «Date of Birth». Отрегулируйте координаты под вашу форму.

```java
        // Polygon for the first field (e.g., First Name)
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},   // X‑coordinates
                new int[]{100, 100, 150, 150}, // Y‑coordinates
                4);

        // Polygon for the second field (e.g., Date of Birth)
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);
```

*Почему полигоны, а не прямоугольники?*  
Полигоны дают гибкость для обработки наклонённых или нелинейных полей — часто встречается при сканировании печатных форм, которые не выровнены идеально.

---

## Шаг 3 – Инструктировать Aspose OCR фокусироваться только на этих областях

Теперь мы привязываем полигоны к движку. Метод `setRegionsOfInterest` принимает список, поэтому вы можете добавить столько полей, сколько захотите.

```java
        // Limit OCR to the defined regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));
```

*Что происходит под капотом?*  
Aspose OCR обрезает каждый полигон в отдельный bitmap, запускает алгоритм распознавания и затем объединяет результаты. Это значительно уменьшает количество ложных срабатываний от окружающей графики.

---

## Шаг 4 – Запуск процесса OCR

После полной настройки мы запускаем OCR. Вызов `process()` возвращает объект `OcrResult`, содержащий извлечённый текст и оценки уверенности.

```java
        // Execute OCR on the selected ROIs
        OcrResult ocrResult = ocrEngine.process();
```

Если вам нужна уверенность по каждому полю, можно посмотреть `ocrResult.getRegions()` — каждый регион имеет свою оценку. Для большинства простых форм достаточно общего текста.

---

## Шаг 5 – Вывод (или сохранение) извлечённого текста

Наконец, мы выводим результат в консоль. В реальном приложении вы можете записать его в базу данных, JSON‑файл или отправить через API.

```java
        // Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Ожидаемый вывод (пример):**

```
=== Extracted Text ===
John Doe
12/04/1990
```

Эти две строки соответствуют двум полигоном, которые мы определили. Если видите лишние пробелы, удалите их с помощью `String.trim()`.

---

## Как извлекать текст из формы, когда полей много

Когда форма содержит десятки полей, вручную вводить координаты становится утомительно. Вот быстрый шаблон, который можно использовать:

1. **Создайте CSV**, где каждая строка содержит `fieldName, x1, y1, x2, y2, x3, y3, x4, y4`.  
2. **Загрузите CSV** во время выполнения, пройдитесь по каждой строке, создайте `Polygon` и добавьте его в список ROI.  

```java
List<Polygon> rois = new ArrayList<>();
try (BufferedReader br = new BufferedReader(new FileReader("fields.csv"))) {
    String line;
    while ((line = br.readLine()) != null) {
        String[] parts = line.split(",");
        int[] xs = { Integer.parseInt(parts[1]), Integer.parseInt(parts[3]),
                    Integer.parseInt(parts[5]), Integer.parseInt(parts[7]) };
        int[] ys = { Integer.parseInt(parts[2]), Integer.parseInt(parts[4]),
                    Integer.parseInt(parts[6]), Integer.parseInt(parts[8]) };
        rois.add(new Polygon(xs, ys, 4));
    }
}
ocrEngine.getEngineOptions().setRegionsOfInterest(rois);
```

*Зачем это нужно?*  
Автоматизация генерации ROI позволяет переиспользовать один и тот же Java‑код для разных макетов форм, поддерживая принцип DRY (Don’t Repeat Yourself).

---

## Граничные случаи и советы, о которых вы могли не подумать

- **Повернутые сканы:** Если всё изображение повернуто, вызовите `ocrEngine.getEngineOptions().setRotateAngle(degrees)`.  
- **Низкий контраст:** Установите `ocrEngine.getEngineOptions().setContrast(1.5f)`, чтобы улучшить читаемость.  
- **Нелатинские скрипты:** Переключите язык с помощью `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.Spanish)` (или любого поддерживаемого языка).  
- **Частичные сбои OCR:** Всегда проверяйте `ocrResult.getConfidence()`; если она падает ниже 80 %, рассмотрите возможность запроса у пользователя ручной проверки.  

---

## Полный рабочий пример (готовый к копированию и вставке)

Ниже полная программа, готовая к компиляции и запуску. Замените `YOUR_DIRECTORY` на папку, где находится `form.png`.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Step 1 – Initialize engine and load image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));

        // Step 2 – Define polygons for each form field
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},
                new int[]{100, 100, 150, 150},
                4);
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);

        // Step 3 – Limit OCR to those regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));

        // Step 4 – Run OCR
        OcrResult ocrResult = ocrEngine.process();

        // Step 5 – Show the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Скомпилировать с помощью:

```bash
javac -cp "aspose-ocr-23.10.jar" MultiRoiDemo.java
java -cp ".:aspose-ocr-23.10.jar" MultiRoiDemo
```

Вы должны увидеть две строки текста, принадлежащие определённым ROI.

---

## Часто задаваемые вопросы

**В: Работает ли это с PDF?**  
О: Не напрямую. Сначала преобразуйте каждую страницу PDF в изображение (например, с помощью Aspose PDF), а затем передайте изображение в OCR‑движок.

**В: Что делать, если в форме есть флажки?**  
О: OCR не может читать булевы состояния, но вы можете рассматривать область флажка как ROI и проверять плотность пикселей, чтобы определить наличие отметки.

**В: Можно ли извлечь текст из многостраничной формы за один проход?**  
О: Пройдитесь по каждому изображению страницы, переиспользуйте тот же список ROI и объедините результаты.

---

## Заключение

Мы прошли полный сквозной процесс **извлечения текста из изображения** с помощью Aspose OCR и показали, как та же техника позволяет **извлекать текст из полей формы** с точной точностью. Определяя полигоны, ограничивая фокус движка и учитывая распространённые подводные камни, вы получаете быстрые, чистые данные без нагрузки на обработку всей картинки.

Готовы к следующему шагу? Попробуйте передать вывод OCR в JSON‑payload или подать его в модель машинного обучения для валидации. Возможности безграничны, и теперь вы

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}