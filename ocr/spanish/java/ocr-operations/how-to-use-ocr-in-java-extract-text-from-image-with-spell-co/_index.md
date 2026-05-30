---
category: general
date: 2026-05-06
description: Cómo usar OCR para extraer texto de una imagen en Java. Aprende la conversión
  de imagen a texto con OCR, corrige errores de OCR y carga la imagen para OCR con
  Aspose OCR.
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: es
og_description: Cómo usar OCR en Java para extraer texto de una imagen, corregir errores
  de OCR y cargar la imagen para OCR usando Aspose OCR.
og_title: Cómo usar OCR en Java – Guía completa
tags:
- OCR
- Java
- Aspose
title: Cómo usar OCR en Java – Extraer texto de una imagen con corrección ortográfica
url: /es/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar OCR en Java – Extraer texto de una imagen con corrección ortográfica

¿Alguna vez te has preguntado **cómo usar OCR** para convertir una foto borrosa de un recibo en texto limpio y buscable? No estás solo. En muchos proyectos —aplicaciones de seguimiento de gastos, pipelines de digitalización de facturas, o incluso un script rápido para tomar notas— obtener texto fiable de una imagen es el primer obstáculo.  

Este tutorial te muestra exactamente cómo usar OCR en Java, cubriendo todo desde cargar la imagen para OCR hasta corregir errores de OCR para que el resultado se lea como si fuera escrito por un humano. Al final, podrás **extraer texto de una imagen**, realizar la conversión **OCR de imagen a texto**, y corregir automáticamente los errores de reconocimiento más comunes.

## Lo que vas a construir

Crearemos un pequeño programa de consola en Java que:

1. Carga un PNG (o cualquier formato compatible) en el motor Aspose OCR.  
2. Habilita la función de corrección ortográfica incorporada para **corregir errores de OCR**.  
3. Ejecuta el proceso de reconocimiento y muestra el texto limpiado.  

Sin servicios externos, sin frameworks pesados — solo un único JAR y unas pocas líneas de código.

### Requisitos previos

- Java Development Kit (JDK) 8 o superior.  
- Maven (o cualquier herramienta de compilación) para obtener la biblioteca Aspose OCR.  
- Un archivo de imagen (p. ej., `receipt.png`) que deseas analizar.  

Si te falta el JAR de Aspose OCR, agrega esta dependencia a tu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **Consejo profesional:** La versión de evaluación gratuita funciona para pruebas, pero una licencia elimina la marca de agua de evaluación.

## Paso 1 – Inicializar el motor OCR (Palabra clave principal en acción)

Lo primero que debes hacer es crear una instancia de `OcrEngine`. Piensa en ella como el cerebro que leerá los píxeles y los convertirá en caracteres.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*Por qué es importante:* Inicializar el motor configura los recursos internos (modelos de idioma, diccionarios, etc.). Omitir este paso provocaría una `NullPointerException` más adelante cuando intentes cargar una imagen.

## Paso 2 – Cargar imagen para OCR

Ahora realmente **cargamos la imagen para OCR**. Aspose proporciona un práctico ayudante `ImageStream.fromFile`, pero también puedes proporcionar un `byte[]` si lo prefieres.

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*Trampa común:* La ruta del archivo debe ser absoluta o relativa al directorio de trabajo. Si la imagen no se encuentra, el motor lanza una `IOException`. Verifica la ruta, especialmente al ejecutar desde un IDE versus un JAR empaquetado.

## Paso 3 – Habilitar corrección ortográfica para **corregir errores de OCR**

El OCR listo para usar puede ser ruidoso —por ejemplo “l0ve” en lugar de “love” o “0” por “O”. Habilitar la corrección ortográfica indica al motor que ejecute una pasada de post‑procesamiento que corrige errores típicos.

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*Por qué querrías esto:* Sin corrección ortográfica, podrías tener que limpiar manualmente la salida, lo que anula el propósito de la automatización. El diccionario incorporado funciona bien para inglés y varios otros idiomas.

## Paso 4 – Realizar el reconocimiento (**OCR de imagen a texto**)

Con la imagen cargada y la corrección ortográfica habilitada, finalmente podemos pedir al motor que reconozca el texto.

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*Caso límite:* Si la imagen tiene bajo contraste o está muy sesgada, el resultado aún puede contener basura. Considera pre‑procesar (p. ej., binarización, corrección de inclinación) antes de enviarla al motor.

## Paso 5 – Mostrar el texto limpiado

El paso final es simplemente imprimir el resultado. En una aplicación real podrías escribirlo en una base de datos o en un archivo, pero para esta demostración `System.out` es suficiente.

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Salida esperada

Suponiendo que `receipt.png` contenga una lista clara de artículos, podrías ver algo como:

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

Observa cómo “Qty” y “Price” están escritos correctamente aunque el escaneo original tuviera un “Qy” erróneo.

## Ejemplo completo funcionando

A continuación tienes el programa completo que puedes copiar y pegar en un archivo llamado `SpellCorrectDemo.java`. Asegúrate de que el JAR de Aspose OCR esté en tu classpath.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

Ejecuta con:

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

Ahora deberías ver el texto limpiado impreso en la consola.

## Bonus: Ajustar configuraciones para mayor precisión

Aunque la configuración predeterminada funciona para la mayoría de documentos impresos, podrías necesitar ajustar algunos parámetros para escenarios especializados:

| Configuración | Qué hace | Cuándo cambiar |
|---------------|----------|----------------|
| `setLanguage(OcrLanguage.English)` | Fuerza el diccionario inglés (reduce falsos positivos) | Si tu imagen contiene solo texto en inglés. |
| `setResolution(300)` | Indica al motor los DPI de la imagen fuente | Para escaneos de alta resolución. |
| `setEnableAutoSkewCorrection(true)` | Rota automáticamente páginas ligeramente inclinadas | Cuando las imágenes son capturadas con un teléfono. |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## Preguntas frecuentes

**Q: ¿Funciona esto con PDFs?**  
A: Sí. Convierte cada página del PDF a una imagen (p. ej., usando Aspose PDF) y pasa la imagen al motor OCR.

**Q: ¿Qué pasa si mi imagen está en formato BMP?**  
A: `ImageStream.fromFile` admite PNG, JPEG, BMP, TIFF y GIF de forma nativa. Simplemente cambia la extensión del archivo.

**Q: ¿Puedo desactivar la corrección ortográfica?**  
A: Por supuesto—establece `setEnableSpellCorrection(false)` si necesitas la salida cruda de OCR para procesamiento posterior.

## Conclusión

Ahora sabes **cómo usar OCR** en Java para **extraer texto de una imagen**, corregir automáticamente **errores de OCR**, y cargar correctamente **imagen para OCR** usando Aspose OCR. El flujo de cinco pasos —inicializar, cargar, habilitar corrección ortográfica, reconocer y mostrar— cubre la mayoría de las tareas cotidianas de OCR.  

A partir de aquí, considera encadenar esta lógica con una escritura en base de datos, un endpoint REST, o un procesador por lotes para manejar decenas de recibos a la vez. Experimenta con la tabla de configuraciones adicional arriba para exprimir hasta el último carácter de precisión.

¡Feliz codificación, y que tus resultados de OCR siempre sean más limpios que tus recibos manchados de café! 

![diagrama de cómo usar OCR mostrando imagen → motor OCR → flujo de texto corregido]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}