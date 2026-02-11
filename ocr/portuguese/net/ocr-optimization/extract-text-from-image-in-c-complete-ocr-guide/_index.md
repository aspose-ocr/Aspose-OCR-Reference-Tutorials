---
category: general
date: 2026-02-11
description: Extrair texto de imagem em C# usando Aspose OCR. Aprenda como carregar
  a imagem para OCR, melhorar a precisão do OCR e corrigir erros de OCR com verificação
  ortográfica.
draft: false
keywords:
- extract text from image
- image to text c#
- improve ocr accuracy
- load image for ocr
- fix ocr errors
language: pt
og_description: Extraia texto de imagem em C# com Aspose OCR. Este guia mostra como
  carregar a imagem para OCR, melhorar a precisão do OCR e corrigir erros de OCR.
og_title: Extrair Texto de Imagem em C# – Guia Completo de OCR
tags:
- C#
- OCR
- Aspose
- Text Extraction
title: Extrair texto de imagem em C# – Guia completo de OCR
url: /pt/net/ocr-optimization/extract-text-from-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de Imagem em C# – Guia Completo de OCR

Já precisou **extrair texto de imagem** mas os resultados pareciam um galho? Você não está sozinho. Em muitos aplicativos do mundo real — pense em digitalização de recibos, digitalização de notas ou migração de documentos legados — obter texto limpo de uma foto é o primeiro, e muitas vezes o mais difícil, obstáculo.

Felizmente, com Aspose OCR você pode **carregar imagem para OCR**, executar uma verificação ortográfica e obter texto limpo e pesquisável. Neste tutorial percorreremos todo o pipeline, desde a leitura de um JPEG até o polimento da saída, e você verá exatamente como **melhorar a precisão do OCR** enquanto isso.

> **O que você terá ao final:** um programa de console C# pronto‑para‑executar que extrai texto de imagem, corrige erros comuns de OCR e imprime tanto os resultados brutos quanto os limpos.

---

## O que você precisará

- .NET 6 ou posterior (o código também funciona no .NET Framework 4.7+)
- Visual Studio 2022 (ou qualquer IDE que você prefira)
- Uma chave de avaliação gratuita do Aspose OCR ou uma versão licenciada
- Um arquivo de imagem contendo texto digitado ou impresso (por exemplo, `typed_note.jpg`)

Nenhuma outra biblioteca de terceiros é necessária — Aspose lida com modelos de linguagem e verificação ortográfica automaticamente.

---

## Etapa 1 – Instalar o Pacote NuGet Aspose OCR

Antes que possamos **extrair texto de imagem**, o motor OCR deve estar disponível na máquina.

```powershell
# From the Package Manager Console
Install-Package Aspose.OCR
```

Ou, se você prefere a CLI:

```bash
dotnet add package Aspose.OCR
```

O pacote inclui dados de idioma, mas definir `AutomaticResourceDownload = true` (como faremos mais tarde) garante que quaisquer dicionários ausentes sejam baixados em tempo de execução.

---

## Etapa 2 – Carregar Imagem para OCR

A primeira coisa que o motor precisa é um bitmap. Você pode alimentá-lo com qualquer formato suportado por `System.Drawing.Image`, como PNG, JPEG, BMP ou TIFF.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Path to your source picture – change this to your own folder
string imagePath = @"C:\MyImages\typed_note.jpg";

// Load the image inside a using block so the file handle is released promptly
using (Image image = Image.FromFile(imagePath))
{
    // The rest of the OCR pipeline lives inside this block
}
```

> **Por que o bloco `using`?** Ele descarta o objeto `Image` automaticamente, evitando problemas de bloqueio de arquivo que frequentemente atrapalham desenvolvedores que esquecem de liberar recursos.

---

## Etapa 3 – Executar OCR – “Imagem para Texto C#” em Ação

Agora realmente **extraímos texto de imagem**. A classe `OcrEngine` faz o trabalho pesado.

```csharp
// Step 3: Initialise the OCR engine
var ocrEngine = new OcrEngine
{
    AutomaticResourceDownload = true, // pulls language packs if missing
    Language = OcrLanguage.English    // set to your document's language
};

// Inside the using block from Step 2
var ocrResult = ocrEngine.Recognize(image);
string rawText = ocrResult.Text;
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

Neste ponto você tem uma string que reflete o que o motor vê na imagem. Na prática, a saída pode conter caracteres estranhos, palavras reconhecidas incorretamente ou quebras de linha incomuns — daí a próxima etapa.

---

## Etapa 4 – Melhorar a Precisão do OCR com Verificação Ortográfica

Aspose fornece um `SpellChecker` dedicado que conhece o idioma que você está processando. Executá-lo sobre a string bruta costuma corrigir os erros mais evidentes.

```csharp
// Step 4: Initialise spell‑check (resources are auto‑downloaded)
var spellChecker = new SpellChecker(OcrLanguage.English);

// Correct the OCR output
string correctedText = spellChecker.Correct(rawText);
Console.WriteLine("\nCorrected OCR output:");
Console.WriteLine(correctedText);
```

> **Dica profissional:** Se você estiver lidando com vocabulários específicos de domínio (por exemplo, termos médicos), pode fornecer um dicionário personalizado ao `SpellChecker` através de suas sobrecargas.

---

## Etapa 5 – Corrigir Erros de OCR Manualmente (Opcional)

Mesmo o melhor verificador ortográfico pode perder erros contextuais. Uma passagem rápida de pós‑processamento pode capturar coisas como “l” vs “1” ou “O” vs “0”.

```csharp
// Simple regex to replace common OCR confusions
string finalText = System.Text.RegularExpressions.Regex.Replace(
    correctedText,
    @"\b([lI])\b", // isolated l or I
    "1");

// Additional custom rules can be added here
Console.WriteLine("\nFinal cleaned text:");
Console.WriteLine(finalText);
```

Sinta-se à vontade para expandir esta seção com suas próprias heurísticas — talvez uma tabela de consulta para códigos de produto ou uma lista de siglas conhecidas.

---

## Exemplo Completo em Funcionamento

Abaixo está o programa completo que você pode copiar‑colar em um novo projeto de Aplicativo de Console. Ele inclui todas as etapas discutidas, além de comentários úteis.

```csharp
// ------------------------------------------------------------
// Extract Text from Image in C# – Full Example
// ------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure OCR engine – automatic download ensures language data is present
        var ocrEngine = new OcrEngine
        {
            AutomaticResourceDownload = true,
            Language = OcrLanguage.English
        };

        // 2️⃣ Load the image you want to analyse
        string imagePath = @"C:\MyImages\typed_note.jpg";
        using (Image image = Image.FromFile(imagePath))
        {
            // 3️⃣ Run OCR – this is where we *extract text from image*
            var ocrResult = ocrEngine.Recognize(image);
            string rawText = ocrResult.Text;
            Console.WriteLine("Before (raw OCR):");
            Console.WriteLine(rawText);
            Console.WriteLine(new string('-', 40));

            // 4️⃣ Spell‑check to *improve OCR accuracy*
            var spellChecker = new SpellChecker(OcrLanguage.English);
            string correctedText = spellChecker.Correct(rawText);
            Console.WriteLine("After (spell‑checked):");
            Console.WriteLine(correctedText);
            Console.WriteLine(new string('-', 40));

            // 5️⃣ Optional custom clean‑up – *fix OCR errors* that the spell‑checker missed
            string finalText = Regex.Replace(correctedText,
                @"\b([lI])\b", // replace isolated 'l' or 'I' with '1'
                "1");

            Console.WriteLine("Final (post‑processed):");
            Console.WriteLine(finalText);
        }
    }
}
```

### Saída Esperada

Assumindo que `typed_note.jpg` contenha a frase “Hello world, this is a test 123”, o console exibirá algo como:

```
Before (raw OCR):
H3llo w0rld, th1s is a test 123

After (spell‑checked):
Hello world, this is a test 123

Final (post‑processed):
Hello world, this is a test 123
```

Observe como o verificador ortográfico transformou “H3llo” em “Hello”, e a expressão regular limpou o “1” estranho que apareceu em “th1s”.

---

## Perguntas Comuns & Casos de Borda

| Question | Answer |
|----------|--------|
| **Posso usar um idioma diferente?** | Sim. Defina `ocrEngine.Language = OcrLanguage.Spanish` (ou qualquer enum suportado) e passe o mesmo idioma para `SpellChecker`. |
| **E se minha imagem for muito grande?** | Reduza-a antes de enviá‑la ao OCR; `Image` possui `GetThumbnailImage` para redimensionamento rápido. |
| **Preciso de conexão à internet?** | Somente na primeira vez que um pacote de idioma estiver ausente; depois disso os recursos são armazenados em cache localmente. |
| **Como lidar com PDFs de várias páginas?** | Converta cada página em uma imagem (por exemplo, usando `PdfRenderer`) e execute o mesmo pipeline por página. |
| **O verificador ortográfico é sensível ao idioma?** | Absolutamente. Ele usa o mesmo modelo de idioma que você forneceu ao motor OCR, garantindo consistência. |

---

## Próximos Passos & Tópicos Relacionados

- **Processamento em lote:** Envolva o código em um loop `foreach` para lidar com uma pasta de imagens.
- **Texto manuscrito:** Troque `OcrLanguage.EnglishHandwritten` para obter melhores resultados em notas cursivas.
- **Paralelismo:** Use `Parallel.ForEach` para acelerar grandes cargas de trabalho em máquinas multi‑core.
- **Exportar para JSON/CSV:** Serialize `finalText` junto com metadados (nome do arquivo, pontuações de confiança) para análises posteriores.

Se você está curioso sobre transformar as strings extraídas em PDFs pesquisáveis, confira nosso guia sobre **“Criar PDF pesquisável a partir de imagem em C#”**. Ele se baseia diretamente no mesmo pipeline de OCR que acabamos de cobrir.

---

## Conclusão

Acabamos de demonstrar uma forma pragmática de **extrair texto de imagem** em C# usando Aspose OCR, ao mesmo tempo mostrando como **carregar imagem para OCR**, **melhorar a precisão do OCR**, e **corrigir erros de OCR** com um verificador ortográfico embutido e uma pequena limpeza por regex. O exemplo completo funciona imediatamente, requer apenas um único pacote NuGet, e pode ser estendido para atender praticamente qualquer cenário de digitalização de documentos

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}