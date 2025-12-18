---
date: 2025-12-13
description: Aprenda a extraer texto de una imagen usando Aspose.OCR para Java con
  selección de idioma. Este tutorial paso a paso de Aspose OCR para Java muestra una
  configuración de OCR precisa.
linktitle: How to Extract Text from Image with Language Selection Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Cómo extraer texto de una imagen con selección de idioma usando Aspose.OCR
url: /es/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo extraer texto de una imagen con selección de idioma usando Aspose.OCR

## Introducción

Extraer texto de archivos de imagen es un requisito común, ya sea que estés digitalizando documentos escaneados, procesando recibos o creando archivos archivables buscables. Aspose.OCR para Java hace que esta tarea sea sencilla y te brinda un control granular sobre la selección de idioma, la corrección de sesgo y las áreas de reconocimiento. En este tutorial recorreremos un ejemplo completo y práctico que muestra **cómo extraer texto de una imagen** con una configuración de idioma específica, para que puedas integrar OCR confiable en tus aplicaciones Java hoy mismo.

## Respuestas rápidas
- **¿Qué biblioteca maneja OCR en Java?** Aspose.OCR para Java  
- **¿Qué configuración selecciona el idioma?** `settings.setLanguage(Language.Eng)` (o cualquier idioma compatible)  
- **¿Necesito una licencia para desarrollo?** Una licencia de evaluación gratuita funciona para pruebas; se requiere una licencia comercial para producción.  
- **¿Puedo limitar OCR a una región de la imagen?** Sí, usa `RecognitionSettings.setRecognitionAreas()` con rectángulos.  
- **¿Cuál es el tiempo de ejecución típico?** Unos pocos segundos por página en un portátil estándar, dependiendo del tamaño de la imagen y la complejidad del idioma.

## ¿Qué es “extraer texto de una imagen”?
Extraer texto de una imagen (OCR) convierte la representación visual de los caracteres en cadenas legibles por máquina. Esto permite búsquedas, análisis y flujos de trabajo de extracción de datos que de otro modo requerirían transcripción manual.

## ¿Por qué usar Aspose.OCR con selección de idioma?
- **Soporte multilingüe** – Elige el(los) idioma(s) exactos presentes en tu imagen para mejorar la precisión.  
- **Control fino** – Ajusta el sesgo, define áreas de reconocimiento y configura el comportamiento de auto‑sesgo.  
- **API puramente Java** – Sin dependencias nativas, fácil de integrar en cualquier proyecto Java.  
- **Datos de resultado enriquecidos** – Obtén texto plano, JSON, rectángulos delimitadores y advertencias en una sola llamada.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

- **Java Development Kit (JDK)** instalado (JDK 8 o posterior).  
- **Biblioteca Aspose.OCR para Java** – descárgala desde el sitio oficial [here](https://reference.aspose.com/ocr/java/).  
- Un archivo de imagen que contenga el texto que deseas extraer, por ejemplo, `p3.png`.

## Importar paquetes

En tu archivo fuente Java, incluye las clases necesarias de Aspose.OCR y las utilidades estándar de Java:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Guía paso a paso

### Paso 1: Configura tu directorio de documentos

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Reemplaza `"Your Document Directory"` con la ruta absoluta donde se encuentra `p3.png`.

### Paso 2: Define la ruta de la imagen

```java
// The image path
String file = dataDir + "p3.png";
```

Asegúrate de que la variable `file` apunte a la imagen exacta que deseas procesar.

### Paso 3: Crea una instancia de la API Aspose.OCR

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

El objeto `AsposeOCR` te brinda acceso a todas las operaciones de OCR.

### Paso 4: Establece las opciones de reconocimiento (Selección de idioma)

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Aquí:

1. Desactivamos el auto‑sesgo porque proporcionamos un valor de sesgo manual.  
2. Definimos una región rectangular (`RecognitionAreas`) para limitar el OCR a la parte de la imagen que realmente contiene texto.  
3. Establecemos el **idioma** a inglés (`Language.Eng`). Cambia esto a `Language.Fra`, `Language.Spa`, etc., según tu imagen de origen.

### Paso 5: Ejecuta OCR y obtén los resultados

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

La llamada `RecognizePage` ejecuta el motor OCR usando la imagen y la configuración que definiste. El resultado se almacena en un objeto `RecognitionResult`.

### Paso 6: Imprime y utiliza los resultados

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

La salida en consola muestra:

- El texto completo extraído (`recognitionText`).  
- Texto para cada rectángulo definido (`recognitionAreasText`).  
- Coordenadas del rectángulo delimitador.  
- Una representación JSON para facilitar el procesamiento posterior.  
- Ángulo de sesgo detectado y cualquier advertencia.

Ahora puedes alimentar `result.recognitionText` a tu lógica de negocio: almacenarlo, indexarlo o pasarlo a otro servicio.

## Problemas comunes y soluciones

| Problema | Causa | Solución |
|----------|-------|----------|
| **Caracteres basura** | Idioma incorrecto seleccionado | Establece el `Language` correcto (p. ej., `Language.Fra` para francés). |
| **No se devuelve texto** | El área de reconocimiento no cubre el texto | Ajusta las coordenadas del `Rectangle` o elimina `RecognitionAreas` para procesar la imagen completa. |
| **Rendimiento lento** | Imagen muy grande o alta resolución | Reduce la escala de la imagen antes del OCR o aumenta la asignación de memoria para la JVM. |
| **Advertencias sobre formato no compatible** | Formato de imagen no reconocido | Convierte la imagen a PNG, JPEG o TIFF antes de procesarla. |

## Preguntas frecuentes

**P: ¿Puedo reconocer varios idiomas en una sola llamada OCR?**  
R: Sí. Usa `settings.setLanguage(Language.Eng | Language.Fra)` para habilitar el reconocimiento multilingüe.

**P: ¿Qué formatos de imagen soporta Aspose.OCR?**  
R: PNG, JPEG, BMP, TIFF, GIF y varios más. Simplemente proporciona la ruta correcta del archivo.

**P: ¿Existe un límite de tamaño para la imagen?**  
R: No hay un límite estricto, pero las imágenes muy grandes aumentan el uso de memoria y el tiempo de procesamiento. Considera redimensionar archivos grandes.

**P: ¿Cómo obtengo una licencia de producción?**  
R: Compra una licencia en el sitio web de Aspose y aplícala mediante la clase `License` como se muestra en la documentación de Aspose.

**P: ¿Puedo extraer texto directamente de una página PDF?**  
R: No directamente con Aspose.OCR. Convierte la página PDF a una imagen primero (p. ej., usando Aspose.PDF) y luego ejecuta OCR.

## Conclusión

Ahora sabes cómo **extraer texto de una imagen** usando Aspose.OCR para Java mientras seleccionas el idioma adecuado y limitas el reconocimiento a regiones específicas. Este enfoque ofrece OCR preciso y de alto rendimiento que puede integrarse en cualquier flujo de trabajo basado en Java, desde sistemas de gestión documental hasta pipelines de captura de datos.

---

**Última actualización:** 2025-12-13  
**Probado con:** Aspose.OCR 24.11 para Java  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}