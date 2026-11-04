---
category: general
date: 2026-06-06
description: Extraia texto de PDFs de imagens usando OCR em Python. Aprenda como converter
  documentos escaneados em texto rapidamente com reconhecimento em lote assíncrono.
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: pt
og_description: Extrair texto de PDFs de imagens com Python. Este guia passo a passo
  mostra como converter documentos escaneados em texto usando OCR assíncrono.
og_title: Extrair Texto de PDFs de Imagens – Tutorial de OCR em Python
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Extrair Texto de PDFs de Imagens – Guia Python para Converter Documentos Escaneados
  em Texto
url: /pt/python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de PDFs de Imagens – Guia Python para Converter Documentos Escaneados em Texto

Já precisou **extrair texto de PDFs de imagens** sem gastar horas digitando novamente? Neste guia, mostraremos como **converter documentos escaneados em texto** usando um fluxo de trabalho OCR assíncrono simples em Python.  

Se você já ficou encarando uma pilha de PDFs escaneados e pensou: “Tem que haver uma maneira mais rápida”, você está no lugar certo. Vamos percorrer cada linha de código, explicar por que cada parte importa e até cobrir alguns casos limites que você pode encontrar.

## O que Você Vai Aprender

- Como iniciar um motor OCR e definir o idioma de reconhecimento.  
- A mecânica de alimentar uma lista mista de PNGs e PDFs em um reconhecedor em lote.  
- Executar o trabalho OCR de forma assíncrona para que seu aplicativo permaneça responsivo.  
- Recuperar os resultados, associá‑los aos arquivos de origem e imprimir uma saída limpa.  

**Pré‑requisitos**: Python 3.8+, compreensão básica de `asyncio` ou `concurrent.futures`, e uma biblioteca OCR que exponha uma classe `OcrEngine` semelhante à do exemplo (por exemplo, Aspose.OCR, wrapper do Tesseract ou um wrapper personalizado). Nenhuma configuração pesada necessária—basta instalar a biblioteca e você está pronto para usar.

![extrair texto de PDFs de imagens](https://example.com/placeholder.png "Captura de tela da saída OCR – extrair texto de PDFs de imagens")

## Extrair Texto de PDFs de Imagens – Configurando o Motor OCR

A primeira coisa que você precisa é uma instância do motor OCR configurada para o idioma dos seus documentos. No nosso caso, usaremos francês, mas você pode trocá‑lo por qualquer idioma suportado.

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**Por que isso importa**: Definir o idioma antecipadamente melhora drasticamente a precisão. O motor usa dicionários e modelos de caracteres específicos do idioma; alimentá‑lo com o idioma errado é uma fonte comum de saída confusa.

## Prepare a Lista de Arquivos – Imagens e PDFs Juntos

Nosso reconhecedor em lote pode lidar tanto com imagens raster (`.png`, `.jpg`) quanto com contêineres PDF. Basta fornecer uma simples lista Python de caminhos de arquivos.

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**Dica**: Mantenha a lista plana; o motor desempacotará internamente cada página PDF em imagens antes do reconhecimento. Se você tem milhares de arquivos, considere dividir a lista em lotes menores para evitar picos de memória.

## Inicie o Reconhecimento em Lote Assíncrono

Em vez de bloquear a thread principal, iniciamos o trabalho OCR em segundo plano. O método retorna um `Future` que eventualmente conterá uma lista de objetos `OcrResult`.

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**Como funciona**: Nos bastidores, o motor cria um pool de threads (ou uma tarefa assíncrona, dependendo da implementação). Isso permite que você continue fazendo outras tarefas—como atualizar uma UI, buscar mais arquivos ou registrar progresso—enquanto o processamento pesado ocorre em outro lugar.

## Faça Algo Útil Enquanto o OCR Executa

Um erro comum é ficar ocioso e sondar o futuro em um loop apertado. Em vez disso, você pode executar qualquer trabalho não relacionado. Para demonstração, vamos apenas imprimir uma linha de status.

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## Recolha os Resultados Quando o Future Completar

Quando estiver pronto para coletar a saída OCR, use `as_completed` de `concurrent.futures`. Esse padrão funciona tanto com um futuro quanto com vários.

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**O que você verá**: Cada caminho de arquivo seguido da representação de texto simples extraído. Para PDFs, `result.text` contém o texto concatenado de todas as páginas.

### Saída Esperada (exemplo)

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

Se você notar caracteres ausentes, verifique se o idioma definido corresponde ao idioma do documento e considere pré‑processar as imagens (corrigir inclinação, aumentar contraste) antes de enviá‑las ao motor.

## Lidando com Casos Limites e Armadilhas Comuns

| Situação | O que Fazer |
|-----------|------------|
| **Idiomas mistos** | Execute uma passagem de detecção de idioma primeiro, então instancie motores separados por idioma. |
| **PDFs enormes (> 100 MB)** | Divida o PDF em páginas individuais no disco (por exemplo, usando `PyPDF2`) e alimente‑as como entradas separadas. |
| **Scripts não latinos** | Garanta que a biblioteca OCR inclua o pacote de idioma necessário; algumas bibliotecas exigem que você baixe arquivos de dados adicionais. |
| **Gargalo de desempenho** | Aumente o tamanho do pool de threads (`engine.set_thread_pool_size(8)`) ou troque para um backend acelerado por GPU, se disponível. |
| **Texto ausente em imagens de baixa resolução** | Pré‑procese com OpenCV: `cv2.resize`, `cv2.threshold` e `cv2.medianBlur` para melhorar a legibilidade. |

## Exemplo Completo Funcionando (Pronto para Copiar‑Colar)

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

Salve isso como `extract_text_async.py`, substitua `YOUR_DIRECTORY` pelo caminho dos seus arquivos, instale o pacote OCR (`pip install your-ocr-lib`) e execute `python extract_text_async.py`. Você deverá ver a saída no console ilustrada anteriormente.

## Próximos Passos – Indo Além da Extração Básica

- **Pós‑processamento**: Remover espaços em branco extras, normalizar Unicode (`unicodedata.normalize`) ou executar um verificador ortográfico para limpar o ruído do OCR.  
- **Saída estruturada**: Exportar resultados para CSV, JSON ou diretamente para um banco de dados para busca posterior.  
- **Lotes paralelos**: Se você tem centenas de arquivos, inicie múltiplos futures e use uma fila para manter a CPU ocupada sem sobrecarregar a memória.  
- **Integração com frameworks web**: Conectar este script a um endpoint Flask ou FastAPI para fornecer OCR sob demanda como serviço.

---

### TL;DR

Agora você sabe como **extrair texto de PDFs de imagens** com um script Python mínimo que executa OCR de forma assíncrona, permitindo **converter documentos escaneados em texto** enquanto seu programa permanece responsivo. Brinque com as configurações de idioma, tamanhos de lote e truques de pré‑processamento para extrair a máxima precisão de caracteres.

Tem alguma variação que gostaria de compartilhar—talvez OCR em notas manuscritas ou um serviço baseado em nuvem? Deixe um comentário e feliz codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Extrair Texto de Imagem com Aspose OCR – Guia Passo a Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extrair Texto de Imagens Usando Operação OCR em Pastas](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extrair Texto de Imagens Usando Aspose.OCR – Caracteres Permitidos](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}