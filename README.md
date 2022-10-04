# Factual Consistency Datasets
We introduce a human annotated dataset for factual consistency. Annotations are done on generated responses from different configurations of neural response generators, knowledge snippets, and decoding strategies. 
In addition, to facilitate the  development of a factual consistency detector,  we automatically create a new corpus called
Conv FEVER that is adapted from the Wizard of Wkipedia dataset and includes factually consistent and inconsistent responses.


## Human Annotation Dataset
There are two types of human annoated files. 

The annotation setup is described in "Rome was built in 1776: A Case Study on Factual Correctness in Knowledge-Grounded Response Generation"

(1) Factual Dataset-crowd: We use public crowd-workers in order to annotate a  large amount of data under different configurations,
namely model size, knowledge retrieval, and decoding setups. 

(2) Factual Dataset-expert: We use internal annotators in order to annotate a smaller amount of data for a specific configuration.

### Factual Dataset-crowd

For this dataset we generate outputs from 4 different GPT2 models (small, medium, large, x-large), with three different 
knowledge retrieval mechanisms (ground truth knowledge, K-Nearest Neighbors, Dense Passage Retrieval) and three different decoding mechanisms.

Each knowledge retrieval mechanism has it's own respective .csv file

`human_annotations/factual_dataset_crowd/dpr.csv`

`human_annotations/factual_dataset_crowd/knn.csv`

`human_annotations/factual_dataset_crowd/gt.csv`

Duplicate rows which contained the same model_type, decoding and knowledge retrieval mechanisms were dropped.

### Factual Dataset-expert

`human_annotations/factual_dataset_expert.csv`

For this dataset we generate outputs from a GPT2-small model fine-tuned on the Wizard of Wikipedia dataset using the ground-truth knowledge and nucleus sampling with
p=0.9. 

### Columns for each dataset
model_type - describes the GPT2 model size used to generate the response

decoding - describes the decoding strategy used to generate the response

context - the dialog context fed into the neural response generator

knowledge - the knowledge sentence fed into the neural response generator

response - the generated response from the model

Avg Factual Correctness - Is the response generated factually accurate with regards to the input knowledge? Took the average of three scores where each score was on  a three-point scale: factually incorrect (0), partially correct (0.5), and completely correct (1).

Hallucination - Is the response generated making up more  information than what is provided in the conversational
context and input knowledge? Took the majority of three scores where each score was either Yes or No.

Verifiable - Does the response need to be verified (y/n)


## Citation
If you use the dataset in your work please cite with the following 

```
@misc{santhanam2021rome,
      title={Rome was built in 1776: A Case Study on Factual Correctness in Knowledge-Grounded Response Generation}, 
      author={Sashank Santhanam and Behnam Hedayatnia and Spandana Gella and Aishwarya Padmakumar and Seokhwan Kim and Yang Liu and Dilek Hakkani-Tur},
      year={2021},
      eprint={2110.05456},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
```