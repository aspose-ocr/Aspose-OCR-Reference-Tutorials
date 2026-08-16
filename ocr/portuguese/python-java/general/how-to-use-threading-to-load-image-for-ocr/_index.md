---
category: general
date: 2026-04-26
description: Como usar threading para carregar imagem para OCR em Python. Aprenda
  o processamento assíncrono de OCR com callbacks, threads em segundo plano e carregamento
  de imagens em apenas alguns passos.
draft: false
keywords:
- how to use threading
- load image for OCR
- python threading OCR
- async OCR callback
- background thread image processing
language: pt
og_description: Como usar threading para carregar imagem para OCR em Python. Este
  guia mostra um exemplo completo e executável com callbacks e execução em segundo
  plano.
og_title: Como usar threading para carregar imagem para OCR
tags:
- Python
- Threading
- OCR
- Image Processing
title: Como usar Threading para carregar imagem para OCR
url: /pt/python-java/general/how-to-use-threading-to-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar Threading para Carregar Imagem para OCR

Já se perguntou **como usar threading** para carregar imagem para OCR sem congelar seu aplicativo? É um cenário que aparece tanto se você está construindo um scanner de desktop, um serviço web ou um script simples que processa imagens massivas. A boa notícia? Algumas linhas de Python e o padrão correto de threading manterão sua UI ágil enquanto o motor OCR faz sua mágica.

Neste tutorial vamos percorrer um exemplo completo, de ponta a ponta: carregar um PNG grande, iniciar o OCR em uma thread em segundo plano e tratar o resultado com um callback. Ao final você não apenas saberá **como usar threading**, mas também como **carregar imagem para OCR** de forma limpa e reutilizável.

## O que você precisará

- Python 3.9+ (a sintaxe que usamos funciona em qualquer versão recente)
- `pillow` para manipulação de imagens (`pip install pillow`)
- `pytesseract` como um wrapper leve ao Tesseract OCR (`pip install pytesseract`)
- Motor Tesseract OCR instalado na sua máquina (download em [tesseract‑ocr.org](https://github.com/tesseract-ocr/tesseract))
- Um arquivo de imagem grande que você deseja processar (`large_image.png` neste guia)

Sem frameworks extras, sem async/await — apenas `threading` clássico e um callback.

## Etapa 1: Importar o módulo Threading (necessário para execução em segundo plano)

A primeira coisa que fazemos é trazer o módulo `threading`. Ele nos fornece a classe `Thread`, que permite executar qualquer função em uma thread do SO separada.

```python
import threading
```

*Por que isso importa*: Se você executar OCR na thread principal, seu programa (especialmente uma GUI) congelará até que o OCR termine. Ao delegar o trabalho para uma thread em segundo plano, a thread principal fica livre para atualizar a UI, lidar com entrada do usuário ou iniciar outras tarefas.

## Etapa 2: Definir um Callback que será Invocado Quando o OCR Terminar

Um callback é simplesmente uma função que outro trecho de código chama quando termina. Aqui vamos imprimir o texto reconhecido, mas você poderia armazená‑lo, enviá‑lo pela rede ou atualizar um widget da UI.

```python
def ocr_done(result_text: str) -> None:
    """Called when the OCR thread finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)   # Display the recognized text
```

*Dica de especialista*: Mantenha o callback leve. Processamento pesado dentro do callback anula o propósito do threading porque ainda bloqueará a thread que o chamou (geralmente a thread principal).

## Etapa 3: Carregar a Imagem que Você Quer Processar

Carregar a imagem é uma preocupação separada do OCR, mas ainda faz parte do fluxo geral. Usar Pillow torna isso trivial.

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

*Por que fazemos isso aqui*: Se a imagem for enorme, carregá‑la na thread principal já pode causar um travamento. Em muitos aplicativos reais você também descarregaria o carregamento para uma thread, mas para clareza mantemos síncrono.

## Etapa 4: Criar um Pequeno Wrapper de Motor OCR

O trecho original usava `engine.process_async`. Vamos imitar isso com uma classe pequena que inicia uma thread internamente e chama o callback fornecido quando termina.

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

*Explicação*:  
- `_run_ocr` faz o trabalho pesado.  
- `process_async` cria um objeto `Thread`, marca‑o como daemon (para que o interpretador possa sair mesmo que a thread ainda esteja em execução) e o inicia.  
- O callback recebe ou o texto do OCR ou uma mensagem de erro.

## Etapa 5: Unir Tudo e Fazer Outro Trabalho Enquanto o OCR Executa

Agora orquestramos todo o fluxo: carregamos a imagem, instanciamos o motor, dispararmos o OCR assíncrono e mantemos a thread principal ocupada com outra coisa (aqui apenas imprimimos uma mensagem).

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

**Saída esperada (truncada para brevidade):**

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

Se o OCR falhar, o callback imprimirá uma mensagem de erro em vez do texto.

---

## Por que Essa Abordagem Funciona Melhor do que um Loop Simples

- **Responsividade**: A thread principal nunca bloqueia na chamada ao OCR, que pode levar segundos para imagens grandes.  
- **Escalabilidade**: Você pode iniciar múltiplas instâncias de `SimpleOcrEngine`, cada uma em sua própria thread, para processar um lote de imagens simultaneamente.  
- **Separação de Responsabilidades**: Carregamento, processamento e tratamento de resultados são claramente separados, facilitando testes e manutenção.

## Armadilhas Comuns e Como Evitá‑las

| Armadilha | O que Acontece | Solução |
|-----------|----------------|---------|
| Esquecer de marcar a thread como *daemon* | O script fica pendurado após o trabalho principal terminar porque a thread OCR ainda está viva. | Defina `worker.daemon = True` **ou** chame `join()` na thread antes de sair. |
| Usar uma variável global para o resultado sem locks | Condições de corrida podem corromper os dados quando múltiplas threads escrevem simultaneamente. | Passe o resultado via callback (como fazemos) ou use contêineres thread‑safe como `queue.Queue`. |
| Carregar uma imagem massiva na thread principal | A UI congela antes que o OCR em segundo plano sequer inicie. | Descarregue o carregamento da imagem para uma thread também, ou use técnicas de carregamento preguiçoso. |
| Não tratar exceções dentro da thread de trabalho | Exceções não capturadas matam silenciosamente a thread, deixando‑a sem resultado. | Envolva a lógica do OCR em `try/except` e encaminhe o erro para o callback. |

## Expandindo Esse Padrão

- **Relatório de Progresso**: Use um `queue.Queue` compartilhado para enviar percentuais de progresso intermediários da thread OCR para a thread principal.  
- **Thread Pool**: Para processamento em lote, substitua objetos `Thread` individuais por um `concurrent.futures.ThreadPoolExecutor`.  
- **Integração com GUI**: Em um app Tkinter ou PyQt, agende o callback com `after()` (Tkinter) ou `QTimer.singleShot` (Qt) para garantir que as atualizações da UI ocorram na thread principal.

## Exemplo Completo Funcionando (Pronto para Copiar‑Colar)

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