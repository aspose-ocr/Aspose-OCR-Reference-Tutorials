---
category: general
date: 2026-02-22
description: Gere PDF pesquisável e extraia texto de imagem usando o Aspose OCR. Aprenda
  como converter imagem em PDF e gerar texto simples em um único tutorial.
draft: false
keywords:
- generate searchable pdf
- extract text from image
- convert image to pdf
- output plain text
- convert scanned image pdf
language: pt
og_description: Gere PDF pesquisável a partir de imagens digitalizadas com o Aspose
  OCR. Este guia mostra como extrair texto da imagem, gerar texto simples e converter
  a imagem em PDF.
og_title: Gerar PDF pesquisável a partir de imagens – Tutorial completo de C#
tags:
- C#
- OCR
- PDF generation
- Aspose
title: Gerar PDF pesquisável a partir de imagens em C# – Guia passo a passo
url: /pt/net/text-recognition/generate-searchable-pdf-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gerar PDF pesquisável a partir de imagens em C# – Tutorial completo

Já precisou **gerar PDF pesquisável** a partir de uma foto escaneada, mas não sabia por onde começar? Você não está sozinho—a maioria dos desenvolvedores encontra essa barreira ao se deparar com OCR. A boa notícia? Com Aspose OCR você pode **extrair texto de imagem**, **gerar texto simples**, e **converter imagem em PDF** em apenas algumas linhas de C#.

Neste guia, percorreremos todo o processo, desde o carregamento de um arquivo PNG até a gravação de um PDF pesquisável e de um arquivo de texto simples. Ao final, você terá um trecho reutilizável que pode inserir em qualquer projeto .NET. Sem enrolação, apenas o que realmente funciona.

## O que você aprenderá

- Como configurar **Aspose.OCR** em um aplicativo console .NET.  
- A diferença entre os modos **output plain text** e **searchable PDF**.  
- Como **extract text from image** e gravar em um arquivo `.txt`.  
- Como **convert image to PDF** que mantém o bitmap original enquanto adiciona uma camada de texto oculto.  
- Dicas para lidar com lotes grandes, armadilhas comuns e onde ajustar as configurações para melhor precisão.

> **Pré-requisitos** – Você precisa de .NET 6+ (ou .NET Framework 4.7+), Visual Studio 2022 (ou qualquer editor), e uma licença Aspose OCR (ou um teste gratuito). Nenhuma outra biblioteca de terceiros é necessária.

![exemplo de PDF pesquisável gerado](image-placeholder.png "Exemplo de um PDF pesquisável gerado")

## Etapa 1: Instalar Aspose OCR e criar o Engine

Primeiro de tudo—adicione o pacote NuGet ao seu projeto:

```bash
dotnet add package Aspose.OCR
```

Agora podemos iniciar o OCR engine e informar qual idioma estamos usando. O inglês é o padrão, mas você pode mudar para francês, espanhol, etc., alterando o enum `Language`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine for English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };
```

**Por que isso importa:** O engine contém todas as configurações—idioma, formato de saída e flags opcionais de pré‑processamento. Defini‑lo uma vez e reutilizá‑lo evita a sobrecarga de criar uma nova instância para cada arquivo.

## Etapa 2: Extrair texto e salvar como texto simples

Se você só precisa dos caracteres brutos, altere o engine para `OutputFormat.Text`. Isso instrui o Aspose OCR a pular a geração de PDF completamente e devolver uma string.

```csharp
        // Tell the engine to return plain text
        ocrEngine.OutputFormat = OutputFormat.Text;

        // Path to your source image (PNG, JPEG, BMP, etc.)
        string inputImagePath = @"YOUR_DIRECTORY/input.png";

        // Perform recognition – the result contains the extracted string
        OcrResult plainTextResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Write the text to a .txt file
        string textOutputPath = @"YOUR_DIRECTORY/output.txt";
        File.WriteAllText(textOutputPath, plainTextResult.Text);
```

**Dica profissional:** `plainTextResult.Text` já remove quebras de linha que pertencem ao layout do OCR. Se precisar do espaçamento original, inspecione `plainTextResult.TextBlocks`.

### Resultado esperado

Abra `output.txt` e você deverá ver algo como:

```
Hello, world!
This is a sample scanned document.
```

Esta é a parte de **output plain text** do tutorial—rápida, leve e perfeita para processamento posterior (por exemplo, indexação).

## Etapa 3: Alternar para modo PDF pesquisável

Agora vamos criar um **PDF pesquisável**. O engine incorporará o bitmap original e sobreporá o texto gerado pelo OCR por baixo, tornando o documento pesquisável em qualquer visualizador de PDF.

```csharp
        // Change the output format to searchable PDF
        ocrEngine.OutputFormat = OutputFormat.SearchablePdf;

        // Recognize the same image again – this time we get PDF bytes
        OcrResult pdfResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Save the PDF bytes to a file
        string pdfOutputPath = @"YOUR_DIRECTORY/output.pdf";
        File.WriteAllBytes(pdfOutputPath, pdfResult.RawData);
    }
}
```

**Por que re‑reconhecemos:** O engine OCR mantém em cache a última imagem, mas o formato de saída determina quais dados ele devolve. Alterar o formato força uma nova passagem que inclui a camada de texto oculto.

### Como o PDF fica

Abra `output.pdf` no Adobe Reader ou em qualquer visualizador e tente selecionar texto. Você verá que pode copiar, buscar e destacar o conteúdo—mesmo que a aparência visual ainda seja o bitmap original. Esse é o marco de um **convert scanned image pdf**.

## Etapa 4: Manipular múltiplos arquivos (Opcional)

Projetos do mundo real raramente lidam com uma única imagem. Abaixo há um loop rápido que processa todos os PNGs em uma pasta, produzindo arquivos `.txt` e `.pdf` correspondentes.

```csharp
        string folder = @"YOUR_DIRECTORY";
        foreach (var file in Directory.GetFiles(folder, "*.png"))
        {
            // Plain‑text extraction
            ocrEngine.OutputFormat = OutputFormat.Text;
            var txtResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllText(Path.ChangeExtension(file, ".txt"), txtResult.Text);

            // Searchable PDF generation
            ocrEngine.OutputFormat = OutputFormat.SearchablePdf;
            var pdfResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllBytes(Path.ChangeExtension(file, ".pdf"), pdfResult.RawData);
        }
```

**Nota de caso extremo:** Imagens grandes podem esgotar a memória. Se você encontrar `OutOfMemoryException`, considere reduzir a escala com `Image.Resize` antes do reconhecimento, ou processe arquivos em lotes menores.

## Etapa 5: Ajuste fino da precisão do OCR

Aspose OCR oferece alguns ajustes que você pode modificar:

| Configuração | O que faz | Quando usar |
|--------------|-----------|-------------|
| `ocrEngine.PageSegmentationMode` | Controla como o engine divide a imagem em blocos de texto. | Útil para layouts de múltiplas colunas. |
| `ocrEngine.Deskew` | Rotaciona automaticamente páginas levemente inclinadas. | Documentos escaneados que não estão perfeitamente alinhados. |
| `ocrEngine.RemoveNoise` | Tenta limpar manchas e artefatos de fundo. | Scans de baixa qualidade ou páginas enviadas por fax. |

```csharp
ocrEngine.Deskew = true;
ocrEngine.RemoveNoise = true;
```

Habilitar essas opções pode aumentar o tempo de processamento, mas o ganho na qualidade de **extract text from image** costuma valer a pena.

## Etapa 6: Verificar a saída programaticamente

Às vezes você precisa garantir que o PDF realmente contém texto pesquisável (por exemplo, em testes automatizados). A verificação mais simples é confirmar que o array de bytes do PDF não está vazio e que o comprimento de `RawData` excede o tamanho da imagem.

```csharp
if (pdfResult.RawData.Length > Image.Load(inputImagePath).Data.Length)
{
    Console.WriteLine("Searchable PDF generated successfully!");
}
else
{
    Console.WriteLine("Warning: PDF may not contain hidden text.");
}
```

Para validações mais profundas, você poderia usar uma biblioteca PDF (como iTextSharp) para extrair o fluxo de texto e compará‑lo com `plainTextResult.Text`.

## Armadilhas comuns e como evitá‑las

- **Licença ausente** – Sem uma licença Aspose válida, a biblioteca roda em modo de avaliação, adicionando uma marca d'água aos PDFs. Registre sua licença cedo (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`).  
- **Caminho incorreto** – Codificar caminhos absolutos funciona na sua máquina, mas falha em outros ambientes. Use `Path.Combine` com `AppDomain.CurrentDomain.BaseDirectory` para portabilidade.  
- **Formatos de imagem não suportados** – GIFs e TIFFs com múltiplas páginas precisam de tratamento especial (`Image.LoadMultiPage`). Converta‑os para PNG/JPEG primeiro se precisar apenas da primeira página.  
- **Gargalos de desempenho** – Recriar `OcrEngine` dentro de um loop é custoso. Mantenha uma única instância e altere apenas `OutputFormat` conforme mostrado.

## Recapitulação

Cobrimos todo o fluxo de trabalho para **generate searchable PDF** a partir de uma imagem escaneada usando Aspose OCR:

1. Instale o pacote NuGet e crie um `OcrEngine`.  
2. Defina `OutputFormat.Text` para **output plain text** e grave em um arquivo `.txt`.  
3. Altere para `OutputFormat.SearchablePdf` para **convert image to PDF** com uma camada de texto invisível.  
4. Salve os bytes do PDF e, opcionalmente, faça um loop sobre um diretório para processamento em lote.  
5. Ajuste a precisão com opções de deskew, remoção de ruído e segmentação de página.  

Tudo isso cabe em um programa compacto e autocontido que você pode copiar‑colar no Visual Studio.

## O que tentar a seguir?

- **Processamento em lote** com uma interface UI (WinForms ou WPF) para que os usuários possam arrastar e soltar arquivos.  
- **Detecção de idioma** – Aspose OCR pode detectar automaticamente o idioma; experimente `ocrEngine.Language = Language.AutoDetect`.  
- **Pós‑processamento** – Alimente o texto extraído em um índice de busca (ElasticSearch, Azure Cognitive Search) para recuperação instantânea de documentos.  
- **Saídas alternativas** – Use `OutputFormat.Hocr` para resultados OCR baseados em HTML, útil para pré‑visualizações web.  

Sinta‑se à vontade para experimentar diferentes resoluções de imagem, modos de cor e configurações de OCR. Quanto mais você brincar, melhor entenderá as compensações entre velocidade e precisão.

---

**Feliz codificação!** Se você encontrar algum problema, deixe um comentário abaixo ou consulte a documentação do Aspose OCR para aprofundamentos. Seu próximo projeto—seja faturamento, arquivamento ou construção de uma base de conhecimento pesquisável—acabou de ficar muito mais fácil.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}