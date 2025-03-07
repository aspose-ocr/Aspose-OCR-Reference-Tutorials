---
title: Corrección de resultados con revisión ortográfica en reconocimiento de imágenes OCR
linktitle: Corrección de resultados con revisión ortográfica en reconocimiento de imágenes OCR
second_title: API Aspose.OCR .NET
description: Mejore la precisión del OCR con Aspose.OCR para .NET. Corrija la ortografía, personalice diccionarios y logre un reconocimiento de texto sin errores sin esfuerzo.
weight: 13
url: /es/net/ocr-optimization/result-correction-with-spell-checking/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Corrección de resultados con revisión ortográfica en reconocimiento de imágenes OCR

## Introducción

En el ámbito del reconocimiento óptico de caracteres (OCR), lograr resultados precisos es crucial para extraer información significativa de las imágenes. Un desafío común es lidiar con palabras mal escritas en el proceso de reconocimiento. Afortunadamente, Aspose.OCR para .NET proporciona una solución poderosa para mejorar los resultados de OCR mediante la revisión ortográfica.

Este tutorial lo guiará a través del proceso de corrección de resultados con revisión ortográfica usando Aspose.OCR para .NET. Al final, estará equipado para mejorar la precisión del texto derivado de OCR, garantizando una salida más refinada y sin errores.

## Requisitos previos

Antes de sumergirnos en la magia del corrector ortográfico, asegúrese de cumplir con los siguientes requisitos previos:

-  Aspose.OCR para la biblioteca .NET: descargue e instale la biblioteca Aspose.OCR desde[página de lanzamiento](https://releases.aspose.com/ocr/net/).

- Directorio de documentos: asegúrese de tener un directorio designado para sus documentos. Reemplace "Su directorio de documentos" en los fragmentos de código con la ruta real.

## Importar espacios de nombres

Comencemos importando los espacios de nombres necesarios en su proyecto .NET:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Paso 1: Inicializar Aspose.OCR

Inicialice una instancia de Aspose.OCR para iniciar el proceso de OCR.

```csharp
// La ruta al directorio de documentos.
string dataDir = "Your Document Directory";

// Inicializar una instancia de AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Paso 2: reconocer la imagen

A continuación, reconozca el texto en una imagen usando Aspose.OCR. Aquí hay un fragmento que demuestra este proceso:

```csharp
// Reconocer imagen
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Paso 3: antes de la corrección

Recupere el resultado del OCR antes de la corrección para compararlo con la versión corregida.

```csharp
// Obtener resultado
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Paso 4: después de la corrección

Aplique el corrector ortográfico para obtener el resultado corregido. El siguiente fragmento de código ilustra este paso:

```csharp
// Obtener resultado corregido
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Paso 5: palabras mal escritas y sugerencias

Obtenga una lista de palabras mal escritas junto con las correcciones sugeridas utilizando el siguiente código:

```csharp
// Obtenga una lista de palabras mal escritas con sugerencias
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
	Console.Write("Word:" + word.Word);
	Console.Write(" StartPosition:" + word.StartPosition);
	Console.WriteLine(" Length:" + word.Length);
	Console.WriteLine("SuggestedWords:");
	foreach (var suggest in word.SuggestedWords)
	{
		Console.Write(suggest.Word + " ");
	}
	Console.WriteLine();
}
```

## Paso 6: corregir el texto del usuario

Corrija el texto específico proporcionado por el usuario utilizando la biblioteca Aspose.OCR:

```csharp
// Texto de usuario correcto
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Paso 7: Corrección con el Diccionario del Usuario

Mejore aún más la corrección incorporando un diccionario de usuario personalizado:

```csharp
// Obtener resultado corregido con el diccionario del usuario
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Conclusión

¡Felicidades! Ha navegado con éxito por las capacidades de revisión ortográfica de Aspose.OCR para .NET. Esta función le permite perfeccionar los resultados de OCR, garantizando la precisión y eliminando errores.

## Preguntas frecuentes

### P1: ¿Puedo usar Aspose.OCR en otros idiomas además del inglés?

R1: Sí, Aspose.OCR admite varios idiomas. Ajuste la configuración de idioma en consecuencia.

### P2: ¿Cómo integro Aspose.OCR en mi proyecto .NET?

 A2: Consulte el[documentación](https://reference.aspose.com/ocr/net/) para conocer los pasos de integración detallados.

### P3: ¿Existe una versión de prueba disponible para Aspose.OCR?

 R3: Sí, puedes explorar las funciones con el[versión de prueba gratuita](https://releases.aspose.com/).

### P4: ¿Puedo cargar un diccionario personalizado para revisar la ortografía?

R4: ¡Absolutamente! El tutorial demuestra cómo mejorar la corrección utilizando un diccionario proporcionado por el usuario.

### P5: ¿Dónde puedo buscar soporte para Aspose.OCR?

 A5: Visita el[Foro Aspose.OCR](https://forum.aspose.com/c/ocr/16) para el apoyo y orientación de la comunidad.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
