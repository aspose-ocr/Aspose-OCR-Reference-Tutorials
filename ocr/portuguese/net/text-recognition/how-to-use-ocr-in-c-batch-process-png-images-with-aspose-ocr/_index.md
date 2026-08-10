---
category: general
date: 2026-02-14
description: Como usar OCR em C# para extrair texto de arquivos PNG rapidamente. Aprenda
  OCR em lote de imagens, processe múltiplas imagens e use Aspose OCR C# em um único
  guia.
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: pt
og_description: Como usar OCR em C# com Aspose OCR C#. Este tutorial mostra como extrair
  texto de arquivos PNG, fazer OCR em lote de imagens e processar várias imagens de
  forma eficiente.
og_title: Como usar OCR em C# – Extração em lote de texto de PNG
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Como usar OCR em C# – Processamento em lote de imagens PNG com Aspose OCR
url: /pt/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

the shortcodes at start and end.

Let's produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Usar OCR em C# – Processamento em Lote de Imagens PNG com Aspose OCR

Já se perguntou **como usar OCR** para extrair texto de vários arquivos PNG sem escrever uma rotina separada para cada um? Você não está sozinho. Muitos desenvolvedores encontram dificuldades quando precisam **extrair texto PNG** em escala, especialmente quando as imagens estão em uma pasta e é necessário disparar o motor OCR para cada arquivo.  

Neste guia vamos percorrer uma solução completa, pronta‑para‑executar, que **processa OCR em lote**, **processa múltiplas imagens** em paralelo e utiliza a poderosa biblioteca **Aspose OCR C#**. Ao final, você terá um único executável que lê qualquer quantidade de PNGs, extrai seu texto e imprime os resultados no console — tudo com apenas algumas linhas de código.

## Pré‑requisitos

- .NET 6.0 ou superior (o código funciona também com .NET Core e .NET Framework)  
- Uma licença válida do Aspose.OCR para .NET (ou a versão de avaliação) – você pode obtê‑la no site da Aspose.  
- Uma pasta contendo os arquivos PNG que deseja ler.  
- Visual Studio 2022 (ou qualquer IDE compatível com C#).  

Nenhum pacote NuGet adicional é necessário além do `Aspose.OCR`.

## Etapa 1: Como Usar OCR – Inicializar o Motor Aspose OCR

A primeira coisa que você precisa é uma instância da classe `Engine`. Esse objeto abstrai a tecnologia OCR subjacente e pode ser executado em CPU ou GPU, dependendo do seu hardware e da licença.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*Por que isso importa:* Inicializar o motor uma única vez e reutilizá‑lo entre threads economiza memória e evita a sobrecarga de carregar modelos OCR repetidamente. Também garante configurações consistentes para todas as imagens.

## Etapa 2: Extrair Texto PNG – Coletar os Caminhos das Imagens

Em seguida, precisamos de uma coleção de caminhos de arquivos. Em um projeto real você poderia ler o diretório dinamicamente, mas para clareza listaremos alguns arquivos de exemplo.

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*Dica:* Substitua `YOUR_DIRECTORY` pelo caminho absoluto ou relativo das suas imagens. Se você tiver dezenas de arquivos, pode substituir a lista manual por `Directory.GetFiles("YOUR_DIRECTORY", "*.png")`.

## Etapa 3: OCR em Lote de Imagens – Executar o Reconhecimento em Paralelo

Processar imagens uma após a outra é simples, mas lento. Usando `Parallel.ForEach` podemos **processar múltiplas imagens** simultaneamente, aproveitando CPUs com múltiplos núcleos.

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*Por que paralelo?* Cada chamada ao OCR é intensiva em CPU, mas independente, então executá‑las concorrentemente pode reduzir drasticamente o tempo total, especialmente em máquinas com 4 núcleos ou mais.

## Etapa 4: Processar Múltiplas Imagens – Exibir o Texto Extraído

Agora que temos uma coleção de objetos `OcrResult`, podemos iterar sobre eles e imprimir o texto reconhecido. É aqui que normalmente você armazenaria a saída em um banco de dados ou gravaria em arquivos, mas a saída no console mantém o exemplo conciso.

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**Saída esperada no console (exemplo):**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

Se alguma imagem falhar ao ser carregada, o Aspose lançará uma exceção; você pode envolver a chamada `engine.Recognize` em um bloco try/catch para registrar erros sem abortar todo o lote.

## Etapa 5: Exemplo Completo – Todas as Peças Juntas

Abaixo está o programa completo que você pode copiar‑colar em um novo projeto de console C#. Ele inclui tudo, desde as instruções `using` até o loop final de saída.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### Executando o Exemplo

1. Crie um novo projeto **Console App** no Visual Studio.  
2. Adicione o pacote NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`).  
3. Substitua `YOUR_DIRECTORY` pelo caminho que contém seus arquivos PNG.  
4. Compile e execute – você deverá ver o texto extraído impresso no console.

## Dicas Avançadas & Casos de Borda

- **Aceleração por GPU:** Se você possui uma GPU compatível e uma licença Aspose OCR, habilite‑a via `EngineSettings` antes de criar o motor. Isso pode reduzir segundos por imagem.  
- **Arquivos grandes:** Para imagens maiores que 10 MB, considere redimensioná‑las primeiro para diminuir a pressão de memória.  
- **Suporte a idiomas:** Por padrão o motor assume inglês. Defina `engine.Language = Language.French;` (ou qualquer idioma suportado) para melhorar a precisão em textos não‑ingleses.  
- **Tratamento de erros:** O `try/catch` dentro do loop paralelo garante que um arquivo corrompido não interrompa todo o lote. Você também pode registrar falhas em um arquivo para revisão posterior.  
- **Armazenamento de resultados:** Em vez de imprimir, você pode gravar `result.Text` em um arquivo `.txt` usando `File.WriteAllText(Path.ChangeExtension(path, ".txt"))`.

## Conclusão

Agora você sabe **como usar OCR** em C# para **extrair texto PNG**, **processar OCR em lote** e **processar múltiplas imagens** de forma eficiente com Aspose OCR C#. A solução é totalmente autônoma, roda em paralelo e pode ser estendida para lidar com centenas ou milhares de arquivos com mudanças mínimas.

Pronto para o próximo passo? Experimente substituir a saída do console por um relatório CSV, teste a aceleração por GPU ou alimente o texto OCR em um índice de busca. As possibilidades são infinitas, e o padrão central — inicializar uma vez, executar em paralelo, tratar erros graciosamente — será útil em qualquer pipeline de processamento de imagens.

Bom código, e que seus trabalhos de OCR sejam rápidos e sem erros!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}