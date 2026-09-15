---
date: 2026-02-25
description: Aprende cómo extraer texto de una imagen usando Aspose.OCR para .NET.
  Esta guía te guía paso a paso en la preparación de rectángulos para el reconocimiento
  OCR de imágenes y en cómo mejorar la precisión.
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Cómo extraer texto de una imagen preparando rectángulos en OCR
url: /es/net/ocr-optimization/prepare-rectangles/
weight: 11
---

.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Preparar Rectángulos en el Reconocimiento de Imágenes OCR

## Introducción

El Reconocimiento Óptico de Caracteres (OCR) es esencial para convertir contenido visual en texto buscable y editable. En este tutorial **extraerá texto de una imagen** preparando rectángulos personalizados que enfocan el motor OCR en regiones específicas. Usando Aspose.OCR para .NET, recorreremos cada paso—desde configurar su proyecto hasta obtener el texto reconocido—para que pueda integrar una potente funcionalidad de imagen‑a‑texto en sus aplicaciones .NET.

## Respuestas Rápidas
- **¿Qué significa “extract text from image”?** Significa convertir los caracteres visuales de una imagen en cadenas legibles por máquina.  
- **¿Qué biblioteca ayuda con esto en .NET?** Aspose.OCR para .NET.  
- **¿Necesito una licencia para desarrollo?** Una prueba gratuita funciona para pruebas; se requiere una licencia para producción.  
- **¿Puedo apuntar a áreas específicas?** Sí, definiendo rectángulos que limitan el alcance del OCR.  
- **¿Qué versiones de .NET son compatibles?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Qué es “extract text from image” con rectángulos?
Cuando define zonas rectangulares en una imagen, el motor OCR procesa solo esas zonas. Esto mejora la precisión, reduce el tiempo de procesamiento y le permite ignorar fondos ruidosos o secciones irrelevantes.

## ¿Por qué preparar rectángulos antes del OCR?
- **Enfocar en contenido relevante:** Omitir encabezados, pies de página o gráficos decorativos.  
- **Mejorar el rendimiento:** Regiones más pequeñas significan reconocimiento más rápido.  
- **Mejorar la precisión:** Menos ruido visual conduce a resultados más limpios.

## Por qué esto es importante para proyectos del mundo real
Muchos documentos empresariales—recibos, facturas, tarjetas de identificación—tienen diseños mixtos donde solo ciertas partes contienen texto valioso. Al usar rectángulos, puede extraer solo los campos necesarios, reduciendo drásticamente el trabajo de post‑procesamiento y aumentando la fiabilidad general de su canal de automatización.

## Casos de uso comunes
- **Automatización de entrada de datos:** Extraer campos específicos de formularios escaneados.  
- **Verificaciones de cumplimiento:** Aislar y verificar bloques de texto legal.  
- **Indexación de contenido:** Indexar solo el titular o la leyenda de una imagen para motores de búsqueda.  

## Requisitos Previos

- Familiaridad con C# y desarrollo .NET.  
- Biblioteca Aspose.OCR para .NET instalada – puede descargarla **[aquí](https://releases.aspose.com/ocr/net/)**.  
- Una imagen de ejemplo (p.ej., `sample.png`) que contenga el texto que desea extraer.

## Importar Espacios de Nombres

Primero, incluya los espacios de nombres requeridos en el alcance:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Paso 1: Configurar el Directorio de Documentos

Especifique dónde se encuentran sus archivos de imagen y cree una instancia del motor OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Cómo extraer texto de una imagen usando múltiples rectángulos

### Paso 2: Reconocer Imagen con Múltiples Rectángulos

#### 2.1 Definir los rectángulos

Cree una lista de objetos `Rectangle` que delimiten las áreas que desea que el motor OCR escanee.

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 Realizar reconocimiento OCR

Pase la ruta de la imagen y la lista de rectángulos a `RecognizeImage`. El método devuelve una colección de cadenas—cada entrada corresponde a un rectángulo.

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### Paso 3: Reconocer Imagen con Configuración de Reconocimiento (Enfoque Alternativo)

Si prefiere usar `RecognitionSettings`, puede lograr el mismo resultado con una llamada a la API ligeramente diferente.

#### 3.1 Definir la configuración de reconocimiento

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 Mostrar texto reconocido

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Problemas Comunes y Consejos

- **Coordenadas de rectángulo incorrectas:** Asegúrese de que los valores `X`, `Y`, `Width` y `Height` correspondan correctamente a la región deseada.  
- **Calidad de la imagen:** Imágenes de baja resolución pueden producir resultados de OCR deficientes; considere pre‑procesamiento (p.ej., binarización).  
- **Resultados vacíos:** Verifique que los rectángulos realmente contengan texto; de lo contrario el motor devuelve cadenas vacías.

## Solución de Problemas y Mejores Prácticas

| Síntoma | Causa Probable | Solución |
|---------|----------------|----------|
| No hay salida o cadenas vacías | Rectángulos fuera de los límites de la imagen | Verifique las dimensiones de la imagen y las coordenadas de los rectángulos |
| Caracteres distorsionados | Bajo contraste o ruido | Aplique limpieza de imagen (escala de grises, umbral) antes del OCR |
| Rendimiento lento en archivos grandes | Demasiados rectángulos o imagen muy grande | Divida la imagen o reduzca la cantidad de rectángulos cuando sea posible |

## Conclusión

Ahora ha aprendido cómo **extraer texto de una imagen** preparando rectángulos personalizados con Aspose.OCR para .NET. Esta técnica le brinda un control granular sobre el procesamiento OCR, ayudándole a crear funciones de extracción de texto más rápidas y precisas en sus aplicaciones.

## Preguntas Frecuentes

**Q:** ¿Puedo usar Aspose.OCR para .NET con otros frameworks .NET?  
**A:** Sí, Aspose.OCR para .NET es compatible con varios frameworks .NET.

**Q:** ¿Hay una prueba gratuita disponible para Aspose.OCR para .NET?  
**A:** ¡Por supuesto! Puede acceder a la prueba gratuita **[aquí](https://releases.aspose.com/)**.

**Q:** ¿Cómo obtengo soporte para Aspose.OCR para .NET?  
**A:** Visite el **[foro de Aspose.OCR](https://forum.aspose.com/c/ocr/16)** para soporte dedicado.

**Q:** ¿Puedo obtener una licencia temporal para propósitos de prueba?  
**A:** Sí, puede adquirir una licencia temporal **[aquí](https://purchase.aspose.com/temporary-license/)**.

**Q:** ¿Dónde puedo encontrar la documentación de Aspose.OCR para .NET?  
**A:** La documentación está disponible **[aquí](https://reference.aspose.com/ocr/net/)**.

---

**Última actualización:** 2026-02-25  
**Probado con:** Aspose.OCR 24.11 para .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}