# Lexical Simplification with Pretrained Encoders, AAAI 2020 (Accepted)

   Lexical simplification (LS) aims to replace complex words in a given sentence with their simpler alternatives of equivalent meaning. Recently unsupervised lexical simplification approaches only rely on the complex word itself regardless of the given sentence to generate candidate substitutions, which will inevitably produce a large number of spurious candidates. We present a simple BERT-based LS approach that makes use of the pre-trained unsupervised deep bidirectional representations BERT. We feed the given sentence masked the complex word into the masking language model of BERT to generate candidate substitutions. By considering the whole sentence, the generated simpler alternatives are easier to hold cohesion and coherence of a sentence. Experimental results show that our approach obtains obvious improvement on standard LS benchmark.
   

## Pre-trained models

- [FastText](https://dl.fbaipublicfiles.com/fasttext/vectors-english/crawl-300d-2M-subword.zip) (word embeddings trained using FastText)
- [BERT based on Pytroch-transformers 1.0](https://github.com/huggingface/pytorch-transformers)

## How to run this code

We recommend Python 3.5 or higher. The model is implemented with PyTorch 1.0.1 using [pytorch-transformers v1.0.0](https://github.com/huggingface/pytorch-transformers). 

(1) Download pretrianed BERT. In our experiments, we adopted pretrained [BERT-Large, Uncased (Whole Word Masking)](https://storage.googleapis.com/bert_models/2019_05_30/wwm_uncased_L-24_H-1024_A-16.zip).

(2) download the pre-trained word embeddings using [FastText] (https://dl.fbaipublicfiles.com/fasttext/vectors-english/crawl-300d-2M-subword.zip)  .

(3) run "./run_LS_BERT.sh".

## Idea

Suppose that there is a sentence "the cat perched on the mat" and the complex word "perched". We concatenate the original sequence S and S' as a sentence pair, and feed the sentence pair {S,S'} into the BERT to obtain the probability distribution of the vocabulary corresponding to the mask word. Finally, we select as simplification candidates the top words from the probability distribution, excluding the morphological derivations of the complex word. For this example, we can get the top three simplification candidate words "sat, seated, hopped". 

<center style="padding: 40px"><img width="80%" src="https://github.com/qiang2100/BERT-LS/blob/master/BERT_LS.png" /></center>

## Example or Advantage

Comparison of simplification candidates of complex words using three methods. Given one sentence "John composed these verses." and complex words 'composed' and 'verses', the top three simplification candidates for each complex word are generated by our method BERT-LS and the state-of-the-art two baselines based word embeddings ([Glavas](https://pdfs.semanticscholar.org/26fb/d19be8e26b42f2d849c1db8a287012bfb188.pdf) and [Paetzold-NE](https://www.aclweb.org/anthology/E17-2006)). The top three substitution candidates generated by BERT-LS are not only related with the complex words, but also can fit for the original sentence very well. Then, by considering the frequency or order of each candidate, we can easily choose 'wrote' as the replacement of 'composed and 'poems' as the replacement of 'verses'. In this case, the simplification sentence 'John wrote these poems.' is more easily understand than the original sentence. 


<center style="padding: 40px"><img width="50%" src="https://github.com/qiang2100/BERT-LS/blob/master/Example1.png" /></center>


## Citation

[BERT-LS technical report](https://arxiv.org/pdf/1907.06226.pdf)

```
@article{qiang2019BERTLS,
  title =  {Lexical Simplification with Pretrained Encoders },
  author = {Qiang, Jipeng and 
            Li, Yun and
            Yi, Zhu and
            Yuan, Yunhao and 
            Wu, Xindong},
  journal = {AAAI},
  year  =  {2020}
}


