## 1. 准备运行环境
### 1.1 安装 Anaconda
```bash
wget https://repo.anaconda.com/archive/Anaconda3-2023.03-1-Linux-x86_64.sh  
sudo chmod 777 https://repo.anaconda.com/archive/Anaconda3-2023.03-1-Linux-x86_64.sh  
sudo ./Anaconda3-2023.03-1-Linux-x86_64.sh  
```
### 1.2 创建虚拟环境
创建虚拟环境并指定python的版本号为3.8  
```
conda create -n qlora pip python=3.8
```
激活虚拟环境
```
conda activate qlora
```
### 1.3 安装 Guanaco 依赖库
在qlora项目下，执行：
```
pip install -r requirements.txt
```
## 3. 准备训练数据
可以使用本项目data目录下openassistant_best_replies_train.jsonl 作为训练数据  
## 4. 修改训练参数
下面是一个训练基于llama-7b的基础模型的Finetuning脚本，请注意修改--model_name_or_path 和--dataset 为当前运行环境相关地址。  
```
python qlora.py \
    --model_name_or_path /your/path/base_model/llama-7b \
    --output_dir ./output/guanaco-chinese \
    --logging_steps 10 \
    --save_strategy steps \
    --data_seed 42 \
    --save_steps 500 \
    --save_total_limit 40 \
    --evaluation_strategy steps \
    --eval_dataset_size 1024 \
    --max_eval_samples 1000 \
    --per_device_eval_batch_size 1 \
    --max_new_tokens 32 \
    --dataloader_num_workers 3 \
    --group_by_length \
    --logging_strategy steps \
    --remove_unused_columns False \
    --do_train \
    --do_eval \
    --do_mmlu_eval False\
    --lora_r 64 \
    --lora_alpha 16 \
    --lora_modules all \
    --double_quant \
    --quant_type nf4 \
    --bf16 \
    --bits 4 \
    --warmup_ratio 0.03 \
    --lr_scheduler_type constant \
    --gradient_checkpointing \
    --dataset /your/path/qlora/data/guanaco_chinese/guanaco_chinese.jsonl \
    --dataset_format oasst1 \
    --source_max_len 16 \
    --target_max_len 512 \
    --per_device_train_batch_size 1 \
    --gradient_accumulation_steps 16 \
    --max_steps 1875 \
    --eval_steps 187 \
    --learning_rate 0.0002 \
    --adam_beta2 0.999 \
    --max_grad_norm 0.3 \
    --lora_dropout 0.1 \
    --weight_decay 0.0 \
    --seed 0
```

## 5. 执行训练
在本运行环境根目录下，运行 ./scripts/finetune_guanaco_7b.sh
