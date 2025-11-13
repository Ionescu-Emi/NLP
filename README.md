# NLP
The experiment revealed a stark difference in performance. The corpus was intentionally designed with three subjects whose vocabularies have very little overlap, making it a relatively simple test.

The Successful Models (LDA, NMF, LSA-TFIDF)
Initial LDA (Gensim): This model performed perfectly. The Document-topic mixture table (Section 7) shows that every document was assigned with 100% (1.0) probability to its correct topic.

NMF (TF-IDF): This model also achieved a near-perfect separation. The "NMF document-topic proportions" table shows that each document was assigned a very high proportion (e.g., >0.5) to its correct topic and near-zero values for the others.

LSA (TF-IDF): Despite a lower coherence score (see below), this model's top words list shows it successfully identified the three pure topics.

These models all produced clean, distinct, and interpretable topics, as seen in their top-10 word lists:

Topic (Art): leonardo, michelangelo, renaiss, paint, artist, chapel

Topic (ML): learn, model,s data, train, algorithm, network

Topic (Climate): climat, chang, emiss, carbon, warm, greenhous

The Failed Model (LSA-BoW)
As you correctly identified, the LSA (BoW) model failed to separate the topics.

The "LSA-BoW top words" list clearly shows the problem. While it found the Art topic, it conflated Machine Learning and Climate Change:

Topic 0: climat, learn, emiss, carbon, energi, warm, global... data (This is a mix of Climate and ML)

Topic 1: learn, machin, data, network, deep (This is a pure ML topic)

Topic 2: leonardo, michelangelo, paint, renaiss (This is a pure Art topic)

Because Topic 0 is not a coherent theme, the model failed this test.

📊 Quantitative Comparison: NMF Wins on Coherence
A quantitative comparison using the Coherence Score (c_v)—which measures how semantically related the top words in a topic are—confirms the model differences.

NMF (TF-IDF): 0.691 (Highest Score)

Initial LDA (Gensim): 0.643

LSA (BoW): 0.640

Improved LDA (Gensim): 0.633

LSA (TF-IDF): 0.550 (Lowest Score)

The key takeaway here is that NMF (TF-IDF) was the best-performing model both in terms of its clean topic separation and its high coherence score.

It is critical to note that the high score for LSA (BoW) (0.640) is misleading. While the words within its mixed topic (like climat and learn) might co-occur, the topic itself is incoherent and useless for this analysis. This highlights the danger of relying on a single metric.

🖼️ Visualization Confirms the Failure
The pyLDAvis interactive visualizations provide the final, definitive proof.

Successful Plots (LDA, NMF, LSA-TFIDF): The visualizations for the Initial LDA, NMF, and LSA-TFIDF models all show three large circles (representing the three topics) that are far apart and do not overlap. This is the ideal visual outcome, indicating three highly distinct themes.

Failed Plot (LSA-BoW): In sharp contrast, the pyLDAvis plot for LSA (BoW) visually confirms its failure.Two of the circles (Topic 0 and Topic 1) are shown overlapping significantly. This is the direct visual consequence of Topic 0 being an incoherent mix of Machine Learning and Climate Change terms, causing it to "bleed into" the pure Machine Learning topic.
