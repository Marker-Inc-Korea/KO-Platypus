# KO-platypus (Ko-Platy🥮)
![KO-platypus](./KO_platypus.png)
**Korean-Open-platypus를 활용하여 llama-2를 fine-tuning한 Korean-platypus model**  
**KO-platypus2-13B🥮:** [![Hugging Face](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Spaces-blue)](https://huggingface.co/kyujinpy/KO-Platypus2-13B)   

# Introduction
  
# Quick start
1. First download the origina repo [Platypus](https://github.com/arielnlee/Platypus)
2. 🥮Run the file🥮: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1qtGQroKPwGFA1L9b3WGyHC84NDIEs6s_?usp=sharing)   
*Note: You must access the original [llama-2](https://huggingface.co/meta-llama/Llama-2-7b).    
**Note: You must generate your huggingface token. And after login, you implement this code.
***Note: If you run Platypus-13B in colab, you must use A100 GPU. Training time is about 160 hours.  

# Datasets
**KOpen-platypus🥮:** [![Hugging Face](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Spaces-blue)](https://huggingface.co/datasets/kyujinpy/KOpen-platypus)   

I think that **KOpen-platypus** is very high-quality korean-translation dataset. Because I almost check translation-error.  
*Note: (9/1; Currently private repo yet. Will be change public..!)   

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

# References
[Kopen-platypus🥮](https://huggingface.co/datasets/kyujinpy/KOpen-platypus)   
[KO-platypus2-13B🥮](https://huggingface.co/kyujinpy/KO-Platypus2-13B)   
[Platypus](https://github.com/arielnlee/Platypus)  
[llama-2](https://huggingface.co/meta-llama/Llama-2-7b)  
[ko-lm-evaluation-harness](https://github.com/Beomi/ko-lm-evaluation-harness)   
  
# TODO
- [ ] Make KO-Platypus-7B-ex  
- [x] Share huggingface repo
- [x] Share evaluation results
- [x] Share sample code

## Additional about image
I make the image, inspired by [Platypus-LLM]()
I use [Playground AI](https://playgroundai.com/), then using prompt engineering (for example, img2img, guidance etc.)

When I make `Ko-platy` image, I use prompt like below.
```
Prompt: 'Platypus wears a pretty traditional Korean clothes with 한국어 책'
Guidance: 10
Quality: 70~100
img2img: 'Platypus.png'
Model: SDXL
```  
