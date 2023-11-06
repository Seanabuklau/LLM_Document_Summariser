# LLM_Document_Summariser

## Introduction
This project was created as part of an assignment to summarise law judgements, as such documents tend to be long in nature i.e. averaging more than 50 pages per case. However, the methodology used can be applied to any text that needs to be summarised. What is showcased here is an automated document summariser pipeline that leverages LLM and the LangChain library as the mainstay summary tools. The LLM of choice here is Google's LLM text-bison which is well suited for summarisation tasks.

## Methodology
There are 3 main steps which span the pipeline, namely Pre-processing, In-processing, and Post-processing. These steps will be further elaborated below.

### i. Pre-processing 
In this step, the following text processing methods will be employed in a chronologically manner, namely Sentence Tokenization, Sentence Cleansing, Stop Word Removal, and Lemmatization. Popular NLP libraries like spaCy and NLTK will be used to carry out these aforementioned tasks. The idea here is to reduce noise and other non-value words which might waste token space in the input since LLMs tend to have input limitations, and in this case 8192 tokens for text-bison.

### ii. In-processing
Here, the Map Reduce chain from LangChain will be employed which enables the iteration over a list of documents, generating individual outputs for each document input, which will then be combined to produce a final result. 

### iii. Post-processing
While generally step ii would suffice for most summarisation tasks, there may be instances where the need to cut down the text even more could arise. Thus, this step addresses such challenges. Here, we can employ Refine chain from LangChain to progressively cut down the result. The aim here is to construct a chain that loops over the input documents while iteratively updating its answer each time. The final yield would be a more refined output. Note that this step here is optional and should only be used if the summarised output from the Map Reduce chain is still too big and verbose. 

## Results and Evaluation 

### i. Metrics
To evaluate the pipeline, 2 metrics were used, namely Jaccard similarity and Cosine similarity were used. The former was chosen as it is often used to measure the similarity between two sets of words or tokens, particularly when the focus is about the presence or absence of terms. The latter on the other hand is concerned with providing a measure of document directional similarity, and is particularly useful to compare the overall semantic similarity between two documents or sentences.

### ii. Results
To evaluate the summarised results, the outputs from the pipeline were compared against summarised judgements i.e. benchmark cases taken from Law firm websites e.g. Rajah & Tann. The idea is that law firms would aim to produce high quality summaries with good amounts of legal substance in order to educate their clients and staff on new cases and on any law updates.

Based on this evaluation, the following was observed:
- The Jacquard Similarity yielded a generally low score between the summarised case and the benchmark case, averaging around 17%. This was no surprise since the length of the summary outputs from the Map Reduce Chain were way shorter than the benchmark text, and therefore the size of the intersection of words and phrases between the two documents would be likewise smaller.
- The Cosine Similarity yielded generally high scores averaging around 80%. This meant that the semantic similarity between the summarised case and the benchmark case were high, or in other words, both documents are similar in their meaning.

### iii. Conslusion
The conclusion derived is that while this summariser pipeline can produce a decent summary of judgements for the layman to get a quick grasp of the case, it might not be able to deliver summarised judgements with enough legal substance i.e. statues, legal terms, jargons that will be useful for research or academia. Nonetheless, the summariser pipeline is still a useful tool should any summarisation tasks of large documents be needed. 
