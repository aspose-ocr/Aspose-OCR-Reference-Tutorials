---
category: general
date: 2026-04-04
description: Узнайте, как использовать Aspose для извлечения данных чека, загрузки
  изображения чека и распознавания изображения чека с помощью OCR, используя полный
  пример на C#. Пошаговое руководство для разработчиков.
draft: false
keywords:
- how to use aspose
- extract receipt data
- how to extract receipt
- load receipt image
- ocr receipt image
language: ru
og_description: Как использовать Aspose для извлечения данных чека из отсканированного
  изображения чека. Полный код на C#, объяснения и советы по обработке изображений
  чеков с помощью OCR.
og_title: Как использовать Aspose – извлекать данные чеков из изображений
tags:
- Aspose
- OCR
- C#
- Receipt Processing
title: Как использовать Aspose — извлекать данные чека из изображений в C#
url: /ru/net/text-recognition/how-to-use-aspose-extract-receipt-data-from-images-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать Aspose – извлечение данных чека из изображений на C#

Когда‑нибудь задавались вопросом **how to use Aspose**, как извлечь структурированную информацию из фотографии чека? Вы не одиноки. Независимо от того, создаёте ли вы приложение для учёта расходов или автоматизируете ввод счетов, проблема одна и та же: у вас есть PNG или JPEG, и вам нужны название магазина, дата и общая сумма без ручного ввода.

Дело в том, что Aspose.OCR делает весь процесс простым как раз, два, три. В этом руководстве мы пройдёмся по загрузке изображения чека, запуску OCR и, наконец, извлечению данных чека несколькими строками C#. К концу у вас будет готовая консольная программа, которая выводит название магазина, дату и общую сумму прямо в консоль.

> **Быстрый результат:** Если вам нужен только код, перейдите к разделу «Complete Working Example» внизу и скопируйте‑вставьте.

## Что понадобится

- **.NET 6.0 или новее** (API работает с .NET Core и .NET Framework)
- **Aspose.OCR for .NET** пакет NuGet (`Install-Package Aspose.OCR`)
- Пример изображения чека (PNG, JPG или BMP), сохранённый локально
- Visual Studio 2022 или любой редактор, поддерживающий проекты C#

Никакие другие сторонние библиотеки не требуются. Единственное требование — базовое понимание консольных приложений C#: если вы писали «Hello World», вы готовы.

## Шаг 1 – Установить и подключить Aspose.OCR

Чтобы **how to use Aspose**, сначала нужно добавить библиотеку в ваш проект. Откройте консоль диспетчера пакетов и выполните:

```powershell
Install-Package Aspose.OCR
```

Либо используйте UI NuGet и найдите «Aspose.OCR». После установки добавьте необходимые пространства имён в начало вашего файла:

```csharp
using Aspose.OCR;
using Aspose.OCR.Structured;
```

> **Совет:** Держите пакеты NuGet в актуальном состоянии. На сегодняшний день (апрель 2026) последняя стабильная версия — 23.11.0, в которой улучшена производительность OCR для изображений чеков высокого разрешения.

## Шаг 2 – Загрузить изображение чека

Когда вы **load receipt image** файлы, у вас есть два распространённых источника: локальный путь или поток из веб‑запроса. Для этого руководства мы упростим задачу и будем читать с диска:

```csharp
// Step 2: Load the receipt image to be processed
var ocrEngine = new OcrEngine
{
    Language = Language.English // set language for better accuracy
};

ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.png");
```

Замените `YOUR_DIRECTORY/receipt.png` на фактический путь к вашему файлу чека. Если вы работаете с загрузками пользователей, вы можете передать `MemoryStream` в `ImageStream.FromStream`.

> **Почему это важно:** Указание языка (English) сообщает движку OCR, какой набор символов ожидать, снижая количество ошибок распознавания — особенно важно, когда вы **ocr receipt image**, содержащий цифры и символы.

## Шаг 3 – Запустить OCR и захватить информацию о разметке

Шаг OCR делает больше, чем просто выдаёт сырой текст; он также захватывает разметку, что критически важно для последующего структурированного извлечения.

```csharp
// Step 3: Run OCR to generate text and layout information (required for structured extraction)
ocrEngine.Recognize();
```

После завершения `Recognize()` объект `ocrEngine` содержит как простой текст, так и позиционные данные каждого слова. Это основа для следующего шага, где мы попросим Aspose автоматически «**how to extract receipt**» поля.

## Шаг 4 – Инициализировать Layout Recognizer

Aspose предоставляет класс `LayoutRecognizer`, который знает, как обычно организованы чеки (название магазина вверху, строка даты, общая сумма внизу). Вы просто передаёте сконфигурированный OCR‑движок:

```csharp
// Step 4: Initialize the layout recognizer with the OCR engine
var layoutRecognizer = new LayoutRecognizer(ocrEngine);
```

Внутри распознаватель применяет набор эвристик — например, поиск символов валюты или шаблонов дат — чтобы сопоставить сырой текст семантическим полям.

## Шаг 5 – Извлечь структурированные данные чека

Теперь наступает приятная часть: **extract receipt data**. Один вызов метода делает всю тяжёлую работу:

```csharp
// Step 5: Extract structured receipt data (merchant, date, total amount)
var receiptData = layoutRecognizer.ExtractReceiptData();
```

`receiptData` — объект типа `ReceiptData` (определён в `Aspose.OCR.Structured`). Он содержит три основных свойства:

- `Merchant` – название магазина
- `Date` – дата покупки как `DateTime` (если обнаружена)
- `TotalAmount` – общая сумма как `decimal`

Если движок не может найти конкретное поле, свойство будет `null` или `0`. При необходимости можно добавить резервную логику (например, запросить подтверждение у пользователя).

## Шаг 6 – Вывести извлечённую информацию

Наконец, выведите результаты в консоль. Здесь вы увидите плоды своего труда:

```csharp
// Step 6: Display the extracted information
Console.WriteLine($"Merchant: {receiptData.Merchant}");
Console.WriteLine($"Date:     {receiptData.Date:d}");
Console.WriteLine($"Total:    {receiptData.TotalAmount:C}");
```

Строки формата (`:d` и `:C`) соответственно выводят короткую дату и строку валюты, делая вывод удобочитаемым.

### Ожидаемый вывод

Предположим, чек принадлежит «Coffee Corner», дата 2025‑12‑01, общая сумма $4.75, консоль выведет:

```
Merchant: Coffee Corner
Date:     12/1/2025
Total:    $4.75
```

Если какое‑то поле отсутствует, вы увидите пустую строку или значение по умолчанию — идеально для отладки.

## Пограничные случаи и распространённые подводные камни

### 1. Низкое разрешение изображений

Если изображение чека размыто или имеет разрешение ниже 150 dpi, точность OCR резко падает. Увеличение изображения простым билинейным фильтром перед передачей в Aspose может улучшить результаты.

```csharp
ocrEngine.Image = ImageStream.FromFile("receipt.png")
    .Resize(2.0, InterpolationMode.Bilinear);
```

### 2. Чеки не на английском

В основном примере используется `Language.English`. Для многоязычных чеков задайте `Language` соответствующим перечислением (например, `Language.French`) или используйте `Language.AutoDetect`, если не уверены.

### 3. Несколько чеков на одном изображении

Распознаватель разметки Aspose ожидает один чек на изображение. Если у вас фото нескольких чеков рядом, потребуется предварительная обработка изображения — обрезать каждый чек в отдельный файл перед запуском OCR.

### 4. Отсутствует символ валюты

Иногда общая сумма указана без знака `$`. Распознаватель всё равно находит числа, но может потребоваться пост‑обработка строки, чтобы обеспечить правильное размещение десятичных знаков.

```csharp
if (receiptData.TotalAmount == 0 && rawText.Contains("Total"))
{
    // fallback parsing logic here
}
```

## Советы для продакшн

- **Кешировать OCR‑движок**, если вы обрабатываете много чеков пакетно; повторное использование того же экземпляра снижает накладные расходы на выделение памяти.
- **Логировать сырой OCR‑текст** (`ocrEngine.Text`) для аудита. Это полезно, когда поле не удалось извлечь.
- **Оборачивать весь процесс в try/catch** и выводить понятное сообщение об ошибке (например, «Не удалось прочитать чек, пожалуйста, загрузите более чёткое изображение»).

## Полный рабочий пример

Ниже представлено автономное консольное приложение, которое можно сразу собрать и запустить. Просто замените путь к изображению, и вы готовы.

```csharp
// ------------------------------------------------------------
// How to Use Aspose – Extract Receipt Data from Images (C#)
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Structured;

namespace ReceiptExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create and configure the OCR engine for English language
            var ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the receipt image you want to process
            // 👉 Make sure the file exists; otherwise an exception will be thrown.
            const string imagePath = "YOUR_DIRECTORY/receipt.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Run OCR – this also captures layout information
            ocrEngine.Recognize();

            // 4️⃣ Initialize the layout recognizer with the OCR engine
            var layoutRecognizer = new LayoutRecognizer(ocrEngine);

            // 5️⃣ Extract structured receipt data (merchant, date, total amount)
            var receiptData = layoutRecognizer.ExtractReceiptData();

            // 6️⃣ Display the extracted information
            Console.WriteLine($"Merchant: {receiptData.Merchant ?? "Not detected"}");
            Console.WriteLine($"Date:     {(receiptData.Date == DateTime.MinValue ? "Not detected" : receiptData.Date.ToShortDateString())}");
            Console.WriteLine($"Total:    {(receiptData.TotalAmount == 0 ? "Not detected" : receiptData.TotalAmount.ToString("C"))}");

            // Keep the console window open when debugging
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Запуск кода**

1. Создайте новый .NET консольный проект (`dotnet new console -n ReceiptExtractor`).
2. Добавьте пакет Aspose.OCR (`dotnet add package Aspose.OCR`).
3. Замените сгенерированный `Program.cs` на фрагмент выше.
4. Поместите изображение чека по указанному пути.
5. Сборка и запуск (`dotnet run`).

Вы должны увидеть название магазина, дату и общую сумму, напечатанные точно так же, как показано ранее.

## Итоги

В этом руководстве мы рассмотрели **how to use Aspose** для **load receipt image**, запуск **ocr receipt image**, и, наконец, **extract receipt data** всего несколькими строками. Главный вывод: Aspose.OCR делает всю тяжёлую работу — после настройки OCR‑движка `LayoutRecognizer` преобразует сырой текст в структурированный объект, которому можно доверять.

Что дальше? Попробуйте сохранить извлечённые значения в базе данных, сгенерировать PDF‑резюме чека или даже передать их в модель машинного обучения для классификации расходов. Вы также можете поэкспериментировать с другими типами структурированных документов, например, счетами‑фактурами или транспортными этикетками — `ExtractInvoiceData` от Aspose работает аналогично.

Есть вопросы о пограничных случаях или хотите увидеть, как обрабатывать многостраничные PDF? Оставьте комментарий или ознакомьтесь с официальной документацией Aspose.OCR для продвинутых сценариев. Приятного кодинга и наслаждайтесь простотой **how to use Aspose** для автоматизации обработки чеков!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}