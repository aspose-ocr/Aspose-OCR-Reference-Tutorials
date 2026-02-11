---
category: general
date: 2026-02-11
description: Crie PDF pesquisável a partir de uma imagem em árabe em C#. Aprenda como
  converter a imagem em PDF, extrair texto em árabe e adicionar texto oculto usando
  Aspose OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract arabic text
- pdf with hidden text
- ocr arabic image
language: pt
og_description: Crie PDF pesquisável a partir de uma imagem em árabe usando Aspose
  OCR em C#. Siga este guia para converter a imagem em PDF, extrair texto em árabe
  e incorporar texto oculto.
og_title: Criar PDF pesquisável a partir de imagem em árabe – passo a passo
tags:
- Aspose
- OCR
- PDF
- C#
- Arabic
title: Criar PDF pesquisável a partir de imagem em árabe – Guia completo
url: /pt/net/text-recognition/create-searchable-pdf-from-arabic-image-complete-guide/
---

we didn't translate any URLs (none present). No file paths besides `arabic_invoice.jpg` and `arabic_invoice_searchable.pdf` which we left unchanged.

Now produce final output with all content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável a partir de imagem em árabe – Guia completo

Já precisou **criar PDF pesquisável** a partir de uma fatura escaneada em árabe, mas não sabia como manter a aparência original enquanto ainda tornava o texto selecionável? Você não está sozinho. Em muitos projetos de automação de documentos o desafio não é apenas converter uma imagem em PDF, mas também preservar o layout visual e adicionar uma camada de texto oculto que os mecanismos de busca podem indexar.

Neste tutorial, percorreremos todo o processo: **converter imagem em PDF**, **extrair texto em árabe** com Aspose OCR e, finalmente, incorporar esse texto como um **PDF com texto oculto**, de modo que o arquivo resultante seja totalmente pesquisável. Ao final, você terá um trecho de código C# pronto para uso que pode ser inserido em qualquer solução .NET. Sem serviços externos, apenas as bibliotecas Aspose que você já possui.

## O que você precisará

- .NET 6 ou posterior (o código também funciona com .NET Core)  
- **Aspose.OCR** e **Aspose.Pdf** pacotes NuGet (as versões mais recentes até fevereiro de 2026)  
- Um arquivo de imagem em árabe (por exemplo, `arabic_invoice.jpg`) que você deseja transformar em um PDF pesquisável  
- Um pouco de conhecimento em C# – os conceitos são simples, mas explicaremos o “porquê” por trás de cada linha.

> **Dica profissional:** Se ainda não adicionou os pacotes NuGet, execute  
> `dotnet add package Aspose.OCR` e  
> `dotnet add package Aspose.Pdf` a partir da pasta do seu projeto.

Agora que os pré-requisitos foram resolvidos, vamos mergulhar na implementação passo a passo.

## Etapa 1 – Configurar o mecanismo OCR para texto em árabe

A primeira coisa que precisamos fazer é configurar o Aspose OCR para reconhecer caracteres árabes. O árabe é um script da direita para a esquerda, portanto devemos informar ao mecanismo qual idioma carregar e habilitar o download automático de recursos caso os dados de idioma ainda não estejam na máquina.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Configure OCR for Arabic and let Aspose fetch the language pack if needed
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Arabic,
    AutomaticResourceDownload = true
};
```

**Por que isso importa:**  
Se você pular a configuração `Language = OcrLanguage.Arabic`, o mecanismo usará o inglês por padrão e você acabará com caracteres ilegíveis. Habilitar `AutomaticResourceDownload` evita que você precise colocar manualmente os arquivos de idioma no servidor.

## Etapa 2 – Carregar a imagem de origem

Em seguida, carregamos a imagem que contém o texto em árabe. Usar `Image.FromFile` garante que a imagem seja lida em um objeto GDI+ `Image`, que o Aspose OCR espera.

```csharp
using System.Drawing;          // For Image
using System.IO;                // For MemoryStream

// Replace with the actual path to your Arabic invoice
string imagePath = @"YOUR_DIRECTORY/arabic_invoice.jpg";

using (var inputImage = Image.FromFile(imagePath))
{
    // The rest of the workflow lives inside this using block
```

**Caso extremo:** Se a imagem for muito grande (por exemplo, uma página A3 escaneada), considere redimensioná‑la primeiro para melhorar o desempenho. O mecanismo OCR pode lidar com arquivos grandes, mas o uso de memória aumenta rapidamente.

## Etapa 3 – Reconhecer texto em árabe e capturar o resultado

Agora realmente executamos o OCR. O método `Recognize` retorna um objeto `OcrResult` que contém o texto detectado, pontuações de confiança e caixas delimitadoras (caso você precise delas para análise avançada de layout).

```csharp
    // Perform OCR on the loaded image
    OcrResult ocrResult = ocrEngine.Recognize(inputImage);
    string extractedText = ocrResult.Text;

    // Quick sanity check: print the first 200 characters to the console
    Console.WriteLine("Extracted Arabic text (preview):");
    Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**Por que manter a pré‑visualização?**  
Ver um trecho do texto extraído ajuda a confirmar que o pacote de idioma foi carregado corretamente antes de perder tempo gerando o PDF.

## Etapa 4 – Criar um novo documento PDF e adicionar uma página em branco

Com o texto em mãos, podemos começar a construir o PDF. O Aspose PDF fornece um objeto `Document` que representa todo o arquivo. Adicionar uma página nos dá uma tela para colocar tanto a imagem original quanto a camada de texto oculto.

```csharp
    // Initialize a new PDF document
    var pdfDocument = new Aspose.Pdf.Document();

    // Add a blank page – this will become the background for our image
    var pdfPage = pdfDocument.Pages.Add();
```

**Observação:** Você poderia adicionar várias páginas se estiver processando um TIFF ou PDF de várias páginas, mas para um cenário de imagem única, uma página é suficiente.

## Etapa 5 – Inserir a imagem original como elemento de fundo

Queremos que o PDF final tenha exatamente a aparência da fatura escaneada, então incorporamos a imagem como um fundo visível. A classe `Image` do Aspose PDF espera um stream, portanto lemos o arquivo em um `MemoryStream`.

```csharp
    // Load the same image bytes for the PDF background
    var backgroundImage = new Aspose.Pdf.Image
    {
        ImageStream = new MemoryStream(File.ReadAllBytes(imagePath))
    };

    // Add the image to the page's paragraph collection
    pdfPage.Paragraphs.Add(backgroundImage);
```

**Por que usar uma imagem de fundo?**  
Colocar a imagem diretamente na página preserva o layout original, cores e quaisquer selos ou logotipos que o mecanismo OCR ignoraria de outra forma.

## Etapa 6 – Adicionar o texto OCR como camada oculta

O ingrediente secreto para um **PDF pesquisável** é uma camada de texto oculta que fica sobre a imagem. Definindo o tamanho da fonte para `0`, tornamos o texto invisível ao olho humano, mas ainda selecionável e pesquisável.

```csharp
    // Create a TextFragment with the extracted Arabic text
    var searchableText = new Aspose.Pdf.Text.TextFragment(extractedText)
    {
        // Hide the visible text; only the text layer remains searchable
        TextState = { FontSize = 0 }
    };

    // Add the hidden text fragment to the same page
    pdfPage.Paragraphs.Add(searchableText);
```

**Nuance importante:**  
Se precisar que o texto oculto alinhe perfeitamente com a imagem (por exemplo, quando o OCR retorna coordenadas), você pode usar `TextFragmentAbsorber` e posicionar cada fragmento manualmente. Para a maioria das faturas, uma sobreposição de página inteira simples funciona bem.

## Etapa 7 – Salvar o PDF pesquisável

Finalmente, gravamos o PDF no disco. O arquivo de saída conterá tanto a imagem visual quanto o texto árabe oculto, tornando‑o totalmente pesquisável no Adobe Reader, Google Drive ou qualquer visualizador que suporte OCR.

```csharp
    // Define the output path
    string outputPath = @"YOUR_DIRECTORY/arabic_invoice_searchable.pdf";

    // Save the document
    pdfDocument.Save(outputPath);

    Console.WriteLine($"Searchable PDF created at: {outputPath}");
}
```

### Exemplo completo em funcionamento

Juntando todas as peças, aqui está o programa completo, pronto para executar:

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure OCR for Arabic
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Arabic,
            AutomaticResourceDownload = true
        };

        // 2️⃣ Load the source image
        string imagePath = @"YOUR_DIRECTORY/arabic_invoice.jpg";
        using (var inputImage = Image.FromFile(imagePath))
        {
            // 3️⃣ Run OCR and get the text
            OcrResult ocrResult = ocrEngine.Recognize(inputImage);
            string extractedText = ocrResult.Text;

            // Optional preview
            Console.WriteLine("Extracted Arabic text (preview):");
            Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));

            // 4️⃣ Create PDF document
            var pdfDocument = new Document();
            var pdfPage = pdfDocument.Pages.Add();

            // 5️⃣ Add original image as background
            var backgroundImage = new Aspose.Pdf.Image
            {
                ImageStream = new MemoryStream(File.ReadAllBytes(imagePath))
            };
            pdfPage.Paragraphs.Add(backgroundImage);

            // 6️⃣ Add hidden searchable text
            var searchableText = new TextFragment(extractedText)
            {
                TextState = { FontSize = 0 }
            };
            pdfPage.Paragraphs.Add(searchableText);

            // 7️⃣ Save the searchable PDF
            string outputPath = @"YOUR_DIRECTORY/arabic_invoice_searchable.pdf";
            pdfDocument.Save(outputPath);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Resultado esperado:** Abra o `arabic_invoice_searchable.pdf` gerado em qualquer visualizador de PDF, pressione **Ctrl + F** e digite uma palavra em árabe que aparece na fatura original. O visualizador deve localizar a palavra mesmo que você não veja nenhuma camada de texto.

## Perguntas comuns e armadilhas

- **Isso funciona com outros idiomas?**  
  Absolutamente. Basta mudar `Language = OcrLanguage.YourLanguage` e garantir que o pacote de idioma esteja disponível. O restante do pipeline permanece o mesmo.

- **E se a confiança do OCR for baixa?**  
  Você pode inspecionar `ocrResult.Confidence` (um valor entre 0 e 1). Se ficar abaixo de um limiar (por exemplo, 0,75), considere pré‑processar a imagem — corrigir inclinação, aumentar o contraste ou converter para escala de cinza — antes de enviá‑la ao mecanismo.

- **Posso adicionar várias imagens a um PDF?**  
  Sim. Percorra uma coleção de caminhos de imagens, adicione uma nova página para cada uma e repita as etapas 5‑6. Apenas lembre‑se de manter o bloco `using` para cada imagem para liberar os recursos GDI.

- **O texto oculto é realmente invisível?**  
  Definir `FontSize = 0` torna o texto invisível na maioria dos visualizadores. Se um visualizador ainda mostrar um glifo fraco, você também pode definir a cor do texto como totalmente transparente (`TextState.FillColor = Color.Transparent`).

## Próximos passos

Agora que você sabe como **criar PDF pesquisável** a partir de uma imagem em árabe, pode querer explorar:

- **Processamento em lote** – ler todas as imagens em uma pasta e gerar um PDF pesquisável único por arquivo.  
- **Adicionar coordenadas OCR** – usar `OcrResult.Regions` para posicionar cada fragmento de texto exatamente onde ele aparece, melhorando a precisão da pesquisa em layouts complexos.  
- **Criptografar o PDF** – o Aspose PDF permite adicionar senhas ou assinaturas digitais se precisar de segurança extra.  
- **Integrar com Azure Blob Storage** – armazenar os PDFs gerados diretamente na nuvem para fluxos de trabalho subsequentes.

Cada um desses tópicos naturalmente envolve as palavras‑chave secundárias **convert image to pdf**, **extract

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}