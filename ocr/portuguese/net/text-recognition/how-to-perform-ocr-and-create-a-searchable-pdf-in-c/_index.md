---
category: general
date: 2026-02-14
description: Aprenda a fazer OCR em um TIFF ou imagem e converter PDF usando OCR para
  criar um PDF pesquisável — guia passo a passo em C#.
draft: false
keywords:
- how to perform OCR
- convert pdf using OCR
- make searchable pdf
- tiff to searchable pdf
- searchable pdf from image
language: pt
og_description: Descubra como realizar OCR em imagens, converter PDF usando OCR e
  criar um PDF pesquisável com o Aspose OCR em um tutorial conciso em C#.
og_title: Como executar OCR e criar um PDF pesquisável em C#
tags:
- OCR
- C#
- Aspose
- PDF conversion
title: Como realizar OCR e criar um PDF pesquisável em C#
url: /pt/net/text-recognition/how-to-perform-ocr-and-create-a-searchable-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Realizar OCR e Criar um PDF Pesquisável em C#

Já precisou **perform OCR** em um documento escaneado mas não sabia como transformar o resultado em um searchable PDF? Você não está sozinho—muitos desenvolvedores encontram esse obstáculo ao lidar com arquivos TIFF legados ou PDFs apenas de imagem. A boa notícia? Com algumas linhas de C# e a biblioteca Aspose.OCR, você pode converter um TIFF ou qualquer imagem em um PDF totalmente pesquisável em questão de segundos.

Neste tutorial, vamos percorrer tudo o que você precisa saber: desde instalar a biblioteca, carregar um TIFF de várias páginas, até chamar `RecognizeToPdf` para que você possa **convert PDF using OCR** e **make searchable PDF** arquivos que seus usuários realmente possam pesquisar. Ao final, você terá um aplicativo console pronto‑para‑executar que produz um searchable PDF a partir de uma fonte de imagem.

## Pré-requisitos

- **.NET 6.0** ou superior (o código também funciona no .NET Framework 4.7+).
- Uma licença válida do **Aspose.OCR** ou uma chave de avaliação temporária (o teste gratuito é suficiente para testes).
- Visual Studio 2022 (ou qualquer editor de sua preferência) com o gerenciador de pacotes **NuGet**.
- Um arquivo de entrada chamado `input.tif` colocado em uma pasta que você controla—TIFFs de várias páginas funcionam imediatamente.

> **Dica profissional:** Se você estiver no Windows, copie o TIFF para a mesma pasta do `.exe` compilado para evitar dores de cabeça relacionadas a caminhos.

## Etapa 1: Instalar o Pacote NuGet Aspose.OCR

Abra a pasta do seu projeto em um terminal e execute:

```bash
dotnet add package Aspose.OCR
```

Isso obtém a versão estável mais recente (a partir de fevereiro 2026 é 23.10) e adiciona todas as dependências necessárias. Após a restauração terminar, você verá `Aspose.OCR` listado em **Dependencies** no Solution Explorer.

## Etapa 2: Criar um Aplicativo Console Minimalista

Crie um novo projeto console se ainda não tiver um:

```bash
dotnet new console -n OcrSearchablePdfDemo
cd OcrSearchablePdfDemo
```

Substitua o `Program.cs` gerado automaticamente pelo código completo mostrado na **Etapa 3**. O programa irá:

1. Instanciar o motor OCR.
2. Carregar a imagem de origem (ou TIFF de várias páginas).
3. Executar OCR e gravar a saída diretamente em um searchable PDF.
4. Notificar o usuário de que o processo foi bem‑sucedido.

## Etapa 3: Código Completo – De Imagem para Searchable PDF

Abaixo está o arquivo fonte **completo**. Copie‑e‑cole em `Program.cs`. Comentários foram incluídos para explicar as partes não óbvias.

```csharp
using System;
using Aspose.OCR;          // Core OCR namespace
using Aspose.OCR.Image;   // Provides ImageStream helpers

namespace OcrSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialise the OCR engine.
            // -------------------------------------------------
            // The Engine class is the entry point for all OCR operations.
            // You can optionally pass a license object here if you have one.
            var ocrEngine = new Engine();

            // -------------------------------------------------
            // 2️⃣ Load the source image.
            // -------------------------------------------------
            // ImageStream.FromFile supports TIFF, PDF, JPEG, PNG, etc.
            // For multi‑page TIFFs the stream automatically contains all pages.
            string inputPath = "YOUR_DIRECTORY/input.tif";
            var imageStream = ImageStream.FromFile(inputPath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR and write a searchable PDF.
            // -------------------------------------------------
            // RecognizeToPdf does the heavy lifting:
            // • It runs the OCR engine on every page.
            // • It embeds the extracted text as an invisible layer.
            // • The visual appearance of the original image is preserved.
            string outputPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.RecognizeToPdf(imageStream, outputPath);

            // -------------------------------------------------
            // 4️⃣ Inform the user.
            // -------------------------------------------------
            Console.WriteLine("Searchable PDF created at: " + outputPath);
        }
    }
}
```

**O que você verá:** Após executar o programa, um arquivo chamado `searchable.pdf` aparece na pasta de destino. Abra-o no Adobe Reader ou em qualquer visualizador de PDF e tente buscar uma palavra que exista no TIFF original. O texto deve ser encontrado instantaneamente, provando que você **made searchable PDF** com sucesso a partir de uma imagem.

### Executando o Aplicativo

```bash
dotnet run
```

Se tudo estiver configurado corretamente, você receberá:

```
Searchable PDF created at: YOUR_DIRECTORY/searchable.pdf
```

Abra o PDF, pressione `Ctrl+F`, digite uma palavra da fonte e veja o destaque pular para a localização correta.

## Etapa 4: Variações Comuns e Casos de Borda

### Convertendo um PDF Normal (apenas‑imagem) para Searchable PDF

Se sua fonte for um PDF que contém imagens escaneadas em vez de texto, você ainda pode usar o mesmo método—basta mudar a fonte do `ImageStream`:

```csharp
var pdfStream = ImageStream.FromFile("YOUR_DIRECTORY/input.pdf");
ocrEngine.RecognizeToPdf(pdfStream, "YOUR_DIRECTORY/searchable_from_pdf.pdf");
```

Isso satisfaz o cenário **convert pdf using OCR** sem nenhum código extra.

### Manipulando Documentos Grandes de Múltiplas Páginas

Para documentos que excedem algumas centenas de páginas, considere:

- **Aumentar limites de memória** (`Engine.MemoryLimit = 2_000; // MB`).
- **Processamento em blocos**: carregue um subconjunto de páginas, escreva PDFs intermediários e depois mescle-os usando uma biblioteca PDF (ex., Aspose.PDF).

### Lidando com Idiomas Diferentes do Inglês

O Aspose.OCR suporta muitos idiomas nativamente. Defina o idioma antes do reconhecimento:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Se você precisar de **tiff to searchable pdf** em um script não‑latino, certifique‑se de que o pacote de idioma apropriado esteja instalado.

### E se o PDF de Saída estiver em Branco?

- Verifique se o arquivo de entrada não está corrompido.
- Garanta que o motor OCR tenha uma licença válida—o modo de avaliação pode impor limites de páginas.
- Verifique se a resolução da imagem é de pelo menos 300 dpi; resoluções menores podem causar reconhecimento ruim.

## Etapa 5: Verificando o Resultado Programaticamente (Opcional)

Às vezes você quer confirmar que o PDF realmente contém uma camada de texto. Você pode usar o Aspose.PDF para extrair texto:

```csharp
using Aspose.Pdf;

var pdfDoc = new Document("YOUR_DIRECTORY/searchable.pdf");
string extracted = pdfDoc.Pages[1].ExtractText();
Console.WriteLine("First page text snippet: " + extracted.Substring(0, 100));
```

Se `extracted` não estiver vazio, você **made searchable pdf** com sucesso.

## Conclusão

Cobrimos **how to perform OCR** em um TIFF (ou qualquer imagem) e de forma contínua **convert PDF using OCR** para criar um **searchable PDF** que se comporta como um documento nativo. As etapas principais são:

1. Instalar o Aspose.OCR.
2. Inicializar `Engine`.
3. Carregar a imagem via `ImageStream`.
4. Chamar `RecognizeToPdf`.

A partir daí você pode experimentar configurações de idioma, processamento em lote de grande volume, ou combinar a saída com outras tarefas de manipulação de PDF. O mesmo padrão funciona para **tiff to searchable pdf**, **searchable pdf from image**, e até PDFs escaneados.

Pronto para o próximo desafio? Tente incorporar OCR em uma API web para que os usuários possam enviar escaneamentos e receber PDFs pesquisáveis instantaneamente, ou explore OCR em notas manuscritas usando as configurações avançadas do `OcrEngine`. As possibilidades são infinitas—bom código!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}