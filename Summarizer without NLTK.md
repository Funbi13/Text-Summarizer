```python
import string

def text_summarizer(text, num_sentences=3):
    text = text.translate(str.maketrans("", "", string.punctuation)).lower()

    words = text.split()

    stop_words = set([
        "i", "me", "my", "myself", "we", "our", "ours", "ourselves", "you", "your", "yours", "yourself", "yourselves",
        "he", "him", "his", "himself", "she", "her", "hers", "herself", "it", "its", "itself", "they", "them", "their",
        "theirs", "themselves", "what", "which", "who", "whom", "this", "that", "these", "those", "am", "is", "are", "was",
        "were", "be", "been", "being", "have", "has", "had", "having", "do", "does", "did", "doing", "a", "an", "the", "and",
        "but", "if", "or", "because", "as", "until", "while", "of", "at", "by", "for", "with", "about", "against", "between",
        "into", "through", "during", "before", "after", "above", "below", "to", "from", "up", "down", "in", "out", "on", "off",
        "over", "under", "again", "further", "then", "once", "here", "there", "when", "where", "why", "how", "all", "any",
        "both", "each", "few", "more", "most", "other", "some", "such", "no", "nor", "not", "only", "own", "same", "so",
        "than", "too", "very", "s", "t", "can", "will", "just", "don", "should", "now", "d", "ll", "m", "o", "re", "ve", "y",
        "ain", "aren", "couldn", "didn", "doesn", "hadn", "hasn", "haven", "isn", "ma", "mightn", "mustn", "needn", "shan", "shouldn", "wasn", "weren", "won", "wouldn"
    ])

    words = [word for word in words if word not in stop_words]

    word_freq = {}
    for word in words:
        if word in word_freq:
            word_freq[word] += 1
        else:
            word_freq[word] = 1

    sentence_scores = {}
    sentences = text.split('.')
    for sentence in sentences:
        for word, freq in word_freq.items():
            if word in sentence:
                if sentence in sentence_scores:
                    sentence_scores[sentence] += freq
                else:
                    sentence_scores[sentence] = freq

    top_sentences = sorted(sentence_scores, key=sentence_scores.get, reverse=True)[:num_sentences]

    summary = '. '.join(top_sentences)

    return summary

input_text = """Your input text goes here. It can be a longer piece of text that you want to summarize."""
summary = text_summarizer(input_text)
print("Original Text:\n", input_text)
print("\nSummary:\n", summary)

```

    Original Text:
     Your input text goes here. It can be a longer piece of text that you want to summarize.
    
    Summary:
     your input text goes here it can be a longer piece of text that you want to summarize

