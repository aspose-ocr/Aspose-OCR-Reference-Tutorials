---
category: general
date: 2026-02-17
description: Reconoce texto en imágenes rápidamente con el soporte GPU de Aspose OCR
  en Java. Aprende a extraer texto de una imagen y a establecer el ID del dispositivo
  GPU para un rendimiento óptimo.
draft: false
keywords:
- recognize text image
- extract text from image
- set gpu device id
- Aspose OCR Java
- GPU acceleration OCR
language: es
og_description: Reconoce texto en imágenes rápidamente con soporte GPU de Aspose OCR
  en Java. Esta guía muestra cómo extraer texto de una imagen y establecer el ID del
  dispositivo GPU.
og_title: reconocer texto de imagen usando Aspose OCR GPU – Java
tags:
- Java
- OCR
- Aspose
- GPU
title: Reconocer texto en imagen usando Aspose OCR GPU – Java
url: /es/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Reconocer texto en imagen usando Aspose OCR GPU – Java

¿Alguna vez necesitaste **reconocer texto en imagen** en una aplicación Java pero la CPU se quedaba sin aliento con archivos grandes? No eres el único—muchos desarrolladores se topan con ese obstáculo al procesar escaneos de alta resolución. ¿La buena noticia? Aspose OCR te permite **extraer texto de una imagen** en la GPU, reduciendo drásticamente el tiempo de procesamiento.  

En este tutorial recorreremos un ejemplo completo, listo para ejecutar, que muestra exactamente cómo configurar la licencia, habilitar la aceleración GPU y **establecer el id del dispositivo GPU** cuando tienes varias tarjetas gráficas. Al final tendrás un programa autónomo que imprime el texto reconocido en la consola—sin pasos adicionales.

## Lo que necesitarás

- **Java 17** o más reciente (la API es compatible con Java 8+, pero el último LTS te brinda mejor rendimiento).  
- Biblioteca **Aspose OCR for Java** (descarga el JAR desde el sitio web de Aspose).  
- Un archivo de licencia válido de **Aspose OCR** (`Aspose.OCR.lic`). La versión de prueba funciona, pero las funciones de GPU están bloqueadas detrás de una versión licenciada.  
- Un archivo de imagen (`sample-image.png`) que contenga texto claro y legible por máquina.  
- Un entorno con GPU habilitada (una tarjeta compatible con NVIDIA CUDA funciona mejor).  

Si alguno de esos conceptos te resulta desconocido, no te preocupes—cada punto se explicará a medida que avanzamos.

## Paso 1: Añadir Aspose OCR a tu proyecto

Primero, incluye el JAR de Aspose OCR en tu classpath. Si usas Maven, agrega la siguiente dependencia a `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Para Gradle, es:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Si prefieres la ruta manual, coloca el JAR en tu carpeta `libs/` y añádelo a la ruta de módulos del IDE.

> **Consejo profesional:** Mantén el número de versión sincronizado con las notas de la versión de la biblioteca; las versiones más recientes a menudo incluyen mejoras de rendimiento para el procesamiento en GPU.

## Paso 2: Cargar la licencia de Aspose OCR (requerido para el uso de GPU)

Sin una licencia, la llamada `setEnableGpu(true)` volverá silenciosamente al modo CPU. Carga la licencia al inicio del método `main`:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

Reemplaza `YOUR_DIRECTORY` con la ruta absoluta o relativa donde guardaste el archivo `.lic`. Si la ruta es incorrecta, Aspose lanzará una `FileNotFoundException`, así que verifica la ortografía.

## Paso 3: Crear el motor OCR y habilitar la aceleración GPU

Ahora instanciamos `OcrEngine` y le indicamos que use la GPU. El método `setGpuDeviceId` te permite elegir una tarjeta específica cuando hay más de una presente.

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

¿Por qué preocuparse por el ID del dispositivo? En un servidor con múltiples GPU podrías reservar una tarjeta para el preprocesamiento de imágenes y otra para OCR. Establecer el ID garantiza que el hardware correcto realice el trabajo pesado.

## Paso 4: Preparar la imagen de entrada

Aspose OCR funciona con una variedad de formatos (PNG, JPG, BMP, TIFF). Envuelve tu archivo en un objeto `OcrInput`:

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

Si necesitas procesar un flujo (p. ej., un archivo subido), usa `ocrInput.add(InputStream)` en su lugar.

## Paso 5: Ejecutar el proceso de reconocimiento y obtener el resultado

El método `recognize` devuelve un `OcrResult` que contiene el texto plano, puntuaciones de confianza e incluso información de diseño si la necesitas.

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

La consola mostrará algo como:

```
Recognized text:
Hello, world!
This is a sample image.
```

Si la imagen está borrosa o el idioma no está soportado, el resultado puede estar vacío. En ese caso, verifica el valor de `ocrResult.getConfidence()` (0‑100) para decidir si volver a intentar con preprocesamiento.

## Ejemplo completo y ejecutable

Juntando todas las piezas obtienes una única clase Java que puedes copiar y pegar en tu IDE:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license – required for GPU usage
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine and turn on GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getDevice().setEnableGpu(true);      // enable GPU acceleration
        ocrEngine.getDevice().setGpuDeviceId(0);       // optional: select GPU index

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/sample-image.png");

        // 4️⃣ Perform recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + ocrResult.getText());
    }
}
```

> **Salida esperada:** La consola imprime el texto exacto que aparece en `sample-image.png`. Si la GPU está activa, notarás que el tiempo de procesamiento disminuye de varios segundos (CPU) a menos de un segundo para escaneos típicos de 300 dpi.

## Preguntas frecuentes y casos límite

### ¿Funciona esto en un servidor sin pantalla (headless)?

Sí. El controlador de GPU debe estar instalado, pero no se requiere pantalla. Simplemente asegúrate de que el toolkit `CUDA` (o su equivalente para tu GPU) esté en el `PATH` del sistema.

### ¿Qué pasa si tengo más de una GPU y quiero usar la GPU 1?

Change the device ID:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

### ¿Cómo extraer texto de una imagen en otro idioma?

Set the language before calling `recognize`:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose soporta más de 30 idiomas; consulta la documentación de la API para la enumeración completa.

### ¿Qué pasa si la imagen contiene varias páginas (p. ej., un PDF convertido a imágenes)?

Create a separate `OcrInput` entry for each page, or loop over the files:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

El motor concatenará los resultados en orden.

### ¿Cómo manejar resultados de baja confianza?

Check the confidence score:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

Los pasos típicos de preprocesamiento incluyen binarización, reducción de ruido o redimensionado a 300 dpi.

## Consejos de rendimiento

- **Procesamiento por lotes:** Añadir muchas imágenes a un solo `OcrInput` reduce la sobrecarga de inicializar repetidamente el contexto GPU.  
- **Calentamiento:** Ejecuta un reconocimiento de prueba una vez después de iniciar la JVM; la primera llamada incurre en latencia de inicialización del controlador.  
- **Gestión de memoria:** Elimina los objetos `OcrInput` grandes (`ocrInput.clear()`) después de usarlos para liberar memoria GPU.  

## Conclusión

Ahora sabes cómo **reconocer texto en imagen** de manera eficiente con el motor GPU de Aspose OCR en Java, cómo **extraer texto de una imagen** en cualquier idioma soportado, y cómo **establecer el id del dispositivo GPU** al trabajar con múltiples tarjetas gráficas. El código completo y ejecutable anterior debería funcionar de inmediato—solo reemplaza tu licencia y las rutas de las imágenes.

¿Listo para el siguiente paso? Prueba procesar una carpeta de PDFs escaneados, experimenta con diferentes opciones `setLanguage`, o combina OCR con un modelo de aprendizaje automático para el post‑procesamiento. Las posibilidades son infinitas, y las mejoras de rendimiento gracias a la aceleración GPU hacen factibles incluso proyectos a gran escala.

¡Feliz codificación, y siéntete libre de dejar un comentario si encuentras algún problema!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}