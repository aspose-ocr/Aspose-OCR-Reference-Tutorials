---
category: general
date: 2026-02-13
description: Crie PDF pesquisável a partir de imagem usando Aspose.OCR. Aprenda a
  converter imagem em PDF, extrair texto da imagem, incorporar fontes no PDF e reconhecer
  texto de PNG.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- embed fonts in pdf
- recognize text from png
language: pt
og_description: Crie PDF pesquisável a partir de imagem com Aspose.OCR. Este guia
  mostra como converter imagem em PDF, incorporar fontes e extrair texto de PNG sem
  esforço.
og_title: Criar PDF pesquisável a partir de imagem – Tutorial passo a passo em C#
tags:
- C#
- OCR
- Aspose
- PDF generation
title: Criar PDF pesquisável a partir de imagem – Guia completo de C#
url: /pt/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável a partir de imagem – Guia completo em C#

Já precisou **criar PDF pesquisável** a partir de um PNG digitalizado, mas não sabia por onde começar? Você não está sozinho. Em muitos projetos — pense em digitalização de faturas ou arquivamento de manuais antigos — poder transformar uma imagem em um PDF que realmente pode ser pesquisado é um divisor de águas.  

Neste tutorial, percorreremos os passos exatos para **converter imagem em PDF**, **extrair texto da imagem**, incorporar as fontes necessárias e, finalmente, obter um arquivo PDF totalmente pesquisável. Sem referências vagas, apenas um exemplo completo e executável que você pode copiar‑colar no Visual Studio hoje.

> **O que você receberá:** um aplicativo de console C# que lê `input.png`, executa OCR, incorpora fontes, mantém a imagem raster original como plano de fundo e grava `output.pdf`. Ao final, você entenderá *por que* cada linha importa e como ajustá‑la para seus próprios cenários.

---

## Pré‑requisitos

- .NET 6.0 SDK ou posterior (o código também funciona com .NET Framework 4.7+).  
- Aspose.OCR for .NET – você pode obtê‑lo no NuGet (`Install-Package Aspose.OCR`).  
- Uma imagem PNG de exemplo (`input.png`) colocada em uma pasta que você controla.  
- Familiaridade básica com projetos de console C# (se nunca criou um, basta abrir o Visual Studio → **Create a new project** → **Console App** → **C#**).

> **Dica:** Aspose oferece uma licença de teste gratuita; basta colocar o arquivo `.lic` ao lado do seu executável e a biblioteca funcionará sem marcas d’água.

---

## Etapa 1: Configurar o mecanismo de OCR – Reconhecer texto do PNG

A primeira coisa que precisamos é um mecanismo de OCR que realmente leia os caracteres em um arquivo PNG. Aspose.OCR torna isso simples.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

// Initialize the OCR engine with English language support
OcrEngine ocrEngine = new OcrEngine
{
    // Primary language – you can add more if needed
    Language = OcrLanguage.English
};
```

**Por que isso importa:**  
Definir `Language` informa ao mecanismo qual conjunto de caracteres esperar. Se você pular isso, o mecanismo usará um modo genérico que pode interpretar erroneamente caracteres acentuados ou números. Para documentos multilíngues, você pode passar uma lista separada por vírgulas como `OcrLanguage.English | OcrLanguage.French`.

---

## Etapa 2: Carregar e reconhecer a imagem – Extrair texto da imagem

Agora que o mecanismo está pronto, alimentamos ele com o PNG que queremos processar.

```csharp
// Path to the source image; adjust as needed
string inputPath = @"YOUR_DIRECTORY/input.png";

// Perform OCR – this populates the engine's internal text representation
ocrEngine.RecognizeImage(inputPath);
```

**O que está acontecendo nos bastidores?**  
`RecognizeImage` escaneia o bitmap, identifica blocos de texto e armazena o resultado em `ocrEngine`. Você pode acessar `ocrEngine.Text` mais tarde se precisar apenas da string bruta, mas para um PDF pesquisável deixaremos o Aspose fazer a conversão diretamente.

> **Caso extremo:** Se o seu PNG for muito grande (mais de 10 MB) você pode ficar sem memória. Nesse caso, considere redimensionar a imagem primeiro ou usar `OcrEngine.RecognizeImage(Stream)` para transmitir os dados.

---

## Etapa 3: Configurar opções de exportação PDF – Incorporar fontes no PDF

Um PDF pesquisável não é útil se as fontes não estiverem incorporadas; o documento ficaria quebrado em máquinas que não possuam as tipografias necessárias. Aspose nos permite alternar isso com um simples objeto de opções.

```csharp
// Define how the searchable PDF should be built
SearchablePdfOptions pdfOptions = new SearchablePdfOptions
{
    // Guarantees the PDF renders correctly everywhere
    EmbedFonts = true,

    // Keeps the original raster image as a visual background
    KeepOriginalImage = true
};
```

**Por que incorporar fontes?**  
Quando `EmbedFonts` é `true`, o PDF carrega os dados da fonte dentro do arquivo. Isso garante que qualquer visualizador — Chrome, Adobe Reader ou um app móvel — exiba o texto exatamente como pretendido, mesmo quando o sistema de destino não possui a fonte.

**Quando você definiria `KeepOriginalImage` como `false`?**  
Se precisar apenas do texto extraído e quiser um arquivo menor, desativar isso remove a imagem de fundo, deixando um PDF “limpo” contendo apenas texto.

---

## Etapa 4: Exportar para PDF pesquisável – Converter imagem em PDF

Com os resultados do OCR e as opções de PDF preparados, o passo final é uma única linha que grava o PDF pesquisável no disco.

```csharp
// Destination path for the generated PDF
string outputPath = @"YOUR_DIRECTORY/output.pdf";

// Export the OCR result as a searchable PDF
ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created.");
```

**O que você verá:**  
Abrindo `output.pdf` em qualquer visualizador, você pode selecionar texto, copiar‑colar e até executar uma busca (`Ctrl + F`) para localizar palavras que originalmente existiam apenas como pixels no PNG.

---

## Exemplo completo em funcionamento

Abaixo está o programa completo que você pode compilar e executar imediatamente. Substitua `YOUR_DIRECTORY` pela pasta que contém `input.png`.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine – set language to English
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Recognize text from the PNG image
        string inputPath = @"YOUR_DIRECTORY/input.png";
        ocrEngine.RecognizeImage(inputPath);

        // 3️⃣ Prepare PDF options – embed fonts & keep raster background
        SearchablePdfOptions pdfOptions = new SearchablePdfOptions
        {
            EmbedFonts = true,
            KeepOriginalImage = true
        };

        // 4️⃣ Export to a searchable PDF file
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

        // 5️⃣ Notify the user
        Console.WriteLine("Searchable PDF created.");
    }
}
```

**Saída esperada no console:**

```
Searchable PDF created.
```

Abra `output.pdf` e tente buscar uma palavra que você sabe que aparece em `input.png`. Se ele destacar, você criou com sucesso **PDF pesquisável** a partir de uma imagem.

---

## Perguntas comuns & Dicas avançadas

### “Posso processar várias imagens em uma única execução?”

Com certeza. Envolva a lógica de reconhecimento e exportação em um loop, talvez usando `Directory.GetFiles(..., "*.png")`. Apenas lembre‑se de dar a cada PDF um nome único, por exemplo, `Path.GetFileNameWithoutExtension(img) + ".pdf"`.

### “E se meu documento contiver texto em inglês e espanhol?”

Defina a propriedade de idioma para uma flag combinada:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

Aspose então tentará detectar caracteres de ambos os alfabetos.

### “O arquivo PDF está enorme — como posso reduzi‑lo?”

Duas dicas rápidas:

1. Defina `pdfOptions.KeepOriginalImage = false` para remover o fundo raster.  
2. Use `pdfOptions.ImageCompression = ImageCompression.Jpeg;` (você precisará adicionar a propriedade) para comprimir a imagem incorporada.

### “Preciso de licença para uso em produção?”

A versão de teste funciona bem para testes, mas para implantação comercial você deve adquirir uma licença e registrá‑la logo no início da sua aplicação:

```csharp
Aspose.OCR.License license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

---

## Expandindo a solução

Agora que você sabe como **criar PDF pesquisável**, pode querer:

- **Adicionar marca d’água** – use `PdfDocument` do Aspose.PDF para sobrepor texto após o OCR.  
- **Processamento em lote de PDFs** – combine vários PDFs pesquisáveis em um só usando `PdfFileEditor`.  
- **Integrar com Azure Blob Storage** – leia/escreva os fluxos de imagem e PDF diretamente da nuvem, eliminando I/O local de arquivos.

Cada uma dessas extensões segue o mesmo padrão: obtenha o resultado do OCR, configure a próxima biblioteca e encadeie as operações.

---

## Conclusão

Você acabou de aprender como **criar PDF pesquisável** a partir de uma imagem PNG usando Aspose.OCR em C#. Ao inicializar o mecanismo de OCR, reconhecer o texto, configurar `SearchablePdfOptions` para **incorporar fontes no PDF** e exportar, você obtém um arquivo que é visualmente idêntico ao original e totalmente pesquisável.  

A partir daqui, sinta‑se à vontade para experimentar conversões em lote, diferentes idiomas ou compressão mais agressiva — o que melhor se encaixar no seu fluxo de trabalho. Se encontrar alguma dificuldade, os fóruns da Aspose e a documentação da API são ótimos recursos, mas os passos principais acima cobrem 90 % dos casos de uso típicos.

Feliz codificação, e que seus PDFs estejam sempre pesquisáveis!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}