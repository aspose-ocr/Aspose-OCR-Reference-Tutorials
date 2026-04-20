---
category: general
date: 2026-03-21
description: Aprende a enderezar archivos de imagen y reconocer texto en imágenes
  con Aspose OCR. Convierte JPG a texto y corrige la rotación de la imagen en unas
  pocas líneas de código C#.
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: es
og_description: Cómo corregir la inclinación de una imagen y extraer texto de JPEGs
  usando Aspose OCR. Sigue esta guía paso a paso para convertir JPG a texto y corregir
  la rotación de la imagen.
og_title: Cómo enderezar una imagen en C# – Tutorial rápido de Aspose OCR
tags:
- OCR
- C#
- Aspose
title: Cómo enderezar una imagen en C# – Guía completa usando Aspose OCR
url: /es/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo corregir la inclinación de una imagen en C# – Guía completa usando Aspose OCR

¿Alguna vez te has preguntado **cómo corregir la inclinación de una imagen** que salió de un escáner inclinada en un ángulo extraño? No estás solo—muchos desarrolladores se topan con ese problema cuando intentan extraer texto de recibos, facturas o notas manuscritas. La buena noticia es que con Aspose OCR puedes corregir la rotación de la imagen y obtener texto limpio y buscable con solo unas pocas líneas.

En este tutorial recorreremos todo el proceso: desde instalar la biblioteca, habilitar la corrección automática de inclinación, hasta reconocer la imagen de texto y finalmente convertir un JPG a texto. Al final tendrás una aplicación de consola lista para ejecutar que **recognize text jpg** files sin necesidad de rotarlos manualmente primero.

## Lo que necesitarás

- **.NET 6.0** o posterior (el código funciona tanto en .NET Core como en .NET Framework)  
- Paquete NuGet **Aspose.OCR for .NET** – se recomienda la versión 23.12 o superior  
- Un **JPEG inclinado** de ejemplo (p.ej., `skewed_receipt.jpg`) colocado en un lugar que tu aplicación pueda leer  
- Visual Studio, VS Code, o cualquier editor de C# que prefieras  

No se requieren otras herramientas de terceros. La biblioteca maneja la corrección de inclinación, OCR e incluso la detección de idioma internamente.

![ejemplo de cómo corregir la inclinación de la imagen](/images/deskew-example.png "cómo corregir la inclinación de la imagen usando Aspose OCR")

## Paso 1: Configurar el proyecto e instalar Aspose.OCR

Para mantener todo ordenado, inicia un nuevo proyecto de consola:

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

La línea `dotnet add package` descarga los binarios de **Aspose.OCR** junto con todas las dependencias nativas. Si estás en Windows obtendrás los DLLs nativos automáticamente; en Linux/macOS puede que necesites el paquete `libgdiplus`, pero es una instalación única.

## Paso 2: Habilitar la corrección automática de inclinación (Corregir rotación de la imagen)

Ahora abre `Program.cs` y reemplaza su contenido con el código a continuación. La línea clave aquí es `ocrEngine.Settings.Deskew = true;` – esa es la bandera que indica al motor **cómo corregir la inclinación de la imagen** automáticamente.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### ¿Por qué habilitar la corrección de inclinación?

Cuando un escáner alimenta una página en ángulo, la línea base del texto está inclinada. Los motores OCR tradicionales leerían cada carácter como una versión inclinada, reduciendo drásticamente la precisión. Al establecer `Deskew = true`, Aspose OCR ejecuta una rápida transformación de Hough internamente, rota el mapa de bits de vuelta a la horizontal y luego realiza el reconocimiento. El resultado es el mismo que si hubieras rotado manualmente la imagen en Photoshop, solo que más rápido y totalmente automatizado.

## Paso 3: Reconocer la imagen de texto y convertir JPG a texto

La llamada `Recognize` hace dos cosas a la vez:

1. **Corrige la inclinación** de la imagen (porque activamos la bandera).  
2. **Extrae** el contenido textual, devolviéndolo en un objeto `OcrResult`.

Puedes tratar `ocrResult.Text` como una cadena simple, escribirla a un archivo o pasarla a tuberías de procesamiento posteriores. Si necesitas los puntajes de confianza sin procesar por palabra, `ocrResult.Words` te brinda una colección con valores `Confidence`.

### Ejemplo de salida

Suponiendo que `skewed_receipt.jpg` contenga un recibo simple, podrías ver algo como:

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

Observa cómo los números se alinean correctamente a pesar de que la imagen original esté rotada aproximadamente 7°. Esa es la magia de la **rotación correcta de la imagen** incorporada en la biblioteca.

## Paso 4: Ejecutar el ejemplo y verificar los resultados

Compila y ejecuta:

```bash
dotnet run
```

Si todo está configurado correctamente verás el texto extraído impreso en la consola. Si obtienes una excepción como `FileNotFoundException`, verifica nuevamente la ruta a tu JPEG y asegura que el archivo sea legible.

### Errores comunes y consejos profesionales

- **Imágenes grandes** – El uso de memoria del OCR crece con las dimensiones de la imagen. Redimensiona archivos demasiado grandes (p.ej., > 3000 px de ancho) antes de enviarlos al motor.  
- **Scripts no latinos** – Por defecto el motor asume inglés. Establece `ocrEngine.Settings.Language = OcrLanguage.French;` (o cualquier idioma soportado) si necesitas **recognize text image** en otros alfabetos.  
- **Procesamiento por lotes** – Para muchos archivos, reutiliza la misma instancia de `OcrEngine`; crear un nuevo motor por archivo genera una sobrecarga innecesaria.  
- **Verificación de calidad** – Después de corregir la inclinación puedes exportar el mapa de bits corregido mediante `ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");` para verificar visualmente la corrección de rotación.

## Ejemplo completo funcional (Todo junto)

A continuación se muestra el programa completo y autónomo que puedes copiar y pegar en `Program.cs`. Incluye comentarios, manejo de errores y un paso opcional para guardar la imagen corregida.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

Ejecutar el programa **recognize text jpg** files, automatically correct any skew, and print clean, searchable text to the console.

## Conclusión

Ahora tienes un fragmento sólido y listo para producción que muestra **cómo corregir la inclinación de una imagen** y extraer su contenido usando Aspose OCR. El enfoque funciona para recibos, facturas, contratos escaneados o cualquier JPEG donde el texto no esté perfectamente horizontal.

Próximos pasos que podrías explorar:

- **Procesamiento por lotes** de una carpeta de JPEGs y escribir cada resultado en un archivo `.txt` (vuelve a *convert jpg to text*).  
- Integrar el paso OCR en una API ASP.NET Core para que los clientes puedan subir imágenes y recibir texto en formato JSON.  
- Experimentar con diferentes configuraciones OCR como `ocrEngine.Settings.Language` o `ocrEngine.Settings.RecognitionMode` para mejorar la precisión en documentos que no están en inglés.

Pruébalo, ajusta la configuración y deja que el motor haga el trabajo pesado. Como siempre, si encuentras algún problema o tienes una optimización ingeniosa para compartir, deja un comentario abajo. ¡Feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}