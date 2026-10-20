---
category: general
date: 2026-06-03
description: Получите версию Aspose OCR в C# с помощью простого фрагмента кода. Узнайте,
  как получить версию библиотеки Aspose OCR, используя OcrEngine.GetVersion.
draft: false
keywords:
- get aspose ocr version
- aspose ocr library
- ocrengine getversion
- c# ocr example
- retrieve aspose version
language: ru
og_description: Быстро получите версию Aspose OCR в C#. Этот учебник точно показывает,
  как получить версию библиотеки Aspose OCR с помощью OcrEngine.GetVersion.
og_title: Получите версию Aspose OCR на C# – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Get Aspose OCR version in C# with a simple snippet. Learn how to retrieve
    the Aspose OCR library version using OcrEngine GetVersion.
  headline: Get Aspose OCR Version in C# – Complete Guide
  type: TechArticle
- description: Get Aspose OCR version in C# with a simple snippet. Learn how to retrieve
    the Aspose OCR library version using OcrEngine GetVersion.
  name: Get Aspose OCR Version in C# – Complete Guide
  steps:
  - name: Why this matters
    text: When you install the package, the assembly version on disk may differ from
      the version reported by the library at runtime. Querying the version via code
      ensures you’re reading the exact build that the CLR loaded, which is crucial
      for debugging and for compliance audits.
  - name: Expected output
    text: 'When you run `dotnet run` inside the project folder, you should see something
      similar to:'
  - name: What if `GetVersion()` returns an empty string?
    text: That usually signals a corrupted installation or a missing native dependency.
      Re‑install the NuGet package and verify that the `Aspose.OCR.Native.dll` (or
      the appropriate platform‑specific binary) sits alongside your executable.
  - name: Does the method work on .NET Core 2.0?
    text: Yes, **Aspose OCR** supports .NET Standard 2.0 and higher, so any .NET Core
      version that implements that standard can call `OcrEngine.GetVersion()`. Just
      make sure you reference the correct runtime identifiers (`win-x64`, `linux-x64`,
      etc.) if you’re publishing a self‑contained app.
  - name: Can I retrieve the version without a license file?
    text: Absolutely. `GetVersion()` does **not** require a license; it simply reports
      the library build number. However, if you attempt to perform OCR without a valid
      license, you’ll get a runtime exception. That’s why the `try/catch` in our snippet
      is valuable—it isolates the version check from the OCR exec
  type: HowTo
tags:
- Aspose
- OCR
- C#
- .NET
title: Получить версию Aspose OCR в C# – Полное руководство
url: /ru/net/ocr-configuration/get-aspose-ocr-version-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Получить версию Aspose OCR в C# – Полное руководство

Вы когда‑нибудь задумывались, как **получить версию Aspose OCR** из вашего проекта .NET? Возможно, вы устраняете несоответствие или просто хотите записать точную сборку библиотеки, работающую в продакшене. Какова бы ни была причина, вы попали в нужное место.

В этом руководстве мы пройдемся по небольшому, автономному C#‑приложению, которое вызывает `OcrEngine.GetVersion()` и выводит результат. К концу вы узнаете не только *как* получить версию, но и *почему* проверка версии может избавить вас от головной боли при обновлении **библиотеки Aspose OCR**.

## Что вы узнаете

- Добавить пакет Aspose.OCR NuGet в проект C#  
- Использовать метод `OcrEngine.GetVersion()` (точка входа **ocrengine getversion**)  
- Обработать возможные исключения и проверить вывод  
- Расширить фрагмент для реальных сценариев, таких как логирование или условные переключатели функций  

Предыдущий опыт работы с OCR не требуется — достаточно базовых знаний C# и Visual Studio (или вашего любимого IDE). Поехали.

---

## Шаг 1: Настройка проекта и подключение библиотеки Aspose OCR

Прежде чем вы сможете вызвать какие‑либо OCR‑API, необходимо добавить **библиотеку Aspose OCR** в ваш проект.

1. Откройте терминал или консоль диспетчера пакетов в Visual Studio.  
2. Выполните следующую команду, чтобы установить последнюю стабильную версию:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Если вы нацеливаетесь на .NET Framework вместо .NET Core, используйте UI NuGet Package Manager и выберите версию, соответствующую вашей среде выполнения. Пакет включает класс `OcrEngine`, который мы будем использовать позже.

### Почему это важно

При установке пакета версия сборки на диске может отличаться от версии, которую библиотека сообщает во время выполнения. Запрос версии через код гарантирует, что вы читаете именно ту сборку, которую загрузил CLR, что критично для отладки и аудитов соответствия.

## Шаг 2: Написать минимальный код для **получения версии Aspose OCR**

Создайте новое консольное приложение (`dotnet new console -n OcrVersionDemo`) и замените файл `Program.cs` следующим содержимым:

```csharp
using System;
using Aspose.OCR;

namespace OcrVersionDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // Step 2a: Retrieve the Aspose OCR library version.
                // This is the core of the get aspose ocr version operation.
                string version = OcrEngine.GetVersion();   // e.g., "24.5.7"

                // Step 2b: Display the version information to the console.
                Console.WriteLine($"Aspose OCR version: {version}");
            }
            catch (Exception ex)
            {
                // If something goes wrong (missing DLL, license issue, etc.)
                Console.Error.WriteLine($"Failed to get Aspose OCR version: {ex.Message}");
            }
        }
    }
}
```

**Объяснение каждой части**

- `using Aspose.OCR;` импортирует пространство имён OCR, позволяя вызывать `OcrEngine`.  
- `OcrEngine.GetVersion()` — это статический метод **ocrengine getversion**, возвращающий строку вроде `"24.5.7"`.  
- Обёртывание вызова в блок `try/catch` защищает от неожиданных ошибок во время выполнения — возможно, нативные бинарные файлы не найдены на целевой машине.  
- Интерполированная строка `$"Aspose OCR version: {version}"` выводит понятную, читаемую строку.

### Ожидаемый вывод

При запуске `dotnet run` в папке проекта вы должны увидеть что‑то подобное:

```
Aspose OCR version: 24.5.7
```

Если библиотеку не удалось загрузить, ветка ошибки выведет краткое сообщение, помогая быстро локализовать проблему.

## Шаг 3: Проверить, что версия совпадает с вашей NuGet‑пакетой

Легко предположить, что установленная версия NuGet — это та, что используется во время выполнения, но особенности среды могут вмешаться. Чтобы убедиться:

```csharp
// After retrieving the version, compare it to the package metadata.
var assembly = typeof(OcrEngine).Assembly;
var fileVersion = System.Diagnostics.FileVersionInfo.GetVersionInfo(assembly.Location).FileVersion;

Console.WriteLine($"Assembly file version: {fileVersion}");
```

Выполнение этого дополнительного фрагмента выведет что‑то вроде:

```
Assembly file version: 24.5.7.0
```

Если два значения различаются, возможно, вы загружаете более старый DLL из Global Assembly Cache (GAC) или из предыдущей папки сборки. В этом случае выполните очистку решения (`dotnet clean`) и пересоберите проект.

## Шаг 4: Добавить проверку версии в производственное логирование

Большинство реальных приложений не просто выводят информацию в консоль; они записывают её в файл журнала или систему телеметрии. Вот быстрый пример с использованием `Microsoft.Extensions.Logging`:

```csharp
using Microsoft.Extensions.Logging;
using Microsoft.Extensions.DependencyInjection;

// Set up a minimal logger.
var serviceProvider = new ServiceCollection()
    .AddLogging(builder => builder.AddConsole())
    .BuildServiceProvider();

var logger = serviceProvider.GetService<ILogger<Program>>();

try
{
    string version = OcrEngine.GetVersion();
    logger.LogInformation("Aspose OCR version: {Version}", version);
}
catch (Exception ex)
{
    logger.LogError(ex, "Unable to retrieve Aspose OCR version");
}
```

Теперь версия появляется в ваших структурированных логах, её легко отфильтровать по `{Version}` позже. Такой подход особенно полезен, когда у вас несколько микросервисов, каждый из которых может подтягивать потенциально разную DLL OCR.

## Часто задаваемые вопросы и крайние случаи

### Что если `GetVersion()` возвращает пустую строку?

Это обычно указывает на повреждённую установку или отсутствие нативной зависимости. Переустановите пакет NuGet и убедитесь, что `Aspose.OCR.Native.dll` (или соответствующий платформенно‑специфичный бинарный файл) находится рядом с исполняемым файлом.

### Работает ли метод на .NET Core 2.0?

Да, **Aspose OCR** поддерживает .NET Standard 2.0 и выше, поэтому любой .NET Core, реализующий этот стандарт, может вызвать `OcrEngine.GetVersion()`. Просто убедитесь, что указали правильные идентификаторы среды выполнения (`win-x64`, `linux-x64` и т.д.), если публикуете автономное приложение.

### Можно ли получить версию без файла лицензии?

Абсолютно. `GetVersion()` **не требует** лицензии; он просто сообщает номер сборки библиотеки. Однако попытка выполнить OCR без действующей лицензии приведёт к исключению во время выполнения. Поэтому `try/catch` в нашем примере полезен — он изолирует проверку версии от процесса распознавания.

## Полный рабочий пример (готов к копированию)

Ниже представлен весь код программы, готовый к вставке в новый консольный проект. В нём включён необязательный блок логирования, так что вы увидите как вывод в консоль, так и структурированные логи в действии.

```csharp
using System;
using Aspose.OCR;
using Microsoft.Extensions.Logging;
using Microsoft.Extensions.DependencyInjection;

namespace OcrVersionDemo
{
    class Program
    {
        static void Main()
        {
            // Set up a simple console logger.
            var services = new ServiceCollection()
                .AddLogging(builder => builder.AddConsole())
                .BuildServiceProvider();

            var logger = services.GetService<ILogger<Program>>();

            try
            {
                // Retrieve the Aspose OCR library version.
                string version = OcrEngine.GetVersion();   // get aspose ocr version

                // Log and display the version.
                logger.LogInformation("Aspose OCR version: {Version}", version);
                Console.WriteLine($"Aspose OCR version: {version}");

                // Extra verification – compare with assembly file version.
                var assembly = typeof(OcrEngine).Assembly;
                var fileVersion = System.Diagnostics.FileVersionInfo
                    .GetVersionInfo(assembly.Location).FileVersion;
                logger.LogDebug("Assembly file version: {FileVersion}", fileVersion);
                Console.WriteLine($"Assembly file version: {fileVersion}");
            }
            catch (Exception ex)
            {
                logger.LogError(ex, "Failed to get Aspose OCR version");
                Console.Error.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

Запустите его командой `dotnet run`, и вы увидите две строки, подтверждающие версию, плюс отладочную строку, если включите `LogLevel.Debug`.

## Заключение

Мы рассмотрели всё, что нужно, чтобы **получить версию Aspose OCR** в среде C# — от установки **библиотеки Aspose OCR**, вызова метода **ocrengine getversion**, обработки ошибок до внедрения результата в производственное логирование. Обладая этими знаниями, вы теперь можете надёжно проверять точную сборку OCR, используемую вашим приложением, избегать ошибок, связанных с версиями, и удовлетворять требованиям соответствия без лишних усилий.

Что дальше? Попробуйте сочетать эту проверку версии с реальным вызовом OCR (`OcrEngine` → `RecognizeImage`) и логировать одновременно версию и результат распознавания. Вы также можете изучить шаблон **retrieve aspose version** для других продуктов Aspose (PDF, Slides, Cells), чтобы синхронизировать весь ваш набор библиотек.

Счастливого кодинга, и пусть ваши OCR‑конвейеры остаются острыми!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Как получить результаты OCR с Aspose.OCR для .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Извлечение текста из изображения C# с выбором языка с помощью Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Как пакетно обрабатывать изображения OCR со списком в Aspose.OCR для .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}