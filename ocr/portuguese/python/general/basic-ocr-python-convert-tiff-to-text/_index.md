---
category: general
date: 2026-03-18
description: Tutorial básico de OCR em Python mostra como converter TIFF para texto,
  carregar OCR de imagem, definir camadas GPU e corrigir zeros à esquerda com Aspose
  AI.
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: pt
og_description: Tutorial básico de OCR em Python orienta você na conversão de arquivos
  TIFF em texto limpo, carregamento de imagens, configuração de camadas GPU e correção
  de zeros à esquerda.
og_title: OCR básico em Python – converter TIFF para texto
tags:
- OCR
- Python
- AI
- Aspose
title: OCR básico em Python – converter TIFF em texto
url: /pt/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – Converter TIFF para Texto com Pós‑Processamento de IA

Procurando uma forma de fazer **basic ocr python** nos seus documentos escaneados? Neste guia vamos percorrer o processo de conversão de um arquivo TIFF em texto limpo e pesquisável usando Aspose OCR e um pós‑processador de IA.  

Se você já teve dificuldades para **converter TIFF para texto** porque a saída bruta está cheia de erros de digitação ou símbolos estranhos, não está sozinho. Também vamos mostrar como **carregar imagem OCR**, ajustar o motor para **definir camadas GPU** e até **corrigir zeros à esquerda** que aparecem com frequência em números de notas fiscais.

## O que você vai aprender

- Como inicializar o motor Aspose OCR para documentos impressos.  
- Os passos exatos para **carregar imagem OCR** a partir de um arquivo TIFF e obter texto bruto.  
- Configurar um modelo de IA, baixá‑lo automaticamente e **definir camadas GPU** para inferência mais rápida.  
- Adicionar verificação ortográfica integrada mais uma função personalizada que **corrige zeros à esquerda**.  
- Limpar o resultado do OCR e liberar recursos corretamente.  

Ao final deste tutorial você terá um único script Python reutilizável que transforma qualquer TIFF em texto polido e pesquisável — sem necessidade de copiar‑colar manualmente.  

### Pré‑requisitos

- Python 3.8+ instalado na sua máquina.  
- Pacote `aspose-ocr` (`pip install aspose-ocr`).  
- Opcional: uma GPU com pelo menos 4 GB de VRAM se você quiser **definir camadas GPU**; caso contrário o código recairá automaticamente para a CPU.  

---

## basic ocr python – carregar imagem e reconhecer texto

A primeira coisa que precisamos fazer é **carregar imagem OCR** para que o motor possa ler os pixels. O `OcrEngine` da Aspose lida com muitos formatos, mas aqui nos concentramos em TIFF porque é o mais comum para notas fiscais escaneadas.

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **Dica de especialista:** Se você estiver lidando com TIFFs de várias páginas, a Aspose processa automaticamente cada página em sequência, então não é necessário loops extras.

Agora que a imagem está carregada, vamos executar uma passagem básica de reconhecimento.

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

Você verá algo como:

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Percebe os *zeros* antes das letras? Esse é um artefato clássico de OCR que vamos limpar depois.

![fluxo de trabalho basic ocr python](/images/ocr-workflow.png "diagrama do fluxo de trabalho basic ocr python")

---

## Etapa 2: Converter TIFF para texto – preparar o pós‑processador de IA

O OCR bruto é útil, mas a maioria dos pipelines de produção precisa de uma versão polida. A Aspose fornece um wrapper `AsposeAI` que pode baixar um modelo do Hugging Face, executá‑lo na GPU e aplicar verificação ortográfica automaticamente.

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# Configure the AI model – we’ll download Qwen2.5‑3B‑Instruct automatically
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    directory_model_path="YOUR_DIRECTORY/ocr_ai_models",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25          # <-- this is where we **set GPU layers**
)

ocr_ai = AsposeAI(ai_config)
```

### Por que `definir camadas GPU` importa

O parâmetro `gpu_layers` informa ao modelo GGUF subjacente quantas camadas transformer devem permanecer na GPU. Mais camadas = inferência mais rápida, mas maior uso de VRAM. Se você estiver em um laptop modesto, reduza o valor para `10` ou omita‑o completamente para permanecer na CPU.

---

## Etapa 3: Aplicar verificação ortográfica e **corrigir zeros à esquerda**

A IA da Aspose vem com um verificador ortográfico embutido, que captura a maioria dos erros de ortografia em inglês. No entanto, correções específicas de domínio — como transformar um `0` inicial em um `O` para códigos de notas fiscais — exigem um pós‑processador personalizado.

```python
# Enable the built‑in spell‑check
ocr_ai.set_post_processor("spellcheck")

# Custom function to replace a leading zero before three capital letters
def invoice_fix(txt: str) -> str:
    import re
    # Example: "0ABC" -> "OABC"
    return re.sub(r"\b0([A-Z]{3})\b", r"O\1", txt)

# Register the custom fix – it runs after spellcheck
ocr_ai.set_post_processor(invoice_fix)
```

> **Por que isso funciona:** A expressão regular procura por um limite de palavra (`\b`), um zero, seguido exatamente de três letras maiúsculas. Em seguida, substitui o zero pela letra “O”. Você pode estender o padrão para outras particularidades (ex.: `0[0-9]{2}` para números lidos incorretamente).

---

## Etapa 4: Limpar o resultado do OCR com o pós‑processador de IA

Agora combinamos tudo: a string bruta do **basic ocr python**, a verificação ortográfica e nossa correção de zeros. O método `run_postprocessor` devolve uma versão limpa pronta para sistemas downstream.

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

Saída típica após o pós‑processador:

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Você pode ver que o zero inicial foi transformado em um `O` e os erros de ortografia comuns foram corrigidos. O texto agora está adequado para indexação em um motor de busca ou para ser alimentado em um pipeline de extração de dados.

---

## Etapa 5: Liberar recursos de IA – mantenha sua GPU feliz

Se você estiver executando múltiplos trabalhos de OCR em um serviço de longa duração, é uma boa prática liberar a memória GPU do modelo quando terminar.

```python
ocr_ai.free_resources()
```

Pular esta etapa pode levar a erros de “memória insuficiente” em chamadas subsequentes, especialmente quando **definir camadas GPU** a um valor alto.

---

## Variações opcionais & casos de borda

| Situação | O que mudar |
|-----------|----------------|
| **Documentos manuscritos** | Use `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` em vez de `PRINTED`. |
| **Nenhuma GPU disponível** | Defina `gpu_layers=0` ou omita o argumento; o modelo será executado na CPU (mais lento, mas seguro). |
| **Idioma diferente** | Troque o ID do repositório Hugging Face para um modelo específico de idioma, por exemplo, `microsoft/Florence-2-base`. |
| **Processamento em lote** | Envolva as etapas em um loop `for file in glob("*.tif"):` e acumule os resultados em uma lista ou CSV. |
| **Padrões de zero mais complexos** | Expanda `invoice_fix` com regex adicionais, como `r"\b0+([A-Z]{2,})\b"` para múltiplos zeros à esquerda. |

---

## Conclusão

Acabamos de concluir um pipeline **basic ocr python** que carrega um TIFF, extrai texto bruto e depois o limpa usando um modelo de IA enquanto **define camadas GPU** para desempenho. O pós‑processador personalizado demonstra como **corrigir zeros à esquerda**, um detalhe pequeno mas frequentemente negligenciado que pode quebrar análises downstream.

Sinta‑se à vontade para experimentar: teste uma quantização diferente (`float16` para maior precisão), troque a verificação ortográfica por um dicionário específico de domínio, ou encadeie múltiplas correções personalizadas. O padrão permanece o mesmo — carregar, reconhecer, configurar IA, pós‑processar e limpar.

**Próximos passos** que você pode explorar incluem:

- Integrar a saída limpa a um banco de dados ou índice Elasticsearch.  
- Usar a mesma abordagem para **converter TIFF para texto** em PDFs multilíngues.  
- Adicionar uma UI com Flask ou FastAPI para que usuários não técnicos possam enviar arquivos e receber texto limpo instantaneamente.  

Boa codificação, e que seus resultados de OCR sejam sempre nítidos e sem zeros!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}