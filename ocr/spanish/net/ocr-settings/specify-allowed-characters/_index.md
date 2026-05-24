---
date: 2026-05-24
description: Aprenda cómo mejorar OCR estableciendo caracteres permitidos con Aspose.OCR
  para .NET, lo que permite un reconocimiento preciso de dígitos y un procesamiento
  más rápido. Siga una guía paso a paso.
keywords:
- how to improve ocr
- set allowed characters
- recognize digits
- improve ocr accuracy
- extract serial numbers
linktitle: Cómo mejorar OCR – Establecer caracteres permitidos con Aspose.OCR para
  .NET
schemas:
- author: Aspose
  dateModified: '2026-05-24'
  description: Learn how to improve OCR by setting allowed characters with Aspose.OCR
    for .NET, enabling accurate digit recognition and faster processing. Follow a
    step‑by‑step guide.
  headline: How to Improve OCR – Set Allowed Characters with Aspose.OCR for .NET
  type: TechArticle
- description: Learn how to improve OCR by setting allowed characters with Aspose.OCR
    for .NET, enabling accurate digit recognition and faster processing. Follow a
    step‑by‑step guide.
  name: How to Improve OCR – Set Allowed Characters with Aspose.OCR for .NET
  steps:
  - name: Set the path to your image folder
    text: Define the folder that contains the sample images you want to process.
  - name: Initialize Aspose.OCR with a digit‑only whitelist
    text: '`AllowedCharacters` is a property that sets the whitelist of characters
      the OCR engine may recognize.'
  - name: Recognize a single line containing digits
    text: The `RecognizeLine` method scans the image and returns the best‑matching
      line that conforms to the whitelist.
  - name: Output the recognized digits
    text: Write the result to the console (or log) so you can verify the output instantly.
  - name: Use `RecognitionSettings` for more control
    text: '`RecognitionSettings` allows you to customize OCR parameters such as DPI,
      language packs, and processing mode.'
  - name: Confirm successful execution
    text: By following these steps, you’ve learned **how to improve OCR** accuracy
      by limiting the character set, and you can now reliably extract digit strings
      from images using Aspose.OCR for .NET.
  type: HowTo
- questions:
  - answer: It limits OCR to a predefined whitelist, dramatically increasing accuracy
      for targeted data sets.
    question: What does “specify allowed characters OCR” do?
  - answer: Any combination you need—digits (`0‑9`), uppercase letters, custom symbols,
      or a mix like “ABC‑123”.
    question: Which characters can I allow?
  - answer: Whitelisting reduces false recognitions by up to 70 % and speeds up processing
      by 30 % on average.
    question: Why limit characters?
  - answer: A free trial works for development; a commercial license is required for
      production deployments.
    question: Do I need a license?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: Which .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
title: Cómo mejorar OCR – Establecer caracteres permitidos con Aspose.OCR para .NET
url: /es/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo mejorar OCR – Establecer caracteres permitidos con Aspose.OCR para .NET

En este tutorial descubrirá **cómo mejorar OCR** resultados al **especificar caracteres permitidos** al usar Aspose.OCR para .NET. Restringir el motor OCR a una lista blanca conocida—como solo dígitos—aumenta la precisión, reduce el tiempo de procesamiento y elimina símbolos no deseados. Ya sea que esté extrayendo números de serie, IDs de facturas o lecturas de medidores, los pasos a continuación le permitirán aplicar esta técnica en minutos.

## Respuestas rápidas
- **¿Qué hace “especificar caracteres permitidos OCR”?** Limita OCR a una lista blanca predefinida, aumentando drásticamente la precisión para conjuntos de datos específicos.  
- **¿Qué caracteres puedo permitir?** Cualquier combinación que necesite—dígitos (`0‑9`), letras mayúsculas, símbolos personalizados, o una mezcla como “ABC‑123”.  
- **¿Por qué limitar los caracteres?** La lista blanca reduce los reconocimientos falsos hasta en un 70 % y acelera el procesamiento en un 30 % en promedio.  
- **¿Necesito una licencia?** Una prueba gratuita funciona para desarrollo; se requiere una licencia comercial para implementaciones en producción.  
- **¿Qué versiones de .NET son compatibles?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **¿Puedo combinar esto con paquetes de idioma?** Sí—combina una lista blanca con un paquete de idioma para manejar cadenas de dígitos multilingües.

## Qué es “especificar caracteres permitidos OCR”

**Respuesta directa:** Especificar caracteres permitidos indica a Aspose.OCR que ignore cualquier patrón visual que no coincida con los caracteres que usted lista, de modo que el motor solo devuelva resultados de esa lista blanca. Este enfoque centrado elimina el ruido, mejora las puntuaciones de confianza y reduce el esfuerzo de post‑procesamiento. Además, acelera el proceso de reconocimiento.

## ¿Por qué usar Aspose.OCR para reconocer imágenes de dígitos?

**Respuesta directa:** La función integrada `AllowedCharacters` de Aspose.OCR le permite reconocer imágenes solo con dígitos con una única línea de código, ofreciendo hasta un 95 % de precisión en escaneos de baja resolución sin lógica de filtrado adicional. La biblioteca soporta más de 30 idiomas, procesa lotes de imágenes de 500 páginas en menos de 2 segundos por página, y se ejecuta completamente offline, lo que la hace ideal para escenarios de alto rendimiento y locales, como la lectura de medidores de servicios públicos o la extracción de IDs de facturas.

## Requisitos previos

- Experiencia básica en desarrollo .NET.  
- Biblioteca **Aspose.OCR for .NET** – descárguela del sitio oficial **[aquí](https://releases.aspose.com/ocr/net/)**.  
- Visual Studio 2019+ (o cualquier IDE compatible con .NET).  

## Importar espacios de nombres

Los siguientes espacios de nombres le dan acceso al motor OCR y sus configuraciones:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## ¿Cómo mejorar OCR especificando caracteres permitidos?

`AsposeOcr` es la clase principal del motor OCR proporcionada por la biblioteca Aspose.OCR.  
`RecognizeLine` procesa una sola línea de texto de una imagen y devuelve la cadena reconocida.

**Respuesta directa:** Cargue su imagen, cree una instancia de `AsposeOcr` con una lista blanca solo de dígitos (`"0123456789"`), llame a `RecognizeLine` (o `Recognize` para múltiples líneas) y lea la propiedad `Text` del resultado. Este flujo de tres pasos entrega cadenas numéricas limpias en menos de un segundo para imágenes típicas de 300 dpi.

### Paso 1: Establecer la ruta a su carpeta de imágenes

Defina la carpeta que contiene las imágenes de muestra que desea procesar.

```csharp
string dataDir = "Your Document Directory";
```

### Paso 2: Inicializar Aspose.OCR con una lista blanca solo de dígitos

`AllowedCharacters` es una propiedad que establece la lista blanca de caracteres que el motor OCR puede reconocer.

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

### Paso 3: Reconocer una sola línea que contenga dígitos

El método `RecognizeLine` escanea la imagen y devuelve la línea que mejor coincide y que se ajusta a la lista blanca.

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

### Paso 4: Mostrar los dígitos reconocidos

Escriba el resultado en la consola (o registro) para que pueda verificar la salida al instante.

```csharp
Console.WriteLine(result);
```

### Paso 5: Usar `RecognitionSettings` para mayor control

`RecognitionSettings` le permite personalizar los parámetros OCR como DPI, paquetes de idioma y modo de procesamiento.

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

### Paso 6: Mostrar el resultado del segundo caso

```csharp
Console.WriteLine(result2.RecognitionText);
```

### Paso 7: Confirmar la ejecución exitosa

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Al seguir estos pasos, ha aprendido **cómo mejorar la precisión de OCR** limitando el conjunto de caracteres, y ahora puede extraer de forma fiable cadenas de dígitos de imágenes usando Aspose.OCR para .NET.

## Problemas comunes y solución de problemas

- **Resultado vacío:** Verifique que la imagen tenga un contraste claro y ruido de fondo mínimo; se recomienda un mínimo de 300 dpi.  
- **Caracteres inesperados:** Verifique la cadena de la lista blanca; espacios extra o caracteres invisibles romperán el filtro.  
- **Archivo no encontrado:** Asegúrese de que `dataDir` apunte a la carpeta correcta y que el nombre del archivo coincida con el sistema de archivos sensible a mayúsculas.  
- **Retraso de rendimiento:** Para lotes grandes, reutilice una única instancia de `AsposeOcr` en lugar de crear una nueva por imagen.  

## Preguntas frecuentes

### P1: ¿Es Aspose.OCR para .NET adecuado tanto para principiantes como para desarrolladores experimentados?
**R:** Absolutamente. La API ofrece una configuración de una sola línea para tareas rápidas y `RecognitionSettings` avanzados para usuarios avanzados, cubriendo todos los niveles de habilidad.

### P2: ¿Puedo reconocer caracteres en varios idiomas mientras uso una lista blanca de caracteres permitidos?
**R:** Sí. Cargue el paquete de idioma apropiado (p.ej., `ocrEngine.LoadLanguage("en")`) y combínelo con una lista blanca como `"0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"` para manejar cadenas de dígitos multilingües.

### P3: ¿Con qué frecuencia se actualiza Aspose.OCR para .NET?
**R:** Nuevas versiones se publican aproximadamente cada 6‑8 semanas, añadiendo soporte de idiomas, mejoras de rendimiento y correcciones de errores. Vea los últimos detalles en la [documentación](https://reference.aspose.com/ocr/net/).

### P4: ¿Hay una prueba gratuita disponible?
**R:** Sí—descargue la **[prueba gratuita](https://releases.aspose.com/)** para evaluar todas las funciones sin una licencia. El uso en producción requiere una licencia comercial.

### P5: ¿Dónde puedo obtener ayuda de la comunidad o soporte oficial?
**R:** Únase a la comunidad activa en el **[foro de Aspose.OCR](https://forum.aspose.com/c/ocr/16)** donde puede hacer preguntas, compartir fragmentos y recibir orientación de los ingenieros de Aspose.

---

**Última actualización:** 2026-05-24  
**Probado con:** Aspose.OCR 24.11 para .NET  
**Autor:** Aspose

## Tutoriales relacionados

- [Configuración de reconocimiento de imagen OCR - Especificar caracteres ignorados](/ocr/net/ocr-settings/specify-ignored-characters/)
- [Preprocesar OCR de imagen con filtros Aspose.OCR para .NET](/ocr/net/ocr-optimization/preprocessing-filters-for-image/)
- [Cómo establecer el valor de umbral en el reconocimiento de imagen OCR](/ocr/net/ocr-settings/set-threshold-value/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}