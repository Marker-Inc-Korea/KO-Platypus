# KO-Platypus (Ko-Platy🥮)
![KO-platypus](./KO_platypus.png)
**Korean-Open-platypus를 활용하여 llama-2를 fine-tuning한 Korean-Platypus model**  
**KO-Platypus2-13B🥮:** [![Hugging Face](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Spaces-blue)](https://huggingface.co/kyujinpy/KO-Platypus2-13B)   
**KO-Platypus2-7B-ex:** (Coming soon; private) [![Hugging Face](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Spaces-blue)](https://huggingface.co/kyujinpy/KO-Platypus2-7B-ex)   

# Introduction
- 최근 **llama-2** 등장으로 LLM 분야가 다시 활발해지는 가운데, **Open-Platypus** 데이터셋 활용하여 llama-2를 fine-tuning한 **Platpyus** 모델이 등장하였습니다!🤗
- Platypus는 Open-Platypus 데이터셋을 LORA 방식을 활용하여 적은 파라미터 대비 아주 높은 성능을 보여주고 있고, huggingface LLM 리더보드 상위권에 위치해 있습니다..!
- 하지만 Open-Platypus 데이터셋은 대부분 영어로만 구성되어 있기 때문에 한국어에 접목하기에는 한계가 있었습니다.
- 이것을 동기부여로 삼아서, 한국어 기반의 Open-Platypus 데이터셋을 제작한 후, **Ko-Platypus**를 만들기로 계획하였습니다!🙂🙂
- Open-Platypus를 DeepL Pro API를 활용하여 번역을 진행한 후, 약 25,000개의 데이터를 수작업으로 체크하였고 약 144시간 정도 소요하여서 번역 오류를 대부분 고쳤습니다😭😭
- 이렇게 만들어진 **🥮KOpen-Platypus🥮** 데이터셋을 활용하여 llama-2-13B 모델을 fine-tuning 하였습니다.
- 결과적으로 Ko-Platypus2-13B 모델을 만들게 되었고✌, 성능평가를 위해 Polyglot-Ko와 llama-2-ko 모델과 비교를 진행했습니다.🙂🙃
- **🥮Ko-Platypus🥮** 모델은 NLI(자연어 추론 분야)에 대해서는 상대적으로 성능이 낮았지만, Classification에 대해서는 성능이 높았습니다. 
- 추후에, KOpen-Platypus 데이터셋을 여러 한국어 기반 LLM에 접목하여 fine-tuning한 후, 여러 성능평가를 진행해 볼 예정입니다😄
- 본 연구는 (주)마커와 (주)미디어그룹사람과숲의 오픈소스 LLM 연구 컨소시엄에서 진행되었습니다.

# Quick start
1. First download the origina repo [Platypus](https://github.com/arielnlee/Platypus)
2. 🥮Run the file🥮: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1qtGQroKPwGFA1L9b3WGyHC84NDIEs6s_?usp=sharing)
  
*Note: You must access the original [llama-2](https://huggingface.co/meta-llama/Llama-2-7b).      
**Note: You must generate your huggingface token. And after login, you can implement this [colab](https://colab.research.google.com/drive/1qtGQroKPwGFA1L9b3WGyHC84NDIEs6s_?usp=sharing).  
***Note: If you run Platypus-13B in colab, you must use A100 GPU. Training time is about 160 ~ 200 hours.  

# Datasets
**KOpen-Platypus🥮:** [![Hugging Face](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Spaces-blue)](https://huggingface.co/datasets/kyujinpy/KOpen-platypus)   
> I think that **KOpen-Platypus** is higher quality korean-translation dataset than just using DeepL. Because I almost check translation-error.  

**Procedure**  
- First, I use [DeepL Pro API](https://www.deepl.com/translator) and [Selenium Code](https://github.com/KyujinHan/Korean_selenium_DeepL).
- Second, checking all data. If there are some errors, I modify translation myself.
*If you want more detail, see below `Post-procesing`.  
  
## Post-processing
![example](./example.png)
I focus about **5 type errors.**  
1. Result of just code  
2. Result of code+explanation   
3. Float missing   
4. Math symbol   
5. Not translation or cut off translation result
  
*Note: If you want to see more detail example, visit [Ko-Platypus-blog](https://kyujinpy.tistory.com/101).  
  
# Performance
When I evaluate Ko-Platy, I use this [repo](https://github.com/Beomi/ko-lm-evaluation-harness).  
And, implement below code.
```
# In colab,
!python main.py \
    --model gpt2 \
    --model_args pretrained=kyujinpy/KO-Platypus2-13B \
    --tasks kobest_hellaswag,kobest_copa,kobest_boolq,kobest_sentineg \
    --device cuda:0 \
    --num_fewshot 0
```
  
### COPA (F1)
| Model | 0-shot | 5-shot | 10-shot | 50-shot |
| --- | --- | --- | --- | --- |
| [Polyglot-ko-1.3b](https://huggingface.co/EleutherAI/polyglot-ko-1.3b) | 0.7196 | 0.7193 | 0.7204 | 0.7206 |
| [Polyglot-ko-3.8b](https://huggingface.co/EleutherAI/polyglot-ko-3.8b) | 0.7595 | 0.7608 | 0.7638 | 0.7788 |
| [Polyglot-ko-5.8b](https://huggingface.co/EleutherAI/polyglot-ko-5.8b) | 0.7745 | 0.7676 | 0.7775 | 0.7887 |
| [Polyglot-ko-12.8b](https://huggingface.co/EleutherAI/polyglot-ko-12.8b) | 0.7937 | 0.8108 | 0.8037 | 0.8369 |
| [Llama-2-Ko-7b 20B](https://huggingface.co/beomi/llama-2-ko-7b) | 0.7388 | 0.7626 | 0.7808 | 0.7979 |
| [Llama-2-Ko-7b 40B](https://huggingface.co/beomi/llama-2-ko-7b) | 0.7436 | 0.7927 | 0.8037 | 0.8259 |
| **KO-platypus2-13B(ours)** | 0.5820 | 0.6269 | 0.6267 | 0.6527 |  
| **KO-platypus2-7B-ex(ours)** | NaN | NaN | NaN | NaN |  
  
### HellaSwag (F1)
| Model | 0-shot | 5-shot | 10-shot | 50-shot |
| --- | --- | --- | --- | --- |
| [Polyglot-ko-1.3b](https://huggingface.co/EleutherAI/polyglot-ko-1.3b) | 0.5247 | 0.5260 | 0.5278 | 0.5427 |
| [Polyglot-ko-3.8b](https://huggingface.co/EleutherAI/polyglot-ko-3.8b) | 0.5707 | 0.5830 | 0.5670 | 0.5787 |
| [Polyglot-ko-5.8b](https://huggingface.co/EleutherAI/polyglot-ko-5.8b) | 0.5976 | 0.5998 | 0.5979 | 0.6208 |
| [Polyglot-ko-12.8b](https://huggingface.co/EleutherAI/polyglot-ko-12.8b) | 0.5954 | 0.6306 | 0.6098 | 0.6118 |
| [Llama-2-Ko-7b 20B](https://huggingface.co/beomi/llama-2-ko-7b) | 0.4518 | 0.466751 | 0.4726 | 0.4828 |
| [Llama-2-Ko-7b 40B](https://huggingface.co/beomi/llama-2-ko-7b) | 0.4562 | 0.4657 | 0.4698 | 0.4774 |
| **KO-platypus2-13B(ours)** | 0.3912 | 0.4129 | 0.4144 | 0.4330 |  
| **KO-platypus2-7B-ex(ours)** | NaN | NaN | NaN | NaN |  
  
### BoolQ (F1)
| Model | 0-shot | 5-shot | 10-shot | 50-shot |
| --- | --- | --- | --- | --- |
| [Polyglot-ko-1.3b](https://huggingface.co/EleutherAI/polyglot-ko-1.3b) | 0.3552 | 0.4751 | 0.4109 | 0.4038 |
| [Polyglot-ko-3.8b](https://huggingface.co/EleutherAI/polyglot-ko-3.8b) | 0.4320 | 0.5263 | 0.4930 | 0.4038 |
| [Polyglot-ko-5.8b](https://huggingface.co/EleutherAI/polyglot-ko-5.8b) | 0.4356 | 0.5698 | 0.5187 | 0.5236 |
| [Polyglot-ko-12.8b](https://huggingface.co/EleutherAI/polyglot-ko-12.8b) | 0.4818 | 0.6041 | 0.6289 | 0.6448 |
| [Llama-2-Ko-7b 20B](https://huggingface.co/beomi/llama-2-ko-7b) | 0.3607 | 0.679743 | 0.6801 | 0.6622 |
| [Llama-2-Ko-7b 40B](https://huggingface.co/beomi/llama-2-ko-7b) | 0.5786 | 0.6977 | 0.7084 | 0.7144 |
| **KO-platypus2-13B(ours)** | 0.3539 | 0.7168 | 0.7328 | 0.7172 |  
| **KO-platypus2-7B-ex(ours)** | NaN | NaN | NaN | NaN |  
  
### SentiNeg (F1)
| Model | 0-shot | 5-shot | 10-shot | 50-shot |
| --- | --- | --- | --- | --- |
| [Polyglot-ko-1.3b](https://huggingface.co/EleutherAI/polyglot-ko-1.3b) | 0.6790 | 0.6257 | 0.5514 | 0.7851 |
| [Polyglot-ko-3.8b](https://huggingface.co/EleutherAI/polyglot-ko-3.8b) | 0.4858 | 0.7950 | 0.7320 | 0.7851 |
| [Polyglot-ko-5.8b](https://huggingface.co/EleutherAI/polyglot-ko-5.8b) | 0.3394 | 0.8841 | 0.8808 | 0.9521 |
| [Polyglot-ko-12.8b](https://huggingface.co/EleutherAI/polyglot-ko-12.8b) | 0.9117 | 0.9015 | 0.9345 | 0.9723 |
| [Llama-2-Ko-7b 20B](https://huggingface.co/beomi/llama-2-ko-7b) | 0.4855 | 0.8295 | 0.8711 | 0.8513 |
| [Llama-2-Ko-7b 40B](https://huggingface.co/beomi/llama-2-ko-7b) | 0.4594 | 0.7611 | 0.7276 | 0.9370 |
| **KO-platypus2-13B(ours)** | 0.5216 | 0.8236 | 0.8487 | 0.8789 |  
| **KO-platypus2-7B-ex(ours)** | NaN | NaN | NaN | NaN |  
  
# References
[Kopen-Platypus🥮](https://huggingface.co/datasets/kyujinpy/KOpen-platypus)   
[KO-Platypus2-13B🥮](https://huggingface.co/kyujinpy/KO-Platypus2-13B)   
[Platypus](https://github.com/arielnlee/Platypus)  
[llama-2](https://huggingface.co/meta-llama/Llama-2-7b)  
[ko-lm-evaluation-harness](https://github.com/Beomi/ko-lm-evaluation-harness)   
  
# TODO
- [ ] Make KO-Platypus-7B-ex  
- [x] Share huggingface repo
- [x] Share evaluation results
- [x] Share sample code

## Additional info about image
I made the image, inspired by [Platypus-LLM](https://github.com/arielnlee/Platypus).  
I used [Playground AI](https://playgroundai.com/), then applying prompt engineering. (For example, img2img, guidance etc...)  

When I made `Ko-Platy` image, I use prompt like below.
```
Prompt: 'Platypus wears a pretty traditional Korean clothes with 한국어 책'
Guidance: 10
Quality: 70~100
img2img: 'Platypus.png'
Model: SDXL
```  
