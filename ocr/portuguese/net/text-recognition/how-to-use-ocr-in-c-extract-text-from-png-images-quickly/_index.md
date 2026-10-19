---
category: general
date: 2026-03-29
description: Como usar OCR com Aspose para extrair texto de arquivos PNG e converter
  imagens em texto. Aprenda OCR assíncrono passo a passo em C#.
draft: false
keywords:
- how to use OCR
- extract text from png
- convert images to text
- extract text from images
language: pt
og_description: Como usar OCR com Aspose em C# para extrair texto de arquivos PNG.
  Este guia orienta você sobre OCR assíncrono, código e dicas.
og_title: Como usar OCR em C# – Extrair texto de imagens PNG
tags:
- OCR
- C#
- Aspose
title: Como usar OCR em C# – Extraia texto de imagens PNG rapidamente
url: /pt/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-png-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Usar OCR em C# – Extrair Texto de Imagens PNG Rapidamente

Já se perguntou **como usar OCR** para extrair texto de alguns screenshots PNG? Talvez você tenha recibos escaneados, faturas ou maquetes de UI e precise desse texto em um formato pesquisável. A boa notícia? Com Aspose.OCR você pode converter imagens em texto em apenas algumas linhas de código C# assíncrono.  

Neste tutorial vamos mostrar exatamente como extrair texto de arquivos PNG, explicar por que cada passo importa e fornecer um programa pronto‑para‑executar que imprime o texto reconhecido para cada página. Ao final, você será capaz de **extrair texto de imagens** sem precisar vasculhar a documentação.

## O que Você Vai Aprender

- Instalar e referenciar o pacote NuGet Aspose.OCR.  
- Inicializar o motor OCR e definir o idioma (Inglês neste exemplo).  
- Passar um array de arquivos PNG para `RecognizeImagesAsync` para processamento rápido e não‑bloqueante.  
- Iterar sobre os objetos `OcrResult` e exibir as strings extraídas.  

Sem serviços externos, sem callbacks complicados — apenas C# assíncrono limpo que funciona em .NET 6+.

---

## Pré-requisitos

| Requisito | Motivo |
|-------------|--------|
| .NET 6 SDK (ou posterior) | Recursos modernos da linguagem como `async Main`. |
| Visual Studio 2022 ou VS Code | IDE para compilar e executar o código. |
| Pacote NuGet Aspose.OCR (`Aspose.OCR`) | Fornece a classe `OcrEngine` usada no exemplo. |
| Algumas imagens PNG (`page1.png`, `page2.png`, …) | Arquivos de entrada para o processo de OCR. |

Se você já tem um projeto .NET, basta executar `dotnet add package Aspose.OCR`. Caso contrário, crie um novo aplicativo console com `dotnet new console -n OcrDemo`.

---

## Etapa 1: Instalar Aspose.OCR e Configurar o Projeto

Primeiro, adicione a biblioteca OCR ao seu projeto:

```bash
dotnet add package Aspose.OCR
```

Por que isso importa: Aspose.OCR inclui o motor OCR nativo, pacotes de idioma e uma API simples. Ao obtê‑lo via NuGet você garante compatibilidade de versão e atualizações automáticas.

---

## Etapa 2: Inicializar o Motor OCR e Escolher um Idioma

O motor precisa saber qual idioma procurar. O inglês é o mais comum, mas você pode trocar por `Language.Spanish`, `Language.French`, etc.

```csharp
using Aspose.OCR;

// ...

// Step 2: Create the engine and set the language to English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // Change this if you need a different language
};
```

> **Dica profissional:** Sempre defina o idioma explicitamente; deixá‑lo no padrão pode reduzir a precisão e aumentar o tempo de processamento.

---

## Etapa 3: Preparar a Lista de Arquivos PNG

Você pode fornecer um único arquivo ou um array. Fornecer um array permite que o motor processe em lote de forma assíncrona, o que é ideal para algumas páginas.

```csharp
// Step 3: Define the image files you want to process
string[] imagePaths = { "page1.png", "page2.png", "page3.png" };
```

Se suas imagens estiverem em uma subpasta, basta prefixar o caminho relativo (`"images/page1.png"`). O motor lançará um `FileNotFoundException` claro se um caminho estiver errado — então verifique os nomes dos arquivos.

---

## Etapa 4: Executar OCR Assíncrono em Todas as Imagens

O método `RecognizeImagesAsync` retorna um array de `OcrResult`. Como é async, sua UI (ou console) permanece responsiva enquanto o OCR roda em segundo plano.

```csharp
// Step 4: Perform async OCR on every image
OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);
```

**Por que async?**  
Se você está integrando OCR em uma API web ou em um aplicativo desktop, não quer que a thread bloqueie enquanto o motor escaneia cada pixel. `await` devolve a thread ao pool, melhorando a escalabilidade.

---

## Etapa 5: Exibir o Texto Extraído para Cada Página

Agora que temos os resultados, itere sobre eles e imprima o texto reconhecido. A propriedade `Text` contém a saída em texto puro, pronta para processamento adicional (por exemplo, salvar em um banco de dados).

```csharp
// Step 5: Output the recognized text for every page
for (int i = 0; i < ocrResults.Length; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

### Saída Esperada

Assumindo que `page1.png` contenha “Invoice #12345” e `page2.png` tenha “Total: $89.99”, você verá algo como:

```
--- Page 1 ---
Invoice #12345
Date: 03/28/2026
--- Page 2 ---
Total: $89.99
Paid by: Credit Card
```

Se o OCR não localizar nenhum texto, a propriedade `Text` será uma string vazia — trate esse caso no código de produção verificando `string.IsNullOrWhiteSpace`.

---

## Exemplo Completo Funcional

Abaixo está o programa completo que você pode copiar‑colar em `Program.cs`. Ele inclui todas as diretivas `using`, o `Main` assíncrono e comentários que esclarecem cada passo.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    // Async Main is supported from C# 7.1 onward
    static async Task Main()
    {
        // Step 1: Initialize the OCR engine and set the language to English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Step 2: Define the image files to be processed
        string[] imagePaths = { "page1.png", "page2.png", "page3.png" };

        // Step 3: Perform asynchronous OCR on all images
        OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);

        // Step 4: Output the recognized text for each page
        for (int i = 0; i < ocrResults.Length; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].Text);
        }
    }
}
```

Salve o arquivo, coloque seus PNGs ao lado do executável (ou ajuste os caminhos) e execute:

```bash
dotnet run
```

Você deverá ver o texto extraído impresso no console, confirmando que você converteu imagens em texto com sucesso.

---

## Lidando com Casos de Borda Comuns

| Situação | O que Fazer |
|-----------|------------|
| **PNG de baixa resolução** | Aumente `ocrEngine.ImageProcessingOptions.Dpi` antes do reconhecimento. |
| **Múltiplos idiomas** | Defina `ocrEngine.Language = Language.English | Language.Spanish;` (OR bit a bit). |
| **Grande lote (centenas de arquivos)** | Processar em blocos (por exemplo, 20 arquivos por chamada `RecognizeImagesAsync`) para evitar picos de memória. |
| **Precisa da pontuação de confiança** | Use `ocrResults[i].Confidence` (um float entre 0 e 1) para filtrar resultados de baixa qualidade. |

Esses ajustes mantêm seu pipeline OCR robusto, especialmente quando você passa de uma demonstração para produção.

---

## Bônus: Salvando os Resultados em um Arquivo de Texto

Se preferir uma cópia persistente em vez da saída no console, adicione um pequeno helper:

```csharp
using System.IO;

// After the for‑loop:
File.WriteAllLines("OcrOutput.txt", ocrResults.Select(r => r.Text));
Console.WriteLine("All pages saved to OcrOutput.txt");
```

Agora você tem um único arquivo que **extrai texto de imagens** para processamento posterior — perfeito para indexação, busca ou alimentação a um modelo de linguagem.

---

## Conclusão

Percorremos **como usar OCR** em C# com Aspose para **extrair texto de PNG** e **converter imagens em texto** de forma eficiente. A abordagem async garante que sua aplicação permaneça responsiva, enquanto a API direta mantém o código legível e fácil de manter.  

Experimente com seus próprios documentos, teste diferentes idiomas e, quem sabe, encadeie a saída em um índice de busca ou serviço de sumarização. O céu é o limite quando você pode transformar imagens em strings pesquisáveis de forma confiável.

---

### Próximos Passos & Tópicos Relacionados

- **Extrair texto de imagens** em outros formatos (JPEG, TIFF) – basta mudar as extensões dos arquivos.  
- **Processamento em lote com Parallel.ForEach** para cargas de trabalho massivas.  
- **Limpeza pós‑OCR** usando expressões regulares para normalizar datas, valores ou IDs.  
- **Integrar com Azure Cognitive Services** se precisar de OCR baseado em nuvem com recursos adicionais.  

Sinta-se à vontade para deixar um comentário se encontrar algum problema, ou compartilhar como você estendeu este fluxo básico. Feliz codificação!   (Image: ![Captura de tela do resultado OCR mostrando texto extraído](/images/ocr-result.png){.align-center alt="exemplo de saída de como usar OCR"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}