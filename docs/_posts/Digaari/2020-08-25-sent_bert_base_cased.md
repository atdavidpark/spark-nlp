---
layout: model
title: BERT Sentence Embeddings (Base Cased)
author: John Snow Labs
name: sent_bert_base_cased
date: 2020-08-25
task: Embeddings
language: en
edition: Spark NLP 2.6.0
tags: [open_source, embeddings, en]
supported: false
article_header:
  type: cover
use_language_switcher: "Python-Scala-Java"
---

## Description
This model contains a deep bidirectional transformer trained on Wikipedia and the BookCorpus. The details are described in the paper "[BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding](https://arxiv.org/abs/1810.04805)".

{:.btn-box}
<button class="button button-orange" disabled>Live Demo</button>
<button class="button button-orange" disabled>Open in Colab</button>
[Download](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/sent_bert_base_cased_en_2.6.0_2.4_1598346030732.zip){:.button.button-orange.button-orange-trans.arr.button-icon}

## How to use

<div class="tabs-box" markdown="1">

{% include programmingLanguageSelectScalaPythonNLU.html %}

```python
...
embeddings = BertEmbeddings.pretrained("sent_bert_base_cased", "en") \
      .setInputCols("sentence") \
      .setOutputCol("sentence_embeddings")
nlp_pipeline = Pipeline(stages=[document_assembler, sentence_detector, embeddings])
pipeline_model = nlp_pipeline.fit(spark.createDataFrame([[""]]).toDF("text"))
result = pipeline_model.transform(spark.createDataFrame(pd.DataFrame({"text": ["I hate cancer, "Antibiotics aren't painkiller"]})))
```

```scala
...
val embeddings = BertEmbeddings.pretrained("sent_bert_base_cased", "en")
      .setInputCols("sentence")
      .setOutputCol("sentence_embeddings")
val pipeline = new Pipeline().setStages(Array(document_assembler, sentence_detector, embeddings))
val result = pipeline.fit(Seq.empty["I hate cancer, "Antibiotics aren't painkiller"].toDS.toDF("text")).transform(data)
```

{:.nlu-block}
```python
import nlu

text = ["I hate cancer", "Antibiotics aren't painkiller"]
embeddings_df = nlu.load('en.embed_sentence.bert_base_cased').predict(text, output_level='sentence')
embeddings_df
```

</div>

{:.h2_title}
## Results
```bash
	en_embed_sentence_bert_base_cased_embeddings 	      sentence
		
	[0.6762558221817017, 0.05294809862971306, -0.2... 	I hate cancer
 	[0.3460788130760193, -0.06936988979578018, 0.1... 	Antibiotics aren't painkiller
```


{:.model-param}
## Model Information

{:.table-model}
|---|---|
|Model Name:|sent_bert_base_cased|
|Type:|embeddings|
|Compatibility:|Spark NLP 2.6.0+|
|License:|Open Source|
|Edition:|Official|
|Input Labels:|[sentence]|
|Output Labels:|[sentence_embeddings]|
|Language:|[en]|
|Dimension:|768|
|Case sensitive:|true|

{:.h2_title}
## Data Source
The model is imported from [https://tfhub.dev/google/bert_cased_L-24_H-1024_A-16/1](https://tfhub.dev/google/bert_cased_L-24_H-1024_A-16/1)
