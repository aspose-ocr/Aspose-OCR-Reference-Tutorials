---
category: general
date: 2026-06-03
description: Execute OCR em imagem e extraia texto da imagem usando Aspose.OCR. Aprenda
  como detectar palavras com erros ortográficos e obter sugestões de correção em uma
  única demonstração em C#.
draft: false
keywords:
- perform OCR on image
- extract text from image
- detect misspelled words
- get spelling suggestions
- how to extract text
language: pt
og_description: Execute OCR em uma imagem para extrair texto da imagem, depois detecte
  palavras com erros ortográficos e obtenha sugestões de correção com Aspose.OCR em
  C#.
og_title: Realizar OCR em Imagem e Detectar Palavras com Erros Ortográficos em C#
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Perform OCR on image and extract text from image using Aspose.OCR.
    Learn how to detect misspelled words and get spelling suggestions in a single
    C# demo.
  headline: Perform OCR on Image and Detect Misspelled Words in C#
  type: TechArticle
tags:
- Aspose OCR
- C#
- Spell Checking
title: Realizar OCR em Imagem e Detectar Palavras Ortograficamente Incorretas em C#
url: /pt/net/text-recognition/perform-ocr-on-image-and-detect-misspelled-words-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Realizar OCR em Imagem e Detectar Palavras com Erro de Ortografia em C#

Já se perguntou como **executar OCR em imagem** sem perder a cabeça? Você não está sozinho. Seja digitalizando cartas antigas, escaneando recibos ou construindo um fluxo de trabalho inteligente para documentos, extrair texto limpo de fotos é o primeiro obstáculo. A boa notícia? Com Aspose.OCR você pode montar uma solução em minutos, e o bônus é que também pode **detectar palavras com erro de ortografia** e **obter sugestões de correção** na mesma execução.

Neste tutorial vamos percorrer um aplicativo console C# completo, pronto‑para‑executar, que **extrai texto de imagem**, executa um verificador ortográfico em inglês e imprime cada erro com sugestões úteis. Ao final, você saberá exatamente **como extrair texto**, como conectar a API de verificação ortográfica e como será a saída esperada no console.

## O que você vai construir

- Carregar um bitmap (ou PNG) que contém erros tipográficos.  
- Executar Aspose.OCR para **executar OCR em imagem** e obter os dados brutos em forma de string.  
- Inicializar o verificador ortográfico interno em inglês.  
- **Detectar palavras com erro de ortografia** e **obter sugestões de correção** para cada uma.  
- Imprimir um relatório organizado no console.

Sem serviços externos, sem chamadas HTTP complicadas — apenas um único pacote NuGet e algumas linhas de código.

## Pré‑requisitos

- .NET 6.0 SDK ou superior (o código também funciona no .NET Framework 4.7+).  
- Visual Studio 2022 (ou qualquer editor de sua preferência).  
- Pacote NuGet Aspose.OCR para .NET (`Aspose.OCR`).  
- Um arquivo de imagem (`letter_with_typos.png`) colocado em algum local que você possa referenciar a partir do projeto.

Se você nunca usou Aspose antes, não se preocupe — instalar o pacote é tão fácil quanto executar:

```bash
dotnet add package Aspose.OCR
```

Agora vamos mergulhar na implementação.

## Etapa 1: Configurar o Projeto e Instalar Aspose.OCR

Crie um novo projeto console e adicione a biblioteca OCR:

```bash
dotnet new console -n OcrSpellDemo
cd OcrSpellDemo
dotnet add package Aspose.OCR
```

Depois que a restauração terminar, abra `Program.cs`. Substituiremos o conteúdo padrão pelo código completo do demo mais adiante, mas primeiro vamos entender por que cada namespace é importante.

- `Aspose.OCR` – Núcleo do motor OCR e manipulação de imagens.  
- `Aspose.OCR.SpellCheck` – Utilitários de verificação ortográfica que acompanham a biblioteca.  
- `System` – Classes base padrão do .NET (ex.: `Console`).

## Etapa 2: Carregar a Imagem e Executar OCR em Imagem

O primeiro trabalho real é alimentar a imagem ao motor OCR. Aspose.OCR lê muitos formatos (PNG, JPEG, TIFF). Aqui está o trecho que faz o trabalho pesado:

```csharp
// Step 2: Load the image that contains the text to be recognized
var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

// Step 3: Perform OCR to extract the raw text from the image
var ocrEngine = new OcrEngine();
var ocrResult = ocrEngine.Recognize(image);
```

> **Por que isso importa:** `OcrImage.FromFile` abstrai os detalhes de nível de pixel, enquanto `OcrEngine.Recognize` executa o modelo neural treinado que traduz glifos visuais em caracteres Unicode. A propriedade `ocrResult.Text` agora contém a string bruta — exatamente o que você precisa para **extrair texto de imagem**.

> **Dica profissional:** Se sua imagem contiver múltiplos idiomas, você pode definir `ocrEngine.Language = OcrLanguage.Multilingual;` antes de chamar `Recognize`.

## Etapa 3: Inicializar o Verificador Ortográfico em Inglês

Aspose.OCR vem com um motor de verificação ortográfica interno que entende inglês pronto para uso. Inicializá‑lo é uma linha única:

```csharp
// Step 4: Initialise the English spell‑checker
var spellChecker = new SpellChecker(OcrLanguage.English);
```

> **Por que esta etapa é crucial:** A saída do OCR pode incluir caracteres reconhecidos incorretamente (ex.: “l” vs “1”) ou erros reais de digitação no documento original. O verificador ortográfico analisará a string, localizará tokens suspeitos e sugerirá alternativas.

## Etapa 4: Detectar Palavras com Erro de Ortografia e Obter Sugestões

Agora alimentamos o texto do OCR ao verificador:

```csharp
// Step 5: Check the recognized text for misspelled words and obtain suggestions
var misspellings = spellChecker.Check(ocrResult.Text);
```

`misspellings` é uma coleção onde cada entrada contém a palavra incorreta e um array de possíveis correções.

## Etapa 5: Exibir os Resultados

Por fim, iteramos sobre a coleção e imprimimos um relatório legível:

```csharp
// Step 6: Output each misspelled word together with its suggested corrections
foreach (var entry in misspellings)
{
    Console.WriteLine($"Misspelled: {entry.Word}");
    Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
}
```

### Saída Esperada no Console

Assumindo que `letter_with_typos.png` contenha a frase:

```
Ths is an exampel of a lettter with som misspelled wrds.
```

Executar o demo produzirá algo como:

```
Misspelled: Ths
  Suggestions: This, Thus, The
Misspelled: exampel
  Suggestions: example, exemplar, exampell
Misspelled: lettter
  Suggestions: letter, litter, lett
Misspelled: som
  Suggestions: some, sum, son
Misspelled: wrds
  Suggestions: words, wards, wryds
```

Observe como cada erro de digitação é acompanhado por algumas correções plausíveis — exatamente o que você precisa ao construir uma interface de correção amigável ao usuário.

## Exemplo Completo Funcional

Abaixo está o programa **completo, pronto‑para‑copiar‑e‑colar**. Substitua `YOUR_DIRECTORY` pelo caminho real do seu arquivo de imagem.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Load the image that contains the text to be recognized
        var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

        // Step 2: Perform OCR to extract the raw text from the image
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(image);

        // Step 3: Initialise the English spell‑checker
        var spellChecker = new SpellChecker(OcrLanguage.English);

        // Step 4: Check the recognized text for misspelled words and obtain suggestions
        var misspellings = spellChecker.Check(ocrResult.Text);

        // Step 5: Output each misspelled word together with its suggested corrections
        foreach (var entry in misspellings)
        {
            Console.WriteLine($"Misspelled: {entry.Word}");
            Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
        }

        // Optional: Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

> **Casos Limite a Considerar**  
> - **Imagem Vazia:** Se o motor OCR retornar uma string vazia, `spellChecker.Check` simplesmente retornará uma coleção vazia — sem falhas.  
> - **Texto Não‑Inglês:** Troque `OcrLanguage.English` por `OcrLanguage.French` (ou qualquer idioma suportado) para **detectar palavras com erro de ortografia** em outras localidades.  
> - **Documentos Grandes:** Para PDFs de várias páginas, você faria um loop sobre cada página, executaria OCR e então agregaria os resultados antes da verificação ortográfica.

## Visão Geral Visual (Texto Alternativo da Imagem)

![Diagrama mostrando o fluxo para executar OCR em imagem, extrair texto de imagem e depois detectar palavras com erro de ortografia com sugestões de correção](perform-ocr-on-image-flow.png)

*O diagrama acima ilustra o pipeline de ponta a ponta: imagem → motor OCR → texto bruto → verificador ortográfico → sugestões.*

## Perguntas Frequentes & Dicas Profissionais

| Pergunta | Resposta |
|----------|----------|
| **Preciso de conexão com a internet?** | Não. Aspose.OCR funciona totalmente localmente; ideal para ambientes offline ou seguros. |
| **Quão preciso é o verificador ortográfico?** | Ele usa um dicionário de ~150 k palavras em inglês e correspondência aproximada, então a maioria dos erros comuns são capturados. |
| **Posso personalizar o dicionário?** | Sim. `SpellChecker.AddUserDictionary("custom.txt")` permite carregar termos específicos de domínio (ex.: nomes de produtos). |
| **E se a imagem estiver inclinada?** | O motor OCR detecta a orientação automaticamente, mas você pode chamar manualmente `ocrEngine.ImagePreprocessing.Rotate(angle)` para casos difíceis. |
| **Existe uma forma de destacar sugestões na UI?** | Depois de obter a coleção `misspellings`, você pode mapear cada `entry.Word` de volta à sua posição em `ocrResult.Text` e sublinhá‑la em um RichTextBox ou visualização web. |

## Conclusão

Acabamos de mostrar **como executar OCR em imagem**, **extrair texto de imagem** e então **detectar palavras com erro de ortografia** enquanto **obtemos sugestões de correção** — tudo com um conciso aplicativo console C#. A ideia central é simples: deixe o Aspose.OCR fazer o trabalho pesado de reconhecer caracteres e, em seguida, use seu verificador ortográfico interno para limpar a saída. A partir daqui você pode expandir o demo para um serviço completo de processamento de documentos, integrá‑lo a uma API web ou conectá‑lo a um editor desktop.

Pronto para o próximo passo? Experimente trocar o idioma para espanhol, processar um PDF de várias páginas ou criar uma pequena interface WPF que permita ao usuário clicar em uma palavra para aceitar a sugestão. Os blocos de construção já estão no lugar — basta continuar experimentando.

Se você encontrou algum obstáculo ou tem ideias para extensões, deixe um comentário abaixo. Boa codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Extrair texto de imagem C# com seleção de idioma usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extrair Texto de Imagem Usando Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extrair Texto de Imagem – Otimização de OCR com Aspose.OCR para .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}