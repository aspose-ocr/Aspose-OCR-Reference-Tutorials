---
category: general
date: 2026-04-08
description: Crie PDF pesquisável rapidamente e aprenda como comprimir imagens de
  PDF, incorporar fontes em PDF e reconhecer texto em imagens em C# usando Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- compress pdf images
- embed fonts pdf
- image to searchable pdf
- recognize text image
language: pt
og_description: Crie PDFs pesquisáveis rapidamente com Aspose.OCR. Aprenda a compactar
  imagens de PDF, incorporar fontes ao PDF e reconhecer texto em imagens em um único
  tutorial.
og_title: Criar PDF pesquisável – Guia completo de C#
tags:
- Aspose.OCR
- C#
- PDF Generation
title: Criar PDF pesquisável – Guia completo em C# para converter imagens em PDF
url: /pt/net/text-recognition/create-searchable-pdf-complete-c-guide-for-image-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável – Guia completo em C#

Precisa **criar PDF pesquisável** a partir de uma imagem escaneada? Você não é o único que ficou encarando um PNG gigante e se perguntou como transformá‑lo em um documento leve e pesquisável por texto. A boa notícia é que, com Aspose.OCR, você pode fazer isso em poucas linhas, e ainda aprenderá a **compactar imagens PDF**, **incorporar fontes PDF** e **reconhecer texto em imagem** sem esforço.

Neste tutorial percorreremos todo o processo: desde carregar a imagem, executar OCR, ajustar as opções de salvamento do PDF, até finalmente gravar um PDF pesquisável no disco. Ao final, você terá um método pronto‑para‑uso que pode ser inserido em qualquer projeto .NET, além de algumas dicas avançadas para casos de borda que você pode encontrar mais tarde.

## O que você precisará

- **.NET 6+** (o código também funciona no .NET Framework 4.7, mas vamos focar no .NET 6 para sintaxe moderna).  
- **Aspose.OCR para .NET** – instale via NuGet: `Install-Package Aspose.OCR`.  
- Um arquivo de imagem (PNG, JPEG, TIFF) que contenha o texto que você deseja tornar pesquisável.  
- Um pouco de curiosidade – o resto está coberto abaixo.

> **Dica profissional:** Se você planeja processar dezenas de páginas, considere reutilizar uma única instância de `OcrEngine` para evitar a sobrecarga de carregar repetidamente os dados de idioma.

## Etapa 1: Configurar o mecanismo OCR – Reconhecer texto em imagem

A primeira coisa que precisamos é de um mecanismo OCR que consiga ler os caracteres do bitmap de origem. Aspose.OCR permite especificar o idioma (English, French, etc.) e devolve um objeto `OcrResult` que contém tanto o texto bruto quanto os dados da imagem.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

public static OcrResult LoadAndRecognize(string imagePath)
{
    // Initialize the OCR engine – “en” is the ISO code for English.
    var ocrEngine = new OcrEngine { Language = "en" };

    // Recognize the image and get the result.
    OcrResult result = ocrEngine.RecognizeImage(imagePath);

    // Quick sanity check – throw if nothing was detected.
    if (string.IsNullOrWhiteSpace(result.Text))
        throw new InvalidOperationException("No text was recognized in the image.");

    return result;
}
```

**Por que isso importa:**  
- Definir o idioma melhora a precisão drasticamente; o mecanismo carrega dicionários específicos de idioma nos bastidores.  
- O `OcrResult` não só contém a string extraída, mas também o bitmap subjacente, que mais tarde incorporaremos ao PDF para que o documento permaneça visualmente idêntico ao escaneamento original.

## Etapa 2: Configurar as opções de salvamento PDF – Compactar imagens PDF & Incorporar fontes

Um PDF pesquisável é essencialmente um PDF normal com uma camada de texto invisível sobre a imagem escaneada. Se você ignorar a compactação, o arquivo final pode ficar enorme. A classe `PdfSaveOptions` oferece controle granular sobre a qualidade da imagem, incorporação de fontes e se as fontes devem ser subconjuntos.

```csharp
public static PdfSaveOptions GetPdfSaveOptions()
{
    return new PdfSaveOptions
    {
        // Reduce file size by compressing the raster image.
        CompressImages = true,

        // ImageQuality ranges from 0 (worst) to 100 (best). 75 is a good balance.
        ImageQuality = 75,

        // Embedding fonts ensures the text layer looks the same on any machine.
        EmbedFonts = true,

        // Subsetting keeps only the glyphs we actually use – another size saver.
        FontSubset = true
    };
}
```

**Por que você deve incorporar fontes PDF:**  
Quando um PDF é aberto em um sistema que não possui a fonte exata usada na camada OCR, o texto pode aparecer corrompido. Incorporar garante fidelidade visual em todas as plataformas, o que é crucial para documentos legais ou de arquivo.

## Etapa 3: Salvar o resultado como PDF pesquisável – Imagem para PDF pesquisável

Agora juntamos tudo: pegamos o `OcrResult`, aplicamos nossas `PdfSaveOptions` e gravamos o arquivo. O método `SaveAsSearchablePdf` faz o trabalho pesado — criando uma sobreposição de texto oculta que espelha a saída do OCR enquanto preserva a imagem original.

```csharp
public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
{
    // Step 1: Recognize the image.
    OcrResult ocrResult = LoadAndRecognize(inputImage);

    // Step 2: Prepare PDF options.
    PdfSaveOptions pdfOptions = GetPdfSaveOptions();

    // Step 3: Write the searchable PDF.
    ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);

    Console.WriteLine($"Searchable PDF created at: {outputPdf}");
}
```

### Exemplo completo em funcionamento

Abaixo está um programa de console autônomo que você pode copiar‑colar em um novo projeto .NET console. Ele assume que a imagem está em uma pasta chamada `YOUR_DIRECTORY` relativa ao executável.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

class Program
{
    static void Main()
    {
        string inputPath = "YOUR_DIRECTORY/input.png";
        string outputPath = "YOUR_DIRECTORY/output.pdf";

        try
        {
            CreateCompressedSearchablePdf(inputPath, outputPath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }

    // --- Methods from the previous steps -------------------------------------------------
    public static OcrResult LoadAndRecognize(string imagePath)
    {
        var ocrEngine = new OcrEngine { Language = "en" };
        OcrResult result = ocrEngine.RecognizeImage(imagePath);
        if (string.IsNullOrWhiteSpace(result.Text))
            throw new InvalidOperationException("OCR did not detect any text.");
        return result;
    }

    public static PdfSaveOptions GetPdfSaveOptions()
    {
        return new PdfSaveOptions
        {
            CompressImages = true,
            ImageQuality = 75,
            EmbedFonts = true,
            FontSubset = true
        };
    }

    public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
    {
        OcrResult ocrResult = LoadAndRecognize(inputImage);
        PdfSaveOptions pdfOptions = GetPdfSaveOptions();
        ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);
        Console.WriteLine("Searchable PDF created.");
    }
}
```

Executar o programa gerará `output.pdf` que pode ser aberto no Adobe Reader, Foxit ou qualquer visualizador de PDF e permitirá buscar instantaneamente palavras que originalmente estavam apenas na imagem.

## Etapa 4: Verificar a saída – A busca funciona?

Depois que o arquivo for gerado, abra‑o e teste a busca interna (Ctrl + F). Se você conseguir localizar palavras como “invoice”, “date” ou “total”, você criou com sucesso um **PDF pesquisável**.  

Se a busca não retornar nada:

1. **Verifique a precisão do OCR** – talvez a imagem de origem tenha baixa resolução. Considere aumentar o DPI antes do OCR (Aspose permite definir `Resolution` no engine).  
2. **Confirme a incorporação de fontes** – abra as propriedades do PDF e procure em *Fonts*; a fonte incorporada deve aparecer listada.  
3. **Inspecione a compactação da imagem** – um `ImageQuality` muito baixo pode tornar a camada visual ilegível, o que às vezes confunde ferramentas posteriores.

## Variações comuns & casos de borda

| Cenário | O que ajustar | Por quê |
|----------|----------------|-----|
| **TIFF multipágina** | Percorrer cada quadro, chamar `RecognizeImage` por página, então usar `PdfSaveOptions` com `AppendMode = true`. | Mantém cada página escaneada como sua própria página pesquisável. |
| **Idioma não‑inglês** | Alterar `Language = "fr"` (ou código ISO apropriado) e, opcionalmente, fornecer um dicionário personalizado. | Melhora o reconhecimento de caracteres acentuados e glifos específicos do idioma. |
| **Imagens muito grandes** | Redimensionar o bitmap antes do OCR (`ocrEngine.Image = Image.FromFile(...).GetThumbnailImage(...)`). | Reduz o uso de memória e acelera o OCR sem sacrificar muita precisão. |
| **Precisa da confiança do OCR** | Acessar `ocrResult.RecognizedWords` e inspecionar a propriedade `Confidence`. | Permite sinalizar palavras de baixa confiança para revisão manual. |

## Dicas de desempenho

- **Reutilize o `OcrEngine`** ao processar um lote de arquivos – ele faz cache dos dados de idioma.  
- **Paralelize** a etapa de reconhecimento com `Parallel.ForEach` se estiver em uma máquina multi‑core, mas mantenha as gravações de PDF sequenciais para evitar conflitos de acesso a arquivos.  
- **Ajuste `ImageQuality`**: 85‑90 oferece imagens quase sem perdas, enquanto 60‑70 costuma ser suficiente para documentos predominantemente textuais.

## Conclusão

Cobrimos tudo o que você precisa para **criar PDF pesquisável** a partir de imagens usando Aspose.OCR, além de aprender a **compactar imagens PDF**, **incorporar fontes PDF** e reconhecer texto em imagem de forma eficiente. O exemplo completo está pronto para ser inserido em qualquer projeto C#, e as dicas extras ajudam a adaptar a solução a cargas maiores ou a diferentes idiomas.

Pronto para o próximo passo? Experimente adicionar uma marca d’água, mesclar vários PDFs pesquisáveis ou integrar esta rotina a uma API web para que usuários façam upload de escaneamentos e recebam PDFs pesquisáveis instantaneamente. As possibilidades são infinitas, e com os fundamentos em mãos será fácil estender o fluxo de trabalho.

Boa codificação, e que seus PDFs permaneçam pequenos, pesquisáveis e perfeitamente renderizados!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}