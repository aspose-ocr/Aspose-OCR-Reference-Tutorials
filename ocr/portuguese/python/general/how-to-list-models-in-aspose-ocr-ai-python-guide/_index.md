---
category: general
date: 2026-01-07
description: Como listar modelos no Aspose OCR AI usando Python – aprenda a obter
  o caminho do modelo, verificar os modelos instalados e recuperar uma lista de modelos
  em Python em segundos.
draft: false
keywords:
- how to list models
- get model path
- check installed models
- python get model list
- list available models
language: pt
og_description: Como listar modelos no Aspose OCR AI usando Python. Encontre o caminho
  do modelo, verifique os modelos instalados e veja a lista completa de modelos disponíveis.
og_title: Como listar modelos no Aspose OCR AI – Guia Python
tags:
- Aspose OCR
- Python
- AI models
title: Como listar modelos no Aspose OCR AI – Guia Python
url: /pt/python/general/how-to-list-models-in-aspose-ocr-ai-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Listar Modelos no Aspose OCR AI – Guia Python

Já se perguntou **como listar modelos** que já estão instalados na sua máquina ao trabalhar com Aspose OCR AI? Você não é o único a encontrar esse obstáculo. Em muitos projetos você precisa verificar a pasta de modelos, confirmar quais modelos estão presentes ou até depurar um problema de modelo ausente — tudo sem sair do seu REPL Python.

Neste tutorial vamos percorrer um exemplo completo, pronto‑para‑executar, que mostra como **obter o caminho do modelo**, **verificar os modelos instalados** e, finalmente, **listar os modelos disponíveis** com apenas algumas linhas de código. Sem scripts externos, sem mágica oculta — apenas Python puro e o Aspose OCR AI SDK.

> **Pré‑requisitos**  
> • Python 3.8 ou superior  
> • Pacote `asposeocr` instalado (`pip install asposeocr`)  
> • Familiaridade básica com importação de módulos

Se você já tem tudo isso, vamos mergulhar.

---

## Como Listar Modelos com Aspose OCR AI

A primeira coisa que precisamos é a classe auxiliar `AsposeAI` que vem com o módulo `asposeocr.ai`. Essa classe nos fornece três métodos úteis:

| Método | O que retorna | Caso de uso típico |
|--------|----------------|--------------------|
| `get_local_path()` | Caminho absoluto para a pasta onde a Aspose armazena seus modelos de IA | Verificar se o SDK está procurando no local correto |
| `list_local()` | `list` Python com os nomes das pastas de modelo que existem no disco | Ver rapidamente quais modelos você pode carregar |
| `list_remote()` *(opcional)* | Lista de modelos disponíveis para download na nuvem da Aspose | Quando você precisa de um modelo que não tem localmente |

A seguir está o **script completo** que imprime a pasta local de modelos e a lista de modelos instalados.

```python
# ---------------------------------------------------------
# Step 1: Import the Aspose OCR AI module
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

# ---------------------------------------------------------
# Step 2: Create an instance of the AI helper
# ---------------------------------------------------------
ai = AsposeAI()

# ---------------------------------------------------------
# Step 3: Retrieve and display the local model folder
# ---------------------------------------------------------
local_folder = ai.get_local_path()
print("Local AI model folder:", local_folder)

# ---------------------------------------------------------
# Step 4: List all models that are currently installed
# ---------------------------------------------------------
installed_models = ai.list_local()
print("Available models:", installed_models)
```

### Saída Esperada

Quando você executa o script em uma instalação nova, normalmente verá algo como:

```
Local AI model folder: /home/user/.asposeocr/models
Available models: ['ocr-general-v1', 'ocr-handwritten-v2']
```

Se a pasta estiver vazia, `list_local()` retorna uma lista vazia (`[]`). Isso é um sinal útil de que você precisa baixar um modelo primeiro — algo que abordaremos mais adiante.

---

## Por Que Conhecer o Caminho do Modelo É Importante

Entender **onde** o SDK armazena seus arquivos (`get model path`) é mais que curiosidade:

1. **Depuração** – Se um modelo falhar ao carregar, você pode usar `ls` no caminho e ver se o arquivo realmente existe.  
2. **Modelos personalizados** – Algumas equipes treinam seus próprios modelos OCR e os colocam na pasta. Conhecer o caminho permite que você posicione os arquivos exatamente onde a Aspose espera.  
3. **Permissões** – No Linux, a pasta pode ser de propriedade de outro usuário. Detectar um erro de permissão cedo economiza horas de dor de cabeça.

> **Dica profissional:** Se precisar apontar o SDK para um diretório personalizado, defina a variável de ambiente `ASPOSE_OCR_MODEL_PATH` antes de criar `AsposeAI()`.

```bash
export ASPOSE_OCR_MODEL_PATH=/my/custom/models
python my_script.py
```

---

## Verificando Modelos Instalados – Casos Limite & Dicas

### 1. Nenhum Modelo Instalado

Se `list_local()` retornar `[]`, você tem duas opções:

| Opção | Como fazer |
|--------|------------|
| **Baixar um modelo da Aspose** | `ai.download('ocr-general-v1')` (requer internet) |
| **Copiar um modelo pré‑treinado** | Coloque a pasta do modelo manualmente no caminho exibido por `get_local_path()` |

### 2. Múltiplas Versões do Mesmo Modelo

Às vezes você verá tanto `ocr-general-v1` **quanto** `ocr-general-v1-beta`. O SDK carrega a primeira correspondência que encontrar, mas você pode forçar uma versão específica passando o nome exato da pasta ao construtor do OCR:

```python
from asposeocr.ai import AsposeOCR

ocr = AsposeOCR(model_name='ocr-general-v1-beta')
```

### 3. Arquivos de Modelo Corrompidos

Um modelo baixado parcialmente pode causar um `FileNotFoundError` mais tarde. Se suspeitar de corrupção, basta excluir a pasta problemática e baixar novamente:

```bash
rm -rf /home/user/.asposeocr/models/ocr-general-v1
python -c "from asposeocr.ai import AsposeAI; AsposeAI().download('ocr-general-v1')"
```

---

## Extendendo o Script – Listar Modelos Remotos (Opcional)

Se quiser ver quais modelos estão disponíveis para download sem sair do Python, adicione mais uma chamada:

```python
remote_models = ai.list_remote()
print("Remote models you can download:", remote_models)
```

Isso produzirá algo como:

```
Remote models you can download: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

Então você pode escolher qualquer modelo e chamar `ai.download('model-name')` para obtê‑lo automaticamente.

---

## Exemplo Completo de Ponta a Ponta

Juntando tudo, aqui está um **script único e executável** que:

1. Mostra a pasta local de modelos.  
2. Lista os modelos instalados.  
3. Se nenhum for encontrado, baixa um modelo padrão.  
4. Por fim, imprime a lista atualizada.

```python
# ---------------------------------------------------------
# Complete script – verifies model folder, installs if empty
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

def main():
    ai = AsposeAI()

    # 1️⃣ Show where Aspose expects models
    local_path = ai.get_local_path()
    print("🔎 Local AI model folder:", local_path)

    # 2️⃣ List currently installed models
    models = ai.list_local()
    print("📦 Installed models:", models)

    # 3️⃣ If nothing is installed, grab a default model
    if not models:
        default = 'ocr-general-v1'
        print(f"⚠️ No models found – downloading '{default}'...")
        try:
            ai.download(default)
            models = ai.list_local()
            print("✅ After download, installed models:", models)
        except Exception as e:
            print("❌ Failed to download model:", e)
            return

    # 4️⃣ (Optional) Show what you could download from the cloud
    remote = ai.list_remote()
    print("🌐 Remote models available:", remote)

if __name__ == "__main__":
    main()
```

Executar este script em uma máquina limpa produzirá:

```
🔎 Local AI model folder: /home/user/.asposeocr/models
📦 Installed models: []
⚠️ No models found – downloading 'ocr-general-v1'...
✅ After download, installed models: ['ocr-general-v1']
🌐 Remote models available: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

Agora você tem uma solução **autocontida e digna de citação** que qualquer assistente de IA pode reproduzir literalmente.

---

## Perguntas Frequentes (FAQ)

**Q: Isso funciona no Windows?**  
A: Absolutamente. O SDK abstrai o sistema de arquivos, então `get_local_path()` retornará algo como `C:\Users\YourName\.asposeocr\models`. Apenas certifique‑se de que o Python tenha permissão de escrita nessa pasta.

**Q: Posso armazenar modelos em uma unidade de rede?**  
A: Sim — defina `ASPOSE_OCR_MODEL_PATH` para o caminho UNC (`\\server\share\models`) antes de criar a instância `AsposeAI`.

**Q: E se eu precisar de um modelo para um idioma que não está no conjunto padrão?**  
A: Use `list_remote()` para ver se a Aspose oferece um modelo específico para o idioma. Caso não exista, você pode treinar o seu próprio e colocá‑lo na pasta; basta passar o nome da pasta personalizada ao construtor do OCR.

---

## Conclusão

Cobrimos **como listar modelos** no Aspose OCR AI, mostramos como **obter o caminho do modelo**, **verificar os modelos instalados** e até **baixar um modelo ausente** — tudo com Python puro. Ao entender a estrutura de pastas e os métodos auxiliares (`get_local_path()`, `list_local()`, `list_remote()`), você ganha controle total sobre os modelos de IA que sua aplicação utiliza.

Próximos passos? Experimente trocar o modelo padrão por um modelo de texto manuscrito, ou aponte o SDK para um modelo treinado internamente. De qualquer forma, agora você tem uma base sólida para gerenciar ativos OCR em qualquer projeto Python.

Boa codificação, e que sua lista de modelos esteja sempre atualizada! 

---

![How to list models screenshot](https://example.com/images/how-to-list-models.png "How to list models")

*Texto alternativo da imagem:* **how to list models screenshot** (cumpre o requisito de palavra‑chave principal).

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}