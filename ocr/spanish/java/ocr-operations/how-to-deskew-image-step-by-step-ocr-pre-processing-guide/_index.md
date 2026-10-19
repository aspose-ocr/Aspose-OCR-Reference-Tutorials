---
category: general
date: 2026-02-19
description: Aprende a enderezar imágenes y eliminar el ruido para OCR. Este tutorial
  muestra cómo reconocer imágenes de texto, corregir la rotación de la imagen y preprocesar
  imágenes para OCR con Aspose OCR.
draft: false
keywords:
- how to deskew image
- recognize text image
- how to remove noise
- correct image rotation
- preprocess image ocr
language: es
og_description: Cómo enderezar una imagen y eliminar el ruido para reconocer texto
  rápidamente. Sigue esta guía para corregir la rotación de la imagen y preprocesar
  OCR de imágenes con Aspose.
og_title: Cómo desinclinar una imagen – Tutorial completo de preprocesamiento OCR
tags:
- OCR
- Java
- Image Processing
title: Cómo corregir la inclinación de una imagen — Guía paso a paso de preprocesamiento
  OCR
url: /es/java/ocr-operations/how-to-deskew-image-step-by-step-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo enderezar una imagen — Tutorial completo de pre‑procesamiento OCR

¿Alguna vez te has preguntado **cómo enderezar una imagen** antes de enviarla a un motor OCR? Tal vez escaneaste un lote de recibos y las páginas parecen estar ligeramente inclinadas, o el escaneo está salpicado de puntos aleatorios. Ese es un problema común: las fotos inclinadas y ruidosas dificultan el reconocimiento de texto.  

¿La buena noticia? Puedes corregir la rotación de la imagen y eliminar el ruido (cómo quitar el ruido) con solo unas pocas líneas de Java usando Aspose.OCR. En esta guía recorreremos todo el flujo: desde cargar un PNG ruidoso‑rotado, aplicar enderezado + denoise mediano, hasta **reconocer texto de la imagen** e imprimir el resultado. Al final tendrás un fragmento reutilizable que podrás insertar en cualquier proyecto Java.

## Qué necesitarás

- **Java 17** o superior (el código compila con versiones anteriores, pero 17 es el punto óptimo).  
- **Aspose.OCR para Java** – puedes obtener el último JAR desde Maven Central (`com.aspose:aspose-ocr`).  
- Un archivo de imagen que esté tanto rotado como ruidoso (por ejemplo, `noisy-rotated.png`).  
- Un IDE modesto (IntelliJ, Eclipse o incluso VS Code).  

No se requieren herramientas de compilación sofisticadas; un simple `javac` + `java` funciona sin problemas.

---

## Paso 1 – Crear la instancia del motor OCR  

Lo primero que haces es iniciar un `OcrEngine`. Piensa en él como el cerebro que más tarde leerá los caracteres por ti.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Consejo:** Mantén el motor como singleton si vas a procesar muchas imágenes; reutiliza los buffers internos y acelera el proceso.

## Paso 2 – Habilitar enderezado y denoise mediano (Cómo quitar el ruido)

Ahora indicamos al motor que **corrija la rotación de la imagen** y que **cómo quitar el ruido**. Ambos filtros son opcionales, pero juntos mejoran drásticamente la precisión.

```java
        // Turn on preprocessing filters
        ocrEngine.getPreprocessing().setDeskew(true);          // fixes rotation
        ocrEngine.getPreprocessing().setMedianDenoise(true);   // smooths out speckles
```

¿Por qué denoise mediano? Preserva los bordes (las líneas que definen los caracteres) mientras elimina píxeles aislados, exactamente lo que necesitas para un OCR limpio.

## Paso 3 – Cargar la imagen que deseas procesar  

Aquí apuntamos el motor al archivo que necesita limpieza. `ImageStream.fromFile` lee el PNG en memoria.

```java
        // Load the noisy‑rotated image
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/noisy-rotated.png"));
```

Si tu imagen está en un servidor remoto, simplemente pasa un `InputStream` en su lugar—Aspose lo maneja sin problemas.

## Paso 4 – Ejecutar OCR y capturar el texto reconocido  

Con el pre‑procesamiento activado, el motor ahora lee la imagen corregida. La llamada `recognize()` devuelve un `RecognitionResult` que contiene la cadena extraída.

```java
        // Perform OCR – the engine automatically applies deskew & denoise first
        String recognizedText = ocrEngine.recognize().getText();

        // Show the output
        System.out.println("=== Recognized Text ===");
        System.out.println(recognizedText);
    }
}
```

Deberías ver texto limpio y legible en la consola, incluso si la foto original estaba torcida y granulada.

## Paso 5 – Verificar el resultado (Qué esperar)

Cuando todo funciona, la consola muestra algo como:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑02‑15
Total: $1,234.56
```

Si la salida aún contiene caracteres distorsionados, verifica:

- La resolución de la imagen (≥ 300 dpi es lo ideal).  
- Que la ruta del archivo sea correcta.  
- Si filtros adicionales (p. ej., `setContrastStretch`) podrían ayudar.

---

## Opcional: Confirmación visual con una imagen de ejemplo  

A continuación tienes una pequeña vista previa de un recibo rotado y ruidoso. Observa la inclinación—nuestro código lo enderezará por ti.

![ejemplo de cómo enderezar imagen](deskew-demo.png "cómo enderezar imagen")

*Texto alternativo: cómo enderezar imagen – antes y después del procesamiento.*

---

## Preguntas frecuentes

### ¿Esto funciona con PDFs o solo con PNG/JPEG?  
Aspose.OCR puede leer PDFs directamente; solo reemplaza `ImageStream.fromFile` por `ImageStream.fromPdf`. Las mismas banderas de pre‑procesamiento se aplican, así que aún obtienes **cómo enderezar una imagen** y **cómo quitar el ruido**.

### ¿Qué pasa si necesito conservar la orientación original para pasos posteriores?  
Puedes clonar la imagen antes del pre‑procesamiento:

```java
Image original = ocrEngine.getImage().clone();
ocrEngine.getPreprocessing().apply(); // modifies the internal copy
// Use original later if needed
```

### ¿Puedo cambiar el ángulo de enderezado manualmente?  
Sí—`setDeskewAngle(double degrees)` te permite sobrescribir el algoritmo de detección automática. Útil cuando la detección automática falla con rotaciones extremas.

### ¿En qué se diferencia el denoise mediano del desenfoque gaussiano?  
Los filtros median reemplazan cada píxel por la mediana de sus vecinos, lo que preserva los bordes. El desenfoque gaussiano suaviza todo, potencialmente difuminando los trazos de los caracteres—por eso el filtro mediano es la opción más segura para OCR.

---

## Conclusión  

En este tutorial cubrimos **cómo enderezar una imagen**, demostramos **cómo quitar el ruido** y te mostramos cómo **reconocer texto de la imagen** usando el pre‑procesamiento incorporado de Aspose OCR. Al habilitar `setDeskew(true)` y `setMedianDenoise(true)`, corriges automáticamente la rotación de la imagen y eliminas los puntos, convirtiendo un escaneo desordenado en una cadena de texto limpia.  

Siéntete libre de experimentar: prueba diferentes estrategias de denoise, procesa PDFs o encadena múltiples imágenes en un bucle. El mismo patrón—motor → pre‑procesar → reconocer—se aplica a cualquier escenario, convirtiéndolo en una base sólida para cualquier pipeline OCR.

**Próximos pasos** que podrías explorar:

- **Procesamiento por lotes** – iterar sobre una carpeta de imágenes y escribir cada resultado en un archivo `.txt`.  
- **Paquetes de idioma** – cargar un diccionario de idioma específico para mejorar la precisión en textos que no sean en inglés.  
- **Filtros avanzados** – como `setContrastStretch` o `setBinarization` para escaneos de bajo contraste.  

¿Tienes más preguntas? Deja un comentario, ¡y feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}