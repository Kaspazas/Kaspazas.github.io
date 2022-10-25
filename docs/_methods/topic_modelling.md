---
title: Topic Modelling
name: Topic Modelling
layout: page
desc: Topic modelling of textual social media data
---

Topic modelling is a machine learning powered method of deriving topics present in textual corpora.

<h2>Example of implementation</h2>
More details coming soon

Making of corpus to be fed into the ML process:

    nlp = spacy.load("en_core_web_sm")
    
    stop_words = spacy.lang.en.stop_words.STOP_WORDS #load stop words
    processed_docs = [] #create a list of comments that are already processed
    for doc in nlp.pipe(docs):
        doc = [token.lemma_ for token in doc if token.is_alpha] #Tokenize tweets
        doc = [token for token in doc if token not in stop_words] #remove stop words
        doc = [token for token in doc if len(token) > 2] #??
        processed_docs.append(doc)
    
    dictionary = gensim.corpora.Dictionary(processed_docs)  # create Gensim dictionary which maps word ids to word counts
    dictionary.filter_extremes(no_below=10)  # filter out words which are too frequent or too rare
    dictionary.save('tl_corpus.dict')  # save for later use
    corpus = [dictionary.doc2bow(doc) for doc in processed_docs]  # initialize Gensim corpus
    gensim.corpora.MmCorpus.serialize('corpus.mm', corpus)  # save for later use

Making of the model, note that all sorts of variables need to be experimented with and optimized for best results.

    model = models.LdaModel(corpus=corpus,
                            id2word=dictionary,
                            num_topics=13,
                            chunksize=chunksize,
                            alpha='auto',
                            eta='auto',
                            iterations=iterations,
                            passes=passes,
                            eval_every=eval_every,
                            random_state=42, )
    
    model.print_topics()
    model.save('lda10.model')
    model = models.load('lda10.model')
    
assign topics to downloaded comments:

    i = 0
    topic_comment = pd.DataFrame(columns=['topic','probability']) #in this script the secondary topic group is not saved
    for doc in corpus:
        try:
            topics = model.get_document_topics(doc, minimum_probability=0.25) #only get docs with a 30% probability of association
            if len(topics) > 2:
                topics = topics.drop([1])
            if len(topics) == 0:
                topics = {'topic':'inconclusive', 'probability':'na'}
                topic_comment = topic_comment.append(topics, ignore_index=True)
                print('doc ', i, '=', topics)
                i=i+1
                continue
            topics = {'topic': topics[0][0], 'probability': topics[0][1]}
            topic_comment = topic_comment.append(topics, ignore_index=True)
            print('doc ', i, '=', topics)
        except:
            topics = {'topic': 'inconclusive', 'probability': 'na'}
            topic_comment = topic_comment.append(topics, ignore_index=True)
            print('doc ', i, '=', topics)
    
        i += 1


<h2>Visualizations</h2>
coming soon