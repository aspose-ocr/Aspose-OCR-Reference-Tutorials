---
category: general
date: 2026-02-24
description: Быстро выполняйте пакетное OCR‑распознавание изображений с помощью Aspose.OCR
  в C#. Узнайте, как читать файлы из каталога, распознавать текст на изображении и
  преобразовывать изображение в текст за несколько шагов.
draft: false
keywords:
- batch OCR images
- extract text from images
- read files from directory
- recognize text from image
- convert image to text
language: ru
og_description: Пакетное OCR‑распознавание изображений на C# с использованием Aspose.OCR.
  Этот учебник показывает, как читать файлы из каталога, распознавать текст на изображении
  и эффективно преобразовывать изображение в текст.
og_title: Пакетное OCR‑распознавание изображений в C# – Полное пошаговое руководство
tags:
- C#
- OCR
- Aspose
title: Пакетное OCR изображений в C# — Полное руководство по извлечению текста
url: /ru/net/text-recognition/batch-ocr-images-in-c-full-guide-to-extract-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Пакетное OCR изображений в C# – Полное руководство по извлечению текста

Когда‑нибудь вам нужно было **batch OCR images**, но вы не знали, с чего начать? Вы не одиноки — многие разработчики сталкиваются с тем же, когда впервые пытаются **extract text from images** массово. Хорошая новость в том, что с несколькими строками C# и Aspose.OCR вы можете превратить папку, полную изображений, в аккуратные файлы `.txt` за считанные секунды.

В этом руководстве мы пройдем весь процесс: чтение файлов из каталога, передача каждого изображения в OCR‑движок и, наконец, **convert image to text** файлы, которые вы можете индексировать, искать или передавать в последующие конвейеры. К концу у вас будет автономное консольное приложение, которое можно добавить в любой .NET‑проект.

## Что понадобится

- **.NET 6+** (пример компилируется с .NET 6, но любая современная версия подходит)
- **Aspose.OCR** NuGet пакет (`Install-Package Aspose.OCR`)
- Папка с файлами изображений (`.png`, `.jpg` и т.д.), которые вы хотите обработать
- Visual Studio, Rider или ваш любимый редактор

Без дополнительных файлов конфигурации, без внешних сервисов — только чистый C# код, который работает локально.

## Пакетное OCR изображений — настройка проекта

Сначала создайте новый консольный проект:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

Эта команда создаёт минимальный проект и подключает библиотеку OCR. После завершения восстановления вы готовы добавить основную логику.

### Чтение файлов из каталога

Нужно указать приложению, где находятся исходные изображения и куда сохранять полученные текстовые файлы. Использование `System.IO` делает это простым.

```csharp
using System;
using System.IO;
using Aspose.OCR;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Define input and output folders
        string inputFolder  = @"C:\Images\ToProcess";   // <-- change to your source folder
        string outputFolder = @"C:\Images\OcrResults"; // <-- change to your target folder

        // 2️⃣ Ensure the output folder exists
        Directory.CreateDirectory(outputFolder);
```

> **Почему этот шаг важен:** Если каталог вывода не существует, программа бросит исключение при попытке записать файл `.txt`. `CreateDirectory` идемпотентен — ничего не делает, если папка уже существует, поэтому безопасно вызывать его каждый запуск.

### Распознавание текста из изображения и преобразование изображения в текст

Теперь мы инициализируем OCR‑движок и проходим в цикле каждый найденный файл. Цикл использует `Directory.GetFiles` с шаблоном (`*.*`), поэтому захватывает *все* файлы, но при желании вы можете сузить фильтр до `*.png` или `*.jpg`.

```csharp
        // 3️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 4️⃣ Process each image file in the input folder
        foreach (var imagePath in Directory.GetFiles(inputFolder, "*.*", SearchOption.TopDirectoryOnly))
        {
            // 5️⃣ Recognise text from the current image
            var ocrResult = ocrEngine.RecognizeImage(imagePath);

            // 6️⃣ Save the recognised text to a .txt file in the output folder
            string textFilePath = Path.Combine(
                outputFolder,
                Path.GetFileNameWithoutExtension(imagePath) + ".txt");

            File.WriteAllText(textFilePath, ocrResult.Text);
        }

        Console.WriteLine("✅ All images processed. Check the output folder!");
    }
}
```

**Что происходит здесь?**  
- `ocrEngine.RecognizeImage(imagePath)` читает bitmap, запускает OCR‑алгоритм и возвращает объект `OcrResult`.  
- `ocrResult.Text` содержит текстовое представление всего, что смог прочитать движок.  
- `File.WriteAllText` создаёт новый файл (или перезаписывает существующий) с извлечённым текстом.

Это полностью весь конвейер **batch OCR images** в менее чем 30 строк кода.

## Профессиональные советы и особые случаи

| Ситуация | Рекомендация |
|-----------|----------------|
| Изображения большие ( > 5 МБ ) | Снизьте их до ширины ~1500 px, чтобы ускорить распознавание без потери точности. |
| Необходимо поддерживать PDF | Сначала преобразуйте каждую страницу PDF в изображение (например, с помощью `Aspose.PDF`), затем передайте её в тот же цикл. |
| Некоторые файлы не являются изображениями (например, `.txt`) | Добавьте простой фильтр: `if (!imagePath.EndsWith(".png") && !imagePath.EndsWith(".jpg")) continue;` |
| Требуется поддержка нескольких языков | Установите `ocrEngine.Language = Language.English | Language.Spanish;` перед циклом. |
| Нужна отчётность о прогрессе | Внутри foreach добавьте `Console.WriteLine($"Processing {Path.GetFileName(imagePath)}...");` |

> **Профессиональный совет:** Оберните вызов OCR в `try/catch`. Иногда повреждённое изображение вызывает исключение в `RecognizeImage`; обработка исключения предотвращает остановку всей партии.

## Ожидаемый вывод

После завершения программы в `outputFolder` будет файл `.txt` для каждого исходного изображения:

```
C:\Images\OcrResults\invoice1.txt
C:\Images\OcrResults\receipt_2024-01-15.txt
C:\Images\OcrResults\signage.png.txt   <-- note the .txt extension
```

Каждый файл содержит необработанный текст, извлечённый движком, например:

```
Invoice #12345
Date: 01/15/2024
Total: $1,250.00
Thank you for your business!
```

Теперь вы можете передать эти файлы в поисковый индекс, выполнить анализ тональности или просто архивировать их для соответствия требованиям.

## Часто задаваемые вопросы

**Q: Работает ли это на Linux?**  
A: Абсолютно. Aspose.OCR кросс‑платформенный, а используемые здесь API `System.IO` независимы от ОС. Просто скорректируйте пути к папкам (`/home/user/images`).

**Q: Что делать, если нужно **read files from directory** рекурсивно?**  
A: Замените `SearchOption.TopDirectoryOnly` на `SearchOption.AllDirectories`. Учтите возможные проблемы с правами доступа в более глубоких папках.

**Q: Насколько точен OCR?**  
A: Точность зависит от качества изображения, шрифта и языка. Для лучших результатов используйте сканы высокого разрешения и чистый фон. Также можно настроить `ocrEngine.Config`, включив выравнивание и подавление шума.

## Итоги

Вы только что узнали, как **batch OCR images** в C# с помощью Aspose.OCR, от чтения файлов из каталога до **recognize text from image** и, наконец, **convert image to text** файлов, которые можно сохранять или дальше обрабатывать. Полный, готовый к запуску пример выше должен работать сразу, а раздел советов предоставляет план масштабирования или настройки решения.

Следующие шаги? Попробуйте добавить простой UI с WinForms или WPF, интегрировать вывод с Azure Cognitive Search или поэкспериментировать с другими языками, поддерживаемыми Aspose.OCR. Возможности безграничны, как только вы освоите основной цикл.

Удачной разработки, и пусть ваши OCR‑пакеты будут без ошибок!  

![Схема процесса пакетного OCR изображений](batch-ocr-images-diagram.png "Рабочий процесс пакетного OCR изображений")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}