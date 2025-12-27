---
category: general
date: 2025-12-27
description: Crie um logger de console em C# e habilite o download automático para
  tabelas corretas usando AsposeAI. Aprenda como exibir a saída da tabela corrigida
  em apenas alguns passos.
draft: false
keywords:
- create console logger
- enable auto download
- how to correct tables
- setup console logger
- display corrected table
language: pt
og_description: Crie um registrador de console em C# e habilite o download automático
  para tabelas corretas usando AsposeAI. Siga este guia para exibir rapidamente a
  saída da tabela corrigida.
og_title: Criar registrador de console e corrigir tabelas com AsposeAI
tags:
- AsposeAI
- C#
- OCR
- Table processing
title: Criar logger de console e corrigir tabelas com AsposeAI
url: /pt/net/ocr-optimization/create-console-logger-and-correct-tables-with-asposeai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar logger de console e corrigir tabelas com AsposeAI

Já precisou **criar logger de console** para um pipeline de IA em C# mas não sabia por onde começar? Neste guia vamos percorrer todo o processo — como criar um logger de console, habilitar o download automático de arquivos de modelo e, finalmente, **como corrigir tabelas** que vieram do OCR. Ao final você será capaz de **exibir resultados de tabelas corrigidas** no seu console com apenas algumas linhas de código.

Cobriremos tudo, desde a configuração inicial do logger até a limpeza final, para que você não precise vasculhar documentos espalhados. Não é necessária experiência prévia com AsposeAI; um entendimento básico de C# e .NET basta. Ao longo do caminho, vamos espalhar dicas sobre as melhores práticas de **setup console logger**, falar sobre casos de borda e mostrar como a saída deve ser.

---

## Pré-requisitos

- .NET 6.0 ou posterior (o código usa recursos modernos da linguagem)
- Visual Studio 2022 ou qualquer IDE que suporte projetos C#
- **Aspose.AI** pacote NuGet instalado (`Install-Package Aspose.AI`)
- **Aspose.OCR** pacote NuGet instalado (`Install-Package Aspose.OCR`)
- Um objeto de resultado OCR de exemplo (`ocrResult`) de uma chamada anterior ao Aspose.OCR

Se algum desses estiver faltando, pause agora e resolva—você vai agradecer a si mesmo depois.

## Etapa 1: Criar logger de console e inicializar AsposeAI

A primeira coisa que precisamos é de um logger que escreva diretamente no console. Isso facilita a depuração e nos fornece feedback em tempo real enquanto o motor de IA executa.

```csharp
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

// Step 1: Create a logger that writes to the console
ILogger consoleLogger = new ConsoleLogger();

// Step 2: Initialise the AsposeAI engine with the logger
AsposeAI asposeAI = new AsposeAI(consoleLogger);
```

**Por que isso importa:**  
`ConsoleLogger` implementa a interface `ILogger`, então quaisquer mensagens internas do AsposeAI (carregamento de modelo, status do pós‑processador, erros) aparecem instantaneamente no seu terminal. É a maneira mais simples de **setup console logger** sem incorporar frameworks de logging externos.

> **Dica profissional:** Se mais tarde precisar de logging em arquivo, basta trocar `ConsoleLogger` por um logger personalizado que implemente `ILogger` — o resto do código permanece inalterado.

## Etapa 2: Habilitar download automático para modelos de IA

AsposeAI pode buscar os arquivos de modelo necessários sob demanda. Ativar isso salva você de baixar manualmente grandes blobs binários.

```csharp
// Step 3: (Optional) Configure automatic model download and set the model directory
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,               // <‑‑ enable auto download
    DirectoryModelPath = "YOUR_DIRECTORY"   // change to a writable folder
};
```

**O que pode dar errado?**  
Se `DirectoryModelPath` apontar para um local somente leitura, o download automático falhará e você verá uma exceção no console. Certifique‑se de que a pasta exista e que seu aplicativo tenha permissões de escrita.

## Etapa 3: Criar um pós‑processador de tabela (como corrigir tabelas)

Tabelas extraídas do OCR costumam ser bagunçadas — células mescladas, bordas ausentes ou texto desalinhado. O `TableAIProcessor` da AsposeAI pode limpá‑las automaticamente.

```csharp
// Step 4: Create a table post‑processor that lets the engine decide when to run correction
TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);
```

**Por que modo AUTO?**  
`AITableDetectionMode.AUTO` permite que o motor inspecione a saída do OCR e decida se uma correção é necessária. Se preferir controle manual, você pode usar `MANUAL` e invocar `RunCorrection()` você mesmo.

## Etapa 4: Anexar o pós‑processador e sua configuração

Agora vinculamos tudo — logger, configuração de modelo e o processador de tabela.

```csharp
// Step 5: Attach the post‑processor and its configuration to the AI engine
asposeAI.SetPostProcessor(tableProcessor, modelConfig);
```

Neste ponto o motor de IA sabe *onde* armazenar os modelos, *como* registrar logs e *qual* pós‑processamento aplicar. É uma separação limpa de responsabilidades que torna mudanças futuras indolores.

## Etapa 5: Executar o pós‑processador no seu resultado OCR

Assumindo que você já tem um `ocrResult` do Aspose.OCR, basta entregá‑lo ao motor.

```csharp
// Step 6: Run the post‑processor on the OCR result returned by Aspose.OCR
asposeAI.RunPostprocessor(ocrResult);
```

**Alerta de caso de borda:**  
Se `ocrResult` não contiver tabelas, o processador pulará a correção silenciosamente. Você pode verificar `tableProcessor.GetResult().Count` depois para confirmar que algo foi realmente processado.

## Etapa 6: Recuperar e **exibir tabela corrigida** 

Finalmente, vamos extrair o texto da tabela limpa e imprimi‑lo no console.

```csharp
// Step 7: Retrieve and display the corrected table text
Console.WriteLine("Corrected table output:");
Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
```

A saída terá algo parecido com isto (dependendo da sua imagem de origem):

```
Corrected table output:
| Item   | Quantity | Price |
|--------|----------|-------|
| Apple  | 10       | $1.20 |
| Banana | 5        | $0.80 |
```

Se você vir uma string vazia, verifique novamente se o OCR realmente detectou uma tabela e se `AllowAutoDownload` foi bem‑sucedido.

## Etapa 7: Limpar recursos

Ser um bom cidadão significa descartar objetos pesados quando terminar.

```csharp
// Step 8: Release resources used by the AI engine
asposeAI.Dispose();
```

Pular esta etapa pode deixar manipuladores de arquivos abertos, especialmente no Windows onde os arquivos de modelo permanecem bloqueados.

## Exemplo Completo Funcional

Abaixo está o programa completo que você pode copiar‑colar em um novo projeto de console. Substitua `"YOUR_DIRECTORY"` por um caminho real e certifique‑se de que `ocrResult` esteja preenchido antes de chamar `RunPostprocessor`.

```csharp
using System;
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

namespace AsposeAITableCorrection
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a console logger
            ILogger consoleLogger = new ConsoleLogger();

            // 2️⃣ Initialise AsposeAI with the logger
            AsposeAI asposeAI = new AsposeAI(consoleLogger);

            // 3️⃣ Configure auto‑download (optional but recommended)
            AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
            {
                AllowAutoDownload = true,
                DirectoryModelPath = @"C:\AsposeModels" // <-- change this
            };

            // 4️⃣ Create the table processor (auto‑detect mode)
            TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);

            // 5️⃣ Attach processor and config
            asposeAI.SetPostProcessor(tableProcessor, modelConfig);

            // 6️⃣ Obtain OCR result (replace with your own OCR call)
            // Example placeholder – you should have this from Aspose.OCR already
            OcrResult ocrResult = GetOcrResultSomehow();

            // 7️⃣ Run post‑processor on the OCR output
            asposeAI.RunPostprocessor(ocrResult);

            // 8️⃣ Display corrected table
            Console.WriteLine("Corrected table output:");
            if (tableProcessor.GetResult().Count > 0)
            {
                Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
            }
            else
            {
                Console.WriteLine("No tables were detected or corrected.");
            }

            // 9️⃣ Clean up
            asposeAI.Dispose();
        }

        // Dummy method – replace with your actual OCR logic
        static OcrResult GetOcrResultSomehow()
        {
            // For illustration only
            OcrEngine engine = new OcrEngine();
            engine.Image = ImageStream.FromFile("sample-table.png");
            return engine.Recognize();
        }
    }
}
```

**Saída esperada no console** (assumindo uma imagem de tabela simples):

```
Corrected table output:
| Name   | Age | City      |
|--------|-----|-----------|
| Alice  | 30  | New York  |
| Bob    | 25  | Seattle   |
```

## Perguntas Frequentes & Respostas

- **Preciso de conexão à internet para o download automático?**  
  Sim. Na primeira vez que o modelo é solicitado, AsposeAI acessa seu CDN. Depois que o arquivo chega em `DirectoryModelPath`, execuções subsequentes são offline.

- **E se minha tabela tiver células mescladas?**  
  O modelo de IA tenta dividir células mescladas com base em pistas visuais. Se o resultado parecer errado, considere pré‑processar a imagem (aumentar contraste, corrigir rotação) antes do OCR.

- **Posso processar várias tabelas de uma vez?**  
  Absolutamente. `tableProcessor.GetResult()` retorna uma lista; itere sobre ela para imprimir cada tabela.

- **O `ConsoleLogger` é thread‑safe?**  
  Ele escreve diretamente em `System.Console`, que é thread‑safe para gravações simples. Para cenários multi‑thread intensos, um logger personalizado com sincronização pode ser preferível.

## Próximos Passos & Tópicos Relacionados

Agora que você sabe **como corrigir tabelas**, pode querer:

- **Habilitar download automático** para outros modelos AsposeAI (ex.: tradução de idioma).
- **Setup console logger** com diferentes níveis de log (Info, Warning, Error) para controle mais fino.
- Explorar **exibir tabela corrigida** em uma GUI (WinForms ou WPF) ao invés do console.
- Combinar correção de tabela com **data extraction** para alimentar diretamente um banco de dados.

Cada um desses se baseia na fundação que acabamos de construir, então sinta‑se à vontade para experimentar.

## Conclusão

Percorremos todo o ciclo de vida de **criar console logger**, habilitar download automático e **corrigir tabelas** com AsposeAI, finalizando com uma forma limpa de **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}