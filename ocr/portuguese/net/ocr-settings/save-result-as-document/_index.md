---
title: Salvar o resultado como documento no reconhecimento de imagem OCR
linktitle: Salvar o resultado como documento no reconhecimento de imagem OCR
second_title: API Aspose.OCR .NET
description: Desbloqueie o potencial do Aspose.OCR para .NET. Reconheça facilmente texto em imagens e salve resultados em vários formatos de documento.
weight: 10
url: /pt/net/ocr-settings/save-result-as-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salvar o resultado como documento no reconhecimento de imagem OCR

## Introdução

Bem-vindo ao emocionante mundo do reconhecimento óptico de caracteres (OCR) com Aspose.OCR para .NET! Neste tutorial abrangente, nos aprofundaremos nas complexidades do uso do Aspose.OCR para reconhecer texto em imagens e demonstraremos como salvar os resultados em vários formatos de documento.

## Pré-requisitos

Antes de embarcarmos nesta jornada de OCR, certifique-se de ter os seguintes pré-requisitos em vigor:

-  Aspose.OCR para .NET. Certifique-se de ter a biblioteca Aspose.OCR instalada. Você pode baixá-lo[aqui](https://releases.aspose.com/ocr/net/).

-  Diretório de documentos: tenha um diretório designado para seus documentos e atualize o`dataDir` variável no código fornecido de acordo.

## Importar namespaces

Comece importando os namespaces necessários. Esses são os blocos de construção que capacitarão seu código com recursos de OCR.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Agora, vamos dividir o exemplo em várias etapas:

## Etapa 1: inicializar Aspose.OCR

```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";

// Inicialize uma instância do AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Esta etapa prepara o cenário inicializando a API Aspose.OCR.

## Etapa 2: reconhecer a imagem

```csharp
// Reconhecer imagem
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

Aqui, usamos Aspose.OCR para reconhecer texto dentro da imagem especificada (substitua “sample.png” pelo seu arquivo de imagem).

## Etapa 3: salve o resultado em formatos diferentes

```csharp
// Salve o resultado no formato de sua preferência
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

Personalize esta etapa com base em suas necessidades. Aspose.OCR permite salvar o texto reconhecido em vários formatos de documento, como DOCX, TXT, PDF e XLSX.

## Etapa 4: exibir mensagem de sucesso

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

Uma simples mensagem de confirmação para informar que o processo foi concluído sem problemas.

Seguindo essas etapas, você aproveitou com sucesso o poder do Aspose.OCR for .NET para reconhecer texto em imagens e salvar os resultados em diferentes formatos de documento.

## Conclusão

Concluindo, Aspose.OCR for .NET abre um mundo de possibilidades para reconhecimento de texto em imagens. Esteja você extraindo dados ou criando documentos pesquisáveis, o Aspose.OCR simplifica o processo com sua API intuitiva.

## Perguntas frequentes

### Q1. O Aspose.OCR é compatível com diferentes formatos de imagem?

A1: Sim, o Aspose.OCR oferece suporte a uma ampla variedade de formatos de imagem, garantindo flexibilidade em suas tarefas de OCR.

### P2: Posso personalizar as configurações de reconhecimento para obter melhor precisão?

A2: Com certeza! Aspose.OCR fornece configurações de reconhecimento para ajustar o processo de OCR de acordo com seus requisitos específicos.

### Q3: Existe um teste gratuito disponível?

 A3: Sim, você pode começar com uma avaliação gratuita[aqui](https://releases.aspose.com/).

### Q4: Como posso obter licenças temporárias para Aspose.OCR?

 A4: Licenças temporárias podem ser obtidas[aqui](https://purchase.aspose.com/temporary-license/).

### P5: Onde posso procurar ajuda ou me conectar com a comunidade?

 A5: Junte-se à comunidade Aspose.OCR em[Aspor Fórum](https://forum.aspose.com/c/ocr/16) para apoio e discussões.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
