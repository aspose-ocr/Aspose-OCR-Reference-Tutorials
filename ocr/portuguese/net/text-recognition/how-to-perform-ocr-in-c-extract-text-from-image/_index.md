---
category: general
date: 2026-04-03
description: Aprenda a realizar OCR em C# e extrair texto de imagens usando o Aspose
  OCR, com verificação ortográfica para o idioma russo.
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- how to spell check
- ocr russian language
language: pt
og_description: Aprenda a realizar OCR em C# e extrair texto de imagens usando o Aspose
  OCR, com verificação ortográfica para o idioma russo.
og_title: Como fazer OCR em C# – Extrair texto de imagem
tags:
- OCR
- C#
- Aspose
- SpellCheck
title: Como Realizar OCR em C# – Extrair Texto de Imagem
url: /pt/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Realizar OCR em C# – Extrair Texto de Imagem

Já se perguntou **como realizar OCR** em uma foto de um bilhete manuscrito? Talvez você tenha um recibo escaneado, uma placa em idioma estrangeiro ou uma página PDF que se recusa a copiar‑colar. A boa notícia? Com algumas linhas de C# e a biblioteca Aspose OCR você pode transformar essa imagem em texto editável num instante.  

Neste guia não apenas mostraremos **como realizar OCR**, mas também percorreremos **extrair texto de imagem**, **converter imagem em texto** e ainda **como fazer correção ortográfica** do resultado ao lidar com documentos em russo. Parece muito? Fique conosco – vamos dividir tudo passo a passo.

## O Que Você Vai Aprender

Ao final deste tutorial você será capaz de:

* Configurar o Aspose OCR para suporte ao idioma russo.  
* Carregar um arquivo de imagem e executar reconhecimento óptico de caracteres para **extrair texto de imagem**.  
* Usar o corretor ortográfico embutido para corrigir automaticamente palavras erradas – a resposta perfeita para “**como fazer correção ortográfica**” da saída de OCR.  
* Imprimir a string limpa no console, pronta para processamento ou armazenamento adicional.

**Pré‑requisitos** – você precisará de:

* .NET 6.0 ou superior (o código também funciona com .NET Framework 4.8).  
* Uma licença válida do Aspose OCR ou uma chave de avaliação temporária.  
* Um arquivo de imagem que contenha texto em russo (para a demonstração chamaremos de `russian_note.jpg`).  

Se algum desses itens lhe for desconhecido, não se preocupe. Os passos abaixo incluem o comando NuGet exato para obter o Aspose OCR, e o código está totalmente autocontido.

![exemplo de como realizar OCR](/images/ocr-demo.png "exemplo de como realizar OCR em C#")

## Etapa 1 – Instalar Aspose OCR e Adicionar Namespaces

Primeiro de tudo, você precisa da biblioteca. Abra um terminal na pasta do seu projeto e execute:

```bash
dotnet add package Aspose.OCR
```

Esse comando traz a versão estável mais recente (em abril 2026 é 22.9). Após a restauração do pacote, adicione as diretivas `using` necessárias no topo do seu arquivo C#:

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;
```

*Dica:* Se você estiver usando o Visual Studio, a IDE sugerirá a adição automática dessas diretivas assim que você digitar o nome da primeira classe.

## Etapa 2 – Inicializar o Motor OCR para Idioma Russo

A parte **como realizar OCR** começa com a criação de uma instância `OcrEngine`. Ao especificar `OcrLanguage.Russian` informamos ao motor que ele deve carregar o conjunto de caracteres cirílicos e as heurísticas específicas do idioma.

```csharp
// Step 2: Initialise OCR engine for Russian
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Russian   // Enables Russian language support
};
```

Por que isso é importante? Sem definir o idioma, o motor usa inglês por padrão e interpretará muitos caracteres cirílicos de forma errada, gerando saída confusa. Configurar explicitamente o idioma melhora a precisão drasticamente.

## Etapa 3 – Carregar a Imagem e **Converter Imagem em Texto**

Agora trazemos a foto para a memória. O método `Image.FromFile` funciona com a maioria dos formatos comuns (JPG, PNG, BMP). Após o carregamento, chamamos `Recognize` para **converter imagem em texto**.

```csharp
// Step 3: Load the image that contains Russian text
Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

// Step 4: Perform OCR – this is the core “how to perform OCR” call
string rawText = ocrEngine.Recognize(sourceImage);
```

A variável `rawText` agora contém a saída bruta do OCR, que ainda pode ter erros de digitação ou caracteres reconhecidos incorretamente. Você pode imprimi‑la para ver o que o motor capturou:

```csharp
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

## Etapa 4 – **Como Fazer Correção Ortográfica** no Resultado do OCR

OCR em russo pode ser ruidoso, especialmente com digitalizações de baixa resolução. A Aspose fornece a classe `SpellChecker` que entende dicionários russos prontamente. Veja como invocá‑la:

```csharp
// Step 5: Initialise the spell checker
SpellChecker spellChecker = new SpellChecker();

// Step 6: Correct spelling mistakes in the recognized text
string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);
```

O método `CheckAndCorrect` devolve uma nova string onde palavras incorretas são substituídas pelas alternativas mais prováveis. Ele também respeita a pontuação, evitando que você acabe com um bloco de texto sem formatação.

*Caso extremo:* Se a saída do OCR estiver vazia (por exemplo, a imagem for totalmente branca), `CheckAndCorrect` simplesmente retornará uma string vazia. É recomendável proteger contra isso caso você pretenda gravar o resultado em um arquivo.

## Etapa 5 – Exibir o Resultado Limpo

Por fim, exibimos a string corrigida. Em um aplicativo real você poderia gravá‑la em um banco de dados, em uma API JSON ou em um documento Word. Para esta demonstração, imprimir no console já basta:

```csharp
// Step 7: Show the corrected result
Console.WriteLine("\nCorrected text:");
Console.WriteLine(correctedText);
```

Ao executar o programa, você deverá ver algo como:

```
Raw OCR output:
Привeт мир! Этo тeкcт c русcкoй оcнoвнoй.

Corrected text:
Привет мир! Это текст с русской основой.
```

Observe como o corretor ortográfico transformou “Привeт” (e latino misturado) no correto cirílico “Привет”. Essa é a magia de **como fazer correção ortográfica** da saída de OCR.

## Exemplo Completo Funcional

Abaixo está o programa completo e executável que reúne todas as etapas. Copie‑e‑cole em um novo projeto de console e pressione **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine configured for Russian language
        OcrEngine ocrEngine = new OcrEngine { Language = OcrLanguage.Russian };

        // Step 2: Load the image that contains the text to be recognized
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

        // Step 3: Perform OCR to extract raw text from the image
        string rawText = ocrEngine.Recognize(sourceImage);

        // Optional: Show raw OCR output
        System.Console.WriteLine("Raw OCR output:");
        System.Console.WriteLine(rawText);

        // Step 4: Initialise the spell checker
        SpellChecker spellChecker = new SpellChecker();

        // Step 5: Correct spelling mistakes in the recognized text
        string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);

        // Step 6: Display the corrected result
        System.Console.WriteLine("\nCorrected text:");
        System.Console.WriteLine(correctedText);
    }
}
```

### Saída Esperada

Executar o programa com uma foto clara e de alta resolução de escrita manual russa normalmente produz uma frase limpa e legível. Se a imagem estiver borrada, ainda podem aparecer palavras parcialmente corretas, mas o corretor ortográfico suavizará a maioria dos erros óbvios.

## Armadilhas Comuns & Dicas

| Problema | Por Que Acontece | Como Corrigir / Evitar |
|----------|------------------|------------------------|
| **Caracteres estranhos** | DPI baixo ou fundo ruidoso | Pré‑processar a imagem (aumentar contraste, redimensionar para ≥300 dpi) antes de chamar `Recognize`. |
| **Saída vazia** | Caminho de arquivo errado ou formato não suportado | Verifique o caminho e use `Image.FromFile` dentro de um bloco `try/catch` para exibir erros. |
| **Corretor ortográfico não detecta erros** | Palavras raras fora do dicionário | Amplie o dicionário carregando uma lista personalizada via `spellChecker.AddUserDictionary("mywords.txt")`. |
| **Desempenho lento em lotes grandes** | OCR consome muita CPU | Execute OCR em uma thread em segundo plano ou use `Parallel.ForEach` para múltiplas imagens. |
| **Exceção de licença** | Uso da versão de avaliação além do período de teste | Adquira uma licença e chame `License license = new License(); license.SetLicense("Aspose.Total.lic");` antes de criar `OcrEngine`. |

## Próximos Passos – Indo Além do OCR Simples

Agora que você dominou **como realizar OCR**, considere estas extensões:

* **Processamento em lote** – Percorra uma pasta de imagens e grave cada texto corrigido em um arquivo `.txt`.  
* **Conversão para PDF** – Use Aspose PDF para inserir o texto extraído de volta em um PDF pesquisável.  
* **Detecção de idioma** – Se precisar lidar com vários idiomas, inspecione primeiro o resultado do OCR e altere `OcrLanguage` conforme necessário.  
* **Integração com Azure Cognitive Services** – Compare os resultados da Aspose com a API OCR da Microsoft para uma abordagem híbrida.

Todos esses tópicos naturalmente envolvem as palavras‑chave secundárias **extrair texto de imagem**, **converter imagem em texto** e **como fazer correção ortográfica**, então

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}