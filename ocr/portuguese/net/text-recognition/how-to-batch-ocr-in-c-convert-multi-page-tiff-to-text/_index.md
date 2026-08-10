---
category: general
date: 2026-03-28
description: Aprenda como fazer OCR em lote em C# e converter TIFF para texto facilmente.
  Este guia passo a passo mostra como extrair texto de arquivos TIFF usando o Aspose
  OCR.
draft: false
keywords:
- how to batch ocr
- convert tiff to text
- extract text from tiff
- c# ocr tutorial
language: pt
og_description: Como fazer OCR em lote em C#? Siga este tutorial completo para converter
  arquivos TIFF de várias páginas em texto pesquisável usando o Aspose OCR.
og_title: Como fazer OCR em lote em C# – Converter TIFF multipágina em texto
tags:
- OCR
- C#
- Aspose
title: Como fazer OCR em lote em C# – Converter TIFF multipágina em texto
url: /pt/net/text-recognition/how-to-batch-ocr-in-c-convert-multi-page-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR em lote em C# – Converter TIFF de várias páginas para texto

Já se perguntou **como fazer OCR em lote** em uma pilha de páginas escaneadas sem precisar escrever um loop para cada imagem? Você não está sozinho. Em muitos projetos — pense em processamento de notas fiscais ou digitalização de arquivos — a necessidade de **converter TIFF para texto** surge diariamente, e fazer isso página por página rapidamente se torna um pesadelo.

A boa notícia? Com algumas linhas de C# e Aspose OCR você pode alimentar um TIFF de várias páginas inteiro no motor e obter um dicionário de números de página mapeados para suas strings extraídas. Neste tutorial vamos percorrer um exemplo completo e executável que mostra exatamente **como fazer OCR em lote**, como **extrair texto de TIFF**, e por que essa abordagem supera a alternativa manual.

## O que você vai aprender

- Configurar a biblioteca Aspose OCR em um projeto .NET.  
- Carregar um arquivo TIFF de várias páginas usando `Image.FromMultiPageFile`.  
- Executar `RecognizeBatch` para obter um `Dictionary<int,string>` com os resultados por página.  
- Imprimir a saída em um formato limpo e legível.  

Ao final, você terá um aplicativo de console pronto‑para‑executar que transforma qualquer TIFF de várias páginas em texto simples — sem ferramentas extras necessárias.  

### Pré‑requisitos

- .NET 6.0 SDK (ou qualquer versão recente do .NET).  
- Visual Studio 2022 ou VS Code — seu IDE favorito serve.  
- Uma licença válida do Aspose OCR ou uma chave de avaliação gratuita (a API funciona sem licença, mas adiciona uma marca d'água).  
- Um TIFF de várias páginas de exemplo chamado `multipage.tif` colocado em uma pasta que você possa referenciar.

> **Dica profissional:** Se você estiver no Windows, a pasta padrão do projeto é um local conveniente para colocar o TIFF; no Linux/macOS basta ajustar o caminho conforme necessário.

## Etapa 1: Instalar o pacote NuGet Aspose OCR

Antes de escrever qualquer código, precisamos da biblioteca OCR. Abra um terminal na pasta do seu projeto e execute:

```bash
dotnet add package Aspose.OCR
```

Isso baixa a versão estável mais recente (a partir de março 2026 v23.9) e adiciona os DLLs necessários ao seu projeto. Nenhuma configuração extra é necessária para um aplicativo de console simples.

## Etapa 2: Criar o esqueleto do aplicativo de console

Vamos gerar um programa mínimo que referencia o motor OCR. As diretivas `using` são cruciais — sem elas o compilador reclamará de tipos ausentes.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Required for Image class
```

> **Por que isso importa:** A classe `Image` está em um sub‑namespace, e esquecer a importação `ImageProcessing` resultará em um erro “type or namespace not found” que pode desperdiçar uma hora de depuração.

Agora adicione o método `Main` e um breve comentário descrevendo o propósito:

```csharp
/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        // Implementation will go here
    }
}
```

## Etapa 3: Inicializar o motor OCR

O `OcrEngine` é o responsável principal. Instanciá‑lo uma única vez e reutilizá‑lo para todas as páginas é tanto econômico em memória quanto rápido.

```csharp
// Step 3: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **O que está acontecendo nos bastidores?** O motor carrega modelos de idioma e pré‑configura as definições padrão (ex.: inglês, rotação automática). Você pode ajustar isso depois, mas os padrões são sólidos para a maioria dos documentos.

## Etapa 4: Carregar o TIFF de várias páginas

Aspose torna o carregamento de imagens com múltiplos quadros simples. Forneça o caminho completo ou um relativo a partir do diretório de trabalho do executável.

```csharp
// Step 4: Load a multi‑page TIFF image
string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // ← replace with your actual path
var multiPageImage = Image.FromMultiPageFile(tiffPath);
```

Se o arquivo não for encontrado, `FromMultiPageFile` lança uma `FileNotFoundException`. Envolva‑o em um `try/catch` se precisar de tratamento de erro elegante — algo que mostraremos na próxima etapa.

## Etapa 5: Executar OCR em lote

Agora vem a estrela do show: `RecognizeBatch`. Ele devolve um `Dictionary<int,string>` onde a chave é o índice da página (começando em 0) e o valor é o texto reconhecido.

```csharp
// Step 5: Perform batch OCR on all pages
Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);
```

> **Caso extremo:** Alguns TIFFs contêm páginas em branco. Aspose devolve uma string vazia para essas páginas, que você pode filtrar depois se não quiser lixo na saída.

## Etapa 6: Exibir os resultados

Finalmente, itere sobre o dicionário e imprima o texto de cada página. Usar strings interpoladas mantém o código organizado.

```csharp
// Step 6: Output the recognized text for each page
foreach (var pageResult in ocrResults)
{
    Console.WriteLine($"--- Page {pageResult.Key + 1} ---"); // +1 for human‑friendly numbering
    Console.WriteLine(pageResult.Value);
    Console.WriteLine(); // Blank line for readability
}
```

Executar o programa deve produzir algo como:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
...

--- Page 2 ---
Terms and Conditions
...
```

Se você vir saída ilegível, verifique se o TIFF de origem não está corrompido e se o idioma do texto corresponde ao padrão do motor (Inglês). Você também pode definir `ocrEngine.Language = OcrLanguage.Spanish;` para documentos que não estejam em inglês.

## Exemplo completo funcionando

Juntando todas as peças, aqui está o programa completo que você pode copiar‑colar em `Program.cs` e executar:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Needed for Image class

/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        try
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Load a multi‑page TIFF image
            string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // Change to your actual file location
            var multiPageImage = Image.FromMultiPageFile(tiffPath);

            // Step 3: Perform batch OCR on all pages
            Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);

            // Step 4: Output the recognized text for each page
            foreach (var pageResult in ocrResults)
            {
                Console.WriteLine($"--- Page {pageResult.Key + 1} ---");
                Console.WriteLine(pageResult.Value);
                Console.WriteLine(); // Extra line for visual separation
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

Salve, compile e execute:

```bash
dotnet run
```

Você deverá ver o conteúdo extraído de cada página impresso no console. Esse é todo o **c# ocr tutorial** que você pediu.

## Perguntas frequentes & casos de borda

### E se o meu TIFF contiver dezenas de páginas?

`RecognizeBatch` processa todos os quadros em uma única chamada, mas o uso de memória cresce linearmente com o número de páginas. Para documentos muito grandes (centenas de páginas) considere processar em blocos:

```csharp
for (int i = 0; i < multiPageImage.PageCount; i += 50)
{
    var subImage = multiPageImage.GetPages(i, Math.Min(50, multiPageImage.PageCount - i));
    var partialResults = ocrEngine.RecognizeBatch(subImage);
    // Merge partialResults into the main dictionary...
}
```

### Posso salvar o texto extraído em arquivos ao invés de imprimir?

Com certeza. Substitua o bloco `Console.WriteLine` por operações de I/O de arquivos:

```csharp
string outputFolder = "ExtractedText";
Directory.CreateDirectory(outputFolder);

foreach (var pageResult in ocrResults)
{
    string filePath = Path.Combine(outputFolder, $"Page_{pageResult.Key + 1}.txt");
    File.WriteAllText(filePath, pageResult.Value);
}
```

Agora cada página recebe seu próprio arquivo `.txt` — perfeito para indexação posterior.

### Como altero o idioma de saída ou habilito rotação automática?

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
ocrEngine.AutoRotate = true;             // Detects rotated text automatically
```

Essas configurações devem ser aplicadas **antes** de chamar `RecognizeBatch`.

## Conclusão

Cobremos **como fazer OCR em lote** em um TIFF de várias páginas usando Aspose OCR em C#. Ao carregar a imagem uma única vez, chamar `RecognizeBatch` e iterar sobre o dicionário resultante, você pode **converter TIFF para texto** em questão de segundos. O exemplo também mostra como **extrair texto de TIFF**, lidar com erros e, opcionalmente, gravar os resultados em arquivos — tudo dentro de um aplicativo de console limpo e autocontido.

Pronto para o próximo passo? Experimente combinar essa abordagem com uma biblioteca de geração de PDF para produzir PDFs pesquisáveis, ou conecte a saída a um banco de dados para arquivos pesquisáveis. Você também pode experimentar outros formatos de imagem (PNG, JPEG) trocando `Image.FromMultiPageFile` por `Image.FromFile`.

Tem mais perguntas sobre OCR, licenciamento ou otimização de desempenho? Deixe um comentário abaixo, e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}