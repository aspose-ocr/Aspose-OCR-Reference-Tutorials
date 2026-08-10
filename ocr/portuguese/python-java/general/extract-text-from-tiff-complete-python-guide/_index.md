---
category: general
date: 2026-06-16
description: Extraia texto de arquivos TIFF usando OCR em Python. Aprenda como converter
  TIFF em texto passo a passo, manipulando documentos de várias páginas com facilidade.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: pt
og_description: Extraia texto de arquivos TIFF com OCR em Python. Siga este guia para
  converter TIFF em texto, lidar com digitalizações de várias páginas e obter resultados
  limpos.
og_title: Extrair Texto de TIFF – Guia Completo de Python
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: Extrair Texto de TIFF – Guia Completo de Python
url: /pt/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de TIFF – Guia Completo em Python

Já precisou **extrair texto de imagens TIFF** mas não sabia por onde começar? Você não está sozinho—muitos desenvolvedores enfrentam esse obstáculo ao lidar com arquivos escaneados ou documentos legados. A boa notícia? Com algumas linhas de Python você pode **converter TIFF em texto** em um instante, mesmo quando o arquivo contém dezenas de páginas.

Neste tutorial vamos percorrer um exemplo real: carregar um TIFF multipágina, definir o idioma do OCR para francês e extrair o texto reconhecido de cada página. Ao final você terá um script pronto para executar, entenderá por que cada passo é importante e saberá como adaptá‑lo para outros idiomas ou formatos de imagem.

## Pré‑requisitos

Antes de mergulharmos, certifique‑se de que você tem:

- Python 3.8 ou superior instalado.
- O pacote `ocr` (ou qualquer biblioteca OCR compatível que ofereça a classe `OcrEngine`). Você pode instalá‑lo com `pip install ocr-lib`—substitua pelo nome real do pacote que está usando.
- Um arquivo TIFF multipágina (por exemplo, `french-scans.tif`) que você deseja processar.
- Familiaridade básica com scripts em Python.

Sem dependências pesadas, sem serviços externos—apenas Python puro e um motor OCR.

---

## Etapa 1: Configurar o Motor OCR para **Extrair Texto de TIFF**

Primeiro de tudo—precisamos de uma instância do motor OCR e devemos informar qual idioma usar. No nosso caso o material de origem está em francês, então definiremos o idioma adequadamente.

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**Por que isso importa:**  
A configuração do idioma melhora drasticamente a precisão. Caracteres franceses como “é” ou “ç” seriam lidos como símbolos genéricos se o motor permanecer no padrão inglês. Ao selecionar explicitamente o francês fornecemos ao motor o mapa de caracteres correto.

> **Dica profissional:** Se você estiver processando documentos em vários idiomas, pode alterar `engine.language` dinamicamente antes de cada chamada a `recognize()`.

---

## Etapa 2: Carregar o TIFF Multipágina que Você Quer **Converter TIFF em Texto**

Um TIFF pode conter vários quadros—pense em cada quadro como uma página separada. A biblioteca OCR abstrai isso para nós, então basta apontá‑la para o arquivo.

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**Alerta de caso extremo:**  
Se o caminho do arquivo estiver errado ou o TIFF estiver corrompido, o método `load_from_file` lançará uma exceção. Envolva‑a em um bloco `try/except` para código de produção:

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## Etapa 3: Executar OCR em Todo o Documento – O Núcleo de **Extrair Texto de TIFF**

Agora deixamos o motor fazer a mágica. A chamada `recognize()` processa todas as páginas de uma vez e devolve um objeto de resultado rico.

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**O que está acontecendo nos bastidores?**  
O motor itera sobre cada quadro, aplica pré‑processamento (deskew, binarização), executa a rede neural e agrega a saída. Como chamamos `recognize()` apenas uma vez, a biblioteca pode compartilhar recursos entre as páginas, o que é mais rápido do que percorrer manualmente.

---

## Etapa 4: Extrair o Texto Reconhecido do Resultado JSON – **Converter TIFF em Texto** Página por Página

O objeto de resultado pode ser serializado para JSON. Dentro desse JSON você encontrará um array `pages`, cada um contendo um campo `text`.

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

Agora temos uma lista Python limpa onde cada elemento corresponde à saída OCR de uma página.

---

## Etapa 5: Imprimir ou Salvar o Texto de Cada Página – A Peça Final de **Extrair Texto de TIFF**

Vamos percorrer as páginas e exibir o texto extraído. Você também pode gravar cada página em um arquivo `.txt` separado, se preferir.

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### Saída Esperada (exemplo)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

Se o OCR foi bem‑sucedido, você verá um bloco limpo de frases em francês para cada página. Caso note caracteres estranhos, verifique novamente a configuração de idioma ou considere aumentar a resolução da imagem antes do OCR.

---

## Lidando com Problemas Comuns ao **Converter TIFF em Texto**

| Problema | Por que Acontece | Solução Rápida |
|----------|------------------|----------------|
| **Array `pages` vazio** | O TIFF não foi carregado corretamente ou não tem quadros. | Verifique o caminho do arquivo e assegure que o TIFF não seja um PNG de página única disfarçado de TIFF. |
| **Caracteres lixo** | Incompatibilidade de idioma ou baixa qualidade da imagem. | Defina o `engine.language` correto e pré‑procese a imagem (ex.: aumente DPI). |
| **Estouro de memória em TIFFs enormes** | Carregar todas as páginas de uma vez consome RAM. | Processar em blocos: carregue um quadro, reconheça, descarte antes de passar ao próximo. |
| **Erros de Unicode ao imprimir** | A codificação do console não suporta caracteres acentuados. | Use `print(page["text"].encode('utf-8').decode('utf-8'))` ou configure seu terminal para UTF‑8. |

---

## Expandindo o Script: De **Extrair Texto de TIFF** para Processamento em Lote

Agora que você tem uma base sólida, considere os próximos passos:

1. **Conversão em lote** – Envolva todo o fluxo em uma função `def ocr_tiff(path):` e itere sobre um diretório de arquivos TIFF.
2. **Saída para arquivos** – Em vez de imprimir, grave o texto de cada página em `page_{i}.txt` ou concatene tudo em um único documento.
3. **Motores OCR alternativos** – Se precisar de maior precisão, troque `ocr.OcrEngine()` por Tesseract (`pytesseract`) ou Azure Cognitive Services—mantendo a mesma lógica de “extrair texto de TIFF”.
4. **Pós‑processamento** – Execute correção ortográfica, detecção de idioma ou limpeza com regex para refinar a saída bruta do OCR.

---

## Script Completo, Pronto‑para‑Executar

A seguir está o código completo, pronto para copiar e colar. Ele inclui tratamento básico de erros e salvamento opcional do texto de cada página em arquivos separados.

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

Execute este script, aponte `tiff_file` para o seu documento e veja o console se encher de frases francesas limpas. Se você definiu `out_folder`, também encontrará uma série de arquivos `page_#.txt` prontos para processamento posterior.

---

## Conclusão

Acabamos de **extrair texto de arquivos TIFF** usando um fluxo OCR simples em Python, e agora você sabe como **converter TIFF em texto** de forma confiável. Desde a inicialização do motor com o idioma correto até a iteração sobre o resultado JSON de cada página, cada passo foi explicado com o “porquê” por trás, permitindo que você adapte o padrão a outros idiomas, formatos de imagem ou trabalhos em lote maiores.

Qual é o próximo passo? Experimente trocar o backend OCR por Tesseract, teste diferentes pacotes de idioma ou integre a saída a um banco de dados pesquisável. O céu é o limite quando você pode transformar imagens escaneadas em texto pesquisável.

Sinta‑se à vontade para deixar um comentário se encontrar algum obstáculo ou tiver ideias para melhorias adicionais. Boa codificação!

## O Que Você Deve Aprender a Seguir?

Os tutoriais abaixo abordam tópicos estreitamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Extrair Texto de Imagem com Aspose OCR – Guia Passo a Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extrair Texto de Imagens Usando Operação OCR em Pastas](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Converter Imagem em Texto – Executar OCR em Imagem a partir de URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}