---
category: general
date: 2026-02-17
description: Como fazer OCR em lote de vários PDFs e imagens em C# usando Aspose OCR.
  Aprenda a extrair texto de PDF, converter PDF para texto e reconhecer texto de imagens.
draft: false
keywords:
- how to batch OCR
- extract text from pdf
- convert pdf to text
- recognize text from images
- extract text scanned pdf
language: pt
og_description: Como fazer OCR em lote de vários documentos em C# com Aspose OCR.
  Obtenha código passo a passo para extrair texto de PDF, converter PDF em texto e
  reconhecer texto de imagens.
og_title: Como fazer OCR em lote de arquivos em C# – Guia completo
tags:
- OCR
- C#
- Aspose
- PDF
- Text Extraction
title: Como fazer OCR em lote de arquivos em C# – Exemplo completo de código
url: /pt/net/text-recognition/how-to-batch-ocr-files-in-c-full-code-example/
---

. We'll keep exactly as is.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR em lote de arquivos em C# – Guia Completo

Já se perguntou **como fazer OCR em lote** de uma pilha de PDFs e digitalizações de imagens sem escrever um loop separado para cada arquivo? Você não está sozinho. A maioria dos desenvolvedores esbarra nessa barreira quando precisam extrair texto de dezenas de páginas de uma só vez. A boa notícia? Com o Aspose OCR você pode alimentar uma coleção de arquivos a um único motor e deixá‑lo fazer o trabalho pesado.  

Neste tutorial vamos percorrer uma solução prática que permite **extrair texto de pdf**, **converter pdf para texto** e **reconhecer texto de imagens** tudo em uma única execução em lote. Ao final você terá um aplicativo console pronto‑para‑executar que imprime o resultado do OCR para cada página, e entenderá o porquê de cada passo para poder adaptá‑lo aos seus próprios projetos.

## Pré-requisitos – O que você precisa antes de começar

- **.NET 6.0 ou superior** (o código também funciona no .NET Framework, mas .NET 6+ é recomendado)
- **Pacote NuGet Aspose.OCR** – instale com `dotnet add package Aspose.OCR`
- Alguns arquivos de exemplo: um PDF multipágina (`doc1.pdf`) e um TIFF escaneado (`doc2.tif`). Coloque‑os em uma pasta que você possa referenciar, por exemplo, `C:\OCRSamples`.
- Conhecimento básico de C# – você deve estar confortável com declarações `using` e coleções.

> Dica de especialista: Se você não tem uma licença, a Aspose oferece uma chave temporária gratuita que remove o limite de 100 páginas durante o desenvolvimento.

## Etapa 1: Configurar o Projeto e Importar Namespaces

Primeiro, crie um novo projeto console (ou adicione a um existente) e importe os namespaces necessários.

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;          // Aspose OCR core library
using Aspose.OCR.Image;   // ImageStream helper class
```

> **Por que isso importa:** Importar `Aspose.OCR.Image` fornece o conveniente método `ImageStream.FromFile`, que divide automaticamente as páginas do PDF em fluxos de imagem separados. Esse é o ingrediente secreto que torna o processamento em lote indolor.

## Etapa 2: Inicializar o Motor OCR

O motor é o cavalo de batalha que se comunica com o motor OCR subjacente. Você precisa de apenas uma instância para todo o lote.

```csharp
// Step 2: Create a single OcrEngine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **Explicação:** Reutilizar o mesmo `OcrEngine` reduz a rotatividade de memória e acelera o processamento porque as bibliotecas nativas permanecem carregadas entre as páginas.

## Etapa 3: Construir uma Lista de Fluxos de Imagem

Aqui reunimos todos os documentos que queremos processar. `ImageStream.FromFile` é inteligente o suficiente para dividir um PDF em páginas individuais, de modo que um PDF de três páginas se torne três fluxos separados nos bastidores.

```csharp
// Step 3: Assemble the collection of image streams
List<ImageStream> imageStreams = new List<ImageStream>
{
    ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
    ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
};
```

> **Caso extremo:** Se você tem uma mistura de PDFs, TIFFs, JPEGs ou PNGs, basta adicioná‑los à mesma lista – o Aspose detecta o formato automaticamente.

## Etapa 4: Executar a Operação de OCR em Lote

Agora entregamos a lista ao motor. `RecognizeBatch` devolve uma coleção de objetos `OcrResult`, um por página.

```csharp
// Step 4: Perform batch OCR on the supplied streams
IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

> **Por que em lote?** Executar OCR página a página em um loop manual força o motor a reinicializar a cada iteração, o que pode dobrar o tempo de processamento. `RecognizeBatch` mantém o motor aquecido e devolve os resultados à medida que ficam disponíveis.

## Etapa 5: Exibir o Texto Reconhecido

Finalmente, percorremos os resultados e escrevemos o texto de cada página no console. É aqui que você pode substituir `Console.WriteLine` por gravações em arquivo, inserções em banco de dados ou qualquer outra ação subsequente.

```csharp
// Step 5: Display the OCR output for each page
for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResults[pageIndex].Text);
}
```

### Saída esperada no console

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Se você executar o programa com os arquivos de exemplo, deverá ver um bloco de texto para cada página, provando que você **extraiu texto de pdf escaneado** com sucesso em uma única passagem.

## Lidando com armadilhas comuns

| Problema | Por que acontece | Correção rápida |
|----------|------------------|-----------------|
| **Erros de falta de memória** | PDFs grandes geram muitas imagens de alta resolução. | Limite o DPI ao carregar PDFs: `ocrEngine.Settings.ImageDpi = 200;` |
| **Caracteres estranhos** | A digitalização original é de baixa qualidade ou usa um idioma não suportado. | Defina o idioma explicitamente: `ocrEngine.Language = Language.English;` |
| **Resultados parciais** | A lista em lote contém um arquivo corrompido. | Envolva `RecognizeBatch` em um try/catch e registre `e.Message` para o arquivo problemático. |
| **Gargalo de desempenho** | Execução em thread única em máquina multi‑core. | Use `Parallel.ForEach` com instâncias separadas de `OcrEngine` por thread (avançado). |

## Bônus: Salvando resultados de OCR em arquivos de texto

Se preferir manter um arquivo `.txt` separado por página, basta adicionar um pequeno bloco de gravação dentro do loop:

```csharp
string outputPath = @"C:\OCRResults";
System.IO.Directory.CreateDirectory(outputPath);

for (int i = 0; i < ocrResults.Count; i++)
{
    string fileName = System.IO.Path.Combine(outputPath, $"Page_{i + 1}.txt");
    System.IO.File.WriteAllText(fileName, ocrResults[i].Text);
}
```

Agora você transformou **converter pdf para texto** em uma pasta organizada de arquivos de texto puro — perfeito para indexação ou busca subsequente.

## Exemplo completo em funcionamento

A seguir está o programa completo, pronto para copiar e colar. Sem dependências ocultas, sem scripts externos.

```csharp
// FullProgram.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Initialise OCR engine (reuse for the whole batch)
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: tweak settings for speed or accuracy
        ocrEngine.Settings.ImageDpi = 200;          // lower memory usage
        ocrEngine.Language = Language.English;     // set language explicitly

        // Build the list of image streams (PDF pages auto‑split)
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
            ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
        };

        // Perform batch OCR
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Output each page's text to console
        for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
        {
            Console.WriteLine($"--- Page {pageIndex + 1} ---");
            Console.WriteLine(ocrResults[pageIndex].Text);
        }

        // (Optional) Save each page to a .txt file
        string outputFolder = @"C:\OCRResults";
        System.IO.Directory.CreateDirectory(outputFolder);
        for (int i = 0; i < ocrResults.Count; i++)
        {
            string txtPath = System.IO.Path.Combine(outputFolder, $"Page_{i + 1}.txt");
            System.IO.File.WriteAllText(txtPath, ocrResults[i].Text);
        }
    }
}
```

Execute `dotnet run` a partir da pasta do projeto e veja o console se encher com o texto extraído. Esse é **como fazer OCR em lote** de uma coleção de documentos em apenas algumas linhas de C#.

## O que cobrimos – Resumo rápido

- Configurou um aplicativo console .NET e instalou o Aspose.OCR.  
- Criou uma única instância de `OcrEngine` para manter o processo eficiente.  
- Montou uma lista de objetos `ImageStream` que dividem PDFs em páginas automaticamente.  
- Executou `RecognizeBatch` para **extrair texto de pdf** e outros formatos de imagem de uma só vez.  
- Imprimiu os resultados e, opcionalmente, salvou‑os como arquivos `.txt` individuais, completando o fluxo de trabalho **converter pdf para texto**.  

## Próximos passos e tópicos relacionados

- **Escalar**: Use `Parallel.ForEach` com um pool de objetos `OcrEngine` para processar centenas de arquivos simultaneamente.  
- **Pacotes de idioma**: Troque `Language.English` por `Language.French` ou carregue um dicionário personalizado quando precisar **reconhecer texto de imagens** em outros idiomas.  
- **Pós‑processamento**: Encadeie a saída do OCR por um corretor ortográfico ou um analisador de linguagem natural para melhorar a precisão em contratos escaneados.  
- **Bibliotecas alternativas**: Compare o Aspose OCR com o Tesseract.NET se estiver buscando uma opção open‑source — ambos podem **extrair texto de pdf escaneado**, mas diferem em licenciamento e precisão pronta‑para‑uso.

---

![how to batch OCR example](alt="how to batch OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}