# deepchar

[github.com/deepchar](https://github.com/deepchar) *Transliteration with sequence-to-sequence models and transfer learning*

<img src="/favicon.ico" align="left"/>

<details><summary><strong>About transliteration</strong></summary>

About half of the billions of internet users speak languages written in non-Latin alphabets, like Russian, Arabic, Persian, Hebrew, Chinese, Greek, Armenian, Hindi and Tamil.  Very often, they haphazardly use the Latin alphabet to write those languages.

`Привет` => `Privet` , `Privyet`, `Priwjet`, ...  
`كيف حالك` => `kayf halk`, `keyf 7alek`, ...  
`Բարև Ձեզ` => `Barev Dzez`, `Barew Dzez`, ...  

So a growing share of user-generated text content is in these "Latinized" or "romanized" formats known as *translit*, *arabizi*, *Greeklish* and so on that are difficult to parse, search or even identify.

Transliteration is the task of automatically converting this content back into the native canonical format.

`Privet` => `Привет`,  
`Privyet` => `Привет`,  
`Priwjet` => `Привет`,  
...
`Aydpes aveli sirun e.` => `Այդպես ավելի սիրուն է:`

You can read more about what makes this problem non-trivial at [*Automatic transliteration with LSTM*](http://yerevann.github.io/2016/09/09/automatic-transliteration-with-lstm/) and [*Interpreting neurons in an LSTM network*](https://yerevann.github.io/2017/06/27/interpreting-neurons-in-an-LSTM-network/).

Another flavour of this task is transliteration of named entities.  You can read more about that in [deepchar/entities](/entities).

</details>

### Our approach

Our baseline approach is to train **character-level sequence-to-sequence** models on generated data.

Besides our modification to character-level, [Sockeye](https://github.com/awslabs/sockeye) and [Fairseq](https://github.com/pytorch/fairseq) are standard modern implementations of sequence-to-sequence, developed primarily for machine *translation* but in principle applicable to a wide range of tasks with sequence input and sequence output

Sockeye was developed by AWS Labs on Apache MXNet, and Fairseq was developed by Facebook AI Research on PyTorch.  Fairseq models can be launched and scaled in production with [pytorch/translate](https://github.com/pytorch/translate).

#### Transfer learning

Universal or languageless models can solve numerous problems when scaling to hundreds of languages.

From a research perspective, many difficult aspects of the transliteration task - ambiguity, named entities, long-distance dependencies - are similar between two or more languages, so accuracy can be improved for many languages, especially smaller languages.

From an engineering perspective, accuracy held equal, it is more practical to launch one model per target language or even one model for all languages, 

From a product perspective, it is also ideal, because in the real world the data even from the same user contains multiple languages.

Training universal or languageless models requires only a change in datasets or data generation, and more computing power to train each model, but no fundamental change in the neural network architecture.

Read more about the results of transfer learning in **Benchmarks**.

#### Adversarial learning



### Datasets

Constrained by lack of parallel corpora, and inspired by similar approaches to transliteration and other sequence-to-sequence tasks like grammar correction, we rely primarily on **data generation**.

See the [deepchar/data](https://github.com/deepchar/data) repo

### Benchmarks

See the [deepchar/benchmarks](https://github.com/deepchar/benchmarks) repo

### Results

TODO

### References

Sockeye

> Felix Hieber, Tobias Domhan, Michael Denkowski, David Vilar, Artem Sokolov, Ann Clifton and Matt Post. 2017.
> [Sockeye: A Toolkit for Neural Machine Translation](https://arxiv.org/abs/1712.05690). ArXiv e-prints.

Fairseq

> @inproceedings{gehring2017convs2s,
>  author    = {Gehring, Jonas, and Auli, Michael and Grangier, David and Yarats, Denis and Dauphin, Yann N},
>  title     = "{Convolutional Sequence to Sequence Learning}",
>  booktitle = {Proc. of ICML},
>  year      = 2017,
> }

