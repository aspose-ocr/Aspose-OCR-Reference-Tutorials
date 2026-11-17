---
category: general
date: 2026-03-26
description: como fazer OCR em lote de forma eficiente usando Python — aprenda a extrair
  texto de imagens e a conversão OCR de PDFs com processamento paralelo.
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: pt
og_description: como fazer OCR em lote de forma eficiente — guia passo a passo para
  extrair texto de imagens, conversão OCR de PDF e processamento em lote de OCR usando
  Python.
og_title: 'como fazer OCR em lote: extração rápida de texto em paralelo'
tags:
- OCR
- Python
- Parallel Computing
title: 'como fazer OCR em lote: extração rápida de texto em paralelo'
url: /pt/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# como fazer batch ocr: extração de texto paralela rápida

Já se perguntou **como fazer batch ocr** quando você tem dezenas de páginas escaneadas, capturas de tela e PDFs espalhados por aí? Você não está sozinho — a maioria dos desenvolvedores bate na mesma parede: processar cada arquivo um‑por‑um se torna um gargalo doloroso.  

A boa notícia é que você pode iniciar um pequeno conjunto de threads de trabalho, alimentar todas as suas arquivos e observar o motor OCR devorar o lote em paralelo. Neste tutorial vamos percorrer um exemplo completo, pronto‑para‑executar, que mostra **extract text from images**, realiza **pdf ocr conversion** e aproveita **parallel ocr processing** para velocidade.

> **O que você levará consigo**  
> * Um script Python totalmente funcional que processa uma lista mista de arquivos PNG, TIFF, PDF e JPG de uma só vez.  
> * Entendimento de por que um pool de threads acelera tarefas de OCR ligadas a I/O.  
> * Dicas para lidar com erros, PDFs grandes e contagens de threads personalizadas.  

## Prerequisites

Antes de mergulharmos, certifique‑se de que você tem:

| Requirement | Reason |
|-------------|--------|
| Python 3.8+ | Sintaxe moderna & `concurrent.futures` |
| `ocr` library (or any compatible OCR wrapper) | Provides `OcrBatchProcessor` and result objects |
| A handful of sample files (PNG, TIFF, PDF, JPG) | To see the **extract text from images** in action |
| Basic familiarity with threads (optional) | Helpful but not mandatory |

Se ainda não instalou o pacote `ocr`, execute:

```bash
pip install ocr-lib   # replace with the actual package name
```

Agora que o ambiente está pronto, vamos dividir o problema.

## Step 1: Import helpers and instantiate the batch processor

A primeira coisa que precisamos é um local para coletar todos os trabalhos de OCR. A classe `OcrBatchProcessor` faz exatamente isso — enfileira itens de trabalho e devolve uma lista de objetos `Future`.

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*Why this matters*: Importar `as_completed` nos permite reagir a cada trabalho concluído instantaneamente, em vez de esperar pelo arquivo mais lento. Este é o núcleo do **batch ocr processing**.

## Step 2: Tune the worker pool for parallel execution

Por padrão o processador pode usar uma única thread, o que anula o propósito do batching. Pedimos explicitamente quatro workers — sinta‑se à vontade para aumentar esse número até o número de núcleos de CPU que você possui.

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*Pro tip*: Para tarefas I/O‑bound como OCR, você costuma obter retornos decrescentes após `CPU cores * 2`. Teste alguns valores e escolha o ponto ideal.

## Step 3: Queue every file you want to OCR

Aqui adicionamos um conjunto misto de arquivos de imagem e PDF. O método `add` simplesmente registra o caminho; o trabalho real só começará quando enviarmos o lote.

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

Se precisar processar uma pasta inteira, um rápido loop `glob` resolve:

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## Step 4: Fire off the jobs and collect futures

Chamar `submit_all` dá ao processador o sinal verde. Ele retorna uma lista de objetos `Future` — pense neles como placeholders para resultados que aparecerão mais tarde.

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

Neste ponto o motor OCR está ocupado em segundo plano, cada thread mastigando um arquivo.

## Step 5: Pull results as soon as they finish

Usando `as_completed` iteramos sobre os futures na ordem em que terminam, não na ordem em que foram enviados. Isso mantém nosso script responsivo, especialmente quando alguns PDFs demoram mais que PNGs simples.

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**Expected output** (truncated for brevity):

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

Cada bloco corresponde à representação em texto puro do arquivo original. Se você estiver fazendo **pdf ocr conversion**, o texto incluirá tudo que o motor OCR conseguiu decifrar de cada página.

## Handling Edge Cases & Common Pitfalls

| Situation | What to watch for | Quick fix |
|-----------|-------------------|-----------|
| A corrupted image | `future.result()` raises `OSError` | Wrap in `try/except` (see code above) |
| Very large PDFs ( > 100 MB ) | Memory pressure, slower threads | Increase `thread_count` modestly or split PDF into chapters first |
| Mixed language documents | Default OCR model may mis‑detect | Pass language hints to `OcrBatchProcessor` if the library supports it |
| Need to preserve layout | Plain `get_text()` loses columns | Use `ocr_result.get_hocr()` or similar layout‑aware method |

### Pro tip: Custom thread count based on file type

Se você sabe que a maior parte da sua carga de trabalho são PDFs, pode alocar mais threads para eles e menos para PNGs pequenos. Algumas bibliotecas permitem passar uma `priority` por job; caso contrário, você pode criar dois lotes separados — um para imagens, outro para PDFs — e executá‑los simultaneamente.

## Visual Overview (optional)

![diagrama do fluxo de batch ocr](https://example.com/ocr-workflow.png "fluxo de batch ocr")

*O diagrama ilustra o fluxo desde a descoberta de arquivos → criação do lote → execução paralela → agregação de resultados.*

## Full Script You Can Copy‑Paste

Abaixo está o programa completo, pronto para ser colocado em um arquivo `.py`. Ele inclui todos os trechos acima, além de um pequeno helper que descobre automaticamente arquivos suportados em um diretório.

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

Salve isso como `batch_ocr.py`, aponte para uma pasta contendo seus escaneamentos e observe o console se encher de texto extraído.  

### Why this works

* **Thread pool** – OCR passa a maior parte do tempo aguardando I/O de disco e chamadas ao motor externo, então múltiplas threads mantêm a CPU ocupada.  
* **`as_completed`** – Você obtém resultados assim que eles ficam prontos, o que é ideal para feedback de UI ou pipelines de streaming.  
* **Error isolation** – Um arquivo ruim não derruba todo o lote; o bloco `try/except` isola as falhas.

## Conclusion

Em resumo, agora você sabe **como fazer batch ocr** usando `concurrent.futures` do Python junto com uma biblioteca OCR que suporta processamento em lote. Ao configurar um pool de threads modesto, enfileirar cada arquivo suportado e puxar os resultados à medida que terminam, você obtém **parallel ocr processing** rápido sem sacrificar a confiabilidade.  

A partir daqui você pode:

* Conectar a saída a um índice de busca para recuperação rápida de documentos.  
* Estender o script para gravar cada resultado em um arquivo `.txt` ao lado do original.  
* Substituir o pool de threads interno por `asyncio` se sua biblioteca OCR oferecer APIs assíncronas.  

Continue experimentando — troque por Tesseract, Azure Cognitive Services ou Google Vision, e verá que o mesmo padrão se aplica. Boa extração de OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}