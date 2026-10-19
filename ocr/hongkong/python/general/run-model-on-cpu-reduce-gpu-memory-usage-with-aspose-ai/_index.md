---
category: general
date: 2026-06-22
description: 在 CPU 上執行模型，並學習透過在 Aspose AI 中設定 GPU 層來減少 GPU 記憶體使用量。附有程式碼片段的逐步指南。
draft: false
keywords:
- run model on cpu
- reduce gpu memory usage
- limit gpu layers
- configure gpu layers
language: zh-hant
og_description: 在 CPU 上執行模型，並透過設定 GPU 層以減少 GPU 記憶體使用量。Aspose AI 模型設定完整教學。
og_title: 在 CPU 上執行模型 – 減少 GPU 記憶體使用
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Run model on CPU and learn to reduce GPU memory usage by configuring
    GPU layers in Aspose AI. Step-by-step guide with code snippets.
  headline: Run Model on CPU – Reduce GPU Memory Usage with Aspose AI
  type: TechArticle
- description: Run model on CPU and learn to reduce GPU memory usage by configuring
    GPU layers in Aspose AI. Step-by-step guide with code snippets.
  name: Run Model on CPU – Reduce GPU Memory Usage with Aspose AI
  steps:
  - name: Attach any required post‑processors.
    text: Attach any required post‑processors.
  - name: Choose a configuration (`gpu_layers=0` for pure CPU, or a modest number
      for mixed mode).
    text: Choose a configuration (`gpu_layers=0` for pure CPU, or a modest number
      for mixed mode).
  - name: Initialize the model with that configuration.
    text: Initialize the model with that configuration.
  - name: Verify placement and run a test inference.
    text: Verify placement and run a test inference.
  type: HowTo
tags:
- AsposeAI
- CPU inference
- GPU optimization
title: 在 CPU 上執行模型 – 使用 Aspose AI 減少 GPU 記憶體使用量
url: /zh-hant/python/general/run-model-on-cpu-reduce-gpu-memory-usage-with-aspose-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 CPU 上執行模型 – 使用 Aspose AI 減少 GPU 記憶體使用量

有沒有想過在伺服器沒有 GPU 時 **在 CPU 上執行模型**？或是你的 GPU 記憶體不足而頻繁出現 OOM 錯誤，想要 **減少 GPU 記憶體使用量** 同時又不犧牲太多速度？本教學將一步步說明：掛載後處理器、在 CPU 上初始化 Aspose AI，以及微調 GPU 層數以保持記憶體佔用極小。

我們會從第一行程式碼說起，直到驗證模型真的使用了你設定的配置。完成後，你將能 **在 CPU 上執行模型**、**限制 GPU 層數**，以及 **配置 GPU 層數** 以因應任何工作負載——不需要魔法，只要純粹的 Python。

## 前置條件

- 已安裝 Python 3.8+（程式碼使用型別提示，但在較舊版本亦可執行）
- `asposeai` 套件（使用 `pip install asposeai` 安裝）
- 具備基本的神經網路推論概念（不需要博士，只要有好奇心）
- 可選：具備 GPU 的機器，用來比較 CPU 與 GPU 的執行差異

如果缺少上述任一項，請先安裝 SDK；接下來的教學假設匯入可以順利完成。

![Diagram illustrating how to run model on cpu instead of gpu](run-model-on-cpu-diagram.png)

## 步驟 1：掛載拼寫檢查後處理器（不需要自訂設定）

在考慮 CPU 或 GPU 之前，先把 Aspose AI 內建的拼寫檢查後處理器掛上。養成一開始就掛載後處理器的好習慣，讓它成為每次推論的必備環節。

```python
from asposeai import AI, spell_check_processor

# Create the AI client
ai = AI()

# Attach the built‑in spell‑check processor; no custom settings required
ai.set_post_processor(spell_check_processor, custom_settings={})
```

*為什麼這很重要*：後處理器會在模型產生原始 token 後 **執行**。現在就將它接上，保證之後無論在 CPU 或 GPU 上產生的文字，都會自動完成清理。這是一個小步驟，卻能避免下游的錯誤。

## 步驟 2：在 CPU 上執行模型 – 初始化 Aspose AI 並關閉 GPU

接下來進入本教學的核心：告訴 Aspose AI **在 CPU 上執行模型**。SDK 提供 `AsposeAIModelConfig`，其中的 `gpu_layers` 參數決定有多少層會保留在 GPU。將它設為 `0` 即可強制整個網路跑在 CPU 上。

```python
from asposeai import AsposeAIModelConfig

# Initialize the model configuration to use zero GPU layers (i.e., CPU only)
cpu_config = AsposeAIModelConfig(gpu_layers=0)

# Apply the configuration; this will load the model onto the CPU
ai.initialize(cpu_config)

print("✅ Model initialized on CPU – ready for inference.")
```

*底層發生了什麼*？當 `gpu_layers=0` 時，執行階段會把所有張量配置到主機記憶體。這樣就不需要 CUDA 驅動，腳本可以在任何伺服器上執行。缺點是吞吐量較慢，但對於批次工作或低延遲原型而言，簡易性往往比純粹速度更重要。

## 步驟 3：限制 GPU 層數以減少 GPU 記憶體使用量

如果你手上有 GPU 但記憶體吃緊，可以 **限制 GPU 層數** 而不是全部搬到 CPU。只保留少數前置層在 GPU 上，仍能受惠於硬體加速，同時大幅降低記憶體需求。

```python
# Example: keep only the first 10 layers on the GPU; the rest run on CPU
limited_gpu_config = AsposeAIModelConfig(gpu_layers=10)

ai.initialize(limited_gpu_config)

print("✅ Model initialized with 10 GPU layers – memory usage trimmed.")
```

*為什麼限制 GPU 層數有效*：現代 transformer 模型的記憶體主要分配在每一層。把幾層搬離 GPU，就能釋放數百 MB 記憶體。這種做法非常適合「記憶體受限」的工作，同時仍想在最耗時的計算上獲得加速。

## 步驟 4：配置 GPU 層數以彈性管理記憶體

有時需要更細緻的控制——例如根據工作負載大小 **配置 GPU 層數**。SDK 允許你在執行時讀取模型的總層數，並計算出安全的 GPU 層數。

```python
# Determine total number of layers (this is model‑specific; assume 36 for illustration)
total_layers = ai.model_info.total_layers  

# Choose a safe percentage, e.g., 25% of layers on GPU
gpu_layer_fraction = 0.25
desired_gpu_layers = int(total_layers * gpu_layer_fraction)

# Build the config dynamically
dynamic_config = AsposeAIModelConfig(gpu_layers=desired_gpu_layers)

ai.initialize(dynamic_config)

print(f"✅ Configured {desired_gpu_layers}/{total_layers} layers on GPU.")
```

*小技巧*：在共享伺服器上執行時，先查詢可用的 GPU 記憶體 (`torch.cuda.get_device_properties(0).total_memory`) 再決定 `desired_gpu_layers`。這一步可避免超額佔用 GPU，防止 OOM 異常。

## 步驟 5：驗證配置並測試推論

完成配置後，最好再次確認每一層實際所在的裝置。Aspose AI 提供診斷方法，可回傳層與裝置的對映表。

```python
# Retrieve the device placement map
placement = ai.get_layer_placement()

cpu_layers = [l for l, dev in placement.items() if dev == "cpu"]
gpu_layers = [l for l, dev in placement.items() if dev == "gpu"]

print(f"Layers on CPU: {len(cpu_layers)}")
print(f"Layers on GPU: {len(gpu_layers)}")
```

確認無誤後，執行一次快速推論，觀察結果是否如預期：

```python
input_text = "The quick brown fox jumps over the lazy dog."
output = ai.process(input_text)

print("Model output:", output)
```

如果腳本印出正確的文字，且層級分配報告與你的設定相符，即表示你已成功 **在 CPU 上執行模型**、**減少 GPU 記憶體使用量**，並 **配置 GPU 層數** 以符合你的情境。

## 常見問題與避免方式

| 症狀 | 可能原因 | 解決方法 |
|------|----------|----------|
| `CUDA out of memory` 錯誤 | GPU 層數過多 | 減少 `gpu_layers` 或改為 `gpu_layers=0` |
| `ai.process` 沒有輸出 | 模型未正確初始化 | 確認在掛載後處理器 **之後** 呼叫 `ai.initialize` |
| GPU 上推論緩慢 | 所有層仍在 CPU | 確認 `gpu_layers` > 0 且裝置映射顯示使用 GPU |
| 出現意外的拼寫錯誤 | 後處理器未掛載 | 在 `initialize` 前先呼叫 `set_post_processor` |

## 加分項：即時在 CPU 與 GPU 之間切換

由於 SDK 每次呼叫 `initialize` 都會重新載入模型，你可以在不重新啟動腳本的情況下，隨時在 CPU 與 GPU 之間切換。

```python
def switch_to_cpu():
    ai.initialize(AsposeAIModelConfig(gpu_layers=0))
    print("🔄 Switched to CPU mode.")

def switch_to_gpu(layers=12):
    ai.initialize(AsposeAIModelConfig(gpu_layers=layers))
    print(f"🔄 Switched to GPU mode with {layers} layers.")
```

需要低記憶體執行時呼叫 `switch_to_cpu()`，想要加速時則呼叫 `switch_to_gpu(12)`。

## 結論

我們完整示範了如何 **在 CPU 上執行模型**、**減少 GPU 記憶體使用量**、**限制 GPU 層數**，以及 **配置 GPU 層數** 的實作步驟。流程如下：

1. 掛載所有必要的後處理器。  
2. 選擇配置（`gpu_layers=0` 代表純 CPU，或設定適當的層數作混合模式）。  
3. 以該配置初始化模型。  
4. 驗證層級分配並執行測試推論。  

掌握這些技巧後，你的推論管線即可保持輕量、避免昂貴的 OOM 崩潰，且在有可用的 modest GPU 時仍能發揮效能。接下來，你可以探索批次處理、量化，或是將模型的部分運算搬到 CPU 而將注意力頭保留在 GPU——所有這些主題都直接建立在 **配置 GPU 層數** 的基礎上。

如有關於特定模型架構的問題，或需要協助微調層數以配合你的工作負載，歡迎提出。

## 接下來該學什麼？

以下教學與本篇內容緊密相關，能進一步延伸本指南所示的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你熟悉更多 API 功能，並在自己的專案中探索其他實作方式。

- [Aspose OCR 教程 – 光學字元辨識](/ocr/english/)
- [使用 Aspose OCR 從影像擷取文字 – 步驟說明](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [使用 Aspose.OCR 依語言執行影像文字辨識](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}