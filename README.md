<p align="center">
  <img src="figures/granite-3_3-language-models-3x-v1.png" />
</p>

<p align="center">
  :books: <a href="https://github.com/ibm-granite/granite-3.3-language-models">Paper (comming soon)</a>&nbsp | :hugs: <a href="https://huggingface.co/collections/ibm-granite/granite-33-language-models-67f65d0cca24bcbd1d3a08e3">HuggingFace Collection</a>&nbsp | 
  :speech_balloon: <a href="https://github.com/orgs/ibm-granite/discussions">Discussions Page</a>&nbsp | 📘 <a href="https://www.ibm.com/granite/docs/">IBM Granite Docs</a>
<br>

---
## Introduction to Granite 3.3 Language Models
Granite 3.3 language models are lightweight, state-of-the-art, open foundation models that natively support multilinguality, coding, reasoning, and tool usage, including the potential to be run on constrained compute resources. All the models are publicly released under an Apache 2.0 license for both research and commercial use. The models' data curation and training procedure were designed for enterprise usage and customization, with a process that evaluates datasets for governance, risk and compliance (GRC) criteria, in addition to IBM's standard data clearance process and document quality checks.

Granite 3.3 models retain key capabilities of earlier versions, such as a long context support, and features to control the response length and originality through annotations. Additionally, the models introduce fill-in-the-middle (FIM) support for code completion and improve the clarity of model reasoning by separating intermediate thoughts from final answers. Granite 3.3 models are available in two different sizes and are built on a dense architecture.

Granite 3.3 was trained on synthetic data generated from a variety of different open source LLMs, including but not limited to open source models like Mistral and Gemma. Gemma is provided under and subject to the Gemma Terms of Use found a `https://ai.google.dev/gemma/terms`. A detailed attribution of datasets can be found in the [Granite 3.0 Technical Report](https://github.com/ibm-granite/granite-3.0-language-models/blob/main/paper.pdf), Granite 3.1 Technical Report (coming soon), and [Accompanying Author List](https://github.com/ibm-granite/granite-3.0-language-models/blob/main/author-ack.pdf).

We release base model — checkpoints of models after pretraining, as well as instruct checkpoints — models finetuned for dialogue, instruction-following, helpfulness, and safety. Comprehensive evaluation results for all model variants, as well as other relevant information will be available in Granite 3.3 Language Model Cards.

<!-- TO DO: Mention an evaluation highlight -->
<!-- Evaluation results show that Granite-3.3-8B-Instruct outperforms models of similar parameter sizes in [Hugging Face's OpenLLM Leaderboard](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard#/) (see Figure 1). 

<figure>
  <img src="https://github.com/ibm-granite/granite-3.1-language-models/blob/main/figures/granite-3_1-8b-instruct.png"
  alt=" Granite-3.1-8B-Instruct">
  <figcaption>
  Figure 1. Evaluation results from Granite-3.1-8B-Instruct in Hugging Face's OpenLLM Leaderboard.</figcaption>
</figure>
</br> -->

## How to Use our Models?
To use any of our models, pick an appropriate `model_path` from:
1. `ibm-granite/granite-3.3-2b-base`
2. `ibm-granite/granite-3.3-2b-instruct`
3. `ibm-granite/granite-3.3-8b-base`
4. `ibm-granite/granite-3.3-8b-instruct`

### Inference
This is a simple example of how to use Granite-3.1-1B-A400M-Instruct model.

```python
import torch
from transformers import AutoModelForCausalLM, AutoTokenizer

device = "auto"
model_path = "ibm-granite/granite-3.1-8b-instruct"
tokenizer = AutoTokenizer.from_pretrained(model_path)
# drop device_map if running on CPU
model = AutoModelForCausalLM.from_pretrained(model_path, device_map=device)
model.eval()
# change input text as desired
chat = [
    { "role": "user", "content": "What is the largest ocean on Earth?" },
]
chat = tokenizer.apply_chat_template(chat, tokenize=False, add_generation_prompt=True)
# tokenize the text
input_tokens = tokenizer(chat, return_tensors="pt").to(device)
# generate output tokens
output = model.generate(**input_tokens, 
                        max_new_tokens=100)
# decode output tokens into text
output = tokenizer.batch_decode(output)
# print output
print(output)
```
## How to Download our Models?
The model of choice (`ibm-granite/granite-3.1-8b-instruct` in this example) can be cloned using:
```shell
git clone https://huggingface.co/ibm-granite/ibm-granite/granite-3.1-8b-instruct
```

## How to Contribute to this Project?
Plese check our [Guidelines](/CONTRIBUTING.md) and [Code of Conduct](/CODE_OF_CONDUCT.md) to contribute to our project.

## Model Cards
The model cards for each model variant are available in their respective HuggingFace repository. Please visit our collection [here](https://huggingface.co/collections/ibm-granite/granite-33-language-models-67f65d0cca24bcbd1d3a08e3).

## License 
All Granite 3.0 Language Models are distributed under [Apache 2.0](./LICENSE) license.

## Would you like to provide feedback?
Please let us know your comments about our family of language models by visiting our [collection](https://huggingface.co/collections/ibm-granite/granite-33-language-models-67f65d0cca24bcbd1d3a08e3). Select the repository of the model you would like to provide feedback about. Then, go to *Community* tab, and click on *New discussion*. Alternatively, you can also post any questions/comments on our [github discussions page](https://github.com/orgs/ibm-granite/discussions).

<!-- ## Citation
If you find granite models useful, please cite:

```
@misc{granite2024granite,
  title={Granite 3.3 Language Models},
  url={},
  author={Granite Team, IBM},
  month={October},
  year={2024}
}
``` -->
