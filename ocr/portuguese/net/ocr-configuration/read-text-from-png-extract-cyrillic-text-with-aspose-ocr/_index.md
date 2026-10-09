---
category: general
date: 2026-03-07
description: Aprenda a ler texto de arquivos PNG e extrair texto cirílico usando o
  Aspose OCR, converter a imagem em texto e baixar o pacote de idioma cirílico.
draft: false
keywords:
- read text from png
- extract cyrillic text
- convert image to text
- load image for ocr
- download cyrillic language pack
language: pt
og_description: Aprenda a ler texto de PNG, extrair texto cirílico e converter imagem
  em texto usando o Aspose OCR em C#.
og_title: ler texto de PNG – extrair texto cirílico com Aspose OCR
tags:
- Aspose OCR
- C#
- Image Processing
title: Ler texto de PNG – extrair texto cirílico com Aspose OCR
url: /pt/net/ocr-configuration/read-text-from-png-extract-cyrillic-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ler texto de png – extrair texto cirílico com Aspose OCR

Precisa **ler texto de png** arquivos e extrair caracteres cirílicos? Neste guia vamos mostrar como ler texto de png usando Aspose OCR, extrair texto cirílico e **converter imagem em texto** em apenas algumas linhas de C#.  

Se você já ficou olhando para uma captura de tela de uma fatura russa e se perguntou como obter as palavras em uma string pesquisável, está no lugar certo. Também vamos mostrar como **baixar o pacote de idioma cirílico** automaticamente, para que você não precise procurar arquivos extras.

## O que você irá alcançar

* **Carregar uma imagem para OCR** diretamente do disco ou de um stream.  
* Defina o motor para **idioma Cirílico** sem downloads manuais.  
* Execute o reconhecimento e **extraia texto cirílico** de um arquivo PNG.  
* Veja o texto reconhecido impresso no console – um resultado limpo, em texto simples, que você pode inserir em bancos de dados, índices de busca ou qualquer outro fluxo de trabalho.

Sem serviços externos, sem chaves de nuvem, apenas o pacote NuGet Aspose OCR e algumas linhas de C#.

## Pré-requisitos

* .NET 6.0 ou superior (o código funciona em .NET Core, .NET Framework e .NET 5+).  
* Visual Studio 2022 ou qualquer editor de sua preferência.  
* O pacote NuGet Aspose.OCR (`dotnet add package Aspose.OCR`).  
* Uma imagem PNG que contenha caracteres cirílicos – por exemplo `cyrillic_sample.png` colocada em uma pasta chamada `YOUR_DIRECTORY`.

> **Dica profissional:** Se você estiver usando o Visual Studio, clique com o botão direito no projeto → **Gerenciar Pacotes NuGet** → procure por “Aspose.OCR” e instale a versão estável mais recente.

---

## Etapa 1 – Instalar Aspose OCR e criar o motor

Primeiro precisamos da instância do motor OCR. A classe `OcrEngine` é o ponto de entrada para todas as operações.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Create an OCR engine – this object holds all settings and results
var ocrEngine = new OcrEngine();
```

> **Por que isso importa:** O motor encapsula pacotes de idioma, dados de imagem e opções de reconhecimento. Instanciá‑lo uma vez e reutilizá‑lo em várias imagens pode melhorar o desempenho.

---

## Etapa 2 – **carregar imagem para ocr** e definir o idioma

Agora informamos ao motor qual imagem processar e qual idioma procurar. Definir `Language.Cyrillic` baixa automaticamente o pacote de idioma necessário na primeira execução.

```csharp
// 1️⃣ Load the PNG that contains Cyrillic text
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_sample.png");

// 2️⃣ Tell Aspose we want to read Cyrillic characters
ocrEngine.Settings.Language = Language.Cyrillic;   // downloads pack if missing
```

> **Caso extremo:** Se seu PNG for muito grande (mais de 5 MB) você pode querer redimensioná‑lo primeiro para acelerar o reconhecimento. A propriedade `Image` também aceita um `Stream`, permitindo carregar da memória, de uma requisição web ou de um Azure Blob sem tocar no sistema de arquivos.

---

## Etapa 3 – **converter imagem em texto** com uma única chamada

O reconhecimento é tão simples quanto invocar `Recognize()`. Após essa chamada, a propriedade `Text` contém a string extraída.

```csharp
// Run the OCR engine – this does the heavy lifting
ocrEngine.Recognize();

// Grab the result; it’s plain Unicode text
string extractedText = ocrEngine.Text;
```

> **O que acontece nos bastidores?** Aspose executa um classificador baseado em rede neural treinado com milhões de glifos cirílicos. A biblioteca abstrai toda essa complexidade, de modo que você obtém Unicode limpo.

---

## Etapa 4 – Exibir o resultado (ou encaminhá‑lo para outro lugar)

Para fins de demonstração, imprimiremos o texto no console, mas você pode facilmente gravá‑lo em um arquivo, em um banco de dados ou enviá‑lo para um índice de busca.

```csharp
// Show the OCR result in the console
Console.WriteLine("=== Recognized Cyrillic Text ===");
Console.WriteLine(extractedText);
```

**Saída esperada** (supondo que `cyrillic_sample.png` contenha a frase “Привет мир”):

```
=== Recognized Cyrillic Text ===
Привет мир
```

Se a saída parecer confusa, verifique se a imagem está nítida e se você definiu `Language.Cyrillic`. O motor usa English como padrão, o que trataria caracteres cirílicos como símbolos desconhecidos.

---

## Etapa 5 – Exemplo completo e executável

Juntando tudo, aqui está um programa autônomo que você pode copiar e colar em um novo projeto de console.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // 2️⃣ Load the PNG and select Cyrillic language
        // -------------------------------------------------
        // Replace the path with the location of your PNG
        ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_sample.png");
        ocrEngine.Settings.Language = Language.Cyrillic; // auto‑downloads pack

        // -------------------------------------------------
        // 3️⃣ Perform recognition
        // -------------------------------------------------
        ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== Recognized Cyrillic Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

Salve o arquivo como `Program.cs`, execute `dotnet run` e você deverá ver o texto cirílico impresso.

---

## Perguntas comuns & solução de problemas

| Pergunta | Resposta |
|----------|----------|
| **E se o pacote de idioma não for baixado?** | Verifique se a máquina tem acesso à internet. O pacote é armazenado em cache em `%USERPROFILE%\.Aspose\OCR\Languages`. Excluir essa pasta força um novo download. |
| **Posso ler outros idiomas além de cirílico?** | Claro – substitua `Language.Cyrillic` por `Language.English`, `Language.Arabic`, etc. A mesma lógica de download automático se aplica. |
| **Meu PNG está ruidoso – os resultados são ruins. O que posso fazer?** | Pré‑processar a imagem: aumentar o contraste, converter para escala de cinza ou aplicar um filtro mediano. Aspose OCR também oferece opções `Settings.ImagePreprocess`. |
| **Existe uma maneira de obter caixas delimitadoras para cada palavra?** | Sim, após `Recognize()` você pode inspecionar `ocrEngine.Regions`, que devolve retângulos para cada palavra detectada. |
| **Preciso de uma licença para uso em produção?** | A avaliação gratuita funciona para até 100 páginas. Para projetos comerciais adquira uma licença – ela remove a marca d’água de avaliação e desbloqueia o processamento em lote de alta velocidade. |

---

## Próximos passos – estendendo a solução

* **Processamento em lote:** Percorrer uma pasta de PNGs, coletar todos os textos em um arquivo CSV.  
* **Integração com Azure Cognitive Search:** Indexar as strings cirílicas extraídas para busca rápida.  
* **Combinar com conversão de PDF:** Use Aspose.PDF para converter PDFs escaneados em PNGs primeiro, então executar o mesmo fluxo OCR.  

Todos esses cenários reutilizam o padrão central que acabamos de cobrir: **carregar imagem para OCR → definir idioma → reconhecer → usar o texto**.

---

## Conclusão

Agora você sabe como **ler texto de png**, **extrair texto cirílico** e **converter imagem em texto** com Aspose OCR em C#. As etapas principais são criar o motor, carregar a imagem, selecionar o idioma correto (que baixa automaticamente o **pacote de idioma cirílico**), e finalmente chamar `Recognize()`.

Experimente com diferentes imagens, experimente as opções `Settings` e veja suas aplicações se tornarem pesquisáveis, multilíngues e muito mais inteligentes.  

Boa codificação, e sinta‑se à vontade para deixar um comentário se encontrar algum problema!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}