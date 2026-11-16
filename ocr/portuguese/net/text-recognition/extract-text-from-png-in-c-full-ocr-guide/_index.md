---
category: general
date: 2026-03-07
description: Extraia texto de arquivos PNG usando C#. Aprenda como converter imagem
  em texto em C# e ler texto de imagens digitalizadas rapidamente.
draft: false
keywords:
- extract text from png
- convert image to text c#
- read text from scanned images
- how to run ocr on images
language: pt
og_description: Extraia texto de arquivos PNG usando C#. Este guia mostra como converter
  imagem em texto C# e ler texto de imagens digitalizadas com Aspose OCR.
og_title: Extrair Texto de PNG em C# – Guia Completo de OCR
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Extrair Texto de PNG em C# – Guia Completo de OCR
url: /pt/net/text-recognition/extract-text-from-png-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de PNG em C# – Guia Completo de OCR

Já precisou **extrair texto de PNG** arquivos mas não sabia por onde começar? Você não está sozinho—a maioria dos desenvolvedores encontra essa barreira ao se deparar com gráficos escaneados ou capturas de tela que precisam se tornar texto pesquisável. A boa notícia? Com algumas linhas de C# e Aspose OCR você pode transformar qualquer PNG em strings editáveis em um instante.

Neste tutorial percorreremos todo o processo: desde localizar PNGs no disco, iniciar tarefas de OCR em paralelo, até exibir uma pré‑visualização organizada de cada resultado. Ao final você saberá como **convert image to text C#** (manter termo), poderá **read text from scanned images** eficientemente, e também verá a melhor forma de **run OCR on images** sem sobrecarregar a thread da UI.

## O que você precisará

- .NET 6.0 ou posterior (o código funciona também em .NET Core e .NET Framework)  
- Pacote NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Uma pasta cheia de arquivos *.png* que você deseja processar  
- Qualquer IDE que preferir (Visual Studio, VS Code, Rider…)

Nenhuma configuração extra é necessária; a biblioteca já inclui tudo que é preciso para decodificar PNGs, JPEGs, TIFFs, o que você precisar.

## Etapa 1: Localizar Todos os Arquivos PNG – “Extract Text from PNG” Começa

Primeiro precisamos encontrar cada PNG que pretendemos processar com OCR. Usar `Directory.GetFiles` é rápido e confiável.

```csharp
// Step 1: Find all PNG images in the input folder
string[] imageFiles = Directory.GetFiles("YOUR_DIRECTORY", "*.png");

// Quick sanity check – throw if nothing was found
if (imageFiles.Length == 0)
    throw new FileNotFoundException("No PNG files found in the specified folder.");
```

*Por que isso importa:* Escanear o diretório uma única vez mantém o restante do pipeline simples, e a verificação inicial impede uma situação silenciosa de “sem saída” que pode ser difícil de depurar depois.

## Etapa 2: Iniciar Tarefas de OCR Paralelas – Executar **run OCR on images** de forma eficiente

Executar OCR sequencialmente funciona para alguns poucos arquivos, mas projetos reais frequentemente lidam com dezenas ou centenas. Ao iniciar uma `Task` por imagem mantemos a CPU ocupada enquanto a biblioteca realiza o processamento pesado.

```csharp
// Step 2: Prepare a list to hold OCR tasks (one per image)
var ocrTasks = new List<Task<string>>();

// Step 3: Launch a parallel task for each image
foreach (var filePath in imageFiles)
{
    ocrTasks.Add(Task.Run(() =>
    {
        // Load the image and run OCR
        var engine = new OcrEngine();
        engine.Image = ImageStream.FromFile(filePath);
        engine.Recognize();
        return engine.Text;          // This is the extracted string
    }));
}
```

*Dica profissional:* `Task.Run` delega o trabalho ao pool de threads, o que significa que sua UI (se houver) permanece responsiva. Se você estiver em um servidor, o mesmo padrão escala bem entre os núcleos.

## Etapa 3: Aguardar Todas as Tarefas – Coletar os Resultados

Agora aguardamos que cada operação de OCR termine. `Task.WhenAll` devolve um array que segue a ordem original dos arquivos, facilitando o pareamento dos resultados com os nomes dos arquivos.

```csharp
// Step 4: Await all tasks and gather the recognized texts
string[] ocrResults = await Task.WhenAll(ocrTasks);
```

*Observação de caso extremo:* Se alguma imagem gerar exceção (arquivo corrompido, formato não suportado) todo o `WhenAll` propagará a exceção. Você pode envolver o `Task.Run` interno em um try/catch e retornar uma string vazia ou uma mensagem de diagnóstico se precisar de tolerância a falhas.

## Etapa 4: Mostrar uma Pré‑visualização – Verificar a saída do **convert image to text C#**

Uma pré‑visualização rápida ajuda a confirmar que o OCR funcionou antes de você começar a persistir os dados em outro lugar.

```csharp
// Step 5: Show a short preview of each result
for (int i = 0; i < ocrResults.Length; i++)
{
    string fileName = Path.GetFileName(imageFiles[i]);
    string preview = ocrResults[i].Length > 100
        ? ocrResults[i][..100] + "..."
        : ocrResults[i];
    Console.WriteLine($"{fileName}: {preview}");
}
```

A saída típica do console se parece com:

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
```

Se a pré‑visualização mostrar caracteres ilegíveis, verifique novamente a qualidade da imagem ou considere pré‑processamento (ex.: binarização) – mas para a maioria dos PNGs limpos o Aspose OCR acerta na primeira tentativa.

## Opcional: Salvar Resultados em CSV – Um Caso de Uso Real

A maioria dos projetos precisa do texto extraído em um formato estruturado. Abaixo há um pequeno helper que grava o nome do arquivo e o texto completo do OCR em um arquivo CSV.

```csharp
string csvPath = Path.Combine("YOUR_DIRECTORY", "ocr-results.csv");
using var writer = new StreamWriter(csvPath);
writer.WriteLine("FileName,ExtractedText");

for (int i = 0; i < imageFiles.Length; i++)
{
    string escaped = ocrResults[i].Replace("\"", "\"\"");
    writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
}
Console.WriteLine($"All results saved to {csvPath}");
```

Agora você pode importar o CSV para Excel, Power BI ou qualquer sistema downstream que espere **read text from scanned images**.

## Perguntas Frequentes

**E se meus PNGs forem enormes (mais de 5 MB)?**  
Aspose OCR automaticamente reduz imagens grandes para manter o uso de memória sob controle, mas você pode redimensionar manualmente com `engine.Image = ImageStream.FromFile(filePath).Resize(2000, 0);` para limitar a largura a 2000 px preservando a proporção.

**Posso executar isso no Linux?**  
Sim. Aspose OCR é multiplataforma; apenas certifique‑se de que as dependências nativas (`libgdiplus` em algumas distribuições) estejam instaladas.

**A linguagem do OCR está configurada para Inglês por padrão?**  
Correto. Se precisar de outro idioma, defina `engine.Language = OcrLanguage.French;` (ou qualquer enum suportado) antes de chamar `Recognize()`.

**Como lidar com PDFs protegidos por senha que contêm PNGs?**  
Converta as páginas do PDF em imagens primeiro (usando Aspose PDF ou outra biblioteca), depois alimente esses PNGs no mesmo pipeline. O princípio de **how to run OCR on images** permanece o mesmo.

## Exemplo Completo Funcional (Async Main)

Abaixo está um programa autônomo que você pode copiar‑colar em um projeto de console. Ele inclui todas as partes acima, além de um pequeno helper para validar a pasta de entrada.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // -------------------------------------------------
        // 1️⃣ Locate PNGs – the heart of “extract text from png”
        // -------------------------------------------------
        const string folder = @"YOUR_DIRECTORY";   // <-- change this
        if (!Directory.Exists(folder))
        {
            Console.WriteLine($"Folder not found: {folder}");
            return;
        }

        string[] imageFiles = Directory.GetFiles(folder, "*.png");
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to do.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Fire off OCR tasks – best way to “run OCR on images”
        // -------------------------------------------------
        var ocrTasks = new List<Task<string>>();
        foreach (var filePath in imageFiles)
        {
            ocrTasks.Add(Task.Run(() =>
            {
                var engine = new OcrEngine();
                engine.Image = ImageStream.FromFile(filePath);
                engine.Recognize();
                return engine.Text;
            }));
        }

        // -------------------------------------------------
        // 3️⃣ Await results
        // -------------------------------------------------
        string[] ocrResults = await Task.WhenAll(ocrTasks);

        // -------------------------------------------------
        // 4️⃣ Show previews
        // -------------------------------------------------
        for (int i = 0; i < ocrResults.Length; i++)
        {
            string fileName = Path.GetFileName(imageFiles[i]);
            string preview = ocrResults[i].Length > 100
                ? ocrResults[i][..100] + "..."
                : ocrResults[i];
            Console.WriteLine($"{fileName}: {preview}");
        }

        // -------------------------------------------------
        // 5️⃣ Optional: write CSV – perfect for “read text from scanned images”
        // -------------------------------------------------
        string csvPath = Path.Combine(folder, "ocr-results.csv");
        using var writer = new StreamWriter(csvPath);
        writer.WriteLine("FileName,ExtractedText");
        for (int i = 0; i < imageFiles.Length; i++)
        {
            string escaped = ocrResults[i].Replace("\"", "\"\"");
            writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
        }

        Console.WriteLine($"✅ OCR complete – results saved to {csvPath}");
    }
}
```

**Saída esperada** (exemplo para dois PNGs):

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
✅ OCR complete – results saved to C:\MyImages\ocr-results.csv
```

## Conclusão

Acabamos de cobrir tudo que você precisa para **extract text from PNG** arquivos usando C#. Desde localizar os arquivos, iniciar trabalhos de OCR paralelos, pré‑visualizar as strings, até persistí‑las em um CSV—este guia oferece um padrão pronto para produção em cenários de **convert image to text C#**.  

Se você está pronto para o próximo passo, experimente alimentar o mesmo pipeline com arquivos JPEG ou TIFF, teste diferentes idiomas de OCR, ou conecte os resultados a um índice de busca para que você possa **read text from scanned images** instantaneamente.  

Tem dúvidas sobre casos extremos, otimização de desempenho ou licenciamento? Deixe um comentário ou entre em contato com a comunidade Aspose—bom código!

![Exemplo de extração de texto de PNG](extract-text-png.png "Extrair texto de PNG usando Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}