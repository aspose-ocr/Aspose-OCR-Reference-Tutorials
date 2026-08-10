---
category: general
date: 2026-02-19
description: Aprenda a fazer OCR em lote com Aspose.OCR em C#. Este guia mostra como
  extrair texto de imagens e converter imagens em txt de forma eficiente.
draft: false
keywords:
- how to batch ocr
- extract text from images
- convert images to txt
- Aspose OCR batch processing
- C# image to text conversion
language: pt
og_description: Como fazer OCR em lote com Aspose.OCR em C#. Extraia texto de imagens
  e converta imagens para txt em alguns passos fáceis.
og_title: Como fazer OCR em lote em C# – Conversão rápida de imagem para texto
tags:
- OCR
- C#
- Aspose
title: Como fazer OCR em lote no C# – Extraia texto de imagens rapidamente
url: /pt/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR em lote no C# – Guia Completo Passo a Passo

Já se perguntou **como fazer OCR em lote** em uma pasta inteira de imagens sem escrever um programa separado para cada arquivo? Você não está sozinho. Muitos desenvolvedores esbarram em um obstáculo quando precisam extrair texto de dezenas — ou até milhares — de páginas escaneadas, recibos ou capturas de tela. A boa notícia? Com o Aspose.OCR você pode automatizar todo o fluxo, **extrair texto de imagens** e **converter imagens em txt** com apenas algumas linhas de código.

Neste tutorial vamos percorrer um exemplo completo, pronto‑para‑executar, que mostra exatamente como configurar um processador de OCR em lote, ajustar o pré‑processamento, lidar com paralelismo e gravar cada resultado em um arquivo `.txt`. Ao final, você terá um aplicativo console autônomo que pode ser inserido em qualquer projeto .NET.

## O que você vai precisar

- .NET 6.0 ou superior (o código funciona também em .NET Core e .NET Framework)
- Pacote NuGet Aspose.OCR for .NET (`Aspose.OCR`)  
- Uma pasta cheia de arquivos de imagem (`.png`, `.jpg`, etc.) que você deseja processar
- Uma quantidade moderada de RAM; a demonstração usa 4 threads paralelas, mas você pode ajustá‑las

Sem serviços externos, sem arquivos de configuração ocultos — apenas código C# puro que você pode compilar e executar hoje.

![Diagrama ilustrando o fluxo de processamento de OCR em lote](/images/how-to-batch-ocr-flow.png "diagrama do fluxo de OCR em lote")

## Etapa 1: Instalar o Aspose.OCR e Configurar o Projeto

Primeiro, adicione o pacote Aspose.OCR ao seu projeto:

```bash
dotnet add package Aspose.OCR
```

Por que isso importa: o Aspose.OCR inclui o motor de OCR, os dados de idioma e as utilidades de pré‑processamento, então você não precisará de binários de terceiros. Depois que o pacote for instalado, crie um novo aplicativo console (ou adicione o código a um existente) e importe os namespaces necessários:

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
```

Essas instruções `using` dão acesso às classes do processador em lote e aos auxiliares de I/O.

## Etapa 2: Configurar o Processador de OCR em Lote

Agora vamos instanciar `OcrBatchProcessor` e dizer a ele qual idioma procurar, como limpar as imagens e quantas threads executar em paralelo. Este é o coração de **como fazer OCR em lote** de forma eficiente.

```csharp
// Step 2: Create and configure the OCR batch processor
var ocrBatch = new OcrBatchProcessor
{
    // Language selection – English is the most common, but you can change it
    Language = Language.English,

    // Preprocessing improves accuracy; Deskew removes rotation
    Preprocessing = new PreprocessingOptions
    {
        Deskew = DeskewAdvanced.Enable()
    },

    // Parallelism – adjust based on your CPU/GPU capabilities
    MaxDegreeOfParallelism = 4
};
```

**Por que habilitar Deskew?** Muitos documentos escaneados não estão perfeitamente alinhados; o algoritmo de deskew os rotaciona de volta a uma linha de base reta, o que costuma aumentar as taxas de reconhecimento em 10‑15 %.

## Etapa 3: Conectar um Callback de Resultado para Salvar Arquivos de Texto

O processador em lote dispara um evento para cada imagem concluída. Vamos nos inscrever em `ResultProcessed` para que possamos gravar cada resultado de OCR em um arquivo `.txt` — efetivamente **converter imagens em txt** em tempo real.

```csharp
// Step 3: Register a callback to save each OCR result as a text file
ocrBatch.ResultProcessed += (sender, args) =>
{
    // Change the original file extension to .txt
    string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");

    // Write the recognized text to the new file
    File.WriteAllText(txtPath, args.Result.Text);

    // Inform the console for debugging / progress monitoring
    Console.WriteLine($"Processed: {args.ImagePath}");
};
```

Dica rápida: se precisar preservar a estrutura de pastas original, você pode modificar `txtPath` para incluir subpastas ou um diretório de saída separado.

## Etapa 4: Executar o Lote na Sua Pasta de Imagens

Só falta apontar o processador para a pasta que contém as imagens das quais você quer **extrair texto de imagens**. O método `ProcessFolder` varre subpastas recursivamente, então você pode soltar uma árvore inteira de escaneamentos e deixar a biblioteca cuidar do resto.

```csharp
// Step 4: Run the batch on all image files in the target folder
ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
```

Ao iniciar o programa, você verá uma saída no console como:

```
Processed: C:\Path\To\Your\Images\invoice1.png
Processed: C:\Path\To\Your\Images\receipt_2024.jpg
...
```

Cada imagem agora tem um arquivo `.txt` irmão contendo o texto extraído.

## Exemplo Completo Funcionando

Juntando tudo, aqui está o programa completo que você pode copiar‑colar em `Program.cs`:

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR batch processor
        var ocrBatch = new OcrBatchProcessor
        {
            Language = Language.English,
            Preprocessing = new PreprocessingOptions
            {
                Deskew = DeskewAdvanced.Enable()
            },
            // Step 2: Define the level of parallelism (adjust for your CPU/GPU)
            MaxDegreeOfParallelism = 4
        };

        // Step 3: Register a callback to save each OCR result as a text file
        ocrBatch.ResultProcessed += (sender, args) =>
        {
            string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");
            File.WriteAllText(txtPath, args.Result.Text);
            Console.WriteLine($"Processed: {args.ImagePath}");
        };

        // Step 4: Run the batch on all image files in the target folder
        ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
    }
}
```

### Saída Esperada

- Para cada `*.png` ou `*.jpg` no diretório de origem, aparece um arquivo `*.txt` correspondente ao lado.
- O console imprime uma linha por arquivo, fornecendo feedback em tempo real.
- Se uma imagem não puder ser lida (arquivo corrompido, formato não suportado), o Aspose.OCR registra um erro mas continua processando o restante — graças à robustez embutida do motor em lote.

## Perguntas Frequentes & Casos de Borda

### E se eu precisar processar PDFs em vez de imagens?

O Aspose.OCR pode aceitar páginas de PDF como imagens internamente, mas você precisará converter o PDF em imagens raster primeiro (por exemplo, usando Aspose.PDF). Uma vez que você tenha PNGs, o mesmo código de lote funciona sem alterações.

### Posso mudar o idioma em tempo de execução?

Sim. A propriedade `Language` aceita qualquer valor do enum `Language` (Spanish, French, Chinese, etc.). Se você tem documentos multilíngues, considere executar duas passagens — uma por idioma — ou usar `Language.AutoDetect`.

### Como limitar o lote a tipos de arquivo específicos?

`ProcessFolder` aceita um `SearchOption` opcional e um `string[] extensions`. Exemplo:

```csharp
ocrBatch.ProcessFolder(@"C:\Images", new[] { ".png", ".tif" });
```

### E quanto à aceleração por GPU?

O Aspose.OCR oferece suporte a GPU via a configuração `OcrEngine`, mas o `MaxDegreeOfParallelism` do processador em lote continua sendo o principal controle de concorrência. Se você possui uma GPU compatível, habilite‑a nas configurações do engine antes de criar o `OcrBatchProcessor`.

### Como lidar com pastas muito grandes (dezenas de milhares de arquivos)?

- Aumente `MaxDegreeOfParallelism` com cautela; muitas threads podem esgotar a memória.
- Use uma pasta de saída dedicada para evitar desordem.
- Periodicamente despeje logs em disco para prevenir aumento de memória.

## Dicas Profissionais para OCR de Alta Qualidade

- **DPI Importa**: Imagens com 300 DPI ou mais oferecem a melhor precisão. Se suas digitalizações forem menores, considere aumentar a escala com um filtro bicúbico antes do processamento.
- **Redução de Ruído**: Ative `Preprocessing.NoiseRemoval` se as imagens de origem forem granuladas.
- **Nomeação de Arquivos**: Mantenha nomes curtos e alfanuméricos; caracteres especiais podem confundir a lógica do caminho no callback.
- **Logging**: Substitua `Console.WriteLine` por um logger adequado (ex.: `Serilog`) para cargas de trabalho em produção.

## Próximos Passos

Agora que você dominou **como fazer OCR em lote**, pode querer:

- **Extrair texto de imagens** e alimentar a saída em um índice de busca (ex.: Elasticsearch) para pesquisa full‑text.
- **Converter imagens em txt** e então executar processamento de linguagem natural (NLP) para classificar documentos automaticamente.
- Experimentar **pacotes de idioma diferentes** ou dicionários personalizados para terminologia específica de setores.

Se estiver curioso sobre pós‑processamento, confira tutoriais como “Parsing OCR output with regular expressions” ou “Storing OCR results in a SQL database”.

---

**Feliz codificação!** Sinta‑se à vontade para ajustar o paralelismo, adicionar mais etapas de pré‑processamento ou encapsular tudo em um serviço Windows para monitoramento contínuo. O céu é o limite quando você combina as capacidades de lote do Aspose.OCR com um pouco de engenhosidade .NET.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}