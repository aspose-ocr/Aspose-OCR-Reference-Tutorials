---
category: general
date: 2026-04-26
description: Extraia texto de arquivos PNG rapidamente com C#. Aprenda a converter
  imagens em texto, ler arquivos PNG, percorrer imagens em loop e fazer OCR em lote
  em minutos.
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: pt
og_description: Extraia texto de arquivos PNG rapidamente com C#. Este guia mostra
  como converter imagens em texto, ler arquivos PNG, percorrer imagens e fazer OCR
  em lote nas imagens.
og_title: Extrair Texto de PNG – Tutorial Completo de OCR em Lote com C#
tags:
- C#
- OCR
- Aspose
title: Extrair Texto de PNG – Tutorial Completo de OCR em Lote em C#
url: /pt/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de PNG – Tutorial Completo de OCR em Lote com C#

Já precisou **extract text from PNG** arquivos mas não sabia por onde começar? Você não está sozinho—muitos desenvolvedores encontram essa barreira na primeira vez que tentam OCR em uma pasta de capturas de tela. A boa notícia é que, com algumas linhas de C# e Aspose OCR, você pode converter imagens em texto, ler arquivos PNG, percorrer as imagens e processar tudo em lote de uma só vez.  

Neste tutorial vamos percorrer um aplicativo console pronto‑para‑executar que faz exatamente isso. Ao final, você terá uma solução autônoma que extrai texto de cada PNG em um diretório e cria um arquivo `.txt` correspondente ao lado de cada imagem. Sem scripts extras, sem copiar‑colar manual—apenas código puro.

## O que você vai precisar

- **.NET 6 SDK** (ou qualquer versão mais recente do .NET). É gratuito, rápido e funciona em qualquer lugar.  
- **Aspose.OCR for .NET** (o pacote NuGet). A biblioteca inclui aceleração por GPU se você possuir uma GPU compatível, mas também recorre à CPU automaticamente.  
- Uma pasta com alguns **PNG images** que você deseja processar.  
- Um editor de texto ou IDE—Visual Studio, VS Code, Rider—o que preferir.

É só isso. Se já tem tudo isso, está pronto para começar.

![extract text from png example](image.png "captura de tela de demonstração de extract text from png")

*Texto alternativo da imagem: “extract text from png using C# batch OCR”*

## Etapa 1 – Configurar o Projeto e Instalar Aspose.OCR

Primeiro, crie um novo projeto console e adicione o pacote Aspose OCR.

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

Por que usamos um aplicativo console? É o host mais simples para trabalhos em lote, e você pode executá‑lo a partir da linha de comando ou agendá‑lo com um gerenciador de tarefas. Se mais tarde precisar de uma interface gráfica, basta mover a lógica principal para uma biblioteca de classes.

## Etapa 2 – Inicializar um OCR Engine acelerado por GPU (ou fallback para CPU)

Aspose oferece um `GpuOcrEngine` que detecta automaticamente uma GPU suportada. Se nenhuma for encontrada, ele reverte para o engine padrão de CPU—sem código extra necessário.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine – GPU if available, otherwise CPU
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;   // Latin covers most Western alphabets

        // The rest of the code lives in a separate method for clarity
        ProcessFolder(ocrEngine, @"C:\MyPngFolder");
    }

    // …
}
```

**Dica profissional:** Se você estiver em um servidor headless sem GPU, pode substituir `GpuOcrEngine` por `OcrEngine` e o código se comportará exatamente da mesma forma.

## Etapa 3 – Percorrer as Imagens no Diretório de Destino

Precisamos **loop through images** e selecionar apenas arquivos PNG. O método `Directory.GetFiles` faz o trabalho pesado, e vamos proteger contra uma pasta vazia.

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    if (!Directory.Exists(folderPath))
    {
        Console.WriteLine($"❌ Folder not found: {folderPath}");
        return;
    }

    // Grab every *.png file – this is the “read png files” part
    string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

    if (pngFiles.Length == 0)
    {
        Console.WriteLine("⚠️ No PNG files found. Make sure the folder contains .png images.");
        return;
    }

    foreach (var pngPath in pngFiles)
    {
        Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
        ExtractAndSave(engine, pngPath);
    }
}
```

Observe o uso de `SearchOption.TopDirectoryOnly`. Se mais tarde precisar percorrer subpastas, basta mudar para `AllDirectories`. Essa pequena alteração permite **convert images to text** em toda a árvore com uma única linha.

## Etapa 4 – Executar OCR e Salvar o Resultado

Agora vem o núcleo do fluxo de **batch OCR images**. Carregamos cada PNG, executamos `Recognize()` e gravamos a string extraída em um arquivo `.txt` que compartilha o mesmo nome base.

```csharp
static void ExtractAndSave(OcrEngine engine, string imagePath)
{
    try
    {
        // Load the PNG into the engine
        engine.Image = ImageStream.FromFile(imagePath);

        // Run recognition – this returns a RecognitionResult object
        RecognitionResult result = engine.Recognize();

        // Build the output path (same name, .txt extension)
        string txtPath = Path.ChangeExtension(imagePath, ".txt");

        // Write the OCR text to disk
        File.WriteAllText(txtPath, result.Text);

        Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        // Edge case: corrupted PNG or unsupported format
        Console.WriteLine($"❗ Error processing {Path.GetFileName(imagePath)}: {ex.Message}");
    }
}
```

**Por que envolver em try/catch?** Lotes de imagens do mundo real frequentemente contêm um arquivo corrompido ou um PNG que usa um perfil de cor incomum. Capturar a exceção impede que a execução inteira falhe e permite continuar processando os arquivos restantes.

## Etapa 5 – Executar a Aplicação e Verificar a Saída

Compile e inicie o aplicativo:

```bash
dotnet run
```

Você deverá ver um log no console semelhante a:

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

Abra qualquer um dos arquivos `.txt` gerados—lá está o texto extraído. Se um arquivo estiver vazio, verifique a qualidade da imagem; OCR funciona melhor com texto claro e de alto contraste.

### Script de Verificação Rápida (opcional)

Se quiser garantir que cada PNG recebeu um arquivo de texto correspondente, execute este pequeno one‑liner PowerShell:

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## Variações Comuns & Casos de Borda

| Situação | O que mudar |
|-----------|----------------|
| **Non‑Latin languages** (ex.: Cyrillic) | Defina `ocrEngine.Language = Language.Cyrillic;` |
| **Large image set (>10 000 files)** | Use `Parallel.ForEach` para acelerar o processamento, mas monitore o uso de memória da GPU. |
| **Need to keep original image order** | Ordene `pngFiles` antes do `foreach` (`Array.Sort(pngFiles);`). |
| **Running on a CI server without a GPU** | Substitua `GpuOcrEngine` por `OcrEngine` para evitar erros de inicialização da GPU. |
| **You only want to process files that contain a specific keyword** | Após obter `result.Text`, verifique `result.Text.Contains("Invoice")` antes de gravar o arquivo. |

Essas adaptações permitem que você ajuste o pipeline **convert images to text** para praticamente qualquer cenário que encontrar.

## Código Fonte Completo (Pronto para Copiar‑Colar)

```csharp
// ------------------------------------------------------------
// Extract Text from PNG – Batch OCR using Aspose.OCR (C#)
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine (GPU if possible)
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;

        // 2️⃣ Define the folder that holds your PNG files
        string targetFolder = @"C:\MyPngFolder";   // <-- change to your path

        // 3️⃣ Process every PNG in the folder
        ProcessFolder(ocrEngine, targetFolder);
    }

    static void ProcessFolder(OcrEngine engine, string folderPath)
    {
        if (!Directory.Exists(folderPath))
        {
            Console.WriteLine($"❌ Folder not found: {folderPath}");
            return;
        }

        string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

        if (pngFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No PNG files found.");
            return;
        }

        foreach (var pngPath in pngFiles)
        {
            Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
            ExtractAndSave(engine, pngPath);
        }
    }

    static void ExtractAndSave(OcrEngine engine, string imagePath)
    {
        try
        {
            engine.Image = ImageStream.FromFile(imagePath);
            RecognitionResult result = engine.Recognize();

            string txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, result.Text);

            Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❗ Error on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

Salve como `Program.cs`, execute `dotnet run` e veja a mágica acontecer.

## Conclusão

Agora você tem uma **complete, production‑ready way to extract text from PNG** usando C#. O tutorial cobriu tudo—desde a configuração do projeto, inicialização de um OCR engine acelerado por GPU, **loop through images**, até **batch OCR images** e a gravação dos resultados como texto simples.  

Se estiver curioso sobre os próximos passos, experimente:

- **Convert images to text** para outros formatos (JPG, BMP

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}