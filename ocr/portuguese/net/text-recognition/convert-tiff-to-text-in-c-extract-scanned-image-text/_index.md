---
category: general
date: 2026-03-05
description: Converter TIFF para texto em C# com Aspose OCR — extraia rapidamente
  texto de arquivos de imagens escaneadas e aprenda como carregar arquivos de imagem
  em C# para processamento OCR.
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: pt
og_description: Converta TIFF em texto em C# usando Aspose OCR. Aprenda todo o fluxo
  de trabalho para extrair texto de imagens digitalizadas e carregar arquivos de imagem
  de forma eficiente.
og_title: Converter TIFF para Texto em C# – Extrair Texto de Imagem Digitalizada
tags:
- OCR
- C#
- Aspose
title: Converter TIFF para Texto em C# – Extrair Texto de Imagem Escaneada
url: /pt/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter TIFF para Texto em C# – Extrair Texto de Imagem Digitalizada

Precisa **converter TIFF para texto em C#**? Você não é o único lutando com imagens digitalizadas de várias páginas que se recusam obstinadamente a se tornar strings pesquisáveis.  
Neste guia, vamos percorrer uma solução completa, pronta‑para‑executar, que recebe um arquivo TIFF, o envia para o Aspose OCR e gera texto simples — sem serviços adicionais, sem mágica oculta.

> **Dica profissional:** Se você estiver lidando com digitalizações de alta resolução, habilitar o processamento GPU pode economizar segundos em cada página.

Também mostraremos como **extrair texto de imagens digitalizadas** e a melhor forma de **carregar arquivo de imagem C#** no motor OCR, para que você possa incorporar essa lógica em qualquer projeto .NET hoje.

---

## O que você precisará

| Requisito | Motivo |
|-----------|--------|
| .NET 6.0+ (or .NET Framework 4.7.2+) | Runtime moderno, suporta `Span<T>` e I/O assíncrono |
| Aspose.OCR for .NET (NuGet package `Aspose.OCR`) | O motor OCR que usaremos |
| A valid Aspose OCR license file (`Aspose.OCR.lic`) | Sem ele você atingirá limites de avaliação |
| A TIFF file (single‑ or multi‑page) to test | Exemplo usado: `scanned_multi_page.tif` |
| GPU with CUDA 11+ (optional) | Acelera o reconhecimento quando `EngineMode = Gpu` |

Se estiver faltando algum desses, obtenha o pacote NuGet agora:

```bash
dotnet add package Aspose.OCR
```

---

## Etapa 1: Configurar o Projeto e Importar Namespaces

Crie um novo aplicativo console (ou adicione o código a um projeto existente). A primeira coisa que fazemos é importar as classes que precisaremos.

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **Por que isso importa:** Importar `Aspose.OCR.Image` nos fornece a fábrica `ImageStream`, que pode ler arquivos TIFF diretamente do disco ou de um stream. Pular esta etapa causará um erro de compilação.

---

## Etapa 2: Inicializar o Motor OCR e Escolher o Modo de Processamento

O motor OCR deve ser configurado **antes** de atribuir qualquer imagem. É aqui que decidimos se ele será executado na CPU ou utilizará a GPU.

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*Se você estiver em um servidor sem interface gráfica e sem placa de vídeo, altere `Gpu` para `Cpu` ou `Auto`.*  
O modo do motor influencia a alocação de memória e a velocidade; o modo GPU pode ser 2‑3× mais rápido em TIFFs grandes e de alta resolução.

---

## Etapa 3: Aplicar sua Licença Aspose OCR

Executar sem licença limita você a algumas páginas e marcas d'água. Carregue sua licença cedo para que todas as operações subsequentes sejam ilimitadas.

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **Armadilha comum:** Colocar `SetLicense` após `Recognize()` fará com que o motor volte ao modo de avaliação para essa chamada.

---

## Etapa 4: Carregar o Arquivo TIFF – Manipulando Imagens de Página Única e Multi‑Página

O Aspose OCR pode ler TIFFs multi‑página nativamente, mas você precisa fornecer o stream correto. Aqui está um padrão robusto que funciona em ambos os cenários.

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### Por que usar `ImageStream.FromFile`?

- Ele abstrai o `FileStream` subjacente, lidando com a enumeração de páginas TIFF internamente.  
- Também funciona com `MemoryStream`, permitindo carregar imagens de um banco de dados ou de uma API web sem tocar no sistema de arquivos.

### Caso extremo: TIFFs muito grandes

Se o seu TIFF exceder 200 MB, considere carregá‑lo página por página para evitar exceções de falta de memória:

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

---

## Etapa 5: Verificar a Saída

Ao executar o programa, você deverá ver algo como:

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

Se o texto parecer confuso, verifique novamente:

1. **Resolution** – OCR funciona melhor com 300 dpi ou mais.  
2. **EngineMode** – Troque para `Cpu` se o driver da GPU estiver desatualizado.  
3. **License** – Certifique‑se de que o caminho do arquivo de licença está correto e que o arquivo é legível.

---

## Perguntas Frequentes (FAQ)

### Isso funciona com outros formatos de imagem?

Absolutamente. `ImageStream.FromFile` suporta JPEG, PNG, BMP e até PDF (via Aspose.PDF). Basta substituir a extensão do arquivo.

### E se eu precisar processar imagens armazenadas em um banco de dados?

Leia o BLOB em um `MemoryStream` e passe‑o para `ImageStream.FromStream(memoryStream)`. O motor OCR o trata da mesma forma que um stream baseado em arquivo.

### Posso executar isso no Linux?

Sim — o Aspose OCR é multiplataforma. Instale o runtime .NET adequado e certifique‑se de que as bibliotecas nativas necessárias para GPU (se usadas) estejam disponíveis.

---

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

Abaixo está o programa completo, pronto para compilar. Substitua `YOUR_DIRECTORY` e o caminho do arquivo de licença pelos seus locais reais.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

Salve isso como `Program.cs`, execute `dotnet run` e observe o texto

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}