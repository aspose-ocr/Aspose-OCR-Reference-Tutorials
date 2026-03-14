---
category: general
date: 2026-03-13
description: Como usar OCR em C# para extrair texto de digitalizações. Aprenda a converter
  TIFF em texto com Aspose OCR, aceleração por GPU e código passo a passo.
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: pt
og_description: Como usar OCR em C# para extrair texto de digitalizações. Este guia
  mostra como converter TIFF em texto com Aspose OCR e aceleração por GPU.
og_title: Como usar OCR em C# – Extraia texto de digitalizações rapidamente
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Como usar OCR em C# – Extraia texto de digitalizações rapidamente
url: /pt/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

sure to keep markdown formatting.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Usar OCR em C# – Extrair Texto de Scans Rápido

Já se perguntou **como usar OCR** para extrair texto legível de uma pilha de arquivos TIFF escaneados? Você não está sozinho. Em muitos projetos do mundo real—pense em digitalização de faturas, arquivamento de documentos históricos ou simplesmente tornar PDFs pesquisáveis—os desenvolvedores precisam de uma maneira confiável de **extrair texto de scans** sem esforço.

A boa notícia? Com Aspose OCR e algumas linhas de C# você pode converter TIFF em texto em questão de segundos, mesmo em uma estação de trabalho modesta. A seguir você encontrará um exemplo completo, pronto‑para‑executar, além do raciocínio por trás de cada escolha para que você possa adaptá‑lo ao seu fluxo de trabalho.

## O Que Você Precisa

Antes de mergulharmos, certifique‑se de que tem o seguinte à mão:

| Pré‑requisito | Por que importa |
|--------------|----------------|
| .NET 6+ (ou .NET Framework 4.7+) | O pacote NuGet Aspose OCR tem como alvo runtimes .NET modernos. |
| Visual Studio 2022 (ou qualquer IDE de sua preferência) | Fornece IntelliSense e depuração fácil. |
| GPU compatível com CUDA & driver (opcional) | Permite `ocrEngine.UseGpu = true` para um aumento de velocidade perceptível em lotes grandes. |
| Uma pasta com imagens TIFF que você deseja processar | Este tutorial usa arquivos `*.tif`, mas você pode adaptar o padrão. |
| Pacote NuGet Aspose.OCR (`Install-Package Aspose.OCR`) | A biblioteca central que faz o trabalho pesado. |

Se estiver faltando algum desses itens, obtenha‑os agora—não adianta continuar a leitura só para encontrar uma dependência ausente depois.

## Visão Geral da Solução

Em alto nível o programa faz três coisas:

1. **Criar um motor OCR** e, opcionalmente, ativar a aceleração por GPU.  
2. **Iterar sobre cada arquivo TIFF** em um diretório, executar o reconhecimento e capturar o texto resultante.  
3. **Gravar o texto** em um arquivo `.txt` ao lado da imagem original.

É isso. O código é deliberadamente pequeno, mas demonstra boas práticas como seleção explícita de idioma, descarte adequado de recursos e tratamento de erros para os casos de borda mais comuns.

![Exemplo de como usar OCR em C#](/images/how-to-use-ocr-csharp.png "Ilustração de como usar OCR em C# para extrair texto de scans")

## Etapa 1: Inicializar o Motor OCR (Como Usar OCR)

A primeira coisa que você precisa é uma instância de `OcrEngine`. Esse objeto é a porta de entrada para toda a funcionalidade do Aspose OCR. Por padrão ele funciona na CPU, mas definir `UseGpu = true` indica à biblioteca que descarregue os cálculos de matriz pesados para sua placa de vídeo—desde que você tenha um driver compatível com CUDA instalado.

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**Por que isso importa:**  
- **Aceleração por GPU** pode reduzir o tempo de processamento em até 70 % para scans de alta resolução.  
- **Seleção explícita de idioma** evita que o motor adivinhe e melhora a precisão, especialmente para scripts não latinos.

## Etapa 2: Apontar o Motor para Seus Scans (Converter TIFF em Texto)

Em seguida, informamos ao programa onde procurar as imagens. Usar `Directory.GetFiles` com um filtro `*.tif` mantém a lógica simples e evita trazer arquivos não relacionados como `.jpg` ou `.png`.

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**Observação de caso de borda:** Se o diretório estiver vazio, o loop abaixo simplesmente nunca será executado, o que é perfeitamente aceitável. Você verá uma mensagem amigável “Nenhum arquivo encontrado” mais adiante.

## Etapa 3: Processar Cada Arquivo TIFF (Extrair Texto de Scans)

Agora o coração do programa: carregar cada imagem, executar OCR e persistir a saída. O helper `ImageStream.FromFile` transmite o arquivo diretamente para a memória, o que é mais eficiente que carregar um `Bitmap` primeiro.

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**Por que envolvemos cada iteração em um `try/catch`:**  
Processar um lote de documentos é bagunçado; um TIFF corrompido ou um pico de falta de memória não deve abortar toda a execução. O bloco `catch` registra o problema e segue em frente, mantendo o pipeline robusto.

### Saída Esperada

Para cada `example.tif` você encontrará um `example.txt` irmão contendo algo como:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

Se o motor OCR não conseguir ler uma linha, ele simplesmente deixará uma linha em branco ou um caractere distorcido—nada falha.

## Etapa 4: Limpeza e Descarte (Boa Prática)

`OcrEngine` implementa `IDisposable`, portanto é educado liberar recursos nativos quando terminar. Em um pequeno aplicativo console você poderia contar com o GC, mas o descarte explícito é um hábito que vale a pena cultivar.

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

Abaixo está o programa completo que você pode colar em um novo projeto de Console App. Ele compila como‑está, assumindo que você já adicionou o pacote NuGet Aspose.OCR.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### Lista de Verificação Rápida

- **Flag de GPU** – remova ou defina como `false` se não houver driver CUDA.  
- **Idioma** – troque `Language.English` por qualquer outro idioma suportado.  
- **Padrão de arquivo** – altere `"*.tif"` para `"*.png"` ou `"*.*"` se seus scans estiverem em outro formato.  

## Armadilhas Comuns & Dicas Profissionais (tutorial c# OCR)

| Armadilha | Como evitá‑la |
|----------|---------------|
| **Erros de falta de memória** em lotes enormes | Processar arquivos em blocos menores ou chamar `GC.Collect()` a cada 50 arquivos (raramente necessário). |
| **GPU não detectada** mas `UseGpu = true` | O motor recua silenciosamente para a CPU, mas você pode verificar `ocrEngine.IsGpuAvailable` após a construção. |
| **Pacote de idioma errado** gera saída distorcida | Sempre defina `ocrEngine.Language` explicitamente; o padrão pode ser `Language.Unknown`. |
| **Caminho de arquivo contém caracteres Unicode** | Use `Path.GetFullPath` para normalizar, ou prefixe com `@"\\?\"` no Windows se os caminhos excederem |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}