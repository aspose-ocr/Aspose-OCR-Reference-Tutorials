---
category: general
date: 2026-08-18
description: Aprenda a criar um logger de console em C# e a usar o Aspose AI para
  corrigir texto OCR com um pós‑processador de verificação ortográfica.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create console logger
- correct ocr text
- spell check ocr
language: pt
lastmod: 2026-08-18
og_description: Crie um logger de console em C# e corrija o texto OCR usando o Aspose
  AI. Siga este guia completo para adicionar um pós‑processador de verificação ortográfica
  ao seu pipeline de OCR.
og_image_alt: Illustration of creating a console logger in C# code editor
og_title: Crie um registrador de console e verifique a ortografia de texto OCR em
  C# – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-08-18'
  description: Learn how to create console logger in C# and use Aspose AI to correct
    OCR text with a spell‑check post‑processor.
  headline: How to create console logger and spell‑check OCR text in C#
  type: TechArticle
tags:
- C#
- OCR
- AI
- logging
title: Como criar um logger de console e verificar a ortografia de texto OCR em C#
url: /pt/net/text-recognition/how-to-create-console-logger-and-spell-check-ocr-text-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar um logger de console e corrigir texto OCR com verificação ortográfica em C#

Se você precisa **criar um logger de console** para saída de diagnóstico ao processar documentos digitalizados, este guia mostra uma solução completa. Ao final do tutorial você será capaz de **corrigir texto OCR** com um pós‑processador de verificação ortográfica integrado usando o Aspose AI SDK.

Os resultados de OCR frequentemente contêm erros de ortografia que afetam análises posteriores. Adicionar uma etapa de verificação ortográfica garante que o texto esteja limpo e pronto para indexação, tradução ou extração de dados. As seções a seguir orientam você por cada peça necessária, desde a criação do logger até a verificação final.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 ou superior instalado  
* Visual Studio 2022 (ou qualquer IDE compatível com C#)  
* Pacote NuGet Aspose.AI adicionado ao seu projeto (`dotnet add package Aspose.AI`)  

Nenhum serviço externo adicional é necessário porque o modelo Aspose AI pode ser baixado automaticamente.

## Etapa 1: Como criar um logger de console para diagnóstico

Um logger captura informações de tempo de execução, facilitando a solução de problemas de carregamento de modelo ou execução do pós‑processador. A interface `ILogger` permite trocar implementações sem alterar o restante do código.

```csharp
// Step 1: (Optional) Create a logger for diagnostic output
ILogger logger = new ConsoleLogger();   // set to null if logging is not needed
```

O `ConsoleLogger` grava cada entrada de log no fluxo de saída padrão. Usar uma interface mantém o código testável e permite substituir o logger por um baseado em arquivo ou em nuvem posteriormente.

## Etapa 2: Configurar o modelo AI para habilitar download automático

Aspose AI pode baixar os arquivos de modelo necessários sob demanda. Especificar uma pasta local evita tráfego de rede repetido e dá controle sobre o armazenamento.

```csharp
// Step 2: Configure the AI model – enable automatic download and specify a local folder
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,
    DirectoryModelPath = "YOUR_DIRECTORY"
};
```

`AllowAutoDownload` garante que o SDK busque o modelo na primeira execução. `DirectoryModelPath` aponta para um local persistente na sua máquina, o que é útil em pipelines de CI.

## Etapa 3: Inicializar o motor AsposeAI com o logger

Passar o logger para o motor vincula a saída de diagnóstico a cada operação interna, incluindo carregamento de modelo e execução do pós‑processador.

```csharp
// Step 3: Initialise the AsposeAI engine with the logger
AsposeAI ai = new AsposeAI(logger);
```

O construtor `AsposeAI` aceita uma instância de `ILogger`. Se você forneceu `null` na Etapa 1, o motor será executado silenciosamente.

## Etapa 4: Criar o pós‑processador de verificação ortográfica integrado

Aspose AI fornece um componente de verificação ortográfica pronto que funciona diretamente nos resultados de OCR. Instanciá‑lo não requer nenhuma configuração.

```csharp
// Step 4: Create the built‑in spell‑check post‑processor
SpellCheckAIProcessor spellChecker = new SpellCheckAIProcessor();
```

O `SpellCheckAIProcessor` implementa a interface `IAIProcessor`, permitindo que seja registrado junto à configuração do modelo.

## Etapa 5: Registrar o processador de verificação ortográfica junto com a configuração do modelo

Vincular o processador ao motor garante que os resultados de OCR passem automaticamente pela etapa de verificação ortográfica.

```csharp
// Step 5: Register the spell‑check processor together with the model configuration
ai.SetPostProcessor(spellChecker, modelConfig);
```

`SetPostProcessor` associa o `spellChecker` ao `modelConfig`. Quando você chamar `RunPostprocessor` mais tarde, o motor invocará a lógica de verificação ortográfica usando o modelo baixado.

## Etapa 6: Executar o pós‑processador nos resultados de OCR já obtidos

Assumindo que você já tem a saída de OCR armazenada na variável `ocrResult`, invoque o pós‑processador para obter o texto corrigido.

```csharp
// Step 6: Execute the post‑processor on previously obtained OCR results (variable `ocrResult`)
ai.RunPostprocessor(ocrResult);
```

`RunPostprocessor` processa cada página de `ocrResult`. O algoritmo de verificação ortográfica analisa as strings reconhecidas, aplica dicionários específicos de idioma e produz uma versão corrigida.

## Etapa 7: Recuperar e exibir o texto corrigido

Após o processamento, o `SpellCheckAIProcessor` contém os resultados limpos. Você pode obtê‑los e enviá‑los ao console.

```csharp
// Step 7: Retrieve and display the corrected text
Console.WriteLine("CORRECTED RESULT\n");
Console.WriteLine(spellChecker.GetResult()[0].RecognitionText);
```

O primeiro elemento de `GetResult()` corresponde à primeira página do documento OCR. Se você processou um arquivo com várias páginas, itere a coleção para exibir o texto corrigido de cada página.

## Etapa 8: Liberar recursos ao terminar

Descartar a instância `AsposeAI` libera recursos não gerenciados e fecha quaisquer manipuladores de arquivos abertos.

```csharp
// Clean up resources when finished
ai.Dispose();
```

Chamar `Dispose` é uma prática recomendada para qualquer objeto que implemente `IDisposable`, especialmente ao trabalhar com bibliotecas nativas.

## Saída esperada

Quando o programa for executado com sucesso, você verá uma saída semelhante ao exemplo abaixo:

```
CORRECTED RESULT

The quick brown fox jumps over the lazy dog.
```

O texto acima reflete a entrada original de OCR com os erros de ortografia corrigidos pelo pós‑processador de verificação ortográfica.

## Perguntas comuns e casos de borda

**E se o resultado de OCR estiver vazio?**  
O pós‑processador lida graciosamente com páginas vazias e retorna uma string vazia. Nenhuma exceção é lançada.

**Posso usar um dicionário personalizado?**  
`SpellCheckAIProcessor` aceita uma propriedade opcional `CustomDictionaryPath`. Defina‑a antes de chamar `SetPostProcessor` se precisar de termos específicos de domínio.

**O logger de console é thread‑safe?**  
`ConsoleLogger` grava em `Console.Out`, que é sincronizado pelo runtime .NET. Para cenários de alto volume, você pode substituí‑lo por um logger que faça buffer das mensagens.

**E se eu precisar processar muitos documentos simultaneamente?**  
Crie uma instância separada de `AsposeAI` por thread ou use um padrão de pool thread‑safe. Compartilhar uma única instância pode gerar condições de corrida, pois o estado interno do modelo não é local à thread.

## Conclusão

Agora você sabe como **criar um logger de console** em C# e integrar um **pós‑processador de verificação ortográfica OCR** para **corrigir texto OCR**. O fluxo completo — desde a inicialização do logger, passando pela configuração do modelo, processamento e liberação de recursos — cobre todas as etapas essenciais para um pipeline robusto de correção de OCR.

Em seguida, considere estender esse pipeline com pós‑processadores adicionais, como detecção de idioma ou extração de entidades. Você também pode experimentar frameworks de logging alternativos, como Serilog, para capturar dados de diagnóstico mais ricos. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Create Searchable PDF with Aspose OCR Batch Processing – C# Guide](/ocr/english/net/ocr-optimization/create-searchable-pdf-with-batch-ocr-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}