---
category: general
date: 2026-03-05
description: Как использовать OCR в C# для извлечения текста из изображений чеков.
  Узнайте, как загрузить изображение для OCR и распознать чек за несколько минут.
draft: false
keywords:
- how to use OCR
- extract text from receipt
- load image for OCR
- recognize receipt image
language: ru
og_description: как использовать OCR в C# для извлечения текста из чеков. Следуйте
  этому пошаговому руководству, чтобы загрузить изображение для OCR и эффективно распознавать
  изображение чека.
og_title: Как использовать OCR в C# — быстрое извлечение текста из чека
tags:
- OCR
- C#
- Aspose
- Receipt Processing
title: Как использовать OCR в C# — быстро извлекать текст из чеков
url: /ru/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-receipts-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# как использовать OCR в C# – быстро извлекать текст из чеков

Когда‑нибудь задумывались **как использовать OCR**, чтобы сразу получить данные из фотографии кассового чека? Вы не одиноки. Во многих приложениях для малого бизнеса узким местом является преобразование размытого PNG в структурированный текст, с которым действительно можно работать.  

Хорошие новости? С несколькими строками C# и Aspose.OCR вы можете **загрузить изображение для OCR**, запустить движок и **распознать изображение чека** менее чем за минуту. Ниже вы увидите полностью готовый пример, а также советы по сложным моментам, которые большинство руководств упускают.

## Что покрывает это руководство

Мы пройдем всё, что нужно знать:

* Установка пакета NuGet Aspose.OCR.  
* Настройка OCR‑движка – ядра **как использовать OCR** правильно.  
* Загрузка файла чека (это шаг **загрузить изображение для OCR**).  
* Запуск процесса распознавания и извлечение как JSON, так и XML‑данных о макете.  
* Обработка распространённых подводных камней, таких как отсутствие лицензии или неподдерживаемые форматы изображений.  

К концу вы получите автономную программу, которая извлекает текст из любого чека, помещённого в папку. Без внешних сервисов, без скрытой магии.

## Предварительные требования

* .NET 6 SDK или новее (код также компилируется с .NET Core).  
* Действительный файл лицензии Aspose.OCR (`Aspose.OCR.lic`). Вы можете получить бесплатную пробную версию от Aspose, если её ещё нет.  
* Пример изображения чека – `receipt.png` подойдет, но любой распространённый растровый формат тоже подойдёт.  

Если всё это уже есть, отлично – приступаем.

![how to use OCR example](https://example.com/ocr-receipt.png "how to use OCR example")

## Шаг 1: Установите Aspose.OCR и создайте новый проект

Первое, что нужно: библиотека, которая действительно делает тяжёлую работу. Откройте терминал в папке проекта и выполните:

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Эта команда создаёт консольное приложение и подтягивает последнюю версию пакета Aspose.OCR. По моему опыту, короткое название проекта упрощает чтение сгенерированных путей, особенно когда вы начинаете работать с несколькими демонстрационными приложениями.

## Шаг 2: Инициализируйте OCR‑движок – сердце **как использовать OCR**

Теперь напишем код, отвечающий на вопрос «**как использовать OCR** в C#». Откройте `Program.cs` и замените его содержимое фрагментом ниже. Обратите внимание на комментарии – они объясняют *почему* каждой строки, а не только *что* она делает.

```csharp
using System;
using System.IO;
using Aspose.OCR;          // Aspose OCR namespace
using Aspose.OCR.Image;   // For loading images

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create and configure the OCR engine.
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // Why set a license? Without it the engine runs in evaluation mode,
        // which adds a watermark to the output and limits batch size.
        ocrEngine.SetLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Load the receipt image – this is the **load image for OCR** step.
        // -------------------------------------------------
        // Change the path to point at your own receipt file.
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");

        // The ImageStream class abstracts file I/O and supports many formats.
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣ Run the recognition process – this is where we **recognize receipt image**.
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Export the layout information as JSON.
        // -------------------------------------------------
        string jsonResult = ocrResult.ToJson();
        File.WriteAllText("receipt.json", jsonResult);
        Console.WriteLine("✅ JSON saved to receipt.json");

        // -------------------------------------------------
        // 5️⃣ Export the same layout information as XML.
        // -------------------------------------------------
        string xmlResult = ocrResult.ToXml();
        File.WriteAllText("receipt.xml", xmlResult);
        Console.WriteLine("✅ XML saved to receipt.xml");

        // -------------------------------------------------
        // 6️⃣ Quick preview – print the plain text to console.
        // -------------------------------------------------
        Console.WriteLine("\n--- Extracted Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Почему это работает

* **`OcrEngine`** – точка входа; он хранит всю конфигурацию, которую можно будет менять позже (язык, DPI и т.д.).  
* **`SetLicense`** убирает водяной знак оценки – важный шаг, если планируете распространять код.  
* **`ImageStream.FromFile`** выполняет работу **загрузить изображение для OCR**, поддерживая PNG, JPEG, BMP, TIFF и другие форматы.  
* **`Recognize()`** – метод, который действительно **распознаёт изображение чека**. Под капотом он проводит бинаризацию, сегментацию и классификацию символов.  
* Экспорт в JSON и XML даёт вам как человекочитаемый дамп, так и машинно‑дружелюбную структуру, которую можно передать последующим парсерам.

## Шаг 3: Запустите демо и проверьте вывод

Скомпилируйте и выполните:

```bash
dotnet run
```

Если всё правильно подключено, вы увидите что‑то вроде:

```
✅ JSON saved to receipt.json
✅ XML saved to receipt.xml

--- Extracted Text ---
Walmart Supercenter
Date: 03/04/2026
Item    Qty   Price
Milk    2     2.58
Bread   1     1.99
Total   4.57
```

Консоль выводит простой текст, а `receipt.json` и `receipt.xml` содержат подробную информацию о макете (координаты, оценки уверенности и т.д.). Эти файлы полезны, если позже нужно сопоставить каждую строку с полем базы данных.

## Пограничные случаи и профессиональные советы

### 1️⃣ Отсутствующая или недействительная лицензия
Если `SetLicense` не сработает, движок переключится в пробный режим и в выводе появится водяной знак. Оберните вызов в try/catch и выведите дружелюбное сообщение:

```csharp
try { ocrEngine.SetLicense("Aspose.OCR.lic"); }
catch (Exception ex)
{
    Console.WriteLine("⚠️ License not found – running in trial mode.");
    Console.WriteLine(ex.Message);
}
```

### 2️⃣ Неподдерживаемые форматы изображений
Aspose.OCR поддерживает большинство растровых форматов, но если вы передаёте PDF или многостраничный TIFF, сначала нужно преобразовать нужную страницу в изображение. Для этого подойдёт библиотека `Aspose.PDF`.

### 3️⃣ Большие чеки и производительность
Обработка изображения размером 10 МБ может быть медленной. Снизьте разрешение перед передачей в движок:

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath).Resize(1024, 0);
```

Метод `Resize` сохраняет соотношение сторон (`0` для высоты) и значительно уменьшает размер файла без потери точности OCR для типичных чеков.

### 4️⃣ Проблемы с языком и шрифтами
В чеках могут встречаться специальные символы (€, ¥ и т.п.). Установите язык явно, если знаете локаль:

```csharp
ocrEngine.Language = Language.English; // or Language.Spanish, etc.
```

Для чеков с несколькими языками можно включить многоязычный режим:

```csharp
ocrEngine.Language = Language.English | Language.French;
```

### 5️⃣ Извлечение структурированных данных
Сырой текст полезен, но большинству приложений нужны структурированные поля (дата, итог, позиции). В JSON‑макете есть координаты `BoundingBox` для каждого слова. Их можно пост‑обработать так:

```csharp
var layout = Newtonsoft.Json.Linq.JObject.Parse(jsonResult);
foreach (var word in layout["Words"])
{
    string text = (string)word["Text"];
    // Simple heuristics: look for "$" or "Total"
}
```

Этот фрагмент демонстрирует идею; в продакшене, скорее всего, вы будете использовать регулярные выражения или небольшой движок правил.

## Часто задаваемые вопросы

**В: Можно ли запускать это на Linux?**  
О: Абсолютно. Aspose.OCR кроссплатформенный; просто установите .NET runtime на ваш Linux‑сервер, и тот же код будет работать.

**В: Что делать, если нужно обрабатывать десятки чеков в минуту?**  
О: Запустите цикл `Parallel.ForEach` и переиспользуйте один экземпляр `OcrEngine` – он потокобезопасен для операций только чтения. Не забудьте учесть ограничения лицензии на параллельность.

**В: Работает ли это с фотографиями, снятыми под углом?**  
О: Движок включает базовую коррекцию наклона, но для сильно искривлённых изображений имеет смысл предварительно обработать их библиотекой обработки изображений (например, OpenCV), чтобы выпрямить чек.

## Полный рабочий пример (копировать‑вставить)

Ниже представлен *полный* код программы, который можно поместить в `Program.cs`. Других файлов не требуется, кроме лицензии и изображения чека.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        try
        {
            ocrEngine.SetLicense("Aspose.OCR.lic");
        }
        catch (Exception)
        {
            Console.WriteLine("⚠️ Running in trial mode – license not found.");
        }

        // Load the image to be processed (load image for OCR)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}