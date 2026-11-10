---
category: general
date: 2026-02-09
description: extraia texto de imagens rapidamente com C# definindo paralelismo máximo
  para OCR em lote – aprenda a converter páginas escaneadas, lidar com OCR de múltiplas
  imagens e ler texto de PNGs de forma eficiente.
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: pt
og_description: Extrair texto de imagens em C# definindo paralelismo máximo. Este
  tutorial mostra como converter páginas escaneadas, executar OCR em múltiplas imagens
  e ler texto de PNG com Aspose OCR.
og_title: Extrair texto de imagens PNG com C# – Guia completo de OCR em lote
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: Extrair texto de imagens PNG com C# – OCR em lote usando Aspose OCR
url: /pt/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# extrair imagens de texto de PNGs com C# – OCR em lote usando Aspose OCR

Já precisou **extrair imagens de texto** de uma pasta de PNGs escaneados, mas ficou preso na pergunta “como faço isso rápido?”? Você não está sozinho. Em muitos projetos reais, os desenvolvedores precisam **definir o paralelismo máximo** para que dezenas de páginas sejam processadas em segundos em vez de minutos.  

Neste guia, percorreremos um exemplo completo e executável que **converte páginas escaneadas**, executa **OCR em múltiplas imagens**, e finalmente **lê texto de PNG** sem esforço. Sem links vagos de “veja a documentação” — apenas código que você pode copiar‑colar, explicações do porquê cada linha importa e dicas para evitar armadilhas comuns.

> **Dica profissional:** Se você já usa Aspose OCR em outro lugar, notará que a mesma classe `OcrEngine` aparece aqui, mas ajustaremos sua configuração para processamento paralelo verdadeiro.

---

## O que você precisará

- **.NET 6+** (ou .NET Framework 4.6+). A API funciona da mesma forma, mas runtimes mais recentes oferecem melhor gerenciamento de threads.  
- **Aspose.OCR for .NET** – instale via NuGet: `Install-Package Aspose.OCR`.  
- Uma pasta que contém alguns scans PNG (`page1.png`, `page2.png`, …).  
- Uma IDE ou editor com o qual você se sinta confortável (Visual Studio, Rider, VS Code…).

É isso. Sem serviços extras, sem chaves de nuvem, apenas processamento local puro.

---

## extrair imagens de texto – Definindo o Paralelismo Máximo para OCR em Lote

Quando você dispara OCR em vários arquivos, o motor, por padrão, usa um único thread. Isso é seguro, mas extremamente lento. Ao configurar `MaxDegreeOfParallelism`, você informa ao motor quantos threads ele pode iniciar simultaneamente.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**Por que 4?**  
Quatro é um ponto ideal na maioria dos laptops modernos — núcleos suficientes para manter a CPU ocupada, mas não tantos a ponto de privar outros processos. Se você executar isso em um servidor com 16 núcleos, aumente o número para 12 ou 14 para obter um ganho de velocidade perceptível.

---

## Converter páginas escaneadas – Construindo a Coleção de ImageStream

Aspose espera cada imagem como um `ImageStream`. O helper `FromFile` lê o arquivo, mantém‑o na memória e o entrega ao motor OCR. Você também pode fornecer um `MemoryStream` se suas imagens vierem de um banco de dados ou de uma resposta HTTP.

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**Caso de borda:** Se algum arquivo estiver ausente ou corrompido, `FromFile` lançará uma `FileNotFoundException`. Envolva a construção em um `try/catch` se você esperar entradas não confiáveis.

---

## OCR em múltiplas imagens – Executando OCR em Lote

Agora o trabalho pesado acontece. `RecognizeBatch` cria até o número de threads que você definiu anteriormente, processa cada imagem e retorna uma lista de objetos `OcrResult`.

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

Nos bastidores, cada thread carrega sua imagem, executa a rede neural e extrai o texto puro. A ordem dos resultados corresponde à ordem da lista de entrada, de modo que você pode mapear com segurança página 1 → resultado 0, e assim por diante.

---

## ler texto PNG – Exibindo o Conteúdo Extraído

Finalmente, iteramos pelos resultados e imprimimos o texto puro no console. É aqui que você pode direcionar a saída para um arquivo, um banco de dados ou até mesmo um serviço de NLP downstream.

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### Saída esperada no console

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

Se você vir seções em branco, verifique se os PNGs não são imagens totalmente brancas — OCR precisa de algum contraste.

---

## Dicas práticas e armadilhas comuns

| Situação | O que fazer |
|-----------|------------|
| **Pressão de memória** em lotes grandes | Processar imagens em blocos de 10‑20 arquivos, então chamar `GC.Collect()` se notar picos. |
| **Detecção de idioma incorreta** | Defina `ocrEngine.Configuration.Language = OcrLanguage.English;` (ou o idioma desejado) antes de chamar `RecognizeBatch`. |
| **Desempenho lento apesar do paralelismo** | Verifique se seu SSD não está limitando I/O; leia todos os arquivos para a memória primeiro (como fazemos com `ImageStream.FromFile`). |
| **Caracteres ausentes** | Aumente `ocrEngine.Configuration.DPI = 300;` para processamento em alta resolução. |

---

## Expandindo o exemplo – De PNG para PDF ou DOCX

Se eventualmente precisar **converter páginas escaneadas** em PDFs pesquisáveis, basta alimentar o mesmo `ocrResults[i].PlainText` em uma biblioteca PDF (por exemplo, Aspose.PDF) e sobrepor o texto como uma camada invisível. O mesmo truque de paralelismo funciona lá também.

---

## Código-fonte completo (pronto para copiar‑colar)

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

Salve isso como `BatchExample.cs`, execute `dotnet run` e veja seu console se encher com o texto que antes estava oculto dentro desses scans PNG.

---

## Resumo visual

![extract text images example](images/ocr-batch.png){alt="exemplo de extração de imagens de texto"}

O diagrama mostra o fluxo: **Arquivos PNG → coleção ImageStream → OcrEngine (paralelismo máximo) → resultados OCR → Console / armazenamento downstream**.

---

## Conclusão

Agora você tem uma receita sólida, de ponta a ponta, de como **extrair imagens de texto** em C# enquanto **define o paralelismo máximo**, **converte páginas escaneadas**, lida com **OCR em múltiplas imagens**, e **lê texto PNG** de forma eficiente. O código é autônomo, as explicações cobrem tanto o “como” quanto o “por quê”, e as dicas evitam dores de cabeça comuns.

O que vem a seguir? Experimente substituir a lista de PNGs por um loop dinâmico `Directory.GetFiles`, experimente diferentes contagens de threads, ou alimente a saída em um PDF pesquisável. O mesmo padrão escala para centenas de páginas com quase nenhuma linha de código extra.

Têm perguntas ou um caso de borda complicado? Deixe um comentário abaixo, e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}