---
category: general
date: 2026-05-31
description: Como fazer OCR em lote em C# com Aspose OCR. Aprenda a converter imagens
  em texto, extrair texto de imagens e processar vários arquivos de forma eficiente.
draft: false
keywords:
- how to batch OCR
- convert images to text
- extract text from images
- OCR multiple files
- batch OCR processing
language: pt
og_description: Como fazer OCR em lote em C# usando Aspose OCR. Converta imagens em
  texto, extraia texto de imagens e manipule OCR de múltiplos arquivos com facilidade.
og_title: Como fazer OCR em lote em C# – Guia completo de programação
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: How to batch OCR in C# with Aspose OCR. Learn to convert images to
    text, extract text from images, and process multiple files efficiently.
  headline: How to Batch OCR in C# – Complete Programming Guide
  type: TechArticle
- description: How to batch OCR in C# with Aspose OCR. Learn to convert images to
    text, extract text from images, and process multiple files efficiently.
  name: How to Batch OCR in C# – Complete Programming Guide
  steps:
  - name: '**.NET 6 SDK** (or later) installed – the latest runtime gives you better
      performance and native support for async I/O.'
    text: '**.NET 6 SDK** (or later) installed – the latest runtime gives you better
      performance and native support for async I/O.'
  - name: '**Visual Studio 2022** (Community Edition works fine) or any editor you
      like.'
    text: '**Visual Studio 2022** (Community Edition works fine) or any editor you
      like.'
  - name: 'The **Aspose.OCR** NuGet package. Install it via the Package Manager Console:'
    text: 'The **Aspose.OCR** NuGet package. Install it via the Package Manager Console:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- batch-processing
title: Como fazer OCR em lote em C# – Guia completo de programação
url: /pt/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR em lote no C# – Guia de Programação Completo

Já se perguntou **como fazer OCR em lote** de uma pasta inteira de imagens escaneadas sem abrir cada arquivo manualmente? Você não está sozinho. Em muitos projetos reais—pense em automação de faturas ou arquivamento de fotos históricas—você precisa **converter imagens em texto** em massa, e fazer isso um por um consome muito tempo.

Neste tutorial vamos percorrer um aplicativo console C# pronto‑para‑executar que pega cada PNG, JPG ou TIFF em um diretório de origem, executa Aspose OCR em cada um e grava um arquivo *.txt* correspondente em uma pasta de saída. Ao final você estará confortável em **extrair texto de imagens**, lidar com **OCR de múltiplos arquivos** e terá uma base sólida para qualquer **processamento de OCR em lote** que precisar mais tarde.

## O que você vai aprender

- Configurar um projeto .NET com o pacote NuGet Aspose OCR.  
- Definir pastas de origem e destino para uma execução de **OCR em lote**.  
- Enumerar tipos de imagem suportados e enviá‑los ao motor OCR.  
- Gravar o texto reconhecido em arquivos *.txt* individuais, efetivamente **converter imagens em texto**.  
- Lidar com armadilhas comuns como pastas ausentes, formatos não suportados e ajustes de desempenho.

Nenhuma experiência prévia com Aspose é necessária; apenas um entendimento básico de C# e Visual Studio será suficiente.

---

![Diagrama mostrando o fluxo de processamento de OCR em lote de pasta de imagens para saída de texto – como fazer OCR em lote](/images/batch-ocr-flow.png){alt="diagrama do fluxo de como fazer OCR em lote"}

## Como fazer OCR em lote – Configurando o Projeto

Antes de mergulharmos no código, certifique‑se de que você tem:

1. **.NET 6 SDK** (ou superior) instalado – a runtime mais recente oferece melhor desempenho e suporte nativo para I/O assíncrono.  
2. **Visual Studio 2022** (a edição Community funciona bem) ou qualquer editor de sua preferência.  
3. O pacote **Aspose.OCR** NuGet. Instale‑o via Package Manager Console:

   ```powershell
   Install-Package Aspose.OCR
   ```

É só isso. O restante do tutorial assume que o pacote está referenciado corretamente.

## Etapa 2: Preparar Pastas de Origem e Destino (converter imagens em texto)

Primeiro, precisamos de duas pastas: uma que contém as imagens brutas e outra onde os arquivos *.txt* gerados serão armazenados. O código abaixo cria a pasta de destino caso ela ainda não exista—nenhum passo manual necessário.

```csharp
// Define where the images live and where the text files will go
string sourceFolder = @"C:\OCR\Batch";
string outputFolder = @"C:\OCR\BatchTxt";

// Ensure the output directory exists; CreateDirectory is idempotent
Directory.CreateDirectory(outputFolder);
```

> **Por que isso importa:** Se você pular a chamada `CreateDirectory`, o programa lançará uma `DirectoryNotFoundException` no momento em que tentar gravar o primeiro arquivo de texto. Ao tratá‑la antecipadamente, você torna o processo de OCR em lote mais robusto.

## Etapa 3: Enumerar Arquivos de Imagem para OCR de Múltiplos Arquivos

Em seguida, coletamos todos os arquivos que correspondem aos formatos que suportamos. Usar LINQ mantém o código conciso e ainda legível.

```csharp
// Grab all PNG, JPG, and TIFF files from the source folder (non‑recursive)
var imageFiles = Directory.EnumerateFiles(sourceFolder, "*.*", SearchOption.TopDirectoryOnly)
    .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase));
```

> **Dica:** Se mais tarde precisar lidar com PDFs ou BMPs, basta estender a cláusula `Where`. Manter o filtro em um único lugar facilita ajustes futuros.

## Etapa 4: Executar o Motor OCR em Cada Imagem (como fazer OCR em lote)

Agora o coração da questão: alimentar cada imagem ao Aspose OCR e extrair o texto reconhecido. O laço abaixo cria uma nova instância de `OcrEngine` para cada arquivo—isso garante que a memória da imagem anterior seja liberada antes que a próxima seja processada.

```csharp
foreach (var imagePath in imageFiles)
{
    // Initialize the OCR engine with the current image
    OcrEngine ocrEngine = new OcrEngine
    {
        Image = ImageStream.FromFile(imagePath)
    };

    // Perform recognition; Recognize() returns an OcrResult object
    OcrResult ocrResult = ocrEngine.Recognize();

    // Build the output .txt file path (same base name, .txt extension)
    string textFilePath = Path.Combine(outputFolder,
        Path.GetFileNameWithoutExtension(imagePath) + ".txt");

    // Persist the extracted text
    File.WriteAllText(textFilePath, ocrResult.Text);

    Console.WriteLine($"Processed {Path.GetFileName(imagePath)} → {Path.GetFileName(textFilePath)}");
}
```

**O que está acontecendo?**  

- `ImageStream.FromFile` carrega a imagem em um stream que o Aspose pode ler.  
- `ocrEngine.Recognize()` executa o algoritmo OCR propriamente dito, retornando uma string em `ocrResult.Text`.  
- `File.WriteAllText` grava essa string no disco, efetivamente **extrair texto de imagens**.

### Tratamento de Casos Limítrofes

- **Imagens corrompidas** – envolva a chamada de reconhecimento em um `try/catch` e registre a falha, então continue com o próximo arquivo.  
- **Lotes grandes** – considere processar arquivos de forma assíncrona com `Parallel.ForEach` se você possuir uma máquina multi‑core.  
- **Idiomas diferentes** – defina `ocrEngine.Language = Language.English;` ou qualquer outro idioma suportado antes de chamar `Recognize()`.

## Etapa 5: Salvar Texto Extraído (extrair texto de imagens)

O trecho anterior já salva a saída do OCR, mas vamos isolar essa lógica em um método auxiliar. Isso deixa o laço principal mais limpo e incentiva a reutilização.

```csharp
static void SaveOcrResult(string outputFolder, string imagePath, string recognizedText)
{
    string textFilePath = Path.Combine(outputFolder,
        Path.GetFileNameWithoutExtension(imagePath) + ".txt");

    File.WriteAllText(textFilePath, recognizedText);
}
```

Você então substituiria a chamada inline `File.WriteAllText` por:

```csharp
SaveOcrResult(outputFolder, imagePath, ocrResult.Text);
```

> **Por que extrair isso para um método?** Ele separa preocupações—reconhecimento vs. persistência—e oferece um único ponto para adicionar pós‑processamento (como remover espaços em branco ou acrescentar timestamps).

## Exemplo Completo – Processamento de OCR em Lote no C#

Juntando todas as peças, aqui está um programa autocontido que você pode copiar‑colar em um novo projeto Console App e executar imediatamente.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Define source & destination folders
            string sourceFolder = @"C:\OCR\Batch";
            string outputFolder = @"C:\OCR\BatchTxt";

            // 2️⃣ Make sure the output folder exists
            Directory.CreateDirectory(outputFolder);

            // 3️⃣ Get all supported image files (convert images to text)
            var imageFiles = Directory.EnumerateFiles(sourceFolder, "*.*", SearchOption.TopDirectoryOnly)
                .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                            f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                            f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase));

            // 4️⃣ Process each image (how to batch OCR)
            foreach (var imagePath in imageFiles)
            {
                try
                {
                    // Initialise OCR engine for the current file
                    OcrEngine ocrEngine = new OcrEngine
                    {
                        Image = ImageStream.FromFile(imagePath)
                    };

                    // Run OCR – this extracts text from images
                    OcrResult result = ocrEngine.Recognize();

                    // 5️⃣ Save the result (extract text from images)
                    SaveOcrResult(outputFolder, imagePath, result.Text);

                    Console.WriteLine($"✅ {Path.GetFileName(imagePath)} processed.");
                }
                catch (Exception ex)
                {
                    // Gracefully handle problematic files
                    Console.WriteLine($"⚠️ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }

            Console.WriteLine("🎉 Batch OCR processing complete!");
        }

        // Helper to write the OCR output to a .txt file
        static void SaveOcrResult(string outputFolder, string imagePath, string recognizedText)
        {
            string textFilePath = Path.Combine(outputFolder,
                Path.GetFileNameWithoutExtension(imagePath) + ".txt");

            File.WriteAllText(textFilePath, recognizedText);
        }
    }
}
```

### Saída Esperada

Ao executar o programa, o console exibirá linhas semelhantes a:

```
✅ invoice001.png processed.
✅ receipt123.jpg processed.
✅ map.tif processed.
🎉 Batch OCR processing complete!
```

Enquanto isso, a pasta `C:\OCR\BatchTxt` conterá:

- `invoice001.txt`
- `receipt123.txt`
- `map.txt`

Cada arquivo possui a representação em texto puro de sua imagem de origem, pronto para indexação, busca ou análises posteriores.

## Dicas Profissionais & Armadilhas Comuns (processamento de OCR em lote)

- **Gerenciamento de memória:** Aspose OCR libera buffers de imagem após cada chamada `Recognize()`, mas se você processar milhares de arquivos, considere invocar `GC.Collect()` com moderação para manter a pegada de memória baixa.  
- **Aceleração:** Use `OcrEngine.RecognizeAsync()` no .NET 6+ e dispare múltiplas tarefas com `Task

## O que você deve aprender a seguir?

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Perform OCR on Archive Images with Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}