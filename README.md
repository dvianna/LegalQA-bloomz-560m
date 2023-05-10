# LegalQA

Finetuning a small BLOOMZ model (bloomz-560m) on a small dataset and with limited resources. 

The first step towards finetuning BLOOMZ, was to build the Portuguese question answering dataset, called LegalQA. Then, a dataset of concise and clear prompts were defined for the given task. Finally, the model bloomz-560m was tuned on the dataset of QA prompts resulting in a finetuned model called LegalQA-bloom-560.

# Requirements

```pip install -r requirements.txt```

# The LegalQA Dataset

The LegalQA dataset was built by extracting text from pdf files downloaded from the Brazilian Internal Revenue Service (Receita Federal) website. In total, five pdf files were parsed resulting in a total of 396 pairs of questions and answers related to five different topics. 

The original pdfs can be downloaded from:
https://www.gov.br/receitafederal/pt-br/centrais-de-conteudo/publicacoes/perguntas-e-respostas

Then, they can be parsed using the extracttext.ipynb notebook, resulting in the file LegalQA_dataset.csv with the 396 pairs of questions and answers.


# The LegalQA Prompt Dataset

Using the LegalQA dataset, a prompt dataset was built by adding natural language instructions to the question answering input. The code that generates the prompt is prepareprompts.ipynb and will result in a json file called prompts.json. 

The prompts have the following format:

``` "Given the question delimited by triple backticks ```{question}```, 
what is the answer? Answer: {answer}" ```

# Finetuning BLOOMZ

The final steps is to finetune the pretrained bloomz-560m model using the prompts from prompts.json.

Check the finetuning code in LegalQABloom.ipynb. The finetuned model was called LegalQA-bloom-560m and can be found in:

https://1drv.ms/u/s!Ai1xbfjwnU1-goRKIAjm5AwwkM2l3w?e=kVvLLW

The quality of the finetuned model was superficially checked by running the code test_finetuned_model.ipynb. 
The notebook exposes both models, the original bloomz-560m and the finetuned LegalQA-bloom-560m, 
to the same question. The finetuned model was the only one capable of answering the given question.