---
category: general
date: 2026-03-17
description: Como fazer OCR em lote de imagens PNG em C# rapidamente. Aprenda a extrair
  texto de arquivos PNG, converter PNG para texto e ler imagens de um diretório com
  um script simples.
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: pt
og_description: Como fazer OCR em lote de imagens PNG em C# com código passo a passo.
  Extraia texto de arquivos PNG, converta PNG para texto e leia imagens de um diretório
  sem esforço.
og_title: Como fazer OCR em lote de imagens PNG em C# – Guia completo
tags:
- OCR
- C#
- Image Processing
title: Como fazer OCR em lote de imagens PNG em C# – Guia completo
url: /pt/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

top-button >}}

We must keep them unchanged.

Now ensure we didn't miss any markdown elements: code blocks placeholders remain. No actual code blocks to translate.

Check for any other markdown like blockquote > lines we translated.

Make sure we keep the same number of headings.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Processar OCR em Lote de Imagens PNG em C# – Guia Completo

Já se perguntou **como fazer OCR em lote** em uma pasta cheia de capturas de tela sem abrir cada arquivo manualmente? Você não está sozinho—desenvolvedores perguntam constantemente como fazer OCR em lote de grandes coleções de PNGs, especialmente quando o objetivo é extrair texto de arquivos PNG para análise posterior.  

Neste tutorial vamos percorrer um exemplo pronto‑para‑executar em C# que **extrai texto PNG** de arquivos, **converte PNG para texto**, e mostra a melhor forma de **ler imagens de um diretório**. Ao final você terá um único script que gera um `.txt` ao lado de cada imagem, economizando horas de cópia‑e‑cola manual.

## O que Você Vai Conquistar

- Inicializar um motor OCR uma única vez e reutilizá‑lo para todo o lote.  
- Escanear cada `*.png` em uma pasta especificada sem escrever um loop você mesmo.  
- Gravar cada resultado de OCR em seu próprio arquivo de texto, preservando o nome original do arquivo.  
- Lidar com casos de borda comuns, como pastas vazias ou arquivos que não são imagens, de forma elegante.

### Pré‑requisitos

- .NET 6.0 ou superior (o código funciona também em .NET Core e .NET Framework).  
- Uma biblioteca OCR que exponha os tipos `OcrEngine`, `ImageStream` e `OcrResult` (por exemplo, o fictício SDK **FastOCR** usado nos trechos).  
- Conhecimento básico de C#—nenhum padrão avançado é necessário.

---

## Como Processar OCR em Lote de Imagens PNG – Visão Geral

Abaixo está o **programa completo e executável**. Sinta‑se à vontade para copiar‑colar em um novo projeto de console, substituir os caminhos de placeholder e pressionar **F5**.

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **Saída esperada:** Para cada `image01.png` você encontrará um `image01.txt` contendo os caracteres reconhecidos. O console listará cada arquivo conforme for gravado.

![Como processar OCR em lote diagrama](how-to-batch-ocr-diagram.png "Diagrama ilustrando como processar OCR em lote de imagens PNG usando C#")

---

## Explicação Passo a Passo

### 1. Inicializar o Motor OCR – o Coração do Processo  

A linha `var ocrEngine = new OcrEngine();` cria uma única instância do motor que será reutilizada para todo o lote. Reutilizar o motor é **crucial** porque a maioria das bibliotecas OCR aloca recursos pesados (como modelos de linguagem) na construção. Inicializar uma única vez melhora o desempenho drasticamente—especialmente quando você tem dezenas ou centenas de PNGs.

> **Dica profissional:** Se precisar de um idioma diferente do inglês, defina `ocrEngine.Config.Language = Language.Spanish;` (ou qualquer enum suportado).  

### 2. Ler Imagens do Diretório – localizando cada PNG  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` faz exatamente o que a palavra‑chave secundária *read images from directory* promete. Ele retorna um array de caminhos absolutos, que mais tarde alimentamos ao motor OCR.  

> **Por que não usar `SearchOption.AllDirectories`?** Se suas imagens estiverem aninhadas, você pode mudar para `GetFiles(path, "*.png", SearchOption.AllDirectories)`. Apenas lembre‑se de que varreduras mais profundas podem trazer arquivos indesejados, então filtre adequadamente.

### 3. Converter Caminhos de Arquivo para Objetos ImageStream  

A maioria dos SDKs OCR espera um stream ao invés de um caminho bruto. A expressão LINQ `Select(path => ImageStream.FromFile(path)).ToList()` cria uma **lista de streams** que o reconhecedor em lote pode consumir em uma única chamada. Esta etapa também garante que os handles de arquivos sejam abertos apenas uma vez, reduzindo a sobrecarga de I/O.

> **Caso de borda:** Se um arquivo estiver corrompido, `ImageStream.FromFile` pode lançar exceção. Envolva a conversão em um `try/catch` se precisar de resiliência.

### 4. Reconhecer Texto em Todo o Lote  

`ocrEngine.RecognizeBatch(imageStreams)` é o ponto ideal para *how to batch OCR*. Em vez de iterar sobre cada imagem e chamar um método de imagem única, entregamos a coleção inteira ao motor. Internamente a biblioteca pode paralelizar o trabalho, proporcionando um aumento de velocidade em máquinas multi‑core.

> **Dica:** Se sua biblioteca OCR não expõe um método em lote, você ainda pode alcançar desempenho semelhante usando `Parallel.ForEach` ao redor da chamada `Recognize` de imagem única.

### 5. Gravar Cada Resultado OCR – convertendo PNG para texto  

O loop `for` final grava `ocrResults[i].Text` em um arquivo `.txt` cujo nome espelha o PNG original. Isso é exatamente o que a palavra‑chave secundária *convert PNG to text* descreve. A chamada `Path.Combine` garante que a pasta de saída exista e previne bugs de travessia de caminho.

> **Armadilha comum:** Esquecer de criar a pasta de saída primeiro causará um `DirectoryNotFoundException`. A linha `Directory.CreateDirectory(outputFolder);` resolve isso preventivamente.

---

## Lidando com Variações do Mundo Real

| Situação | O que mudar | Por quê |
|-----------|----------------|-----|
| **Pasta de entrada vazia** | Mantenha a verificação inicial `if (imagePaths.Length == 0)` | Impede uma chamada OCR desnecessária e fornece uma mensagem amigável |
| **Tipos de arquivo misturados** | Use `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` | Garante que você processe apenas PNGs, atendendo *extract text png* sem erros |
| **Imagens enormes ( > 5 MB )** | Reduza antes de enviar ao OCR: `ImageStream.FromFile(path).Resize(1920, 1080)` (se a API suportar) | Reduz a pressão de memória e frequentemente melhora a precisão do reconhecimento |
| **Idioma OCR diferente** | Defina `ocrEngine.Config.Language = Language.French;` | Alinha o motor com o idioma das imagens de origem |

---

## Perguntas Frequentes (FAQ)

**Q: Isso funciona com arquivos JPEG ou TIFF?**  
A: A lógica central permanece a mesma; basta mudar o padrão de busca para `"*.jpg"` ou `"*.tif"` e garantir que a biblioteca OCR possa decodificar esses formatos.

**Q: Como posso processar milhares de imagens sem ficar sem memória?**  
A: Substitua a chamada em lote por uma abordagem de streaming—processar um bloco de, por exemplo, 50 imagens por vez, então liberar os streams antes de carregar o próximo bloco.

**Q: Preciso da pontuação de confiança do OCR. Onde a encontro?**  
A: A maioria dos objetos `OcrResult` expõe uma propriedade `Confidence`. Você pode estender a etapa de gravação:

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

---

## Conclusão

Acabamos de cobrir **como fazer OCR em lote** de imagens PNG em C# do início ao fim. Ao inicializar um único motor, ler imagens do diretório, convertê‑las em streams, reconhecer todo o lote e, finalmente, gravar cada resultado em um arquivo de texto, você agora tem um padrão sólido e pronto para produção para as tarefas **extract text PNG**, **convert PNG to text** e **read images from directory**.

O que vem a seguir? Experimente trocar o provedor OCR, adicionar pós‑processamento multithread (por exemplo, correção ortográfica), ou alimentar os arquivos `.txt` em um índice de busca. O céu é o limite depois que você dominar o fluxo de trabalho em lote.

Tem uma variação que gostaria de compartilhar? Deixe um comentário, e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}