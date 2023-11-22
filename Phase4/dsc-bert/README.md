# BERT - Pair Programming

## Introduction

**BERT (Bidirectional Encoder Representation from Transformer)** is a linguistic embedding model published by Google. It is a context-based model, unlike other embedding models such as word2vec, which are context-free. The context-sensitive nature of BERT was built upon a dataset of 3.3 billion words, in particular approximately 2.5 billion from Wikipedia and the balance from Google's [BookCorpus](https://www.english-corpora.org/googlebooks/#).

## Objectives

You will be able to: 

* To understand how to implement BERT in Python
* To apply BERT to NLP
* Understand the possibility of bias when working with BERT


## Some details of the BERT Model

Based on our previous discussion of the transformer, we can see where the terms "encoder representation from transformer" come from. But what about "Bidirectional?" Bidirectional simply mean the encoder can read the sentence in both directions, e.g. both Cogito ergo sum to I think therefore I am and vice versa.

BERT has three main hyperparameters
* $L$ is the number of encoder layers
* $A$ is the number of attention heads
* $H$ is the number of hidden units

The model also comes in some pre-specified configurations, and here are the two standard ones
* BERT-base: $L=12$, $A=12$, $H=768$
* BERT-large: $L=42$, $A=16$, $H=1,024$

In particular, we'll be using BERT to help discover the missing word in a sentence. BERT can also be used for translation and Next Sentence Prediction (NSP) as well as a myriad of other applications.

## Using BERT

We'll need to use the [Python library `transformers`](https://huggingface.co/transformers/v3.0.2/index.html). The `transformers` library provides general-purpose architectures such as BERT for NLP, with over 32 pretrained models in more than 100 languages.

The intent is to run this exercise in SaturnCloud since there can be some issues when trying to [install `transformers` locally](https://huggingface.co/docs/transformers/installation).


```python
# Import the german libraries
from transformers import pipeline
```

## Masking with BERT

The model ```bert-base-uncased``` is one of the pretrained BERT models and it has 110 million parameters. [Details of this model can be found on Hugging Face](https://huggingface.co/bert-base-uncased). We'll be using ```bert-base-uncased``` for masking.

You may get a comment from BERT regarding weights of ```bert-base-uncased```, but this is nothing to worry about for our purposes.


```python
# Define our function unmasker
unmasker = pipeline('fill-mask', model='bert-base-uncased')
```

Let's try a sentence and see how BERT does.


```python
# [MASK] goes in the place you want BERT to predict the correct word
unmasker("Artificial Intelligence [MASK] take over the world.")
```

The top five possibilities are shown. Further, the token string with the highest score is the one with the highest probability of being correct according to BERT. In this example, it is "can" as in "artificial intelligence can take over the world" at a 32% probability.

On supposes we should be happy that "can" has a higher probability than "will."

In the output, ```token``` refers to the position of the masked token in the list that is generated from the transformer. For our purposes, we don't have to worry about that, but only ```score``` and ```token_str``` with the corresponding ```sequence```.

### Task 1: Masking Twice

What happens if one used ```[MASK]``` two times in a sentence?

For example, run the following in the code block below and interpret the results.


```
unmasker("Artificial Intelligence [MASK] take over the [MASK].")
```



```python
# Using [MASK] twice
```

*Explain and interpret the "double-mask" here.*

### Task 2: Using unmasker

Use unmasker on three other sentences. At least one of them should be a "double-mask." Explain and interpret each one.


```python
# Your code here, you may want a separate code block for each of the three sentences.
```

### Literary Interlude

How does ```unmasker``` perform with a quote from literature or other notable work?

Let's look first a "To be, or not to be, that is the question" from William Shakespeare's *Hamlet* (Act 3, Scene 1).


```python
# Let's mask "question"
unmasker("To be, or not to be, that is the [MASK]:")
```

We can see that the highest probability does give us the correct answer.

Let's look at another one.

The opening line of James Joyce's Ulysses is “Stately, plump Buck Mulligan came from the stairhead, bearing a bowl of lather on which a mirror and a razor lay crossed.”


```python
# Let's mask "plump"
unmasker("Stately, [MASK] Buck Mulligan came from the stairhead, bearing a bowl of lather on which a mirror and a razor lay crossed.")
```

We see that the actual word- "plump"- did not make the top 5.

Now let's unmask "plump" and mask "lather."


```python
# Let's mask "lather"
unmasker("Stately, plump Buck Mulligan came from the stairhead, bearing a bowl of [MASK] on which a mirror and a razor lay crossed.")
```

While "lather" is not picked, the 3rd choice of the model is "soap," which is a synonym.

### Task 3: A quote from literature or other notable work

Now it is your turn.

Find a quote from literature or other notable work such as from a philosophical or religious text and make sure to state where the quote is from.

Mask at least two different words and see how BERT performs.


```python
# Type your quote with the source and then your code.
```

### Task 4: Bias in the model

Run the following two code cells.


```python
# Men at work
unmasker("The man worked as a [MASK].")
```


```python
# Women at work
unmasker("The woman worked as a [MASK].")
```

What do you notice about the top five responses for men and women? Explain.

## Summary

We were introduced to using `transformers` in Python with the BERT pretrained model of `bert-base-uncased`.
