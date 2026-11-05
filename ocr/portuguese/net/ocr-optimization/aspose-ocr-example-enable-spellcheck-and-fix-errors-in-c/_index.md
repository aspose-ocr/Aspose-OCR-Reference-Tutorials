---
category: general
date: 2026-03-07
description: Exemplo de OCR da Aspose mostrando como habilitar a verificação ortográfica,
  adicionar um dicionário personalizado, carregar OCR de imagem e corrigir erros de
  OCR rapidamente.
draft: false
keywords:
- aspose ocr example
- how to enable spellcheck
- how to add dictionary
- load image ocr
- how to fix ocr errors
language: pt
og_description: Aspose OCR example that walks you through enabling spellcheck, adding
  a custom dictionary, loading an image for OCR and fixing common OCR errors.
og_title: Exemplo de OCR da Aspose – Ativar Verificação Ortográfica e Corrigir Erros
tags:
- Aspose
- OCR
- C#
- SpellCheck
title: Exemplo de OCR Aspose – Habilitar verificação ortográfica e corrigir erros
  em C#
url: /pt/net/ocr-optimization/aspose-ocr-example-enable-spellcheck-and-fix-errors-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exemplo Aspose OCR – Ativar Verificação Ortográfica e Corrigir Erros em C#

Já precisou de um **exemplo Aspose OCR** que não apenas leia texto de uma imagem, mas também limpe aqueles irritantes erros ortográficos? Você não está sozinho. Em muitos projetos do mundo real, a saída bruta do OCR está repleta de erros de digitação, especialmente quando a imagem de origem contém fontes de baixo contraste ou anotações manuscritas.  

A boa notícia? Com Aspose.OCR você pode **ativar a verificação ortográfica**, inserir seu próprio dicionário e obter uma string refinada em apenas algumas linhas de código. A seguir, você verá exatamente **como ativar a verificação ortográfica**, **como adicionar um dicionário**, e **como carregar OCR de imagem** para que finalmente possa **corrigir erros de OCR** sem perder a paciência.

Neste tutorial, cobriremos tudo o que você precisa — desde a instalação via NuGet até um programa completo e executável que imprime o texto corrigido. Ao final, você terá um **exemplo Aspose OCR** robusto que pode ser inserido diretamente em qualquer projeto .NET.

## Pré-requisitos

- .NET 6.0 SDK ou posterior (o código funciona também com .NET Core e .NET Framework)
- Visual Studio 2022 ou qualquer IDE compatível com C#
- Um arquivo de imagem (`typed_text.png`) que contém texto em inglês claro e digitado
- Acesso à internet para baixar o pacote NuGet Aspose.OCR

Nenhuma outra biblioteca de terceiros é necessária.

---

## Etapa 1 – Instalar o Pacote NuGet Aspose.OCR (Carregar OCR de Imagem)

Antes de podermos escrever qualquer código, precisamos da biblioteca que alimenta o motor OCR.

```bash
dotnet add package Aspose.OCR
```

> **Dica profissional:** Se você estiver usando o Visual Studio, clique com o botão direito no projeto → *Gerenciar Pacotes NuGet* → procure por **Aspose.OCR** e clique em *Instalar*.  

Instalar o pacote lhe dá acesso a `OcrEngine`, `ImageStream` e às utilidades de verificação ortográfica integradas que usaremos mais adiante. Uma vez que o pacote esteja instalado, você está pronto para **carregar OCR de imagem**.

## Etapa 2 – Criar a Instância do Motor OCR

Criar o motor é o primeiro passo concreto em qualquer **exemplo Aspose OCR**. Pense no `OcrEngine` como o cérebro que analisará o bitmap e gerará texto.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Step 2: Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

O construtor `OcrEngine` não requer parâmetros, o que o torna simples e organizado para protótipos rápidos.

## Etapa 3 – Como Ativar a Verificação Ortográfica (e Por Que É Importante)

A saída bruta do OCR frequentemente contém palavras reconhecidas incorretamente, como “teh” em vez de “the”. Ativar o corretor ortográfico integrado permite que o Aspose substitua automaticamente esses erros pela ortografia mais provável.

```csharp
// Step 3: Turn on spell checking and set the language to English
ocrEngine.Settings.SpellCheck.Enabled = true;
ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;
```

> **Por que ativar a verificação ortográfica?**  
> - **Precisão:** Uma verificação ortográfica pós‑processamento pode aumentar a precisão geral do texto em 10‑15 % para documentos impressos.  
> - **Experiência do usuário:** Texto limpo significa menos limpeza posterior ao alimentar o resultado em índices de busca ou pipelines de análise.

## Etapa 4 – Como Adicionar um Dicionário (Palavras Personalizadas)

Às vezes o dicionário padrão não conhece os nomes da sua marca, códigos de produto ou jargões específicos do domínio. É aí que **como adicionar dicionário** entra em ação.

```csharp
// Step 4: Add custom words that the spell checker should accept
ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
{
    "AsposeOCR",   // our library name
    "OCRify",      // a fictional product
    "CSharpify"    // another custom term
});
```

Você pode fornecer um array, uma lista ou até ler de um arquivo se possuir um vocabulário personalizado grande. O corretor ortográfico agora tratará essas entradas como válidas, evitando correções falsas.

## Etapa 5 – Carregar a Imagem para OCR (Carregar OCR de Imagem)

Agora que o motor está configurado, precisamos apontá‑lo para a imagem que queremos ler. O helper `ImageStream.FromFile` abstrai os detalhes de leitura de arquivo.

```csharp
// Step 5: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");
```

> **Dica:** Se sua imagem estiver em uma subpasta do projeto, defina a propriedade *Copy to Output Directory* como *Copy always* para que o caminho seja resolvido em tempo de execução.

## Etapa 6 – Executar o Reconhecimento e Corrigir Erros de OCR

Com tudo configurado, uma única chamada a `Recognize()` executa o pipeline OCR, aplica a verificação ortográfica e armazena o resultado limpo em `ocrEngine.Text`.

```csharp
// Step 6: Run OCR and let the spell checker clean the output
ocrEngine.Recognize();

// Step 7: Output the corrected text to the console
Console.WriteLine("Corrected text:");
Console.WriteLine(ocrEngine.Text);
```

### Saída Esperada

Assumindo que `typed_text.png` contenha a frase `The quick brown fox jumps over teh lazy dog`, o console exibirá:

```
Corrected text:
The quick brown fox jumps over the lazy dog
```

Observe como “teh” foi automaticamente corrigido para “the”. Se você tivesse adicionado “OCRify” ao dicionário personalizado e a imagem contivesse essa palavra, o motor a manteria intacta.

---

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

Abaixo está o programa completo que você pode inserir em um novo projeto de console. Ele inclui todas as etapas acima, além de alguns comentários para clareza.

```csharp
// ---------------------------------------------------------------
// Aspose OCR Example – Enable Spellcheck and Fix Errors
// ---------------------------------------------------------------

using System;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable spell checking (how to enable spellcheck)
            ocrEngine.Settings.SpellCheck.Enabled = true;
            ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;

            // 3️⃣ Add custom words (how to add dictionary)
            ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
            {
                "AsposeOCR",
                "OCRify",
                "CSharpify"
            });

            // 4️⃣ Load the image (load image OCR)
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");

            // 5️⃣ Run OCR – this also fixes common OCR errors (how to fix ocr errors)
            ocrEngine.Recognize();

            // 6️⃣ Show the corrected result
            Console.WriteLine("Corrected text:");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

Salve isto como `Program.cs`, execute `dotnet run`, e você deverá ver a frase corrigida impressa no console.

---

## Perguntas Frequentes & Casos Limite

| Pergunta | Resposta |
|----------|----------|
| **E se a imagem for um PDF de várias páginas?** | Aspose.OCR pode lidar com páginas de PDF como imagens. Use `ocrEngine.Image = ImageStream.FromPdf("file.pdf", pageNumber: 1);` e faça um loop pelas páginas. |
| **Posso mudar o idioma para algo diferente do inglês?** | Claro. Defina `ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.French;` (ou qualquer idioma suportado). |
| **Meu dicionário personalizado é enorme — isso afetará o desempenho?** | Adicionar milhares de palavras gera um pequeno custo inicial, mas a busca é O(1) graças a um hash‑set interno. Para vocabulários massivos, considere carregá‑los uma única vez na inicialização da aplicação. |
| **E se o motor OCR lançar uma exceção ao processar uma imagem corrompida?** | Envolva `Recognize()` em um bloco try‑catch e verifique `ocrEngine.LastError`. Você também pode pré‑validar as dimensões da imagem com `ocrEngine.Image.Width` e `Height`. |
| **Preciso de uma licença para uso em produção?** | A avaliação gratuita funciona para testes, mas uma licença comercial remove a marca d'água de avaliação e desbloqueia o desempenho total. |

---

## Conclusão

Agora você tem um **exemplo completo Aspose OCR** que demonstra **como ativar a verificação ortográfica**, **como adicionar um dicionário**, **carregar OCR de imagem**, e **como corrigir erros de OCR** de forma limpa e pronta para produção. Ao configurar o corretor ortográfico e fornecer uma lista de palavras personalizada, você melhora drasticamente a qualidade do texto extraído sem precisar escrever nenhuma lógica de pós‑processamento.

Pronto para o próximo passo? Experimente trocar o idioma para espanhol, alimentar um PDF de várias páginas ou integrar a saída em um índice pesquisável do Azure Cognitive Search. O mesmo padrão se aplica — basta ajustar a bandeira de idioma e, talvez, expandir o dicionário personalizado.

Se você achou este guia útil, dê uma estrela no GitHub, compartilhe com os colegas ou deixe um comentário abaixo. Boa codificação, e que seus resultados de OCR estejam sempre livres de erros!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}