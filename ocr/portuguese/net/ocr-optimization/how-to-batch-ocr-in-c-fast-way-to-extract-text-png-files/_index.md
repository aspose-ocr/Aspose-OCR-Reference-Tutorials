---
category: general
date: 2026-04-03
description: Aprenda a fazer OCR em lote com Aspose.OCR em C#. Este guia mostra como
  extrair texto de imagens PNG e converter imagens em texto de forma eficiente.
draft: false
keywords:
- how to batch ocr
- extract text png
- convert images to text
- Aspose OCR
- C# parallel processing
language: pt
og_description: Descubra como fazer OCR em lote em C# para extrair texto de imagens
  PNG e converter imagens em texto usando Aspose.OCR. Código completo incluído.
og_title: Como fazer OCR em lote no C# – Guia rápido
tags:
- OCR
- C#
- Aspose
title: Como fazer OCR em lote em C# – Forma rápida de extrair texto de arquivos PNG
url: /pt/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR em lote no C# – Forma rápida de extrair texto de arquivos PNG

Já se perguntou **como fazer OCR em lote** de uma pasta inteira de capturas de tela sem escrever um loop para cada arquivo? Você não está sozinho. Em muitos projetos—pense em digitalização de notas fiscais ou arquivamento de recibos escaneados—acabam surgindo dezenas, às vezes centenas, de arquivos PNG que precisam ter seu texto extraído. A boa notícia? Com Aspose.OCR você pode **extrair texto PNG** de imagens em paralelo, e todo o processo pode ser encapsulado em apenas algumas linhas de C#.

Neste tutorial vamos percorrer um exemplo completo, pronto‑para‑executar, que mostra como **converter imagens em texto** usando um processador em lote. Vamos cobrir os pré‑requisitos, explicar por que cada linha importa e ainda dar algumas dicas profissionais para que você não encontre armadilhas comuns mais tarde.

## Pré‑requisitos

Antes de mergulharmos, certifique‑se de que você tem:

- **.NET 6.0** (ou superior) instalado na sua máquina. Runtimes mais antigos funcionam, mas o mais recente oferece melhor desempenho e suporte a async.
- Pacote **Aspose.OCR for .NET**. Você pode obtê‑lo via NuGet: `dotnet add package Aspose.OCR`.
- Uma pasta cheia de imagens **PNG** que você deseja processar. Vamos chamá‑la de `YOUR_DIRECTORY` ao longo do guia.
- Uma quantidade moderada de RAM—OCR em lote pode consumir bastante memória se você aumentar o paralelismo, mas usar `Environment.ProcessorCount` mantém tudo seguro.

> **Dica profissional:** Se você estiver em um pipeline CI/CD, adicione o arquivo de licença da Aspose como um segredo para evitar o limite de 20 páginas da avaliação gratuita.

Agora, vamos colocar a mão na massa.

## Etapa 1: Configurar o Processador de OCR em Lote (Palavra‑chave principal no cabeçalho)

A primeira coisa que você precisa é uma instância de `BatchOcrProcessor`. Essa classe abstrai a lógica de threading e permite que você se concentre no que fazer com cada imagem.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Create a batch OCR processor and tell it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };
```

**Por que isso importa:**  
- `Engine = new OcrEngine()` fornece um motor OCR novo para cada thread, evitando contenção.  
- `MaxDegreeOfParallelism = Environment.ProcessorCount` escala automaticamente ao número de núcleos, proporcionando o melhor throughput possível sem ajustes manuais.

## Etapa 2: Conectar aos Eventos de Progresso (Ajuda a Monitorar a Extração)

Ver o progresso é essencial ao processar centenas de arquivos. O evento `ProgressChanged` é disparado após cada arquivo ser concluído, permitindo que você registre o status.

```csharp
        // Subscribe to progress updates so we know which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");
```

**Por que você vai adorar:**  
- Feedback em tempo real impede que você se pergunte se o aplicativo está travado.  
- Se precisar pausar ou cancelar, já tem um ponto de conexão para inspecionar `e.Current` vs `e.Total`.

## Etapa 3: Definir a Varredura da Pasta e o Padrão de Arquivo (Extrair Texto PNG)

Agora informamos ao processador onde procurar e que tipo de arquivos capturar. O padrão `"*.png"` garante que apenas imagens PNG sejam tratadas.

```csharp
        // Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"YOUR_DIRECTORY",          // folder containing the images
            "*.png",                    // file pattern
            (imagePath, ocrText) =>     // callback for each processed file
            {
                // Step 4 is inside this callback – see next section
            });
```

**Por que isso é fundamental:**  
- Usar um padrão glob mantém o código flexível; troque `*.png` por `*.jpg` se precisar lidar com JPEGs no futuro.  
- O callback recebe tanto o caminho da imagem quanto o texto reconhecido, dando total controle sobre o que fazer a seguir.

## Etapa 4: Salvar o Texto Reconhecido ao Lado da Fonte (Converter Imagens em Texto)

Dentro do callback escreveremos a saída do OCR em um arquivo `.txt` que ficará ao lado do PNG original. Essa é a maneira mais simples de **converter imagens em texto** para processamento posterior.

```csharp
                // Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
```

**Por que escolhemos um arquivo `.txt` lado a lado:**  
- Mantém a relação óbvia—abra o PNG, abra o TXT, compare.  
- Não há necessidade de banco de dados ou camada de armazenamento extra em projetos de pequena escala.

## Etapa 5: Finalizar com uma Mensagem Amigável de Conclusão

Uma mensagem limpa no console indica quando tudo está concluído.

```csharp
        // Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

Ao executar o programa, você verá uma saída semelhante a:

```
Processed 1/27: C:\Images\invoice1.png
Processed 2/27: C:\Images\invoice2.png
...
Batch processing completed.
```

Cada PNG agora tem um arquivo `.txt` irmão contendo o texto extraído.

## Exemplo Completo Funcional (Todas as Etapas Combinadas)

Abaixo está o programa inteiro que você pode copiar‑colar em um novo projeto de console. Nenhuma parte está faltando—basta substituir `YOUR_DIRECTORY` pelo caminho absoluto das suas imagens.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create a batch OCR processor and configure it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };

        // Step 2: Subscribe to progress updates to see which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");

        // Step 3: Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"C:\MyImages",          // folder containing the images
            "*.png",                // file pattern
            (imagePath, ocrText) => // callback for each processed file
            {
                // Step 4: Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
            });

        // Step 5: Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

### Resultado Esperado

- Para cada `image.png` em `C:\MyImages`, aparece um `image.txt` ao lado.
- O console imprime linhas de progresso, facilitando o monitoramento de grandes lotes.
- Sem loops manuais ou gerenciamento de threads—`BatchOcrProcessor` cuida de tudo.

## Perguntas Frequentes & Casos de Borda

### E se minhas imagens não forem PNG?

Basta mudar o segundo argumento em `ProcessFolder` para `"*.jpg"` ou `"*.*"` para incluir todos os arquivos. O motor OCR funciona com a maioria dos formatos raster.

### Quanto de memória isso consome?

`BatchOcrProcessor` carrega uma imagem por thread. Com `Environment.ProcessorCount` definido, por exemplo, para 8 núcleos, você terá oito imagens na memória simultaneamente. Se ocorrerem exceções de OutOfMemory, reduza o paralelismo:

```csharp
MaxDegreeOfParallelism = 4; // or any number that fits your machine
```

### Posso personalizar o idioma do OCR?

Com certeza. Após criar o engine, defina a propriedade `Language`:

```csharp
Engine = new OcrEngine { Language = Language.English };
```

Aspose suporta muitos idiomas; basta adicionar o pacote NuGet apropriado, se necessário.

### E quanto ao tratamento de erros?

Envolva o callback em um bloco try/catch e registre as falhas. O processador continuará com o próximo arquivo, evitando que uma única imagem corrompida interrompa toda a execução.

```csharp
(imagePath, ocrText) =>
{
    try
    {
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, ocrText);
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Failed on {imagePath}: {ex.Message}");
    }
}
```

## Dicas Profissionais para Escalar

- **Divida a pasta**: Se você tem dezenas de milhares de arquivos, separe‑os em subpastas e execute vários jobs em sequência.
- **Use uma VM na nuvem**: Uma máquina com mais núcleos (ex.: 32‑core) terminará drasticamente mais rápido. Apenas lembre‑se de ajustar os limites da licença.
- **Pós‑processamento do texto**: Após a extração, você pode rodar expressões regulares para capturar números de nota fiscal ou datas. Os arquivos `.txt` são entrada perfeita para esses pipelines.

## Conclusão

Agora você tem uma receita sólida, pronta para produção, de **como fazer OCR em lote** de um diretório de PNGs, **extrair texto PNG** e **converter imagens em texto** usando Aspose.OCR em C#. O exemplo é autocontido, explica o “porquê” de cada linha e inclui dicas para lidar com cargas maiores ou tipos de arquivo diferentes.

Pronto para o próximo passo? Experimente trocar o callback para inserir os resultados em um banco de dados, ou adicione pré‑processamento de imagem (ex.: deskew) antes do OCR. O padrão escala bem, permitindo que você o adapte a qualquer cenário de processamento em lote que encontrar.

Boa codificação, e que seus pipelines de OCR sejam rápidos e livres de erros!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}