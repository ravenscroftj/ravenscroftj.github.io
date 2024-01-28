alias:: TopicModelling, Topic Models

- Topic Modelling covers a family of algorithms for identifying patterns of keywords and themes that occur across many documents.
-
- ## Polylingual and Dialectical Topic Modelling
- Simple topic models like LDA learn one [[Language Model]] per topic. However in some cases it is useful to be able to provide a single model that can assist with information retrieval across multiple languages or dialects.
- [[@Dialect Topic Modeling for Improved Consumer Medical Search]] introduced DiaTM, a topic model that learns to represent topics in different dialects.
-
- ## Changes Over Time
	- [[@Predicting the Rise and Fall of Scientific Topics from Trends in their Rhetorical Framing]]
	-
- ## Latent Dirichlet Allocation (LDA)
	- LDA is the approach that most people think of when you say topic modelling. It was developed by David Blei [^1] who produced a more readable paper about how it works a few years later [^2].
	- In LDA, documents are modelled as a probability distribution over topics and topics are modelled as probability distributions over words.
	- ![lda_figure.png](../assets/lda_figure_1688920664530_0.png)
	- Figure from <a href="https://www.cs.columbia.edu/~blei/papers/Blei2011.pdf">Introduction to Probabilistic Topic Models</a>
- ## Correlated Topic Models (CTM)
	- CTM is an extension of LDA that allows dependencies/relationships between topics to be modelled. This may be useful in some settings where certain topics are more or less likely to occur together in the same document.
	- For example, an article featuring a topic the describes Linux and Unix is likely to also discuss open source and open culture whereas an article about celebrity gossip is unlikely to feature discussions of Linux, Unix or open source software. Having some intuition about the relationships between these things may help us to characterise a larger corpus.
## Resources
	- [Intuitive Guide to Correlated Topic Models](https://scribe.rip/intuitive-guide-to-correlated-topic-models-76d5baef03d3) [(mirror)](https://archive.jamesravey.me/archive/1662103726.849506/singlefile.html)
	  
	  
	  [^1]: https://www.jmlr.org/papers/volume3/blei03a/blei03a.pdf
	  [^2]: https://www.cs.columbia.edu/~blei/papers/Blei2011.pdf