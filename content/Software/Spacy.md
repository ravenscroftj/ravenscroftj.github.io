public:: true
title:: Software/Spacy
alias:: spacy

- ## Introduction
	- Spacy is a [[foss]]  [[Public/AI/NLP/index]] Library
## SpaCy GPU
### Set Up Environment

It's relatively easy to use SpaCy with a GPU these days.

First set up your conda environment and install cudatoolkit (use nvidia-smi to match versions of the tookit with the drivers):

Run `nvidia-smi`:

[![image.png](https://wiki.jamesravey.me/uploads/images/gallery/2022-10/scaled-1680-/hPUimage.png)](https://wiki.jamesravey.me/uploads/images/gallery/2022-10/hPUimage.png)

Create conda env:

```shell
conda create -n test python=3.8
conda activate test
conda install pytorch cudatoolkit=10.2 -c pytorch
```
### Installing SpaCy

Now install spacy - depending on how you like to manage your python environments either carry on using conda for everything or switch to your preferred package manager at this point.

```shell
conda install -c conda-forge spacy cupy
```

or

```
pdm add 'spacy[cuda-autodetect]'
```
### Download Models

Download a spacy transformer model to make use of your GPU/CUDA setup:

```shell
python -m spacy download en_core_web_trf
```
- ### Using GPU
  
  As soon as your code loads you should use the` prefer_gpu() `or `require_gpu()` functions to tell spacy to load cupy then load your model:
  
  ```python
  import spacy
  
  spacy.require_gpu()
  
  nlp = spacy.load('en_core_web_trf')
  ```
  
  Now you can use the model to do some stuff
  
  ```python
  doc = nlp("My name is Wolfgang and I live in Berlin")
  
  for ent in doc.ents:
    print(ent.text, ent.label_)
  ```
- You can check that the GPU is actually in use with `nvidia-smi`:
  
  [![image.png](https://wiki.jamesravey.me/uploads/images/gallery/2022-10/scaled-1680-/ocvimage.png)](https://wiki.jamesravey.me/uploads/images/gallery/2022-10/ocvimage.png)
  
  Also if you try to use transformer models without a GPU it will hang for AGES and max out your CPUs - another tell that something's not quite right.
- ## Spacy Knowledge Graphs
	- SpaCy has some integrations/features for doing relationship extraction documented [on their website](https://spacy.io/api/kb).
	  
	  There is also a guide for integrating spacy knowledge graphs into [neo4j](https://neo4j.com/developer-blog/turn-a-harry-potter-book-into-a-knowledge-graph/).
-