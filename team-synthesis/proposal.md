**Lý do không preprocess cho GPT-4:**
Stemming và stopword removal có thể làm mất 
ngữ cảnh quan trọng mà GPT-4 dùng để hiểu 
requirement. IR methods cần preprocess vì 
dựa trên keyword matching.

### 4.4 IR Implementation

**VSM:**
```python
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity

vectorizer = TfidfVectorizer(stop_words='english')
req_vectors = vectorizer.fit_transform(requirements)
class_vectors = vectorizer.transform(classes)
scores = cosine_similarity(req_vectors, class_vectors)
```

**LSI:**
```python
from gensim import corpora, models, similarities

dictionary = corpora.Dictionary(tokenized_docs)
corpus = [dictionary.doc2bow(doc) for doc in tokenized_docs]
lsi = models.LsiModel(corpus, num_topics=100)
index = similarities.MatrixSimilarity(lsi[corpus])
```

**BM25:**
```python
from rank_bm25 import BM25Okapi

tokenized_classes = [cls.split() for cls in classes]
bm25 = BM25Okapi(tokenized_classes, k1=1.5, b=0.75)
scores = bm25.get_scores(requirement.split())
```

### 4.5 GPT-4 Implementation

**Zero-shot prompt (RQ1, RQ2):**
