---
category: general
date: 2026-01-15
description: Tutorial C# OCR que mostra como reconhecer texto de imagem, extrair texto
  de fatura e converter imagem em texto usando Aspose OCR na GPU.
draft: false
keywords:
- c# ocr tutorial
- recognize text from image
- extract text from invoice
- convert image to text
- load image for ocr
language: pt
og_description: Tutorial de OCR em C# que ensina a reconhecer texto a partir de imagem,
  extrair texto de fatura e converter imagem em texto com Aspose OCR na GPU.
og_title: Tutorial de OCR em C# – Reconhecimento de Texto Rápido com GPU
tags:
- OCR
- C#
- Aspose
- GPU
title: Tutorial de OCR em C# – Reconheça Texto de Imagem com Aceleração por GPU
url: /pt/net/ocr-optimization/c-ocr-tutorial-recognize-text-from-image-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Reconhecer Texto de Imagem com Aceleração GPU

Já precisou de um **c# ocr tutorial** que realmente faça o trabalho sem intermináveis tentativas e erros? Talvez você esteja olhando para uma fatura de alta resolução e se perguntando como **extrair texto de fatura** arquivos em questão de segundos. A boa notícia é que você não precisa reinventar a roda—Aspose.OCR oferece uma API limpa, acelerada por GPU, que faz o trabalho pesado por você.

Neste guia, percorreremos um exemplo completo e executável que mostra como **recognize text from image** arquivos, **convert image to text**, e lidar com os problemas mais comuns. Ao final, você terá um programa autônomo que pode ler qualquer foto de um documento, de recibos a contratos escaneados, e gerar texto limpo e pesquisável.

## O que você aprenderá

- Como instalar e referenciar o pacote NuGet Aspose.OCR.
- Como configurar o mecanismo OCR para rodar na GPU com desempenho ultra‑rápido.
- A maneira correta de **load image for ocr** usando `OcrImage.FromFile`.
- Como chamar `Recognize` com o idioma desejado e obter o resultado.
- Dicas para lidar com PDFs de várias páginas, digitalizações de baixo contraste e tratamento de erros.

Não é necessário ter experiência prévia com Aspose; basta um ambiente de desenvolvimento .NET funcional (Visual Studio 2022 ou VS Code) e uma GPU modesta (até mesmo uma GPU integrada Intel serve).

---

## Etapa 1 – Instalar Aspose.OCR e Preparar seu Projeto

Primeiro de tudo: você precisa da biblioteca Aspose.OCR. A maneira mais fácil é via NuGet.

```bash
dotnet add package Aspose.OCR
```

> **Dica profissional:** Se você está mirando .NET 6 ou posterior, o pacote puxará automaticamente os binários nativos da GPU para Windows, Linux e macOS. Não há DLLs extras para copiar.

Depois que o pacote for adicionado, abra seu arquivo de projeto (`*.csproj`) e verifique a referência:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.12.0" />
</ItemGroup>
```

Agora você tem tudo o que precisa para começar a codificar.

## Etapa 2 – Criar um Motor OCR com Suporte a GPU (c# ocr tutorial)

O núcleo do **c# ocr tutorial** é o `OcrEngine`. Ao definir `Engine = Engine.Gpu` informamos à Aspose que use a placa gráfica em vez da CPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine with GPU acceleration.
            var ocrEngine = new OcrEngine
            {
                Engine = Engine.Gpu // GPU acceleration is selected; the library auto‑detects the device.
            };

            // The rest of the steps are broken out into separate methods for clarity.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            PerformOcr(ocrEngine, imagePath);
        }
    }
}
```

> **Por que GPU?** Uma GPU pode processar milhares de pixels em paralelo, reduzindo o tempo de OCR de segundos para frações de segundo em imagens grandes e de alta DPI.

## Etapa 3 – Carregar Imagem para OCR (load image for ocr)

Carregar a imagem corretamente é mais importante do que você imagina. `OcrImage.FromFile` suporta PNG, JPEG, BMP, TIFF e até páginas PDF. Também lê o DPI da imagem, o que influencia a precisão.

```csharp
static void PerformOcr(OcrEngine engine, string filePath)
{
    // Step 3: Load the image you want to recognize.
    // The FromFile method automatically detects the format.
    var image = OcrImage.FromFile(filePath);

    // Optional: Pre‑process the image for better results.
    // For example, you can increase contrast or convert to grayscale.
    image = ImagePreprocessor.AdjustContrast(image, 1.2);
    image = ImagePreprocessor.ConvertToGrayscale(image);
    
    // Continue to recognition...
    RecognizeAndDisplay(engine, image);
}
```

**Nota:** Se você estiver lidando com um PDF, pode extrair cada página como um `OcrImage` e alimentá‑las uma a uma.

## Etapa 4 – Reconhecer Texto de Imagem (recognize text from image)

Agora a mágica acontece. Pedimos ao motor que reconheça texto em inglês, mas você pode passar qualquer idioma suportado pela Aspose (Espanhol, Alemão, Chinês, etc.).

```csharp
static void RecognizeAndDisplay(OcrEngine engine, OcrImage image)
{
    // Step 4: Perform OCR on the image using the desired language.
    var result = engine.Recognize(image, Language.English);

    // Step 5: Output the recognized text.
    Console.WriteLine("=== OCR RESULT ===");
    Console.WriteLine(result.Text);
}
```

A propriedade `result.Text` contém a string simples. Se precisar da pontuação de confiança para cada palavra, pode inspecionar `result.Regions`.

### Saída Esperada

```
=== OCR RESULT ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,234.56
Thank you for your business!
```

Se a imagem estiver borrada, você pode ver caracteres confusos—é aqui que o pré‑processamento da Etapa 3 ajuda.

## Etapa 5 – Extrair Texto de Fatura – Exemplo do Mundo Real

Suponha que você tenha uma pasta cheia de faturas escaneadas e queira extrair o valor total. Abaixo está uma extensão rápida do código anterior que usa uma expressão regular simples.

```csharp
using System.Text.RegularExpressions;

static void ExtractTotalAmount(string ocrText)
{
    // Look for a pattern like "$1,234.56"
    var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
    if (match.Success)
        Console.WriteLine($"Detected total: {match.Value}");
    else
        Console.WriteLine("Total amount not found.");
}
```

Você chamaria `ExtractTotalAmount(result.Text);` logo após imprimir o resultado do OCR. Isso demonstra quão fácil é **extrair texto de fatura** arquivos assim que você tem a string bruta.

## Etapa 6 – Converter Imagem em Texto em Massa (convert image to text)

Processar um único arquivo é adequado para uma demonstração, mas código de produção frequentemente precisa lidar com dezenas ou centenas de imagens. Aqui está um loop conciso que processa um diretório inteiro:

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    foreach (var file in Directory.EnumerateFiles(folderPath, "*.*", SearchOption.TopDirectoryOnly)
                                 .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
    {
        Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
        var img = OcrImage.FromFile(file);
        var res = engine.Recognize(img, Language.English);
        Console.WriteLine(res.Text);
        ExtractTotalAmount(res.Text); // optional invoice extraction
    }
}
```

Executar `ProcessFolder(ocrEngine, @"C:\Invoices")` irá **converter imagem em texto** para cada arquivo suportado na pasta, aproveitando a GPU para velocidade.

## Casos de Borda e Armadilhas Comuns

| Situação | Por que acontece | Correção rápida |
|-----------|------------------|-----------------|
| **Digitalização de baixo contraste** | OCR tem dificuldade em diferenciar o primeiro plano do fundo. | Aumente o contraste (`ImagePreprocessor.AdjustContrast`) ou aplique limiarização adaptativa. |
| **PDF de várias páginas** | `OcrImage.FromFile` lê apenas a primeira página. | Use `PdfDocument` para extrair cada página como um `OcrImage` e iterar. |
| **Idioma não suportado** | O idioma padrão definido é o inglês. | Passe `Language.Spanish` ou qualquer valor de enumeração suportado. |
| **GPU não detectada** | Binários nativos ausentes ou driver desatualizado. | Verifique se o driver da GPU está atualizado; reinstale o pacote NuGet com a flag `-runtime`. |
| **Falta de memória em imagens enormes** | A memória da GPU é limitada. | Reduza a escala da imagem (`image = ImagePreprocessor.Resize(image, 2000, 0)`). |

## Exemplo Completo Funcional

Abaixo está o programa completo que você pode copiar‑colar em um novo aplicativo de console. Ele inclui todos os métodos auxiliares discutidos acima.

```csharp
using System;
using System.IO;
using System.Linq;
using System.Text.RegularExpressions;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize GPU‑accelerated OCR engine.
            var ocrEngine = new OcrEngine { Engine = Engine.Gpu };

            // 2️⃣ Define the path to a single image or a folder.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            // string folderPath = @"C:\Invoices";

            // Uncomment one of the following lines:
            PerformOcr(ocrEngine, imagePath);
            // ProcessFolder(ocrEngine, folderPath);
        }

        // -------------------------------------------------
        // Load image, preprocess, recognize, and display.
        // -------------------------------------------------
        static void PerformOcr(OcrEngine engine, string filePath)
        {
            var image = OcrImage.FromFile(filePath);
            image = ImagePreprocessor.AdjustContrast(image, 1.2);
            image = ImagePreprocessor.ConvertToGrayscale(image);

            var result = engine.Recognize(image, Language.English);
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(result.Text);

            ExtractTotalAmount(result.Text);
        }

        // -------------------------------------------------
        // Bulk processing of a folder.
        // -------------------------------------------------
        static void ProcessFolder(OcrEngine engine, string folderPath)
        {
            foreach (var file in Directory.EnumerateFiles(folderPath, "*.*")
                                          .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
            {
                Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
                var img = OcrImage.FromFile(file);
                var res = engine.Recognize(img, Language.English);
                Console.WriteLine(res.Text);
                ExtractTotalAmount(res.Text);
            }
        }

        // -------------------------------------------------
        // Simple regex to pull the total amount from an invoice.
        // -------------------------------------------------
        static void ExtractTotalAmount(string ocrText)
        {
            var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
            if (match.Success)
                Console.WriteLine($"Detected total: {match.Value}");
            else
                Console.WriteLine("Total amount not found.");
        }
    }
}
```

**Run it** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}