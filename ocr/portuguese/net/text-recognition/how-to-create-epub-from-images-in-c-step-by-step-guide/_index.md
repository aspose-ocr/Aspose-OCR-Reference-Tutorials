---
category: general
date: 2026-03-07
description: Como criar ePub a partir de imagens digitalizadas usando Aspose OCR –
  aprenda a converter imagem em ePub, extrair texto da imagem, adicionar autor ao
  ePub e carregar imagem para OCR.
draft: false
keywords:
- how to create epub
- convert image to epub
- extract text from image
- add author to epub
- load image for ocr
language: pt
og_description: Como criar ePub a partir de imagens escaneadas em C#. Este tutorial
  mostra como converter imagem para ePub, extrair texto da imagem, adicionar autor
  ao ePub e carregar imagem para OCR.
og_title: Como criar ePub a partir de imagens em C# – Guia completo
tags:
- C#
- Aspose OCR
- ePub
- Document Conversion
title: Como criar ePub a partir de imagens em C# – Guia passo a passo
url: /pt/net/text-recognition/how-to-create-epub-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar ePub a partir de imagens em C# – Guia completo

Já se perguntou **how to create ePub** a partir de uma coleção de páginas digitalizadas? Talvez você tenha alguns PNGs de um romance clássico e queira transformá-los em um ePub organizado que pode ser lido em qualquer dispositivo. A boa notícia é que, com Aspose OCR, você pode **load image for OCR**, extrair o texto e então **convert image to ePub** em apenas algumas linhas de C#.

Neste tutorial, percorreremos todo o pipeline: carregar a imagem, extrair o texto, adicionar alguns metadados (sim, vamos **add author to epub**), e finalmente escrever um arquivo ePub compatível com os padrões. Ao final, você terá um ePub pronto para publicação e uma compreensão sólida de cada etapa, para que possa adaptar o código para livros de várias páginas, fontes personalizadas ou até distribuição sem DRM.

## O que você precisará

- **.NET 6** ou posterior (a API funciona também com .NET Standard 2.0+)  
- **Aspose.OCR for .NET** – você pode obter uma avaliação gratuita no site da Aspose.  
- Uma imagem escaneada como `book_page.png` colocada em algum lugar no disco.  
- Uma IDE favorita (Visual Studio, Rider ou VS Code – eu usarei o Visual Studio nas capturas de tela).

Nenhum pacote NuGet adicional é necessário; o Aspose.OCR inclui tudo o que você precisa para exportar ePub.

---

![Como criar ePub a partir de imagem escaneada](/images/how-to-create-epub.png "Como criar ePub a partir de uma imagem escaneada usando Aspose OCR")

## Etapa 1 – Configurar o Projeto e Instalar o Aspose.OCR

Primeiro de tudo. Crie um novo aplicativo de console:

```bash
dotnet new console -n OcrToEpubDemo
cd OcrToEpubDemo
```

Adicione o pacote Aspose.OCR:

```bash
dotnet add package Aspose.OCR
```

É isso – a biblioteca já inclui recursos de OCR e exportação ePub, portanto você não precisará de dependências extras.

## Etapa 2 – Carregar Imagem para OCR

Antes de podermos **extract text from image**, precisamos fornecer algo para o motor OCR ler. O helper `ImageStream.FromFile` torna isso trivial:

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Load the PNG (or JPG, TIFF, etc.) you want to process
// This is the “load image for OCR” step.
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book_page.png");
```

> **Pro tip:** Se sua imagem estiver em um recurso incorporado, use `ImageStream.FromResource` em vez de `FromFile`.

## Etapa 3 – Extrair Texto da Imagem

Agora o motor realmente lê os pixels e os converte em strings Unicode. O método `Recognize` faz o trabalho pesado.

```csharp
// Run the OCR process – this will fill ocrEngine.RecognitionResult
ocrEngine.Recognize();

// Optional: inspect the raw text
string rawText = ocrEngine.RecognitionResult.Text;
Console.WriteLine("Extracted text (first 200 chars):");
Console.WriteLine(rawText.Substring(0, Math.Min(200, rawText.Length)));
```

Por que chamar `Recognize` separadamente? Isso permite inspecionar a saída bruta do OCR, ajustar as configurações de idioma ou até executar uma verificação ortográfica antes de prosseguir para a criação do ePub.

## Etapa 4 – Preparar Opções de Exportação ePub (Add Author to ePub)

Criar um ePub bem elaborado não é apenas despejar texto; você também quer metadados adequados. A classe `EpubExportOptions` oferece uma maneira simples de **add author to ePub**, definir um título e decidir se deve incorporar as imagens originais.

```csharp
var epubExportOptions = new EpubExportOptions
{
    Title = "Scanned Book",          // Title shown in eReader libraries
    Author = "Unknown",              // This is where we “add author to epub”
    IncludeImages = true             // Embeds the original PNGs for visual fidelity
};
```

Se você tiver várias páginas, pode continuar chamando `ocrEngine.Image = …` e `ocrEngine.Recognize()` dentro de um loop; cada chamada adiciona o conteúdo da nova página ao mesmo documento ePub.

## Etapa 5 – Converter Imagem para ePub e Exportar

Com o texto extraído e os metadados definidos, a etapa final é uma única linha que grava o arquivo ePub no disco:

```csharp
// Export the recognized content to an ePub file
ocrEngine.ExportToEpub("YOUR_DIRECTORY/book.epub", epubExportOptions);

// Confirmation for the user
Console.WriteLine("ePub created.");
```

O `book.epub` resultante pode ser aberto no Calibre, Apple Books ou em qualquer leitor compatível com EPUB. Como definimos `IncludeImages = true`, o PNG original aparecerá como uma página de imagem, preservando a aparência da fonte escaneada.

## Exemplo Completo Funcional

Juntando tudo, aqui está o programa completo, pronto para ser executado:

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // This is the “load image for OCR” step.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book_page.png");

        // Step 3: Run the OCR recognition – we now “extract text from image”
        ocrEngine.Recognize();

        // (Optional) Print a snippet of the extracted text
        string snippet = ocrEngine.RecognitionResult.Text.Substring(0,
            Math.Min(200, ocrEngine.RecognitionResult.Text.Length));
        Console.WriteLine("Extracted text preview:");
        Console.WriteLine(snippet);
        Console.WriteLine();

        // Step 4: Set up ePub export options – we “add author to epub” here
        var epubExportOptions = new EpubExportOptions
        {
            Title = "Scanned Book",
            Author = "Unknown",
            IncludeImages = true   // embed the original images in the ePub
        };

        // Step 5: Export the recognized content – this is how we “convert image to epub”
        ocrEngine.ExportToEpub("YOUR_DIRECTORY/book.epub", epubExportOptions);

        // Step 6: Inform the user that the ePub has been created
        Console.WriteLine("ePub created.");
    }
}
```

### Saída Esperada

```
Extracted text preview:
Chapter 1
It was a bright cold day in April, and the...
 
ePub created.
```

Abra `book.epub` no seu leitor favorito e você verá uma página de título, a linha do autor (mesmo que diga “Desconhecido”) e a imagem escaneada exibida ao lado do texto selecionável.

## Perguntas Frequentes & Casos Limite

### E se o idioma do OCR não for inglês?

O Aspose.OCR suporta mais de 70 idiomas. Basta definir a propriedade `Language` antes de chamar `Recognize`:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

### Como lidar com livros de várias páginas?

Envolva a lógica de carregamento/reconhecimento em um loop `foreach`:

```csharp
string[] pages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
foreach (var pagePath in pages)
{
    ocrEngine.Image = ImageStream.FromFile(pagePath);
    ocrEngine.Recognize();
}
ocrEngine.ExportToEpub("YOUR_DIRECTORY/full_book.epub", epubExportOptions);
```

Cada iteração adiciona o texto recém-reconhecido ao mesmo ePub, preservando a ordem das páginas.

### Posso excluir as imagens originais?

Claro – defina `IncludeImages = false` em `EpubExportOptions`. O ePub resultante será puro texto refluível, o que reduz o tamanho do arquivo drasticamente.

### E quanto a fontes ou estilos personalizados?

O exportador ePub do Aspose.OCR permite que você forneça uma folha de estilos CSS via a propriedade `Css` em `EpubExportOptions`. Dessa forma, você pode impor uma família de fontes específica, altura de linha ou margem.

## Conclusão

Agora você sabe **how to create ePub** a partir de uma imagem escaneada usando Aspose OCR em C#. O tutorial cobriu tudo, desde **load image for OCR**, passando por **extract text from image**, até **add author to epub**, e finalmente **convert image to epub** com uma única chamada de exportação. Com o exemplo completo de código em mãos, você pode expandir a solução para processar em lote bibliotecas inteiras, inserir arte de capa personalizada ou até integrar o fluxo de trabalho em uma API web.

Pronto para o próximo desafio? Tente converter um PDF para ePub, ou experimente ajustar os limites de confiança do OCR para melhorar a precisão em digitalizações ruidosas. O céu é o limite quando você combina OCR poderoso com geração flexível de ePub.

Feliz codificação, e aproveite a leitura do seu ePub recém-criado!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}