---
category: general
date: 2026-06-06
description: Aprenda a criar PDF pesquisável e converter imagem em PDF com OCR. Inclui
  adição de camada, configurações de compressão e código C# completo.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- how to ocr image
- how to add layer
- how to set compression
language: pt
og_description: Crie PDF pesquisável a partir de uma imagem usando OCR. Este guia
  mostra como adicionar uma camada de texto oculta, definir compressão e converter
  a imagem em PDF.
og_title: Crie PDF pesquisável – Tutorial completo de C#
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Learn how to create searchable PDF and convert image to PDF with OCR.
    Includes layer addition, compression settings, and full C# code.
  headline: Create Searchable PDF from an Image – Full Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to create searchable PDF and convert image to PDF with OCR.
    Includes layer addition, compression settings, and full C# code.
  name: Create Searchable PDF from an Image – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - The
      Aspose.OCR and Aspose.Pdf NuGet packages (or any equivalent library that offers
      `OcrEngine` and `PdfSaveOptions`). - A sample image, e.g., `invoice.png`, placed
      in a folder you can reference. - A basic understanding of C# syntax'
  - name: Full Working Example
    text: 'Putting it all together, here’s the complete, ready‑to‑run program:'
  - name: Pro tip
    text: If you need to **convert image to PDF** without OCR (just a plain image
      PDF), set `AddTextLayer = false`. The same `PdfSaveOptions` still lets you control
      compression, which is handy for archiving scanned documents that don’t need
      searchability.
  type: HowTo
tags:
- OCR
- PDF
- C#
- Aspose
title: Criar PDF pesquisável a partir de uma imagem – Guia completo passo a passo
url: /pt/net/ocr-configuration/create-searchable-pdf-from-an-image-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável – Tutorial completo em C#

Já se perguntou como **criar PDF pesquisável** a partir de uma fatura escaneada sem passar horas em uma ferramenta gráfica? Você não está sozinho. Muitos desenvolvedores encontram um obstáculo quando precisam transformar uma imagem em um PDF que mantenha a aparência original e ainda permita copiar ou pesquisar o texto.  

Neste tutorial vamos percorrer passo a passo as etapas exatas para **converter imagem em PDF**, executar OCR nela, adicionar uma camada de texto oculta e ainda ajustar as configurações de compressão. Ao final, você terá um snippet C# pronto‑para‑usar que pode ser inserido em qualquer projeto .NET.

## O que você vai aprender

- Configurar um motor de OCR e entender **como fazer OCR em imagens**.
- Usar as opções de **como adicionar camada** para incorporar uma sobreposição de texto pesquisável.
- Aplicar **como definir compressão** para PDFs menores e compactados em ZIP.
- Transformar uma simples foto em um fluxo de **criar PDF pesquisável** que pode ser automatizado.
- Armadilhas comuns e dicas avançadas para manter seus PDFs nítidos e rápidos.

### Pré‑requisitos

- .NET 6.0 ou superior (o código também funciona no .NET Framework 4.7+).
- Os pacotes NuGet Aspose.OCR e Aspose.Pdf (ou qualquer biblioteca equivalente que ofereça `OcrEngine` e `PdfSaveOptions`).
- Uma imagem de exemplo, por exemplo, `invoice.png`, colocada em uma pasta que você possa referenciar.
- Noções básicas de sintaxe C# — não é necessário conhecimento profundo de OCR.

> **Dica profissional:** Se você estiver usando o Visual Studio, instale os pacotes via Console do Gerenciador de Pacotes:  
> `Install-Package Aspose.OCR`  
> `Install-Package Aspose.Pdf`

---

![Exemplo de criação de PDF pesquisável mostrando uma imagem de fatura transformada em PDF com camada de texto oculta](/images/create-searchable-pdf.png)

## Etapa 1: Inicializar o motor de OCR – **como fazer OCR em imagem**

Primeiro precisamos de um motor de OCR que consiga ler texto em inglês da nossa foto. A classe `OcrEngine` é o ponto de entrada; basta definir o idioma e, depois, fornecer uma imagem.

```csharp
using Aspose.OCR;
using Aspose.Pdf;

// Create and configure the OCR engine
OcrEngine engine = new OcrEngine
{
    Language = OcrLanguage.English
};
```

*Por que isso importa:* Inicializar o motor com o idioma correto melhora drasticamente a precisão. Se você pular essa etapa, pode obter caracteres embaralhados.

## Etapa 2: Carregar a imagem – **converter imagem em pdf**

Agora apontamos o motor para o arquivo que queremos processar. `ImageStream.FromFile` lê os bytes e os prepara para o OCR.

```csharp
// Load the image you want to turn into a searchable PDF
engine.Image = ImageStream.FromFile(@"C:\Docs\invoice.png");
```

Você também pode carregar a partir de um `MemoryStream` se a imagem vier de uma requisição web ou de um banco de dados.

## Etapa 3: Executar o reconhecimento OCR – **como fazer OCR em imagem**

Com a imagem carregada, o trabalho pesado acontece em uma única chamada. O método `Recognize` devolve um `OcrResult` que contém tanto o texto extraído quanto o bitmap original.

```csharp
// Perform OCR on the loaded image
OcrResult ocrResult = engine.Recognize();
```

*Nos bastidores:* O motor analisa cada pixel, detecta caracteres e constrói uma string Unicode. Ele também mantém os dados posicionais necessários para a camada de texto oculta posteriormente.

## Etapa 4: Configurar as opções de salvamento PDF – **como adicionar camada** & **como definir compressão**

É aqui que a mágica de um PDF pesquisável ocorre. Criamos um objeto `PdfSaveOptions` que indica ao Aspose.Pdf como incorporar a imagem original, adicionar uma sobreposição de texto invisível e comprimir o arquivo final.

```csharp
// Set up PDF options for a searchable PDF
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    IncludeImage = true,          // Keep the original image in the PDF
    AddTextLayer = true,          // Add a hidden text layer with OCR results
    Compression = PdfCompression.Zip   // Use ZIP compression for smaller size
};
```

- **IncludeImage** garante a fidelidade visual da digitalização original.
- **AddTextLayer** cria uma camada invisível que navegadores e leitores de PDF podem indexar para pesquisa.
- **Compression** reduz o tamanho do arquivo sem sacrificar a qualidade; ZIP é um bom padrão para a maioria dos documentos.

## Etapa 5: Salvar o resultado – **criar PDF pesquisável**

Por fim, gravamos o resultado do OCR no disco usando as opções que acabamos de definir. O método `Save` recebe o caminho de destino e a instância `PdfSaveOptions`.

```csharp
// Save the OCR result as a searchable PDF
ocrResult.Save(@"C:\Docs\invoice_searchable.pdf", pdfOptions);
```

Ao abrir `invoice_searchable.pdf` no Adobe Reader ou em qualquer visualizador moderno, você verá a imagem original, mas agora poderá selecionar, copiar e pesquisar o texto como se fosse um PDF nativo.

### Exemplo completo em funcionamento

Juntando tudo, segue o programa completo, pronto‑para‑executar:

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine engine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 2️⃣ Load the source image
            string imagePath = @"C:\Docs\invoice.png";
            engine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            OcrResult result = engine.Recognize();

            // 4️⃣ Configure PDF options (layer + compression)
            PdfSaveOptions pdfOptions = new PdfSaveOptions
            {
                IncludeImage = true,
                AddTextLayer = true,
                Compression = PdfCompression.Zip
            };

            // 5️⃣ Save as searchable PDF
            string pdfPath = @"C:\Docs\invoice_searchable.pdf";
            result.Save(pdfPath, pdfOptions);

            Console.WriteLine($"Searchable PDF created at: {pdfPath}");
        }
    }
}
```

**Saída esperada** (no console):  
`Searchable PDF created at: C:\Docs\invoice_searchable.pdf`

Abra o arquivo resultante, pressione **Ctrl F**, digite uma palavra que aparece na fatura e veja o visualizador ir direto para ela instantaneamente. Esse é o cerne de **criar PDF pesquisável** em ação.

## Armadilhas comuns & como evitá‑las

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| Texto não pesquisável | `AddTextLayer` ficou `false` ou está usando uma versão antiga do Aspose | Garanta `AddTextLayer = true` e atualize para o pacote NuGet mais recente |
| PDF enorme (megabytes) | Compressão definida como `PdfCompression.None` | Troque para `PdfCompression.Zip` ou `PdfCompression.Jpeg` para imagens |
| Caracteres embaralhados | Idioma errado ou imagem de baixa resolução | Defina `engine.Language` adequadamente e forneça imagens de pelo menos 300 dpi |
| Camada oculta invisível em alguns visualizadores | PDF gerado com versão não‑padrão | Use `PdfSaveOptions.PdfVersion = PdfVersion.PDF_1_7` (padrão) ou atualize o visualizador |

### Dica profissional

Se precisar **converter imagem em PDF** sem OCR (apenas um PDF de imagem simples), defina `AddTextLayer = false`. As mesmas `PdfSaveOptions` ainda permitem controlar a compressão, o que é útil para arquivar documentos escaneados que não precisam ser pesquisáveis.

## Expandindo a solução

- **Múltiplas páginas**: Percorra uma lista de arquivos de imagem, atribua `engine.Image = ...` a cada iteração e acumule os resultados em um único PDF usando a agregação `PdfDocument`.
- **Idiomas diferentes**: Altere `engine.Language = OcrLanguage.Spanish` (ou qualquer idioma suportado) para lidar com faturas multilíngues.
- **Compressão personalizada**: Para imagens ricas em cores, `PdfCompression.Jpeg` com ajuste de qualidade (`pdfOptions.JpegQuality = 80`) pode reduzir ainda mais o tamanho dos arquivos.

## Conclusão

Acabamos de cobrir tudo o que você precisa para **criar PDF pesquisável** a partir de imagens usando C#. Desde a inicialização do motor de OCR, carregamento da foto, reconhecimento, configuração de uma camada de texto oculta, até a definição de compressão — cada peça desempenha um papel crucial na entrega de um documento rápido e pesquisável.  

Agora você pode automatizar o processamento de faturas, arquivar contratos ou construir uma ferramenta de digitalização em massa que transforma pilhas de papel em PDFs instantaneamente pesquisáveis.  

Pronto para o próximo desafio? Experimente adicionar marcas d'água, mesclar vários PDFs pesquisáveis ou expor essa lógica através de uma Web API para que toda a sua organização possa enviar imagens e receber PDFs pesquisáveis em tempo real.

---

*Se este guia foi útil, dê-lhe uma ⭐, compartilhe com colegas ou deixe um comentário com suas próprias adaptações. Boa codificação!*

## O que você deve aprender a seguir?

Os tutoriais abaixo abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}