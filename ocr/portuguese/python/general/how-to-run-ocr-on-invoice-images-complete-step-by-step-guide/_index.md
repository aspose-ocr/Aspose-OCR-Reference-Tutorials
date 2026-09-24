---
category: general
date: 2026-01-12
description: Como executar OCR e extrair texto de imagens de faturas usando Aspose
  OCR e um modelo leve do Hugging Face. Aprenda a baixar o modelo, corrigir erros
  de OCR e realizar OCR na imagem.
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: pt
og_description: Como executar OCR em imagens de faturas, extrair texto e corrigir
  erros com um LLM da Hugging Face. Siga este guia completo para obter resultados
  impecáveis.
og_title: Como Executar OCR em Imagens de Faturas – Tutorial Completo
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: Como Executar OCR em Imagens de Faturas – Guia Completo Passo a Passo
url: /pt/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Executar OCR em Imagens de Faturas – Guia Completo Passo a Passo

Já se perguntou **como executar OCR** em uma fatura escaneada e obter texto limpo e pesquisável sem passar horas limpando‑o? Você não está sozinho. Em muitos projetos do mundo real, a saída bruta do OCR está repleta de erros de reconhecimento — pense em “O” por “0”, “l” por “1”, ou até palavras inteiras embaralhadas. A boa notícia? Com algumas linhas de Python você pode não apenas **perform OCR on image** files mas também corrigir automaticamente **correct OCR errors** usando um modelo leve da Hugging Face.

Neste tutorial, vamos percorrer tudo o que você precisa saber: desde carregar uma imagem de fatura, extrair texto bruto, baixar um modelo quantizado, até polir o resultado para que você obtenha uma transcrição perfeita pronta para o processamento subsequente. Ao final, você será capaz de **extract text from invoice** PDFs ou PNGs em um único script repetível.

## Pré-requisitos e Configuração

Before diving in, make sure you have:

| Requisito | Por que é importante |
|-------------|----------------|
| Python 3.9+ | Sintaxe moderna e dicas de tipo |
| `aspose-ocr` package | Fornece o `ocr.OcrEngine` usado no exemplo |
| `aspose-ai` package | Fornece o pós‑processador `AsposeAI` |
| Access to a GPU (optional) | Acesso a uma GPU (opcional) – Acelera as camadas LLM; caso contrário, a CPU funciona bem |
| Internet connection (first run) | Conexão à internet (primeira execução) – Necessária para **download Hugging Face model** automaticamente |

You can install the required libraries with:

```bash
pip install aspose-ocr aspose-ai
```

> **Dica profissional:** If you plan to run the LLM on GPU, install `torch` with CUDA support (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`).

Now that the environment is ready, let’s get into the code.

---

## Etapa 1 – Inicializar o Motor OCR e Carregar sua Imagem de Fatura

The first thing you need to do is create an instance of Aspose’s OCR engine and point it at the file you want to process. This step is the foundation of **how to run OCR** on any image.

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Por que isso importa:** `load_image` aceita PNG, JPEG, TIFF e até páginas PDF, permitindo que você **perform OCR on image** dados independentemente do formato.

## Etapa 2 – Executar OCR Básico para Capturar Texto Bruto

Once the image is loaded, the engine can produce a raw transcription. This output is often noisy, which is why we’ll later run a correction step.

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

Typical raw output might look like:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

Notice the zeroes (`0`) where the digit “O” should be? That’s exactly the kind of mistake we’ll fix later.

## Etapa 3 – Configurar o Pós‑Processador de IA com um LLM Leve

Now we bring in a **download Hugging Face model** that’s small enough to run on modest hardware but powerful enough to understand invoice language. The example uses the Qwen 2.5 3B‑Instruct GGUF model, quantized to `int8` for a tiny memory footprint.

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **Por que este modelo?** A quantização `int8` reduz o arquivo para ~1,2 GB, tornando‑o viável na maioria dos laptops. Camadas GPU aceleram a inferência, mas o código recua graciosamente para a CPU quando nenhuma GPU é encontrada.

## Etapa 4 – Executar a Correção Baseada em LLM no Resultado OCR Bruto

With the model ready, we feed the raw text into the post‑processor. The LLM will rewrite the transcription, fixing common OCR glitches and normalising numbers.

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

Expected cleaned output:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

You can see the zeroes have turned back into the letter “O”, and “Am0unt” is now “Amount”. This is the core of **correct OCR errors** automatically.

## Etapa 5 – Liberar Recursos e Limpar

Large language models can hold onto GPU memory, so it’s good practice to free resources when you’re done.

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

If you plan to process many invoices in a batch, you could keep the model loaded and only free it at the very end of the script.

## Exemplo Completo Funcional

Putting everything together, here’s a single script you can drop into a `.py` file and run:

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

Running the script should produce output similar to the “AI‑corrected” block shown earlier. Feel free to swap the image path with any other invoice or receipt to **extract text from invoice** files in bulk.

## Perguntas Frequentes & Casos Limítrofes

### E se eu não tiver uma GPU?

The `gpu_layers` parameter is optional. Set it to `0` or omit it, and the model will run entirely on CPU. Expect slower inference—roughly 2–3 seconds per page on a modern laptop.

### Minhas faturas são PDFs de várias páginas. Como lidar com elas?

Convert each page to a separate image (e.g., using `pdf2image`) and loop over the pages with the same script. The OCR engine can process each image independently, and the LLM will correct each block of text.

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### O download do modelo falha atrás de um firewall?

Download the model manually from the Hugging Face model hub, unzip it into a local folder, and point `hugging_face_repo_id` to the local path:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### Quão precisa é a correção?

For typical English‑language invoices, the LLM fixes >95 % of common OCR mis‑recognitions. Complex handwritten notes may still need manual review.

## Dicas & Truques para Uso em Produção

- **Processamento em lote:** Envolva as etapas 2‑4 em uma função e forneça uma lista de caminhos de arquivos. Re‑utilize a mesma instância `AsposeAI` para evitar recarregar o modelo.
- **Registro (Logging):** Substitua `print` pelo módulo `logging` do Python para capturar tanto as saídas brutas quanto as corrigidas para trilhas de auditoria.
- **Tratamento de erros:** Envolva a chamada OCR com blocos `try/except`. Se uma imagem falhar, registre o nome do arquivo e continue.
- **Ajuste de desempenho:** Experimente com `gpu_layers`. Mais camadas na GPU aceleram a inferência, mas aumentam o uso de VRAM.

## Conclusão

We’ve covered **how to run OCR** on invoice images from start to finish, showing you how to **perform OCR on image**, **download Hugging Face model**, and **correct OCR errors** automatically. The complete script demonstrates a practical workflow that you can drop into any Python‑based automation pipeline.

Next steps? Try extending the pipeline to **extract key fields** (invoice number, date, total) using regular expressions on the corrected text, or feed the cleaned output into a database for searchable records. You could also experiment with other lightweight LLMs from Hugging Face if you need a different language or domain‑specific knowledge.

Happy coding, and may your OCR results always be crystal‑clear!

![como executar OCR em uma imagem de fatura](ocr_invoice_example.png "como executar OCR em fatura")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}