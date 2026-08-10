---
category: general
date: 2026-04-04
description: Aprenda como extrair texto de arquivos TIFF usando um exemplo de motor
  OCR em C#. Guia passo a passo com saída JSON e XML.
draft: false
keywords:
- extract text from tiff
- ocr engine example
- Aspose OCR C#
- multi‑page TIFF OCR
- JSON OCR result
language: pt
og_description: Extrair texto de arquivos TIFF usando um motor OCR – exemplo em C#.
  Passos detalhados, código completo e dicas para saída JSON/XML.
og_title: Extrair Texto de TIFF com o Motor OCR da Aspose – Guia Completo
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Extrair texto de TIFF com o motor OCR da Aspose – Exemplo completo
url: /pt/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-engine-complete-examp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de TIFF – Exemplo Completo de Motor OCR em C#

Já precisou **extrair texto de TIFF** imagens mas não tinha certeza de qual biblioteca poderia lidar com arquivos de várias páginas sem uma série de soluções alternativas? Você não está sozinho. Em muitos sistemas legados, documentos chegam como digitalizações TIFF de múltiplas páginas, e extrair o texto bruto é um recurso indispensável para busca, conformidade ou automação de entrada de dados.

A boa notícia? Com Aspose OCR você pode fazer isso em poucas linhas—sem mexer com buffers de pixels de baixo nível. Este tutorial guia você por um **exemplo completo de motor OCR** que carrega um TIFF de várias páginas, reconhece cada página e gera JSON formatado e XML opcional. Ao final, você terá um aplicativo console C# pronto para executar que extrai texto de arquivos TIFF em segundos.

## O que você aprenderá

- Como configurar o motor Aspose OCR em um projeto .NET.  
- O código exato necessário para **extrair texto de TIFF** arquivos, incluindo o tratamento de múltiplas páginas.  
- Por que você pode preferir saída JSON em vez de XML e como gerar ambos.  
- Dicas para solucionar problemas comuns (ex.: DPI da imagem, uso de memória).  

### Pré-requisitos

- .NET 6.0 SDK ou posterior (o código funciona com .NET Core e .NET Framework).  
- Uma licença válida do Aspose OCR (ou uma chave de avaliação gratuita).  
- Visual Studio 2022 ou qualquer editor C# de sua preferência.  
- Um arquivo TIFF de múltiplas páginas de exemplo (nomeado `multi-page.tiff` no exemplo).  

> **Dica profissional:** Se você tem um orçamento apertado, a avaliação gratuita ainda permite extrair texto de até 100 páginas por mês—perfeito para testes.

---

## Etapa 1 – Inicializar o Motor OCR (exemplo de motor OCR)

Antes de podermos **extrair texto de TIFF**, precisamos de uma instância do motor OCR. Este objeto contém todas as configurações que você pode ajustar posteriormente (idioma, resolução, etc.).

```csharp
using Aspose.OCR;
using System.IO;

// Create a new OCR engine – this is the core of our ocr engine example
var ocrEngine = new OcrEngine();

// Optional: set language if you know the document’s language
// ocrEngine.Language = Language.English;
```

*Por que isso importa:* A classe `OcrEngine` abstrai o trabalho pesado. Instanciá‑la uma vez e reutilizá‑la para várias imagens é mais eficiente em memória do que criar um novo motor por página.

---

## Etapa 2 – Carregar o TIFF de Múltiplas Páginas (extrair texto de TIFF)

Agora apontamos o motor para o nosso arquivo de origem. `ImageStream.FromFile` suporta TIFF, JPEG, PNG e muitos outros, mas neste tutorial focamos em TIFF.

```csharp
// Load the multi‑page TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi-page.tiff");
```

> **Nota:** Substitua `YOUR_DIRECTORY` pelo caminho real da pasta em sua máquina.  
> **Dica:** Se o seu TIFF tem DPI baixo (abaixo de 150), considere pré‑processá‑lo para melhorar a precisão do OCR.

---

## Etapa 3 – Reconhecer Todas as Páginas

Chamar `Recognize()` executa o algoritmo OCR em **todas as páginas** do TIFF. O objeto de resultado contém o texto bruto, pontuações de confiança e segmentação por página.

```csharp
// Run OCR on the loaded image – this extracts text from all pages
var ocrResult = ocrEngine.Recognize();
```

*O que você recebe:* `ocrResult` contém uma coleção de objetos `PageResult`. O texto de cada página pode ser acessado via `ocrResult.Pages[i].Text`. O motor também fornece níveis de confiança, que podem ser úteis para verificações de qualidade.

---

## Etapa 4 – Salvar Resultados como JSON (e XML opcional)

A maioria dos pipelines modernos prefere JSON, mas sistemas legados ainda utilizam XML. Aqui está como gerar ambos, formatados de forma agradável.

```csharp
// Convert the recognition result to pretty‑printed JSON
string jsonResult = ocrResult.ToJson(prettyPrint: true);
File.WriteAllText(@"YOUR_DIRECTORY/result.json", jsonResult);

// Optional: also output XML for older workflows
string xmlResult = ocrResult.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY/result.xml", xmlResult);
```

### Exemplo de Saída JSON (truncado)

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
      "Confidence": 0.97
    },
    {
      "PageNumber": 2,
      "Text": "Itemized List\n1. Widget A – $500.00\n2. Widget B – $750.00",
      "Confidence": 0.95
    }
  ]
}
```

O JSON é legível por humanos, facilitando a depuração. O XML espelha a mesma estrutura caso você precise.

---

## Etapa 5 – Verificar a Extração (extrair texto de TIFF)

Depois que os arquivos são gravados, uma verificação rápida ajuda a garantir que nada deu errado.

```csharp
// Load the JSON back just to confirm it was saved correctly
string loadedJson = File.ReadAllText(@"YOUR_DIRECTORY/result.json");
Console.WriteLine("First 200 characters of JSON output:");
Console.WriteLine(loadedJson.Substring(0, Math.Min(200, loadedJson.Length)));
```

Se você vir o trecho impresso, você extraiu com sucesso **texto de TIFF** e o persistiu. A partir daqui, você pode enviar o JSON para um índice de busca, um banco de dados ou qualquer serviço downstream.

---

## Por que usar Aspose OCR para extrair texto de TIFF?

- **Suporte a múltiplas páginas pronto para uso** – sem necessidade de dividir o TIFF manualmente.  
- **Alta precisão** graças a modelos proprietários de redes neurais.  
- **Multiplataforma** – funciona em runtimes .NET Windows, Linux e macOS.  
- **Formatos de saída ricos** (JSON, XML, texto simples) que atendem tanto a stacks modernos quanto legados.  

Se ainda estiver em dúvida, experimente a avaliação gratuita em um documento de exemplo. Você notará a velocidade e simplicidade em comparação com alternativas de código aberto que frequentemente exigem pré‑processamento extra da imagem.

---

## Armadilhas Comuns & Como Evitá‑las

| Problema | Sintoma | Solução |
|----------|---------|---------|
| TIFF de baixa resolução | Caracteres ausentes, baixa confiança | Aumente a imagem para ≥150 DPI antes do OCR (`ocrEngine.Image = ImageStream.FromFile(...).Resize(150)` ) |
| Idioma errado | Palavras embaralhadas, especialmente para texto não‑inglês | Defina `ocrEngine.Language = Language.Spanish` (ou o apropriado) antes de `Recognize()` |
| Falta de memória em arquivos grandes | `OutOfMemoryException` | Processar páginas em lotes: percorrer `ocrEngine.Image.Pages` e chamar `RecognizePage(i)` |
| Licença não aplicada | Marca d'água “Evaluation” na saída | Registre sua licença: `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

Abaixo está o programa completo que você pode inserir em um novo projeto console. Ele inclui todas as partes que discutimos—inicialização, carregamento, reconhecimento e salvamento.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine (ocr engine example)
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // Optional: set license if you have one
            // var license = new License();
            // license.SetLicense("Aspose.OCR.lic");

            // -------------------------------------------------
            // 2️⃣  Load the multi‑page TIFF (extract text from TIFF)
            // -------------------------------------------------
            string tiffPath = @"YOUR_DIRECTORY/multi-page.tiff";
            if (!File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -------------------------------------------------
            // 3️⃣  Recognize every page
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 4️⃣  Save JSON (pretty) and optional XML
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/result.json";
            string jsonResult = ocrResult.ToJson(prettyPrint: true);
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"JSON saved to {jsonPath}");

            // Optional XML output
            string xmlPath = @"YOUR_DIRECTORY/result.xml";
            string xmlResult = ocrResult.ToXml();
            File.WriteAllText(xmlPath, xmlResult);
            Console.WriteLine($"XML saved to {xmlPath}");

            // -------------------------------------------------
            // 5️⃣  Quick verification (extract text from TIFF)
            // -------------------------------------------------
            string preview = jsonResult.Length > 200 ? jsonResult.Substring(0, 200) + "..." : jsonResult;
            Console.WriteLine("\nPreview of JSON output:");
            Console.WriteLine(preview);
        }
    }
}
```

Salve o arquivo como `Program.cs`, execute `dotnet run` e observe o console informar onde o JSON e o XML foram salvos. É isso—você acabou de concluir um **exemplo de motor OCR** que extrai texto de TIFF.

---

## Próximos Passos & Tópicos Relacionados

- **Processamento em lote:** Envolva a lógica acima em um loop `foreach` para lidar automaticamente com dezenas de arquivos TIFF.  
- **Integração de busca:** Envie o JSON para Elasticsearch ou Azure Cognitive Search para habilitar busca full‑text em documentos digitalizados.  
- **Pré‑processamento de imagem:** Explore a API `ImageProcessing` da Aspose para corrigir inclinação, remover ruído ou ajustar contraste antes do OCR.  
- **Saída alternativa:** Use `ocrResult.ToPlainText()` se você precisar apenas de strings brutas sem metadados.  

Se você tem curiosidade sobre outros formatos de imagem, o mesmo padrão funciona para PDFs (basta mudar o arquivo de origem) ou PNGs. O ponto principal é que, uma vez que o motor está configurado, o resto é um pipeline repetível.

## Conclusão

Percorremos um **exemplo completo de motor OCR** que permite **extrair texto de arquivos TIFF** com Aspose OCR, gerando JSON limpo e XML opcional para qualquer fluxo de trabalho downstream. O código é autocontido, as explicações cobrem o “por quê” de cada etapa

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}