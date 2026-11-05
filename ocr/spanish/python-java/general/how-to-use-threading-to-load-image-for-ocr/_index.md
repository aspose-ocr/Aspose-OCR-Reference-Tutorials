---
category: general
date: 2026-04-26
description: Cómo usar hilos para cargar imágenes para OCR en Python. Aprende el procesamiento
  OCR asíncrono con callbacks, hilos en segundo plano y carga de imágenes en solo
  unos pocos pasos.
draft: false
keywords:
- how to use threading
- load image for OCR
- python threading OCR
- async OCR callback
- background thread image processing
language: es
og_description: Cómo usar hilos para cargar una imagen para OCR en Python. Esta guía
  muestra un ejemplo completo y ejecutable con callbacks y ejecución en segundo plano.
og_title: Cómo usar hilos para cargar imágenes para OCR
tags:
- Python
- Threading
- OCR
- Image Processing
title: Cómo usar hilos para cargar imágenes para OCR
url: /es/python-java/general/how-to-use-threading-to-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar threading para cargar una imagen para OCR

¿Alguna vez te has preguntado **cómo usar threading** para cargar una imagen para OCR sin congelar tu aplicación? Es un escenario que aparece tanto si estás construyendo un escáner de escritorio, un servicio web o un script sencillo que procesa imágenes masivas. ¿La buena noticia? Unas pocas líneas de Python y el patrón de threading adecuado mantendrán tu UI ágil mientras el motor OCR hace su magia.

En este tutorial recorreremos un ejemplo completo, de extremo a extremo: cargar un PNG grande, iniciar OCR en un hilo en segundo plano y manejar el resultado con una devolución de llamada. Al final no solo sabrás **cómo usar threading**, sino también cómo **cargar una imagen para OCR** de forma limpia y reutilizable.

## Lo que necesitarás

- Python 3.9+ (la sintaxis que usamos funciona en cualquier versión reciente)
- `pillow` para manejo de imágenes (`pip install pillow`)
- `pytesseract` como un contenedor ligero alrededor de Tesseract OCR (`pip install pytesseract`)
- Motor Tesseract OCR instalado en tu máquina (descarga desde [tesseract‑ocr.org](https://github.com/tesseract-ocr/tesseract))
- Un archivo de imagen grande que quieras procesar (`large_image.png` en esta guía)

Sin frameworks adicionales, sin async/await—solo `threading` clásico y una devolución de llamada.

## Paso 1: Importar el módulo threading (Requerido para ejecución en segundo plano)

Lo primero que hacemos es importar el módulo `threading`. Este nos proporciona la clase `Thread`, que nos permite ejecutar cualquier función en un hilo del sistema operativo separado.

```python
import threading
```

*Por qué es importante*: Si ejecutas OCR en el hilo principal, tu programa (especialmente una GUI) se congelará hasta que OCR termine. Al delegar el trabajo a un hilo en segundo plano, el hilo principal queda libre para actualizar la UI, manejar la entrada del usuario o iniciar otras tareas.

## Paso 2: Definir una devolución de llamada que se invocará cuando OCR termine

Una devolución de llamada es simplemente una función que otro fragmento de código llama cuando ha terminado. Aquí imprimiremos el texto reconocido, pero podrías almacenarlo, enviarlo a través de la red o actualizar un widget de la UI.

```python
def ocr_done(result_text: str) -> None:
    """Called when the OCR thread finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)   # Display the recognized text
```

*Consejo profesional*: Mantén la devolución de llamada ligera. Un procesamiento pesado dentro de la devolución de llamada anula el propósito del threading porque seguirá bloqueando el hilo que la llamó (a menudo el hilo principal).

## Paso 3: Cargar la imagen que deseas procesar

Cargar la imagen es una preocupación separada de OCR, pero sigue siendo parte del flujo de trabajo general. Usar Pillow hace esto trivial.

```python
from PIL import Image

def load_image(path: str) -> Image.Image:
    """Loads an image from disk and returns a Pillow Image object."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img
    except Exception as exc:
        raise RuntimeError(f"Failed to load image: {exc}") from exc
```

*Por qué lo hacemos aquí*: Si la imagen es enorme, cargarla en el hilo principal ya podría causar un tropiezo. En muchas aplicaciones reales también descargarías la carga a un hilo, pero para mayor claridad la mantenemos sincrónica.

## Paso 4: Crear un pequeño contenedor (wrapper) para el motor OCR

El fragmento original usaba `engine.process_async`. Imitaremos eso con una pequeña clase que inicia un hilo internamente y llama a la devolución de llamada suministrada cuando termina.

```python
import pytesseract

class SimpleOcrEngine:
    """A minimal OCR engine that runs pytesseract in a background thread."""

    def __init__(self, image: Image.Image):
        self.image = image

    def _run_ocr(self, callback):
        """Internal method executed in the worker thread."""
        try:
            # pytesseract returns the recognized text as a plain string
            text = pytesseract.image_to_string(self.image)
            callback(text)
        except Exception as exc:
            callback(f"OCR failed: {exc}")

    def process_async(self, callback):
        """Public method to start OCR on a new thread."""
        worker = threading.Thread(target=self._run_ocr, args=(callback,))
        worker.daemon = True          # Daemon so it won’t block program exit
        worker.start()
        print("OCR thread started…")
```

*Explicación*:  
- `_run_ocr` realiza el trabajo pesado.  
- `process_async` crea un objeto `Thread`, lo marca como daemon (para que el intérprete pueda salir incluso si el hilo sigue ejecutándose) y lo inicia.  
- La devolución de llamada recibe ya sea el texto OCR o un mensaje de error.

## Paso 5: Unir todo y hacer otro trabajo mientras OCR se ejecuta

Ahora orquestamos todo el flujo: cargar la imagen, instanciar el motor, lanzar el OCR asíncrono y mantener el hilo principal ocupado con otra cosa (aquí simplemente imprimimos un mensaje).

```python
if __name__ == "__main__":
    # 1️⃣ Load the image you want to OCR
    img_path = "YOUR_DIRECTORY/large_image.png"
    image = load_image(img_path)

    # 2️⃣ Create the OCR engine instance
    engine = SimpleOcrEngine(image)

    # 3️⃣ Start OCR on a background thread, passing our callback
    engine.process_async(callback=ocr_done)

    # 4️⃣ Do other work while OCR runs (simulated with a loop)
    for i in range(5):
        print(f"Main thread doing other work… ({i+1}/5)")
        # In a real app you might update a progress bar, handle UI events, etc.
        threading.Event().wait(0.5)  # Sleep 0.5 s without blocking the OS thread

    # Give the OCR thread a moment to finish before the script exits
    threading.Event().wait(2)
    print("Script finished.")
```

**Salida esperada (truncada por brevedad):**

```
Image 'YOUR_DIRECTORY/large_image.png' loaded – size: (3840, 2160)
OCR thread started…
Main thread doing other work… (1/5)
Main thread doing other work… (2/5)
...
--- Async OCR finished ---
The quick brown fox jumps over the lazy dog.
Script finished.
```

Si OCR falla, la devolución de llamada imprimirá un mensaje de error en lugar del texto.

---

## Por qué este enfoque funciona mejor que un bucle simple

- **Responsiveness**: El hilo principal nunca se bloquea en la llamada a OCR, que puede tardar segundos para imágenes grandes.
- **Scalability**: Puedes iniciar múltiples instancias de `SimpleOcrEngine`, cada una en su propio hilo, para procesar un lote de imágenes concurrentemente.
- **Separation of Concerns**: La carga, el procesamiento y el manejo de resultados están claramente separados, lo que hace que el código sea más fácil de probar y mantener.

## Errores comunes y cómo evitarlos

| Pitfall | What Happens | Fix |
|---------|--------------|-----|
| Olvidar marcar el hilo como *daemon* | El script se queda colgado después de que el trabajo principal termina porque el hilo OCR sigue vivo. | Establecer `worker.daemon = True` **or** `join()` el hilo antes de salir. |
| Usar una variable global para el resultado sin bloqueos | Las condiciones de carrera pueden corromper los datos cuando varios hilos escriben simultáneamente. | Pasar el resultado mediante una devolución de llamada (como hacemos) o usar contenedores seguros para hilos como `queue.Queue`. |
| Cargar una imagen masiva en el hilo principal | La UI se congela antes de que OCR en segundo plano siquiera comience. | Descargar la carga de la imagen a un hilo también, o usar técnicas de carga perezosa. |
| No manejar excepciones dentro del hilo de trabajo | Excepciones no capturadas matan silenciosamente el hilo, dejándote sin resultado. | Envolver la lógica OCR en `try/except` y reenviar el error a la devolución de llamada. |

## Extender este patrón

- **Progress Reporting**: Usa un `queue.Queue` compartido para enviar porcentajes de progreso intermedios desde el hilo OCR al hilo principal.
- **Thread Pool**: Para procesamiento por lotes, reemplaza objetos `Thread` individuales con un `concurrent.futures.ThreadPoolExecutor`.
- **GUI Integration**: En una aplicación Tkinter o PyQt, programa la devolución de llamada con `after()` (Tkinter) o `QTimer.singleShot` (Qt) para asegurar que las actualizaciones de UI ocurran en el hilo principal.

## Ejemplo completo funcional (listo para copiar‑pegar)

```python
import threading
from PIL import Image
import pytesseract

def ocr_done(result_text: str) -> None:
    """Callback invoked when OCR finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)

def load_image(path: str) -> Image.Image:
    """Load an image and report its size."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}