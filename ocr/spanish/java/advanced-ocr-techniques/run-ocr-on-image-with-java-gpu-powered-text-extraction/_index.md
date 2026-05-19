---
category: general
date: 2026-03-07
description: Ejecuta OCR en una imagen usando Java. Aprende cómo reconocer texto de
  un PNG, extraer texto de un recibo y cargar una imagen para OCR con un ejemplo completo
  de OCR en Java.
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: es
og_description: Ejecuta OCR en una imagen con Java. Esta guía muestra cómo reconocer
  texto de un PNG, extraer texto de un recibo y cargar la imagen para OCR usando un
  ejemplo completo de OCR en Java.
og_title: Ejecutar OCR en una imagen con Java – Extracción de texto impulsada por
  GPU
tags:
- OCR
- Java
- GPU
- Image Processing
title: Ejecutar OCR en una imagen con Java – Extracción de texto impulsada por GPU
url: /es/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ejecutar OCR en Imagen con Java – Extracción de Texto Acelerada por GPU

¿Alguna vez necesitaste **ejecutar OCR en imagen** archivos pero no estabas seguro por dónde comenzar en Java? No estás solo—muchos desarrolladores se topan con el mismo obstáculo cuando intentan extraer texto de un recibo escaneado o de una captura de pantalla PNG.  

En este tutorial te guiaremos a través de un **ejemplo completo de OCR en Java** que no solo **reconoce texto de PNG** archivos sino que también muestra cómo **extraer texto de recibos** imágenes, todo aprovechando la aceleración GPU para mayor velocidad. Al final tendrás un programa listo‑para‑ejecutar que carga una imagen para OCR, la procesa y muestra el resultado en texto plano.

## Lo que aprenderás

- Cómo **cargar imagen para OCR** usando un simple `ImageInputStream`.
- Habilitar soporte GPU para que el motor se ejecute más rápido en hardware moderno.
- Los pasos exactos para **reconocer texto de PNG** y extraer cadenas útiles de un recibo.
- Trampas comunes (p. ej., ID de dispositivo GPU incorrecto) y consejos de mejores prácticas.
- Un fragmento de código completo y ejecutable que puedes copiar‑pegar en tu IDE.

## Requisitos previos

- Java 17 o superior (el código usa la palabra clave `var` por brevedad, pero puedes reemplazarla por tipos explícitos si usas Java 8).
- Una biblioteca OCR que proporcione las clases `OcrEngine`, `ImageInputStream` y `OcrResult` (por ejemplo, el ficticio *FastOCR* SDK; reemplázala por la real que estés usando).
- Una máquina con GPU habilitada si deseas el impulso de rendimiento (opcional pero recomendado).

---

## Paso 1: Ejecutar OCR en Imagen – Habilitar Aceleración GPU

Lo primero es crear el motor OCR y decirle que use la GPU. Este paso es crucial porque sin soporte GPU el motor recurre a la CPU, lo que puede ser notablemente más lento para recibos de alta resolución.

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**Por qué esto importa:**  
La aceleración GPU descarga los cálculos de matrices pesados que realizan los motores OCR. Si tienes varias GPUs, puedes elegir la que tenga más memoria cambiando el valor de `setGpuDeviceId`. Olvidar habilitar la GPU es una causa frecuente de quejas del tipo “¿por qué mi OCR es tan lento?”.

> **Consejo profesional:** Si tu máquina no tiene una GPU compatible, la llamada `setUseGpu(true)` simplemente será ignorada—no habrá crash, solo un procesamiento más lento.

---

## Paso 2: Cargar Imagen para OCR

Ahora que el motor está listo, necesitamos alimentarlo con una imagen. El ejemplo a continuación muestra cómo cargar un recibo PNG almacenado en disco. Puedes reemplazar la ruta por cualquier formato de imagen soportado por tu biblioteca OCR.

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**Caso límite:**  
Si el archivo no existe o la ruta es incorrecta, `ImageInputStream` lanzará una `IOException`. Envuelve la llamada en un bloque try‑catch y registra un mensaje útil:

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## Paso 3: Reconocer Texto de PNG

Con la imagen cargada, el motor OCR puede hacer su magia. Este paso **reconoce texto de PNG** (o cualquier otro formato soportado) y devuelve un objeto `OcrResult`.

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**¿Qué está pasando bajo el capó?**  
El motor realiza preprocesamiento (desviación, binarización), ejecuta una red neuronal para detectar caracteres y luego los ensambla en líneas de texto. Como habilitamos la GPU antes, esos cálculos de red neuronal se ejecutan en la tarjeta gráfica, ahorrando segundos en el tiempo total de ejecución.

---

## Paso 4: Extraer Texto del Recibo

Después del reconocimiento, normalmente solo querrás el texto bruto. La clase `OcrResult` suele ofrecer un método `getText()` que devuelve una única `String`. Luego puedes post‑procesarlo (p. ej., expresiones regulares para extraer totales, fechas, etc.).

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Salida típica de recibo:**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Ahora puedes pasar esta cadena a tu propio analizador para extraer el monto total, los ítems de línea o la información de impuestos.

---

## Paso 5: Ejemplo Completo de OCR en Java – Listo para Ejecutar

Juntando todo, aquí tienes el **ejemplo completo de OCR en Java** que puedes colocar en un archivo `Main.java`. Asegúrate de que la biblioteca OCR esté en tu classpath.

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Salida esperada en consola** (suponiendo el recibo de ejemplo anterior):

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Si la salida se ve distorsionada, verifica que la imagen sea clara (alto DPI) y que el paquete de idioma OCR coincida con el idioma de tu recibo.

---

## Preguntas Frecuentes y Trucos

| Pregunta | Respuesta |
|----------|-----------|
| *¿Qué pasa si mi GPU no es detectada?* | El motor volverá automáticamente a la CPU. Verifica los controladores y que `setGpuDeviceId` coincida con un dispositivo existente (`nvidia-smi` en Linux puede ayudar). |
| *¿Puedo procesar archivos JPEG o TIFF?* | Sí—simplemente cambia la extensión del archivo en `ImageInputStream`. La biblioteca OCR suele detectar el formato automáticamente. |
| *¿Hay una forma de procesar en lote muchos recibos?* | Envuelve el código de reconocimiento en un bucle y reutiliza la misma instancia de `OcrEngine`; volver a inicializar por imagen desperdicia memoria de la GPU. |
| *¿Cómo mejoro la precisión en recibos de bajo contraste?* | Pre‑procesa la imagen (aumenta el contraste, conviértela a escala de grises) antes de enviarla al motor OCR. Algunas bibliotecas exponen una API `preprocess`. |

---

## Conclusión

Ahora sabes **cómo ejecutar OCR en imagen** archivos en Java, desde cargar la foto hasta extraer texto limpio de un recibo. El recorrido cubrió **reconocer texto de PNG**, **extraer texto del recibo**, y mostró un **ejemplo de OCR en Java** que puedes adaptar a cualquier proyecto.  

¿Próximos pasos? Prueba desactivar la bandera GPU para ver la diferencia de rendimiento, experimenta con distintas resoluciones de imagen, o integra un analizador basado en expresiones regulares para extraer totales automáticamente. Si te interesan temas más avanzados, investiga **post‑procesamiento OCR**, **corrección con modelos de lenguaje**, o **pipelines de procesamiento por lotes**.

¡Feliz codificación, y que tus recibos siempre sean legibles!  

![ejemplo de ejecutar OCR en imagen](/images/run-ocr-on-image.png "ejecutar OCR en imagen – ejemplo Java")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}