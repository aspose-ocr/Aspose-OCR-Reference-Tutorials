---
title: Especifique os caracteres permitidos no reconhecimento de imagem OCR
linktitle: Especifique os caracteres permitidos no reconhecimento de imagem OCR
second_title: API Aspose.OCR .NET
description: Desbloqueie OCR preciso em .NET com Aspose.OCR. Reconheça texto de imagens sem esforço. Baixe agora para uma experiência de desenvolvimento transformadora.
type: docs
weight: 13
url: /pt/net/ocr-settings/specify-allowed-characters/
---
## Introdução

No cenário em constante evolução da tecnologia, o reconhecimento óptico de caracteres (OCR) emergiu como uma ferramenta transformadora, permitindo que as máquinas compreendam texto a partir de imagens. Aspose.OCR for .NET se destaca como uma solução poderosa, fornecendo integração perfeita para desenvolvedores que buscam recursos robustos de OCR em seus aplicativos .NET.

## Pré-requisitos

Antes de mergulhar no tutorial, certifique-se de ter os seguintes pré-requisitos em vigor:

- Conhecimento prático de desenvolvimento .NET.
-  Biblioteca Aspose.OCR para .NET. Você pode baixá-lo[aqui](https://releases.aspose.com/ocr/net/).
- Familiaridade com Visual Studio ou qualquer outro ambiente de desenvolvimento .NET preferido.

## Importar namespaces

Em seu projeto .NET, importe os namespaces necessários para aproveitar as funcionalidades do Aspose.OCR for .NET de forma eficaz:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Agora, vamos dividir o tutorial em uma série de etapas abrangentes:

## Etapa 1: especificar caracteres permitidos no reconhecimento de imagem OCR

Para começar, configure o caminho para o diretório do seu documento:

```csharp
string dataDir = "Your Document Directory";
```

## Etapa 2: inicializar Aspose.OCR com símbolos permitidos

Crie uma instância de AsposeOcr, especificando os símbolos permitidos. Neste caso, estamos permitindo dígitos (0-9):

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

## Etapa 3: reconhecer a imagem

Utilize a instância AsposeOcr para reconhecer o texto de uma imagem:

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

## Etapa 4: exibir texto reconhecido

Imprima o texto reconhecido no console:

```csharp
Console.WriteLine(result);
```

## Etapa 5: Segundo caso – Reconhecer imagem com configurações específicas

Inicialize outra instância do AsposeOcr, desta vez com configurações mais específicas:

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

## Etapa 6: exibir o texto reconhecido do segundo caso

Imprima o texto reconhecido do segundo caso no console:

```csharp
Console.WriteLine(result2.RecognitionText);
```

## Etapa 7: Execução bem-sucedida

Por fim, confirme a execução bem-sucedida do tutorial SpecificAllowedCharacters:

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Seguindo essas etapas, você desbloqueou a capacidade de especificar caracteres permitidos no reconhecimento de imagem OCR usando Aspose.OCR for .NET.

## Conclusão

Aspose.OCR for .NET capacita os desenvolvedores a integrar perfeitamente recursos de OCR em seus aplicativos, abrindo portas para soluções inovadoras em vários domínios. Aproveite o poder do OCR e aprimore seus projetos com reconhecimento de texto preciso.

## Perguntas frequentes

### Q1: O Aspose.OCR for .NET é adequado tanto para iniciantes quanto para desenvolvedores experientes?

A1: Com certeza! Aspose.OCR for .NET atende desenvolvedores de todos os níveis de habilidade, fornecendo funcionalidades intuitivas para integração perfeita.

### Q2: Posso usar Aspose.OCR for .NET para reconhecer caracteres em vários idiomas?

A2: Sim, o Aspose.OCR oferece suporte ao reconhecimento em vários idiomas, tornando-o versátil para diversas aplicações.

### Q3: Com que frequência o Aspose.OCR for .NET é atualizado?

 R3: As atualizações são lançadas regularmente para garantir a compatibilidade com as tecnologias mais recentes e resolver possíveis problemas. Verifica a[documentação](https://reference.aspose.com/ocr/net/) para obter as informações mais recentes.

### Q4: Existe uma avaliação gratuita disponível para Aspose.OCR for .NET?

 A4: Sim, você pode explorar os recursos do Aspose.OCR baixando o[teste grátis](https://releases.aspose.com/).

### P5: Onde posso procurar assistência ou contactar a comunidade para obter apoio?

 A5: Visite o[Fórum Aspose.OCR](https://forum.aspose.com/c/ocr/16) para se envolver com a comunidade e obter assistência especializada.