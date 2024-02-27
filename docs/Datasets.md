# M2KR Benchmark Datasets
We release the M2KR Benchmark datasets in Huggingface Dataset format.

We pre-process the datasets into a uniform format and write several task-specific prompting instructions for each dataset. The details of the instruction can be found in the paper. The M2KR benchmark contains three types of tasks:
#### Image to Text (I2T) retrieval
These tasks evaluate the ability of a retriever to find relevant documents associated with an input image.   
Component tasks are WIT, IGLUE-en, KVQA, and CC3M.  

#### Question to Text (Q2T) retrieval
This task is based on MSMARCO and is included to assess whether multi-modal retrievers retain their ability in text-only retrieval after any retraining for images. 

#### Image & Question to Text (IQ2T) retrieval
This is the most challenging task which requires joint understanding of questions and images for accurate retrieval.  It consists of these subtasks:  
OVEN, LLaVA, OKVQA, Infoseek and E-VQA.

We show the dataset statistics in the following table:

<table>
    <thead>
        <tr>
            <th rowspan="2">Datasets</th>
            <th colspan="3">#Examples</th>
            <th colspan="2">#Passages</th>
        </tr>
        <tr>
            <th>Train</th>
            <th>Val</th>
            <th>Test</th>
            <th>Train</th>
            <th>Val/Test</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="6"><b><i>I2T Retrieval</i></b></td>
        </tr>
        <tr>
            <td>WIT</td>
            <td>2.8M</td>
            <td>20,102</td>
            <td>5,120</td>
            <td>4.1M</td>
            <td>40K</td>
        </tr>
        <tr>
            <td><i>IGLUE</i></td>
            <td>-</td>
            <td>-</td>
            <td>685</td>
            <td>-</td>
            <td>1K</td>
        </tr>
        <tr>
            <td>KVQA</td>
            <td>65K</td>
            <td>13,365</td>
            <td>5,120</td>
            <td>16.3K</td>
            <td>4,648</td>
        </tr>
        <tr>
            <td>CC3M</td>
            <td>595K</td>
            <td>-</td>
            <td>-</td>
            <td>595K</td>
            <td>-</td>
        </tr>
        <tr>
            <td colspan="6"><b><i>Q2T Retrieval</i></b></td>
        </tr>
        <tr>
            <td>MSMARCO</td>
            <td>400K</td>
            <td>6,980</td>
            <td>5,120</td>
            <td>8.8M</td>
            <td>200K</td>
        </tr>
        <tr>
            <td colspan="6"><b><i>IQ2T Retrieval</i></b></td>
        </tr>
        <tr>
            <td>OVEN</td>
            <td>339K</td>
            <td>20,000</td>
            <td>5,120</td>
            <td>10K</td>
            <td>3,192</td>
        </tr>
        <tr>
            <td>LLAVA</td>
            <td>351K</td>
            <td>-</td>
            <td>5,120</td>
            <td>351K</td>
            <td>6,006</td>
        </tr>
        <tr>
            <td>OKVQA</td>
            <td>9K</td>
            <td>5,046</td>
            <td>5,046</td>
            <td>110K</td>
            <td>110K</td>
        </tr>
        <tr>
            <td>Infoseek</td>
            <td>100K</td>
            <td>-</td>
            <td>4,708</td>
            <td>100K</td>
            <td>100K</td>
        </tr>
        <tr>
            <td>E-VQA</td>
            <td>212K</td>
            <td>9,852</td>
            <td>3,750</td>
            <td>50K</td>
            <td>50K</td>
        </tr>
    </tbody>
</table>



## Huggingface Datasets 
We release the M2KR on the huggingface [BByrneLab/multi_task_multi_modal_knowledge_retrieval_benchmark_M2KR](https://huggingface.co/datasets/BByrneLab/multi_task_multi_modal_knowledge_retrieval_benchmark_M2KR). 
For the CC3M pretraining dataset, we do not include them in the Huggingface datasets as we use the exact same split as in the [liuhaotian/LLaVA-CC3M-Pretrain-595K](https://huggingface.co/datasets/liuhaotian/LLaVA-CC3M-Pretrain-595K).  

## Example Use
The datasets are available for download and use with the Huggingface datasets library. 


#### Datasets
```python
from datasets import load_dataset
# EVQA datasets
EVQA_ds = load_dataset("BByrneLab/multi_task_multi_modal_knowledge_retrieval_benchmark_M2KR", "EVQA_data")
# WIT datasets
WIT_ds = load_dataset("BByrneLab/multi_task_multi_modal_knowledge_retrieval_benchmark_M2KR", "WIT_data")
# ...
``` 
Each datasets contains the train/val/test split:
```python
train_ds = WIT_ds['train']
val_ds = WIT_ds['valid']
test_ds = WIT_ds['test']
```
#### Passages
```python
# EVQA passages
EVQA_passages = load_dataset("BByrneLab/multi_task_multi_modal_knowledge_retrieval_benchmark_M2KR", "EVQA_passages")
# WIT passages
WIT_passages = load_dataset("BByrneLab/multi_task_multi_modal_knowledge_retrieval_benchmark_M2KR", "WIT_passages")
# ...
```
Each dataset contains the passages for the train/val/test split:
```python
train_passages = WIT_passages['train_passages']
val_passages = WIT_passages['valid_passages']
test_passages = WIT_passages['test_passages']
```

## Images
In the HF datasets, we only include the image path to the dataset without the root image directory (e.g., `train2014/COCO_train2014_000000276336.jpg`). The base image directory can be set using the `image_root_dir` argument in our provided example script to run PreFLMR (i.e., `example_use_preflmr.py`). You will need to change the `image_root_dir` to the correct path to the image directory.
### WIT 
The WIT dataset images can be downloaded with the instruction from the [WIT Github page](https://github.com/google-research-datasets/wit/blob/main/DATA.md). The training images can be downloaded from [Kaggle](https://www.kaggle.com/competitions/wikipedia-image-caption/data) at a size around 275 GB. The validation and test images can be downloaded directly from the github page.
#### IGLUE
Following the instruction from the [IGLUE Github page](https://github.com/e-bug/iglue/tree/main/datasets), the IGLUE-WIT images can be downloaded from their [hosted server](https://sid.erda.dk/sharelink/CwTySJlPdB). You will need the WIT-en split images.   
### KVQA
The KVQA dataset images can be downloaded from the [KVQA Project page](https://malllabiisc.github.io/resources/kvqa/) at a size around 25GB.
### CC3M 
We use the downsampled 595K version of CC3M from LLaVA. The images can be downloaded from the [LLaVA-CC3M-Pretrain-595K](https://huggingface.co/datasets/liuhaotian/LLaVA-CC3M-Pretrain-595K/tree/main). The images can be found in the `images.zip` in their repository.
### OVEN
The OVEN dataset images can be downloaded from the [OVEN Github page](https://github.com/edchengg/oven_eval/tree/main/image_downloads) with their provided script.
### LLaVA
The [LLaVA-Instruct-150K](https://huggingface.co/datasets/liuhaotian/LLaVA-Instruct-150K) images are from MSCOCO, which can be downloaded here: [train2017](http://images.cocodataset.org/zips/train2017.zip). Alternatively, refer to the [MSCOCO website](https://cocodataset.org/#home).
### OKVQA
The preparation of the OKVQA dataset images can be found in the [OKVQA Project page](https://okvqa.allenai.org/download.html).
### Infoseek
Infoseek is obtained from downsampling of the OVEN dataset.  
Please refer to OVEN for the image download.
### E-VQA
To prepare the images for E-VQA, please refer to the [E-VQA Github page](https://github.com/google-research/google-research/tree/master/encyclopedic_vqa). You will need to download the iNaturalist 2021 and Google Landmarks Dataset V2 datasets. 



## Reproduce PreFLMR results
To reproduce the PreFLMR results, you can use the M2KR HF datasets and the PreFLMR models. You will need to change the `image_root_dir` to the correct path to the image directory.
```python
python example_use_preflmr.py \
            --use_gpu --run_indexing \
            --index_root_path "." \
            --index_name EVQA_PreFLMR_ViT-G \
            --experiment_name EVQA \
            --indexing_batch_size 64 \
            --image_root_dir /rds/project/rds-hirYTW1FQIw/shared_space/vqa_data/KBVQA_data/EVQA/eval_image/ \
            --dataset_hf_path BByrneLab/multi_task_multi_modal_knowledge_retrieval_benchmark_M2KR \
            --dataset EVQA \
            --use_split test \
            --nbits 8 \
            --Ks 1 5 10 20 50 100 \
            --checkpoint_path LinWeizheDragon/PreFLMR_ViT-G \
            --image_processor_name laion/CLIP-ViT-bigG-14-laion2B-39B-b160k \
            --query_batch_size 8 
```
By changing the `--dataset`, `--experiment_name` and `image_root_dir`, you can reproduce the results for different datasets in the PreFLMR paper.
