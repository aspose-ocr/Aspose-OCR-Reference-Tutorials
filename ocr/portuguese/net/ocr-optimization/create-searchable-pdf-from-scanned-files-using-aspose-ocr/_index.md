---
category: general
date: 2026-01-04
description: Crie PDF pesquisável a partir de um PDF escaneado rapidamente. Aprenda
  como converter PDF escaneado, adicionar OCR ao PDF e ajustar a qualidade da imagem
  com Aspose OCR em C#.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- add ocr to pdf
- adjust image quality
- how to use ocr
language: pt
og_description: Crie um PDF pesquisável a partir de um PDF escaneado rapidamente.
  Siga este guia passo a passo para converter PDF escaneado, adicionar OCR ao PDF
  e ajustar a qualidade da imagem.
og_title: Criar PDF pesquisável a partir de arquivos digitalizados usando Aspose OCR
tags:
- Aspose OCR
- C#
- PDF processing
title: Criar PDF pesquisável a partir de arquivos escaneados usando Aspose OCR
url: /pt/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável a partir de arquivos digitalizados usando Aspose OCR

Já precisou **criar PDF pesquisável** a partir de uma pilha de documentos digitalizados, mas não sabia por onde começar? Você não está sozinho—muitos desenvolvedores se deparam com esse obstáculo ao montar pipelines de gerenciamento de documentos. A boa notícia? Com Aspose OCR você pode **converter PDF digitalizado**, aplicar OCR e ajustar a qualidade da imagem em apenas algumas linhas de C#.

Neste tutorial vamos percorrer todo o processo, desde o carregamento de um PDF digitalizado até a gravação de uma versão totalmente pesquisável. Ao final, você saberá exatamente **como usar OCR** com Aspose, por que cada configuração importa e o que ajustar quando as coisas não saem como esperado. Sem referências vagas—apenas um exemplo completo e executável que você pode inserir no seu projeto hoje.

## Pré‑requisitos

Antes de mergulharmos, certifique‑se de que você tem:

- .NET 6.0 ou superior (o código funciona também com .NET Core e .NET Framework)
- Uma licença válida do Aspose OCR (a avaliação gratuita serve para testes)
- Um PDF de entrada chamado `input.pdf` colocado em uma pasta que você controla
- Visual Studio 2022 ou qualquer editor C# de sua preferência

É só isso. Se algum desses itens lhe for desconhecido, pause e instale o que falta—não há mais nenhum requisito.

## Etapa 1: Inicializar o mecanismo OCR e carregar o PDF digitalizado  
**(É aqui que **adicionamos OCR ao PDF** pela primeira vez.)**

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Load the scanned PDF from disk
ocrEngine.LoadPdf(@"C:\Docs\input.pdf");
```

*Por que esta etapa?*  
O `OcrEngine` é o coração do Aspose OCR. Carregar o PDF informa ao motor onde procurar as imagens raster que ele analisará posteriormente. Se você pular isso, não haverá nada para converter, e as etapas subsequentes lançarão uma exceção.

> **Dica:** Se o seu PDF estiver protegido por senha, use `ocrEngine.LoadPdf(path, password)` para evitar um erro em tempo de execução.

## Etapa 2: Definir idioma principal e idiomas adicionais  
**(Vamos **converter PDF digitalizado** em inglês, francês e alemão.)**

```csharp
// Primary language – the most common language in the document
ocrEngine.Config.Language = Language.English;

// Add extra languages if the document contains multilingual text
ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };
```

*Por que o idioma importa?*  
A precisão do OCR depende do conjunto de caracteres que ele espera. Ao declarar o inglês como idioma principal e adicionar francês/alemão, o motor pode interpretar corretamente caracteres acentuados e glifos especiais. Esquecer isso costuma gerar texto confuso.

## Etapa 3: Ajustar a qualidade da imagem – Afinar a saída PDF  
**(Aqui **ajustamos a qualidade da imagem** para equilibrar tamanho do arquivo e legibilidade.)**

```csharp
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    ImageQuality = 90,          // JPEG quality for embedded images (0‑100)
    Compress = true,            // Enable PDF compression to shrink file size
    PreserveOriginalLayout = true // Keep the scanned layout intact
};
```

*Por que ajustar `ImageQuality`?*  
Um valor mais alto (90‑100) preserva a nitidez, crucial para a precisão do OCR, mas também aumenta o tamanho do arquivo. Se você estiver arquivando milhões de páginas, reduza para 70‑80 para obter um PDF mais leve sem sacrificar muita legibilidade.

## Etapa 4: Salvar o resultado como PDF pesquisável  
**(Agora finalmente **criamos PDF pesquisável** que você pode indexar.)**

```csharp
// Export the OCR result as a searchable PDF
ocrEngine.SaveAsSearchablePdf(@"C:\Docs\output.pdf", pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created at C:\\Docs\\output.pdf");
```

*O que realmente acontece?*  
Aspose OCR extrai a camada de texto de cada página e a incorpora atrás da imagem original. O PDF permanece visualmente idêntico, mas agora você pode selecionar, copiar e buscar o texto—um grande ganho para fluxos de trabalho posteriores.

## Etapa 5: Verificar a saída (Opcional, mas recomendado)  
É fácil supor que tudo funcionou, mas uma verificação rápida evita dores de cabeça depois.

```csharp
using System.Diagnostics;

// Open the generated PDF automatically (Windows only)
Process.Start(new ProcessStartInfo
{
    FileName = @"C:\Docs\output.pdf",
    UseShellExecute = true
});
```

Abra o arquivo, tente selecionar uma palavra ou pressione `Ctrl+F` e digite uma frase que você sabe que está presente na digitalização original. Se o texto for selecionável, você **criou PDF pesquisável** com sucesso.

## Casos de borda comuns & Como lidar com eles  

| Situação | Por que acontece | Correção rápida |
|-----------|----------------|-----------|
| **Páginas com resolução mista** (algumas 150 dpi, outras 300 dpi) | A qualidade do OCR varia por página, resultando em pesquisabilidade desigual. | Defina `ocrEngine.Config.Dpi = 300;` antes de carregar para forçar up‑sampling, ou pré‑procese com `ImageProcessor` para normalizar o DPI. |
| **PDF criptografado** | Aspose OCR não consegue ler sem a senha. | Passe a senha para `LoadPdf` como mostrado anteriormente. |
| **PDFs grandes (>500 MB)** | O consumo de memória dispara, causando `OutOfMemoryException`. | Processar o documento em partes: `ocrEngine.SplitPdfIntoPages();` então OCR em cada página individualmente e mescle os resultados. |
| **Caracteres não latinos** (ex.: cirílico) | Idioma não adicionado, então os caracteres viram “?”. | Adicione `Language.Russian` (ou outro idioma necessário) a `AdditionalLanguages`. |
| **Qualidade de imagem muito baixa** | O texto fica borrado, OCR falha. | Aumente `ImageQuality` ou use `pdfOptions.Dpi = 300;` para incorporar imagens de alta resolução. |

## Exemplo completo, pronto para executar  

A seguir está o programa completo que você pode copiar‑colar em um novo aplicativo console. Ele inclui todas as etapas, tratamento de erros e comentários para clareza.

```csharp
using System;
using System.Diagnostics;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\Docs\input.pdf";
            string outputPath = @"C:\Docs\output.pdf";

            try
            {
                // 1️⃣ Initialize OCR engine and load scanned PDF
                OcrEngine ocrEngine = new OcrEngine();
                ocrEngine.LoadPdf(inputPath);

                // 2️⃣ Configure languages (primary + additional)
                ocrEngine.Config.Language = Language.English;
                ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };

                // 3️⃣ Set PDF save options – adjust image quality as needed
                PdfSaveOptions pdfOptions = new PdfSaveOptions
                {
                    ImageQuality = 90,
                    Compress = true,
                    PreserveOriginalLayout = true
                };

                // 4️⃣ Save as searchable PDF
                ocrEngine.SaveAsSearchablePdf(outputPath, pdfOptions);
                Console.WriteLine($"✅ Searchable PDF created at {outputPath}");

                // 5️⃣ Optional: open the file to verify
                Process.Start(new ProcessStartInfo
                {
                    FileName = outputPath,
                    UseShellExecute = true
                });
            }
            catch (Exception ex)
            {
                // Friendly error message – helps during debugging
                Console.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
                // For real‑world apps, consider logging the stack trace
            }
        }
    }
}
```

**Saída esperada:**  
```
✅ Searchable PDF created at C:\Docs\output.pdf
```

Ao abrir `output.pdf`, você deve ser capaz de selecionar e buscar qualquer texto que estava presente na digitalização original.

---

## Perguntas Frequentes (FAQs)

**P: Isso funciona com PDFs que contêm imagens digitalizadas e texto nativo?**  
R: Absolutamente. Aspose OCR adiciona uma camada de texto oculta apenas onde for necessário, deixando o texto existente intacto.

**P: Posso processar em lote uma pasta de PDFs?**  
R: Sim. Envolva o código acima em um loop `foreach (var file in Directory.GetFiles(folder, "*.pdf"))` e ajuste o caminho de saída conforme necessário.

**P: Como reduzir ainda mais o tamanho final do PDF?**  
R: Diminua `ImageQuality` para 70‑80, habilite `Compress`, ou use `pdfOptions.Dpi = 150` para fazer downsample das imagens antes de incorporá‑las.

**P: Existe uma forma de extrair o texto OCR sem criar um PDF?**  
R: Chame `ocrEngine.ExtractText();` após carregar o PDF. Isso devolve uma string de texto puro que você pode armazenar ou indexar.

---

## Conclusão  

Acabamos de cobrir **como usar OCR** com Aspose para **criar PDF pesquisável** a partir de um documento digitalizado, mostramos **como converter PDF digitalizado**, demonstramos **como adicionar OCR ao PDF** e explicamos **como ajustar a qualidade da imagem** para resultados ótimos. O código completo está pronto para ser executado, e a tabela de solução de problemas deve mantê‑lo em movimento quando algo inesperado surgir.

O que vem a seguir? Experimente:

- Diferentes pacotes de idioma para arquivos multilíngues
- Pré‑processamento de imagem personalizado (deskew, despeckle) via `ImageProcessor`
- Integração do PDF pesquisável em um pipeline SharePoint ou ElasticSearch

Sinta‑se à vontade para deixar um comentário se encontrar algum obstáculo ou descobrir um ajuste inteligente. Boa codificação e aproveite esses PDFs instantaneamente pesquisáveis! 

![Fluxograma de criação de PDF pesquisável mostrando motor OCR → configuração de idioma → opções de salvamento de PDF → saída de PDF pesquisável](create-searchable-pdf-flow.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}