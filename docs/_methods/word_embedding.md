---
title: Word Embedding
name: test_embedding
layout: page
desc: Application of Word Embedding to textual social media contents
---
Word-embedding is a machine learning powered method of mathematically representing relationships between words.
Academically it has been used to identify biases embedded in large corpora (such as collections of news articles, social media posts).
An example of identifiable biases, revealed through mathematical relationships, include but are not limited to:
On a continuum of female to male, how far away from the center and in which direction do certain professions find themselves?
On a continuum of good to bad, where do certain personality traits appear?

Note that word embeddeding does not reveal people's opinions per say, but rather how closely are given words (or concepts) related.
In the personality trait example, agreeableness might be viewed positively, but many people could discuss the various issues that an agreeable individual might encounter. Hence, one needs to be aware of what the technology allows for and the results imply.

<h2>An example of implementation</h2>
Following the collection of 200,000 Reddit comments from _/r/UkrainianConflict_. The textual data had to be pre-processed, as shown in [sentiment analysis](/methods/sentiment_analysis).

To make the word embeddeding model creation process manageable, the data is divided into _bins_. 

	def chunker(seq, size):
		return (seq[pos:pos + size] for pos in range(0, len(seq), size))

	for i, chunk in enumerate(chunker(uacon_texts, 200)):
		nlp = spacy.load("en_core_web_lg")
		nlp.add_pipe("merge_entities")
		doc_bin = DocBin(store_user_data = True)
		for doc in nlp.pipe(chunk, n_process = 1, batch_size = 200):
			doc_bin.add(doc)
		chunk_name = (r".\doc_bins_ua\ua_chunk_" + str(i) + ".db")
		print("Saving chunk as: ", chunk_name)
		doc_bin.to_disk(chunk_name)
		
Furthermore, the data is saved in a LineSentence format, wherein each line in a dataframe containts a single sentence.

    def make_LineSentence_corpus(list_of_spacy_docbin_paths, spacy_model = "en_core_web_lg", outfile = "myCorpus.cor"):
        nlp = spacy.load(spacy_model)
        with open(outfile, "w") as corpus:
            for path in list_of_spacy_docbin_paths:
                x =+ 1
                db = DocBin().from_disk(path)
                docs = list()
                for doc in list(db.get_docs(nlp.vocab)):
                    doc = cleaning(doc)
                    doc = " ".join(doc)
                    corpus.write(doc)
                    corpus.write("\n")
                print(path, "loaded to corpus file.")
        print("Corpus generation complete. Path to corpus:", os.path.abspath(outfile))

The resulting LineSentence file is then used to create the actual model:

	d2v = gensim.models.doc2vec.Doc2Vec(
		corpus_file = "./ua_d2v_corpus_pos_tagged_ents_merged.cor",
		dm = 1,
		vector_size = 100,
		window = 5,
		workers = 1
	)
	
Voila, we can now examine closeness and relationships between words:
	print(model.wv.most_similar(positive=['orc'], topn= 3)) # listing the three closest words
results in:
	>>> ('animal', 0.5874612927436829), ('vatnik', 0.5697314739227295), ('motherfucker', 0.5686348676681519)

<h3>Some explorations, visualizations</h3>


<h2>Changes over time as a meaningful method of analysis</h2>
somthing
<h2>Visualizations</h2>
Some examples of vizualization and what I've used them for
