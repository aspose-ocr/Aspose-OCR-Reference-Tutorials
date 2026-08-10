---
category: general
date: 2026-03-26
description: Como fazer OCR em lote em C# facilita a extração de texto de arquivos
  PNG. Siga este tutorial passo a passo de OCR em C# para extração em lote de texto
  com Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- c# ocr tutorial
- how to create OCR
- batch text extraction
language: pt
og_description: Como fazer OCR em lote em C# permite extrair rapidamente texto de
  arquivos PNG. Este guia conduz você por um tutorial completo de OCR em C# com extração
  de texto em lote.
og_title: Como fazer OCR em lote no C# – Extrair texto de PNG
tags:
- OCR
- C#
- Aspose
title: Como fazer OCR em lote no C# – Extrair texto de PNG
url: /pt/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR em lote em C# – Extrair texto de PNG

Já se perguntou **como fazer OCR em lote** em uma pilha de capturas de tela sem escrever um programa separado para cada arquivo? Você não está sozinho. Em muitos projetos acabamos com dezenas de PNGs que precisam ter seu texto extraído, e fazer isso um‑por‑um é um incômodo.  

Boa notícia? Com Aspose OCR você pode criar um pequeno aplicativo console C# que processa todas essas imagens em paralelo, oferecendo **extração de texto em lote** rápida e um conjunto de resultados limpo. Neste guia vamos percorrer um **tutorial completo de c# ocr**, explicar por que cada parte importa e mostrar exatamente como a saída se parece.

Ao final deste artigo você será capaz de:

* Carregar uma lista de arquivos PNG (ou qualquer imagem suportada) de uma só vez.  
* Configurar um `OcrEngine` compartilhado para que as configurações permaneçam consistentes ao longo do lote.  
* Executar a fila de reconhecimento com até quatro workers paralelos.  
* Obter o texto reconhecido de cada página e imprimi-lo no console.

Sem mágica, apenas código sólido que você pode inserir na sua solução hoje.

## O que você precisará

Antes de mergulharmos, certifique‑se de que você tem:

* .NET 6 SDK (ou qualquer versão recente do .NET).  
* Uma licença válida do Aspose OCR ou uma chave de avaliação temporária.  
* Uma pasta que contém os arquivos PNG que você deseja processar.  
* Visual Studio 2022 ou seu editor favorito.

É isso — sem pacotes NuGet extras além de `Aspose.OCR` e o padrão `System.Collections.Generic`.

## Como fazer OCR em lote – Configurando o projeto

Primeiro de tudo, crie um novo projeto console e inclua a biblioteca Aspose OCR.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

Depois que a restauração terminar, abra **Program.cs** (ou crie um novo arquivo) e adicione as diretivas `using` habituais:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
```

Essa estrutura simples nos dá acesso ao `OcrEngine`, `RecognitionQueue` e às classes auxiliares que precisaremos mais tarde.

## Extrair texto de PNG – Preparando a lista de imagens

Agora precisamos dizer ao programa **quais PNGs** devem ser processados pelo OCR. A maneira mais direta é construir um `List<string>` que contém caminhos absolutos ou relativos.

```csharp
// Step 1: Define the image files to be processed
var imagePaths = new List<string>
{
    @"YOUR_DIRECTORY/page1.png",
    @"YOUR_DIRECTORY/page2.png",
    @"YOUR_DIRECTORY/page3.png",
    @"YOUR_DIRECTORY/page4.png"
};
```

Substitua `YOUR_DIRECTORY` pelo caminho real da pasta. Se você tem um conjunto dinâmico, também pode usar `Directory.GetFiles(@"YOUR_DIRECTORY", "*.png")` e alimentar o resultado na lista. O ponto principal é que **extrair texto de PNG** é apenas uma questão de fornecer os nomes de arquivos corretos para a fila.

![Fluxo de OCR em lote](https://example.com/placeholder.png "Diagrama ilustrando como fazer OCR em lote em uma coleção de arquivos PNG")

*Texto alternativo da imagem: diagrama do fluxo de OCR em lote*

## Tutorial de OCR em C# – Configurando a fila de reconhecimento

O coração da operação em lote é o `RecognitionQueue`. Pense nele como uma esteira que entrega cada imagem a um `OcrEngine` compartilhado. Ao compartilhar o engine, mantemos o uso de memória baixo e garantimos configurações idênticas para cada página.

```csharp
// Step 2: Create a recognition queue with shared OCR engine and parallelism
var recognitionQueue = new RecognitionQueue
{
    MaxDegreeOfParallelism = 4,          // run up to 4 images at the same time
    Engine = new OcrEngine()            // shared configuration for all images
};
```

Por que definir `MaxDegreeOfParallelism` como 4? Em um laptop quad‑core típico isso oferece o melhor rendimento sem sobrecarregar o SO. Se você executar em um servidor com mais núcleos, aumente o número conforme necessário.

### Dica profissional

Se você precisar de pacotes de idioma personalizados, configurações de DPI ou recorte de região de interesse, faça isso **uma única vez** no `Engine` compartilhado antes de enfileirar quaisquer imagens. Por exemplo:

```csharp
recognitionQueue.Engine.Language = Language.English;
recognitionQueue.Engine.Dpi = 300;
```

Todos os reconhecimentos subsequentes herdam essas opções automaticamente — esta é a essência de **como criar OCR** pipelines que permanecem consistentes.

## Extração de texto em lote – Enfileirando imagens e executando a fila

Com a fila pronta, o próximo passo é inserir cada imagem nela. O método `Enqueue` aceita uma instância `OcrImage`, que criamos a partir de um caminho de arquivo.

```csharp
// Step 3: Enqueue each image for OCR processing
foreach (var path in imagePaths)
    recognitionQueue.Enqueue(OcrImage.FromFile(path));
```

Depois que todos os arquivos são enfileirados, iniciamos o processamento:

```csharp
// Step 4: Run the queue and collect OCR results
List<OcrResult> ocrResults = recognitionQueue.ExecuteAll();
```

`ExecuteAll` bloqueia até que todas as imagens terminem, então retorna uma lista onde cada elemento corresponde à ordem de entrada. Isso garante que o resultado da página 1 esteja no índice 0, da página 2 no índice 1, e assim por diante — útil quando você precisa mapear os resultados de volta aos arquivos de origem.

## Como criar OCR – Exibindo os resultados

Finalmente, vamos imprimir o texto reconhecido no console. É aqui que você realmente vê a **extração de texto em lote** em ação.

```csharp
// Step 5: Output the recognized text for each page
for (int i = 0; i < ocrResults.Count; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

Quando você executar o programa (`dotnet run`), deverá ver algo como:

```
--- Page 1 ---
Welcome to the quarterly report.
--- Page 2 ---
Revenue increased by 12% YoY.
--- Page 3 ---
All figures are provisional.
--- Page 4 ---
Contact finance@example.com for details.
```

Se alguma imagem falhar (por exemplo, arquivo corrompido), o `OcrResult` correspondente terá a propriedade `Text` vazia e você pode inspecionar `ocrResults[i].Exception` para diagnóstico.

## Como criar OCR – Dicas, casos extremos e boas práticas

### Lidando com lotes grandes

Processar centenas de PNGs ainda pode consumir memória se você mantiver todos os objetos `OcrResult` vivos. Nesses casos, envie a saída para um arquivo ou banco de dados assim que cada resultado chegar:

```csharp
recognitionQueue.OnResultReady += (sender, args) =>
{
    File.AppendAllText("OcrOutput.txt",
        $"--- {args.Image.Path} ---{Environment.NewLine}{args.Result.Text}{Environment.NewLine}");
};
```

### Lidando com formatos que não são PNG

Aspose OCR também suporta JPEG, BMP e TIFF nativamente. Basta mudar a extensão do arquivo na sua lista ou usar uma busca com curinga. As mesmas etapas do **tutorial de c# ocr** se aplicam — nenhuma alteração de código necessária.

### Ignorando páginas em branco

Se você tem PDFs escaneados que às vezes contêm páginas em branco, pode filtrar os resultados:

```csharp
if (!string.IsNullOrWhiteSpace(result.Text))
    // process non‑empty text
```

### Considerações de licença

A versão de avaliação marca cada página com uma marca d'água. Para uso em produção, certifique‑se de incorporar seu arquivo de licença no início do `Main`:

```csharp
License lic = new License();
lic.SetLicense("Aspose.OCR.lic");
```

### Ajuste de paralelismo

`MaxDegreeOfParallelism` tem como padrão `Environment.ProcessorCount`. Se você notar alto uso de CPU ou pressão de memória, diminua o valor. Por outro lado, em uma VM na nuvem com muitos núcleos, aumente‑o para explorar totalmente o hardware.

## Resumo

Agora você tem uma solução completa de **como fazer OCR em lote** em C# que pode **extrair texto de arquivos PNG**, executá‑los em paralelo e fornecer resultados limpos e ordenados. Ao compartilhar um único `OcrEngine`, você aprendeu **como criar OCR** pipelines que são ao mesmo tempo eficientes em memória e fáceis de manter. Este **tutorial de c# ocr** também mostra como escalar para **extração de texto em lote** para centenas de imagens com apenas algumas linhas extras.

---

### O que vem a seguir?

* Tente adicionar detecção de idioma (`Engine.Language = Language.AutoDetect`).  
* Experimente formatos de saída — escreva os resultados em JSON ou CSV para análises posteriores.  
* Combine este OCR em lote com uma etapa de conversão de PDF para imagem para processar documentos escaneados completos.

Sinta‑se à vontade para ajustar o paralelismo, trocar pelas suas próprias fontes de imagem ou inserir os resultados em um índice de busca. O céu é o limite quando você domina **como fazer OCR em lote** em C#.

Feliz codificação, e que suas execuções de OCR sejam rápidas e sem erros!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}