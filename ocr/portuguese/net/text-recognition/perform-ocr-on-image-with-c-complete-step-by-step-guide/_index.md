---
category: general
date: 2026-05-21
description: Realize OCR em imagem usando C#. Aprenda a carregar a imagem para OCR,
  extrair texto de PNG e reconhecer texto da imagem com um pequeno exemplo de código.
draft: false
keywords:
- perform OCR on image
- extract text from PNG
- recognize text from image
- load image for OCR
language: pt
og_description: Execute OCR em imagem em C# rapidamente. Este guia mostra como carregar
  a imagem para OCR, extrair texto de PNG e reconhecer texto da imagem com saída HTML
  sensível ao layout.
og_title: Realizar OCR em Imagem com C# – Tutorial Completo de Programação
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  headline: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  name: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  steps:
  - name: Load Image for OCR
    text: The line `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");`
      is where we **load image for OCR**. The `ImageStream` helper abstracts away
      file‑format details, so you can feed JPEG, BMP, or TIFF without changing code.
  - name: Extract Text from PNG
    text: 'Once `engine.Recognize()` finishes, the OCR engine holds the recognized
      text internally. You can pull it out as a string if you only need raw text:'
  - name: Recognize Text from Image
    text: 'The `Recognize()` call does the heavy lifting. Under the hood the engine:'
  - name: Handling Layout‑Aware HTML Output
    text: 'Most developers stop at plain text, but the `HtmlSaveOptions` we used let
      you **perform OCR on image** and keep the visual structure intact. Two flags
      matter:'
  - name: Scaling to Multiple Files
    text: 'If you need to **perform OCR on image** files in a folder, wrap the core
      logic in a simple loop:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Aspose.OCR
title: Realize OCR em Imagem com C# – Guia Completo Passo a Passo
url: /pt/net/text-recognition/perform-ocr-on-image-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Realizar OCR em Imagem com C# – Guia Completo Passo a Passo

Já se perguntou como **perform OCR on image** arquivos sem lidar com GUIs pesados? Você não está sozinho. Seja digitalizando recibos, extraindo dados de formulários escaneados ou simplesmente precisando transformar um PNG em texto pesquisável, algumas linhas de C# podem fazer o trabalho.

Neste tutorial, vamos percorrer o carregamento de uma imagem para OCR, o reconhecimento de texto da imagem e, finalmente, a extração de texto de PNG como HTML limpo. Ao final, você terá um aplicativo de console pronto‑para‑executar que **performs OCR on image** arquivos e preserva o layout original.

## O Que Você Vai Construir

- Um programa de console minimalista que lê um PNG (ou qualquer imagem suportada)  
- Usa um motor OCR para **recognize text from image**  
- Salva o resultado como HTML consciente de layout, incorporando a imagem original  
- Mostra como **load image for OCR**, **extract text from PNG**, e lidar com casos de borda comuns  

> **Prerequisites**  
> - .NET 6.0 SDK ou posterior (você também pode direcionar .NET Framework 4.7+)  
> - Uma biblioteca OCR compatível com NuGet – o exemplo usa *Aspose.OCR*, mas qualquer biblioteca com API semelhante funcionará  
> - Conhecimento básico de C# (nada avançado)  

Tem tudo isso? Ótimo—vamos mergulhar.

## Realizar OCR em Imagem – Visão Completa do Código

Abaixo está o programa **completo e executável**. Copie‑e‑cole em um novo projeto de console (`dotnet new console`) e pressione **F5**.

```csharp
using System;
using Aspose.OCR;               // OCR engine namespace
using Aspose.OCR.Models;        // Save options namespace
using Aspose.OCR.ImageProcessing; // Image loading helpers

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine and set the language
            // -------------------------------------------------
            var engine = new OcrEngine
            {
                Language = OcrLanguage.English   // You can change to French, German, etc.
            };

            // -------------------------------------------------
            // Step 2: Load the image for OCR
            // -------------------------------------------------
            // Replace the path with your actual PNG/JPEG/TIFF file.
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");

            // -------------------------------------------------
            // Step 3: Perform OCR recognition
            // -------------------------------------------------
            engine.Recognize();

            // -------------------------------------------------
            // Step 4: Configure HTML save options – keep layout
            // -------------------------------------------------
            var htmlOptions = new HtmlSaveOptions
            {
                PreserveLayout = true,   // Keep columns, tables, and spacing
                EmbedImages = true       // Embed the original PNG inside the HTML
            };

            // -------------------------------------------------
            // Step 5: Save the recognized content as layout‑aware HTML
            // -------------------------------------------------
            engine.Save("YOUR_DIRECTORY/form.html", htmlOptions);

            Console.WriteLine("HTML with layout saved.");
        }
    }
}
```

> **Expected output**  
> ```
> HTML with layout saved.
> ```  
> Após a execução, você encontrará `form.html` ao lado do seu PNG. Abra‑o em um navegador e verá o mesmo layout, mas agora o texto é selecionável e pesquisável.

### Carregar Imagem para OCR

A linha `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");` é onde **load image for OCR**. O helper `ImageStream` abstrai os detalhes de formato de arquivo, permitindo usar JPEG, BMP ou TIFF sem alterar o código.  

**Por que não passar apenas um `Bitmap`?**  
Porque muitas SDKs OCR esperam um stream que também contém metadados DPI. Usar o carregador interno da biblioteca garante que o motor veja a imagem exatamente como aparece na tela, o que melhora a precisão.

#### Dica Pro
Se você estiver processando um lote de arquivos, envolva a etapa de carregamento em um `try/catch` e registre qualquer `FileNotFoundException`. Isso impede que todo o lote trave porque um arquivo está ausente.

### Extrair Texto de PNG

Quando `engine.Recognize()` termina, o motor OCR mantém o texto reconhecido internamente. Você pode extraí‑lo como uma string se precisar apenas do texto bruto:

```csharp
string plainText = engine.Text;   // Returns the whole document as plain text
Console.WriteLine(plainText);
```

Esta é a maneira mais rápida de **extract text from PNG** quando você não se importa com o layout. Para a maioria dos trabalhos de entrada de dados, texto simples basta—apenas lembre‑se de remover quebras de linha se planeja importar para um CSV.

### Reconhecer Texto da Imagem

A chamada `Recognize()` faz o trabalho pesado. Por trás dos panos, o motor:

1. Normaliza a imagem (corrige inclinação, remove ruído)  
2. Segmenta‑a em linhas e palavras  
3. Executa um classificador de rede neural treinado em milhões de glifos  

Como definimos `Language = OcrLanguage.English`, o motor aplica dicionários específicos para o inglês, o que reduz drasticamente falsos positivos. Se precisar de suporte multilíngue, basta passar um array de idiomas:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

### Manipulando Saída HTML Sensível ao Layout

A maioria dos desenvolvedores para no texto simples, mas o `HtmlSaveOptions` que usamos permite que você **perform OCR on image** e mantenha a estrutura visual intacta. Dois parâmetros são importantes:

- `PreserveLayout = true` – mantém colunas, tabelas e espaçamento.  
- `EmbedImages = true` – insere o PNG original como um elemento `<img>` codificado em Base64, tornando o HTML autônomo.

Se preferir um arquivo mais leve, defina `EmbedImages = false` e o HTML referenciará o PNG original no disco.

#### Caso de Borda: Arquivos Grandes

Para imagens maiores que 5 MB, a incorporação pode inflar o tamanho do HTML. Nesses casos, troque para referências externas de imagem e considere comprimir o PNG previamente com `ImageProcessor.Compress`.

## Armadilhas Comuns e Dicas Pro

| Sintoma | Causa Provável | Solução |
|--------|--------------|-----|
| Caracteres embaralhados | Idioma errado definido ou pacote de idioma ausente | Instale os arquivos de dados de idioma apropriados e defina `engine.Language` corretamente |
| Nenhum texto na saída | Imagem muito escura ou de baixa resolução | Pré‑processar com `engine.Image = ImageProcessor.AdjustContrast(engine.Image, 1.2)` |
| Layout quebrado no HTML | `PreserveLayout` deixado no padrão `false` | Defina `PreserveLayout = true` em `HtmlSaveOptions` |
| Processamento lento em muitas páginas | Motor reinicializa por arquivo | Reutilize a mesma instância `OcrEngine` e altere apenas `engine.Image` a cada loop |

### Escalando para Múltiplos Arquivos

Se precisar **perform OCR on image** arquivos em uma pasta, envolva a lógica central em um loop simples:

```csharp
foreach (var file in Directory.GetFiles("YOUR_DIRECTORY", "*.png"))
{
    engine.Image = ImageStream.FromFile(file);
    engine.Recognize();
    var htmlPath = Path.ChangeExtension(file, ".html");
    engine.Save(htmlPath, htmlOptions);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

Observe que nós **load image for OCR** dentro do loop, mas mantemos os mesmos objetos `engine` e `htmlOptions`. Isso reduz a rotatividade de memória e acelera trabalhos em lote.

## Indo Além: Exportando para PDF ou DOCX

O mesmo `engine` pode salvar em outros formatos:

```csharp
engine.Save("output.pdf", new PdfSaveOptions { PreserveLayout = true });
engine.Save("output.docx", new WordSaveOptions { PreserveLayout = true });
```

Se seu sistema downstream espera PDFs pesquisáveis, isso é uma mudança de uma linha—não há necessidade de escrever um pipeline de conversão separado.

## Conclusão

Acabamos de mostrar como **perform OCR on image** arquivos com C#, desde o carregamento da imagem até **extract text from PNG** e, finalmente, **recognize text from image** em um arquivo HTML sensível ao layout. O exemplo completo está pronto para ser executado, e agora você entende por que cada passo importa, como ajustá‑lo para diferentes idiomas e quais armadilhas observar.

Em seguida, experimente trocar o idioma inglês por outra localidade, experimente `PreserveLayout = false` para obter um HTML mais enxuto, ou canalize a saída de texto simples para um banco de dados para arquivos pesquisáveis. O céu é o limite quando você combina um motor OCR robusto com algumas linhas de C#.

Tem perguntas sobre como lidar com TIFFs de várias páginas, ou quer saber como integrar isso em uma API ASP.NET Core? Deixe um comentário abaixo, e feliz codificação!

## Tutoriais Relacionados

- [Extrair texto de imagem C# com seleção de idioma usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Como Extrair Texto de Imagem Preparando Retângulos no OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extrair Texto de Imagem – Reconhecer Linha com Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}