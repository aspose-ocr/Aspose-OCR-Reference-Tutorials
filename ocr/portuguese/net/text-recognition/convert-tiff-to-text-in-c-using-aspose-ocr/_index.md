---
category: general
date: 2026-03-05
description: Converta TIFF em texto em C# rapidamente com o Aspose OCR. Aprenda a
  exibir o texto OCR de arquivos TIFF de várias páginas em minutos.
draft: false
keywords:
- convert tiff to text
- aspose ocr c#
- display ocr text
language: pt
og_description: Converta TIFF em texto em C# com Aspose OCR. Este guia mostra como
  exibir o texto OCR de imagens TIFF de várias páginas passo a passo.
og_title: Converter TIFF para Texto em C# – Guia Completo de OCR da Aspose
tags:
- Aspose
- OCR
- C#
- TIFF
title: Converter TIFF para Texto em C# usando Aspose OCR
url: /pt/net/text-recognition/convert-tiff-to-text-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter TIFF para Texto em C# Usando Aspose OCR

Precisa **converter TIFF para texto** em C#? Você não está sozinho—muitos desenvolvedores lutam para extrair strings legíveis de arquivos TIFF de várias páginas. A boa notícia é que o Aspose OCR C# torna o trabalho quase indolor, e você pode **exibir texto OCR** no console ou enviá‑lo para outro sistema em segundos.

Neste tutorial vamos percorrer um exemplo completo, pronto‑para‑executar, que mostra exatamente como carregar um TIFF de várias páginas, executar OCR e imprimir o texto de cada página. Sem etapas ocultas, sem atalhos “veja a documentação”. Ao final, você terá um programa autônomo que pode ser inserido em qualquer projeto .NET.

## O que você vai precisar

- .NET 6.0 ou superior (o exemplo tem como alvo o .NET 6, mas o .NET 5 também funciona)  
- Um arquivo de licença válido do Aspose OCR (`Aspose.OCR.lic`). A biblioteca funciona sem licença, mas você encontrará uma marca d'água de avaliação de 20 segundos.  
- Um arquivo TIFF de várias páginas que você deseja processar (vamos chamá‑lo de `multipage.tif`).  
- Visual Studio 2022 ou qualquer editor de sua preferência—nada de exótico.

Se você já marcou todas essas caixas, vamos mergulhar.

## Etapa 1: Instalar o Pacote NuGet Aspose OCR

Antes de qualquer código ser executado, você precisa da própria biblioteca. Abra um terminal na pasta do seu projeto e execute:

```bash
dotnet add package Aspose.OCR
```

Esse comando de uma linha baixa a versão estável mais recente (em março 2026 é a 23.9).  

> **Dica profissional:** Mantenha seus pacotes atualizados; versões mais recentes costumam incluir otimizações de desempenho para TIFFs grandes.

## Etapa 2: Configurar a Licença Aspose OCR C# (Opcional, mas Recomendado)

Executar o motor OCR sem licença é possível, mas a saída será prefixada com um aviso de avaliação. Para evitar isso, aponte o motor para o seu arquivo `.lic`:

```csharp
using Aspose.OCR;

// ...

// Step 2: Apply your Aspose OCR license (optional but recommended)
var ocrEngine = new OcrEngine();
ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

Se você pular esta etapa, o código ainda funciona—apenas lembre‑se do texto extra nos resultados.

## Etapa 3: Carregar e Reconhecer o TIFF de Múltiplas Páginas

Agora realmente **convertemos TIFF para texto**. O helper `ImageStream.FromFile` lê o arquivo para um formato que o motor entende. Em seguida chamamos `Recognize()`, que devolve um objeto `OcrResult` contendo o texto de cada página.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 3: Load the multi‑page TIFF image to be processed
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\multipage.tif");

// Step 4: Perform OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize();
```

> **Por que isso importa:** `Recognize()` faz o trabalho pesado—análise de pixels, detecção de idioma e reconstrução de linhas de texto—tudo em código nativo C#. O objeto de resultado fornece acesso página por página, o que é perfeito para **exibir texto OCR** mais tarde.

## Etapa 4: Percorrer as Páginas e **Exibir Texto OCR**

Com o resultado em mãos, simplesmente iteramos sobre as páginas e imprimimos cada uma. Esta é a parte onde você realmente vê a conversão de imagem para texto simples.

```csharp
// Step 5: Iterate through each page of the result and display the recognized text
for (int pageIndex = 0; pageIndex < ocrResult.PageCount; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResult.GetPageText(pageIndex));
    Console.WriteLine(); // Blank line for readability
}
```

Executar o programa gera uma saída semelhante ao exemplo a seguir (seu texto real será diferente, dependendo do conteúdo do TIFF):

```
--- Page 1 ---
Hello, world!
This is the first page of our multi‑page TIFF.

--- Page 2 ---
Second page starts here.
More sample text follows.
```

É isso—você **converteu TIFF para texto** e **exibiu texto OCR** para todas as páginas com sucesso.

## Exemplo Completo Funcional

Abaixo está o programa completo que você pode copiar‑colar em um novo projeto de console (`dotnet new console`). Ele inclui todas as diretivas `using`, tratamento de licença e verificação de erros.

```csharp
// ConvertTiffToText.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ConvertTiffToText
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -----------------------------------------------------------------
            // Step 2: Apply your Aspose OCR license (optional but recommended)
            // -----------------------------------------------------------------
            try
            {
                ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
            }
            catch (Exception ex)
            {
                Console.WriteLine("License file not found or invalid. Running in trial mode.");
                Console.WriteLine($"Details: {ex.Message}");
            }

            // -----------------------------------------------------------------
            // Step 3: Load the multi‑page TIFF image to be processed
            // -----------------------------------------------------------------
            const string tiffPath = @"C:\Images\multipage.tif";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"Error: TIFF file not found at {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -----------------------------------------------------------------
            // Step 4: Perform OCR – this is where we convert TIFF to text
            // -----------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize();

            // -----------------------------------------------------------------
            // Step 5: Iterate through each page and display OCR text
            // -----------------------------------------------------------------
            Console.WriteLine($"Successfully processed {ocrResult.PageCount} page(s).");
            for (int i = 0; i < ocrResult.PageCount; i++)
            {
                Console.WriteLine($"--- Page {i + 1} ---");
                Console.WriteLine(ocrResult.GetPageText(i));
                Console.WriteLine(); // Add spacing between pages
            }

            // Keep the console window open when debugging
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Saída esperada** (truncada para brevidade) foi mostrada anteriormente. Se aparecer a marca d'água de avaliação, verifique se o caminho da licença está correto.

## Armadilhas Comuns ao Converter TIFF para Texto

| Problema | Por que acontece | Como corrigir |
|----------|------------------|---------------|
| **Falta de memória em TIFFs enormes** | O motor carrega a imagem inteira na RAM. | Use `ImageStream.FromFile(..., loadOnlyFirstPage: false)` e processe as páginas em lotes, ou aumente o limite de memória do processo. |
| **Caracteres estranhos** | Imagens de baixa resolução confundem o motor OCR. | Pré‑procese o TIFF (por exemplo, aumente a DPI para 300) antes de enviá‑lo ao Aspose OCR. |
| **Licença não aplicada** | `SetLicense` lança uma exceção que você ignora. | Envolva a chamada em try/catch (como mostrado) e registre o erro. |
| **Dados de idioma ausentes** | Por padrão o OCR assume inglês. | Defina `ocrEngine.Language = OcrLanguage.French;` (ou qualquer idioma suportado) antes de `Recognize()`. |

Tratar esses casos de borda garante que sua conversão funcione suavemente em produção.

## Próximos Passos: Indo Além da Exibição Simples

Agora que você pode **converter TIFF para texto** e **exibir texto OCR**, talvez queira:

- **Salvar o texto extraído** em um arquivo `.txt` ou em um banco de dados para **análise posterior**.  
- **Combinar vários TIFFs** em um único PDF pesquisável usando Aspose.PDF.  
- **Aplicar pós‑processamento** (correção ortográfica, limpeza com regex) para melhorar a precisão.  

Todas essas extensões se baseiam no mesmo padrão central que acabamos de cobrir.

---

### TL;DR

Percorremos uma solução completa em C# que **converte TIFF para texto** usando Aspose OCR C#. O código cria um `OcrEngine`, opcionalmente **carrega uma licença**, lê um TIFF de múltiplas páginas, executa OCR e **exibe texto OCR** página por página. Com o exemplo completo fornecido, você pode inserir isso em qualquer projeto .NET e começar a extrair texto imediatamente.

Tem dúvidas sobre desempenho, suporte a idiomas ou integração com outros produtos Aspose? Deixe um comentário abaixo—bom código!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}