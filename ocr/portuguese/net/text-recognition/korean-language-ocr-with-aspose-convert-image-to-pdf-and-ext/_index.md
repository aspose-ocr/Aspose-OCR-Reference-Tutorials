---
category: general
date: 2026-05-28
description: Tutorial de OCR de idioma coreano usando Aspose em C#. Aprenda como carregar
  imagem a partir de um stream, extrair texto simples, converter a imagem em PDF e
  exportar PDF pesquisável.
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: pt
og_description: OCR de idioma coreano em C# usando Aspose. Guia passo a passo para
  carregar imagem a partir de um stream, extrair texto simples, converter a imagem
  em PDF e exportar PDF pesquisável.
og_title: OCR de Língua Coreana – Converter Imagem em PDF e Extrair Texto (Guia C#)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 'OCR de idioma coreano com Aspose: converter imagem em PDF e extrair texto
  em C#'
url: /pt/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR de Língua Coreana com Aspose: Converter Imagem em PDF e Extrair Texto em C#

Já se perguntou como executar **OCR de Língua Coreana** em uma foto sem enviar nada para a nuvem? Você não está sozinho. Seja digitalizando placas de rua, processando recibos ou construindo um índice de busca multilíngue, ser capaz de reconhecer caracteres coreanos localmente pode economizar tempo, dinheiro e dores de cabeça com privacidade.

Neste tutorial vamos percorrer um exemplo completo e executável que mostra como **carregar imagem a partir de stream**, **extrair texto simples**, **converter imagem em PDF** e, finalmente, **exportar PDF pesquisável** — tudo com Aspose.OCR e algumas linhas de C#. Sem serviços externos, sem mágica oculta — apenas código .NET puro que você pode inserir em qualquer aplicativo console.

## O que Você Vai Aprender

- Um programa console funcional que lê um arquivo JPEG via stream de arquivo.  
- Texto coreano extraído como strings Unicode simples.  
- Um relatório JSON detalhado da execução do OCR para depuração ou análise.  
- Um PDF pesquisável que pode ser aberto em qualquer leitor de PDF e que permite selecionar as palavras coreanas.  

**Pré‑requisitos**  
- .NET 6.0 ou superior (o código também funciona no .NET Framework 4.7+).  
- Pacote NuGet Aspose.OCR for .NET instalado (`Install-Package Aspose.OCR`).  
- Uma pasta que contenha `korean_sign.jpg` e um local gravável para os arquivos de saída.  

Se você já tem esses itens configurados, ótimo — vamos colocar a mão na massa.

## Etapa 1: Inicializar o Motor OCR para OCR de Língua Coreana

A primeira coisa que você precisa é uma instância de `OcrEngine`. Habilitar a GPU (se você tiver uma) acelera o reconhecimento drasticamente, e desativar o download automático de recursos força a biblioteca a usar os pacotes de idioma offline que você fornece.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **Por que isso importa:**  
> *Aceleração por GPU* pode reduzir o tempo de processamento de segundos para milissegundos em lotes grandes. Definir `AutomaticResourceDownload` como `false` garante que a demonstração funcione offline — um requisito crucial para muitos ambientes corporativos.

## Etapa 2: Carregar Imagem a partir de Stream

Ler a imagem por meio de um stream oferece flexibilidade: você pode puxar arquivos do disco, de compartilhamentos de rede ou até mesmo de blobs armazenados em memória. Aqui abrimos um arquivo JPEG local, mas o mesmo padrão funciona para qualquer `Stream`.

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **Dica profissional:** Se precisar processar imagens enviadas via uma API web, basta substituir `File.OpenRead` por `IFormFile.OpenReadStream()` — o restante permanece idêntico.

## Etapa 3: Selecionar Idioma Coreano e Aplicar Filtros de Pré‑Processamento

Aspose.OCR suporta alguns passos de pré‑processamento que limpam a imagem antes do reconhecimento. Para placas coreanas, correção de inclinação (deskew) e remoção de ruído (denoise) geralmente são suficientes.

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **O que está acontecendo nos bastidores?**  
> O filtro `Deskew` endireita texto girado, enquanto `Denoise` remove granulação que pode confundir o classificador de caracteres. Pular essas etapas costuma gerar saída confusa, especialmente em fotos de baixa resolução.

## Etapa 4: Extrair Texto Simples de Forma Assíncrona

Chegou o momento da verdade — solicitar ao motor que reconheça os caracteres e nos devolva uma string limpa. Usar `RecognizeAsync` mantém a UI responsiva se você incorporar isso em um aplicativo desktop ou web.

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

Ao executar o programa, você deverá ver algo como:

```
OCR complete. Extracted text:
서울시청
```

> **Por que assíncrono?**  
> OCR pode ser intensivo em CPU. Execução assíncrona impede que sua thread fique bloqueada, o que é especialmente útil no ASP.NET Core, onde a escassez de threads é uma preocupação real.

## Etapa 5: Obter Resultado de Reconhecimento Detalhado e Salvar como JSON

Às vezes você precisa de mais do que a string bruta — talvez queira pontuações de confiança, caixas delimitadoras ou os dados da imagem original. O método `RecognizeDetailed` devolve um objeto `RecognitionResult` que pode ser serializado para JSON para análise posterior.

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

Abrir `korean_ocr.json` revelará uma estrutura semelhante a:

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **Quando usar isso?**  
> Se você está construindo um índice de busca, os valores de confiança permitem filtrar resultados de baixa qualidade. Se precisar destacar texto em uma UI, as caixas delimitadoras são seu mapa.

## Etapa 6: Converter Imagem em PDF e Exportar PDF Pesquisável

Aspose torna a transição de raster para vetor sem esforço. Ao definir `OutputFormat` como `SearchablePdf`, a biblioteca incorpora a imagem original e sobrepõe uma camada de texto invisível contendo a saída do OCR. O PDF resultante pode ser pesquisado, copiado e indexado como qualquer PDF nativo.

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

Abra `korean_searchable.pdf` no Adobe Reader ou em qualquer visualizador de PDF, pressione **Ctrl+F**, digite uma palavra coreana e veja-a pular para o local exato na página. Esse é o poder de um PDF pesquisável.

> **Dica extra:** Se precisar apenas de um PDF visual sem a camada de texto oculta, altere `OutputFormat` para `Pdf`.

## Exemplo Completo Funcionando

Abaixo está o programa completo — copie, cole, substitua `YOUR_DIRECTORY` por um caminho real e pressione **F5**.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### Saída Esperada no Console

```
OCR complete. Extracted text:
서울시청
```

E você encontrará três novos arquivos ao lado da sua imagem fonte:

- `korean_ocr.json` – dados completos de reconhecimento.  
- `korean_searchable.pdf` – um PDF que pode ser pesquisado.  
- (opcional) quaisquer logs intermediários que você decidir adicionar.

## Perguntas Frequentes & Casos de Borda

**E se eu não tiver GPU?**  
Defina `EnableGpu = false`; o fallback para CPU funciona perfeitamente para lotes pequenos.

**Posso processar várias imagens em uma única execução?**  
Claro. Envolva a lógica principal em um loop `foreach (var file in Directory.GetFiles(...))` e reatribua `ocrEngine.Image` a cada iteração.

**Como lidar com outros idiomas junto ao coreano?**  
Aspose.OCR permite definir `Language = Language.AutoDetect` ou combinar idiomas com o operador OR bit a bit (ex.: `Language.Korean | Language.English`).

**E se a confiança do OCR estiver baixa?**  
Inspecione `detailedResult.Pages[0].Words` e filtre entradas com `Confidence < 0.7`. Você também pode ajustar os filtros de pré‑processamento — experimente adicionar `PreprocessFilter.ContrastEnhancement`.

## Conclusão

Você acabou de ver como realizar **OCR de Língua Coreana** de ponta a ponta, desde **carregar imagem a partir de stream** até **extrair texto simples**, depois **converter imagem em PDF** e, por fim, **exportar PDF pesquisável**. A abordagem é modular, permitindo trocar a fonte da imagem, mudar o formato de saída ou integrar o JSON em qualquer pipeline subsequente.

O que vem a seguir


## Tutoriais Relacionados

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}