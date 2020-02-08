# 13. Textual Data Analysis with NLTK

Fabio Nelli1

(1)Rome, Italy


In this book, you have seen various analysis techniques and numerous examples that worked on data in numerical or tabular form, which is easily processed through mathematical expressions and statistical techniques. But most of the data is composed of text, which responds to grammatical rules (or sometimes not even that :)) that differ from language to language. In text, the words and the meanings attributable to the words (as well as the emotions they transmit) can be a very useful source of information.

In this chapter, you will learn about some text analysis techniques using the NLTK (Natural Language Toolkit) library, which will allow you to perform otherwise complex operations. Furthermore, the topics covered will help you understand this important part of data analysis.

Text Analysis Techniques

In recent years, with the advent of Big Data and the immense amount of textual data coming from the Internet, a lot of text analysis techniques have been developed by necessity. In fact, this form of data can be very difficult to analyze, but at the same time represents a source of a lot of useful information, given also the enormous availability of data. Just think of all the literature produced, the numerous posts published on the Internet, for example. Comments on social networks and chats can also be a great source of data, especially to understand the degree of approval or disapproval of a particular topic.

Analyzing these texts has therefore become a source of enormous interest, and there are many techniques that have been introduced for this purpose, creating a real discipline in itself. Some of the more important techniques are the following:Analysis of the frequency distribution of words

Pattern recognition

Tagging

Analysis of links and associations

Sentiment analysis

The Natural Language Toolkit (NLTK)

If you program in Python and want to analyze data in text form, one of the most commonly used tools at the moment is the Python Natural Language Toolkit (NLTK).

NLTK is nothing more than a Python library ( https://www.nltk.org/ ) in which there are many tools specialized in processing and text data analysis. NLTK was created in 2001 for educational purposes, then over time it developed to such an extent that it became a real analysis tool.

Within the NLTK library, there is also a large collection of sample texts, called corpora . This collection of texts is taken largely from literature and is very useful as a basis for the application of the techniques developed with the NLTK library. In particular, it’s used to perform tests (a role similar to the MNIST dataset present in TensorFlow, which is discussed in Chapter 9).

Installing NLTK on your computer is a very simple operation. Being a very popular Python library, you simply need to install it using pip or conda.

On Linux systems, use this:pip install nltk

On Windows systems (via Anaconda), use this:conda install nltk

Import the NLTK Library and the NLTK Downloader Tool

In order to be more confident with NLTK, there is no better method than working directly with the Python code. In this way you will be able to see and gradually understand the operation of this library.

So the first thing you need to do is open a session on IPython or on a Jupyter Notebook. The first command imports the NLTK library.import nltk

Then you need to import text from the corpora collection. To do this there is a function called nltk.download_shell(), which opens a tool called NLTK Downloader that allows you to make selections through a guided choice of options.

If you enter this command on the terminal:nltk.download_shell()

You will see the various options in text format.NLTK Downloader

---------------------------------------------------------------------------

d) Download l) List u) Update c) Config h) Help q) Quit

---------------------------------------------------------------------------

Downloader>

Now the tool is waiting for an option. If you want to see a list of possible NLTK extensions, enter L for list and press Enter. You will immediately see a list of all the possible packages belonging to NLTK that you can download to extend the functionality of NLTK, including the texts of the corpora collection.Packages:

[ ] abc................. Australian Broadcasting Commission 2006

[ ] alpino.............. Alpino Dutch Treebank

[ ] averaged_perceptron_tagger Averaged Perceptron Tagger

[ ] averaged_perceptron_tagger_ru Averaged Perceptron Tagger (Russian)

[ ] basque_grammars..... Grammars for Basque

[ ] biocreative_ppi..... BioCreAtIvE (Critical Assessment of Information

Extraction Systems in Biology)

[ ] bllip_wsj_no_aux.... BLLIP Parser: WSJ Model

[ ] book_grammars....... Grammars from NLTK Book

[ ] brown............... Brown Corpus

[ ] brown_tei........... Brown Corpus (TEI XML Version)

[ ] cess_cat............ CESS-CAT Treebank

[ ] cess_esp............ CESS-ESP Treebank

[ ] chat80.............. Chat-80 Data Files

[ ] city_database....... City Database

[ ] cmudict............. The Carnegie Mellon Pronouncing Dictionary (0.6)

[ ] comparative_sentences Comparative Sentence Dataset

[ ] comtrans............ ComTrans Corpus Sample

[ ] conll2000........... CONLL 2000 Chunking Corpus

[ ] conll2002........... CONLL 2002 Named Entity Recognition Corpus

Hit Enter to continue:

Pressing Enter again will continue displaying the list by showing other packages in alphabetical order. Press Enter until the list is finished to see all the possible packages. At the end of the list, the different initial options of the NLTK Downloader will reappear.

To be able to create a series of examples to learn about the library, you need a series of texts to work on. An excellent source of texts suitable for this purpose is the Gutenberg corpus, present within the corpora collection. The Gutenberg corpus is a small selection of texts extracted from the electronic archive called the Project Gutenberg ( http://www.gutenberg.org/ ). There are over 25,000 e-books in this archive.

To download this package, first enter the d option to download it. The tool will ask you for the package name, so you then enter the name gutenberg.---------------------------------------------------------------------------

d) Download l) List u) Update c) Config h) Help q) Quit

---------------------------------------------------------------------------

Downloader> d

Download which package (l=list; x=cancel)?

Identifier> gutenberg

At this point the package will start to download.

For the following times, if you already know the name of the package you want to download, just enter the command nltk.download() with the package name as an argument. This will not open the NLTK Downloader tool, but will directly download the required package. So the previous operation is equivalent to writing:nltk.download ('gutenberg')

Once it’s completed you can see the contents of the package thanks to the fileids() function , which shows the names of the files contained in it.gb = nltk.corpus.gutenberg

print ("Gutenberg files:", gb.fileids ())

An array will appear on the terminal with all the text files contained in the gutenberg package.Gutenberg files : ['austen-emma.txt', 'austen-persuasion.txt', 'austen-sense.txt', 'bible-kjv.txt', 'blake-poems.txt', 'bryant-stories.txt', 'burgess-busterbrown.txt', 'carroll-alice.txt', 'chesterton-ball.txt', 'chesterton-brown.txt', 'chesterton-thursday.txt', 'edgeworth-parents.txt', 'melville-moby_dick.txt', 'milton-paradise.txt', 'shakespeare-caesar.txt', 'shakespeare-hamlet.txt', 'shakespeare-macbeth.txt', 'whitman-leaves.txt']

To access the internal content of one of these files, you first select one, for example Shakespeare's Macbeth (shakespeare-macbeth.txt), and then assign it to a variable of convenience. An extraction mode is for words, that is, you want to create an array containing words as elements. In this regard, you need to use the words() function.macbeth = nltk.corpus.gutenberg.words ('shakespeare-macbeth.txt')

If you want to see the length of this text (in words), you can use the len() function .len (macbeth)

23140

The text used for these examples is therefore composed of 23140 words.

The macbeth variable we created is a long array containing the words of the text. For example, if you want to see the first 10 words of the text, you can write the following command.macbeth [:10]

['[',

'The',

'Tragedie',

'of',

'Macbeth',

'by',

'William',

'Shakespeare',

'1603',

']']

As you can see, the first 10 words contain the title of the work, but also the square brackets, which indicate the beginning and end of a sentence. If you had used the sentence extraction mode with the sents() function , you would have obtained a more structured array, with each sentence as an element. These elements, in turn, would be arrays with words for elements.macbeth_sents = nltk.corpus.gutenberg.sents ('shakespeare-macbeth.txt')

macbeth_sents [: 5]

[['[',

'The',

'Tragedie',

'of',

'Macbeth',

'by',

'William',

'Shakespeare',

'1603',

']'],

['Actus', 'Primus', '.'],

['Scoena', 'Prima', '.'],

['Thunder', 'and', 'Lightning', '.'],

['Enter', 'three', 'Witches', '.']]

Search for a Word with NLTK

One of the most basic things you need to do when you have an NLTK corpus (that is, an array of words extracted from a text) is to do research inside it. The concept of research is slightly different than what you are used to.

The concordance() function looks for all occurrences of a word passed as an argument within a corpus.

The first time you run this command, the system will take several seconds to return a result. The subsequent times will be faster. In fact, the first time this command is executed on a corpus it creates an indexing of the content to perform the search, which once created will be used in subsequent calls. This explains why the system takes more time the first time.

First, make sure that the corpus is an object nltk.Text, and then search internally for the word 'Stage'.text = nltk.Text(macbeth)

text.concordance('Stage')

Displaying 3 of 3 matches:

nts with Dishes and Seruice ouer the Stage . Then enter Macbeth Macb . If it we

with mans Act , Threatens his bloody Stage : byth ' Clock ' tis Day , And yet d

struts and frets his houre vpon the Stage , And then is heard no more . It is

You have obtained three different occurrences of the text.

Another form of searching for a word present in NLTK is that of context. That is, the previous word and the next word to the one you are looking for. To do this, you must use the common_contexts() function .text.common_contexts(['Stage'])

the_ bloody_: the_,

If you look at the results of the previous research, you can see that the three results correspond to what has been said.

Once you understand how NLTK conceives the concept of the word and its context during the search, it will be easy to understand the concept of a synonym. That is, it is assumed that all words that have the same context can be possible synonyms. To search for all words that have the same context as the searched one, you must use the similar() function .text.similar('Stage')

fogge ayre bleeding reuolt good shew heeles skie other sea feare

consequence heart braine seruice herbenger lady round deed doore

These methods of research may seem rather strange for those who are not used to processing and analyzing text, but you will soon understand that these methods of research are perfectly suited to the words and their meaning in relation to the text in which they are present.

Analyze the Frequency of Words

One of the simplest and most basic examples for the analysis of a text is to calculate the frequency of the words contained in it. This operation is so common that it has been incorporated into a single nltk.FreqDist() function to which the variable containing the word array is passed as an argument.

So to get a statistical distribution of all the words in the text, you'll have to enter a simple command.fd = nltk.FreqDist(macbeth)

If you want to see the first 10 most common words in the text, you can use the most_common() function .fd.most_common(10)

[(',', 1962),

('.', 1235),

("'", 637),

('the', 531),

(':', 477),

('and', 376),

('I', 333),

('of', 315),

('to', 311),

('?', 241)]

From the result obtained, you can see that the most common elements are punctuation, prepositions, and articles, and this applies to many languages, including English. Since these have little meaning during text analysis, it is often necessary to eliminate them. These are called stopwords .

Stopwords are words that have little meaning in the analysis and must be filtered. There is no general rule to determine whether a word is a stopword (to be deleted) or not. However, the NLTK library comes to the rescue by providing you with an array of pre-selected stopwords. To download stopwords, you can use the nltk.download() command.nltk.download('stopwords')

Once you have downloaded all the stopwords, you can select only those related to English, saving them in a variable sw.sw = set(nltk.corpus.stopwords.words ('english'))

print(len(sw))

list(sw) [:10]

179

['through',

'are',

'than',

'nor',

'ain',

"didn't",

'didn',

"shan't",

'down',

'our']

There are 179 stopwords in the English vocabulary according to NLTK. Now you can use these stopwords to filter the macbeth variable .macbeth_filtered = [w for w in macbeth if w.lower() not in sw]

fd = nltk.FreqDist (macbeth_filtered)

fd.most_common(10)

[(',', 1962),

('.', 1235),

("'", 637),

(':', 477),

('?', 241),

('Macb', 137),

('haue', 117),

('-', 100),

('Enter', 80),

('thou', 63)]

Now that the first 10 most common words are returned, you can see that the stopwords have been eliminated, but the result is still not satisfactory. In fact, punctuation is still present in the words. To eliminate all punctuation, you can change the previous code by inserting in the filter an array of punctuation containing the punctuation symbols. This punctuation array can be obtained by importing the string function .import string

punctuation = set (string.punctuation)

macbeth_filtered2 = [w.lower () for w in macbeth if w.lower () not in sw and w.lower () not in punctuation]

Now you can recalculate the frequency distribution of words.fd = nltk.FreqDist (macbeth_filtered2)

fd.most_common(10)

[('macb', 137),

('haue', 122),

('thou', 90),

('enter', 81),

('shall', 68),

('macbeth', 62),

('vpon', 62),

('thee', 61),

('macd', 58),

('vs', 57)]

Finally, the result is what you were looking for.

Selection of Words from Text

Another form of processing and data analysis is the process of selecting words contained in a body of text based on particular characteristics. For example, you might be interested in extracting words based on their length.

To get all the longest words, for example words that are longer than 12 characters, you enter the following command.long_words = [w for w in macbeth if len(w)> 12]

All words longer than 12 characters have been entered in the long_words variable. You can list them in alphabetical order by using the sort() function.sorted(long_words)

['Assassination',

'Chamberlaines',

'Distinguishes',

'Gallowgrosses',

'Metaphysicall',

'Northumberland',

'Voluptuousnesse',

'commendations',

'multitudinous',

'supernaturall',

'vnaccompanied']

As you can see, there are 11 words that meet this criteria.

Another example is to look for all the words that contain a certain sequence of characters, such as 'ious'. You only have to change the condition in the for in loop to get the desired selection.ious_words = [w for w in macbeth if 'ious' in w]

ious_words = set(ious_words)

sorted(ious_words)

['Auaricious',

'Gracious',

'Industrious',

'Iudicious',

'Luxurious',

'Malicious',

'Obliuious',

'Pious',

'Rebellious',

'compunctious',

'furious',

'gracious',

'pernicious',

'pernitious',

'pious',

'precious',

'rebellious',

'sacrilegious',

'serious',

'spacious',

'tedious']

In this case, you used sort() to make a list casting, so that it did not contain duplicate words.

These two examples are just a starting point to show you the potential of this tool and the ease with which you can filter words.

Bigrams and Collocations

Another basic element of text analysis is to consider pairs of words (bigrams) instead of single words. The words「is」and「yellow」are for example a bigram, since their combination is possible and meaningful. So「is yellow」can be found in textual data. We all know that some of these bigrams are so common in our literature that they are almost always used together. Examples include「fast food」,「pay attention」,「good morning」, and so on. These bigrams are called collocations.

Textual analysis can also involve the search for any bigrams within the text under examination. To find them, simply use the bigrams() function. In order to exclude stopwords and punctuation from the bigrams, you must use the set of words already filtered previously, such as macbeth_filtered2.bgrms = nltk.FreqDist(nltk.bigrams(macbeth_filtered2))

bgrms.most_common(15)

[(('enter', 'macbeth'), 16),

(('exeunt', 'scena'), 15),

(('thane', 'cawdor'), 13),

(('knock', 'knock'), 10),

(('st', 'thou'), 9),

(('thou', 'art'), 9),

(('lord', 'macb'), 9),

(('haue', 'done'), 8),

(('macb', 'haue'), 8),

(('good', 'lord'), 8),

(('let', 'vs'), 7),

(('enter', 'lady'), 7),

(('wee', 'l'), 7),

(('would', 'st'), 6),

(('macbeth', 'macb'), 6)]

By displaying the most common bigrams in the text, linguistic locations can be found.

In addition to the bigrams, there can also be placements based on trigrams, which are combinations of three words. In this case, the trigrams() function is used.tgrms = nltk.FreqDist(nltk.trigrams (macbeth_filtered2))

tgrms.most_common(10)

[(('knock', 'knock', 'knock'), 6),

(('enter', 'macbeth', 'macb'), 5),

(('enter', 'three', 'witches'), 4),

(('exeunt', 'scena', 'secunda'), 4),

(('good', 'lord', 'macb'), 4),

(('three', 'witches', '1'), 3),

(('exeunt', 'scena', 'tertia'), 3),

(('thunder', 'enter', 'three'), 3),

(('exeunt', 'scena', 'quarta'), 3),

(('scena', 'prima', 'enter'), 3)]

Use Text on the Network

So far you have seen a series of examples that use already ordered and included text (called a corpus) within the NLTK library as gutenberg. But in reality, you will need to access the Internet to extract the text and collect it as a corpus to be used for analysis with NLTK.

In this section, you will see how simple this kind of operation is. First, you need to import a library that allows you to connect to the contents of web pages. The urllib library is an excellent candidate for this purpose, as it allows you to download the text content from the Internet, including HTML pages.

So first you import the request() function, which specializes in this kind of operation, from the urllib library.from urllib import request

Then you have to write the URL of the page that contains the text to be extracted. Still referring to the gutenberg project, you can choose, for example, a book written by Dostoevsky ( http://www.gutenberg.org ). On the site there is text in different formats; at this point we will choose the one in the raw format (.txt).url = "http://www.gutenberg.org/files/2554/2554-0.txt"

response = request.urlopen(url)

raw = response.read().decode('utf8')

Within the raw text is all the textual content of the book, downloaded from the Internet. Always check the contents of what you have downloaded. To do this, the first 75 characters are enough.raw[:75]

'\ufeffThe Project Gutenberg EBook of Crime and Punishment, by Fyodor Dostoevsky\r'

As you can see, these characters correspond to the title of the text. We see that there is also an error in the first word of the text. In fact there is the Unicode character BOM \ufeff. This happened because we used the utf8 decoding system, which is valid in most cases, but not in this case. The most suitable system in this case is utf-8-sig. Replace the incorrect value with the correct one.raw = response.read().decode('utf8-sig')

raw[:75]

'The Project Gutenberg EBook of Crime and Punishment, by Fyodor Dostoevsky\r\n'

Now to be able to work on it, you have to convert it into a corpus compatible with NLTK. To do this, enter the following conversion commands.tokens = nltk.word_tokenize (raw)

webtext = nltk.Text (tokens)

These commands do nothing more than split into tokens (that is, words) the character text with the function nltk.word_tokenize() and then convert tokens into a textual body suitable for NLTK with nltk.Text().

You can see the title by entering this commandwebtext[:12]

['The',

'Project',

'Gutenberg',

'EBook',

'of',

'Crime',

'and',

'Punishment',

',',

'by',

'Fyodor',

'Dostoevsky']

Now you have a correct corpus on which to begin to carry out your analysis.

Extract the Text from the HTML Pages

In the previous example, you created a NLTK corpus from text downloaded from the Internet. But most of the documentation on the Internet is in the form of HTML pages. In this section, you will see how to extract text from HTML pages.

You always use the request() function of the urllib library to download the HTML content of a web page.url = "http://news.bbc.co.uk/2/hi/health/2284783.stm"

html = request.urlopen(url).read().decode('utf8')

html[:120]

'<!doctype html public "-//W3C//DTD HTML 4.0 Transitional//EN" "http://www.w3.org/TR/REC-html40/loose.dtd">\r\n<html>\r\n<hea'

Now, however, the conversion into NLTK corpus requires an additional library, bs4 (BeautifulSoup), which provides you with suitable parsers that can recognize HTML tags and extract the text contained in them.from bs4 import BeautifulSoup

raw = BeautifulSoup(html, "lxml").get_text()

tokens = nltk.word_tokenize(raw)

text = nltk.Text(tokens)

Now you also have a corpus in this case, even if you often have to perform more complex cleaning operations than the previous case to eliminate the words that do not interest you.

Sentimental Analysis

Sentimental analysis is a new field of research that has developed very recently in order to evaluate people’s opinions about a particular topic. This discipline is based on different techniques that use text analysis and its field of work in the world of social media and forums ( opinion mining ).

Thanks to comments and reviews by users, sentimental analysis algorithms can evaluate the degree of appreciation or evaluation based on certain keywords. This degree of appreciation is called opinion and has three possible values: positive, neutral, or negative. The assessment of this opinion thus becomes a form of classification.

So many sentimental analysis techniques are actually classification algorithms similar to those you saw in previous chapters covering machine learning and deep learning (see Chapters 8 and 9).

As an example to better understand this methodology, we reference a classification tutorial using the Naïve Bayes algorithm on the official website ( https://www.nltk.org/book/ch06.html ), where it is possible to find many other very useful examples to better understand this library.

As a training set, this example uses another corpus present in NLTK, which is very useful for these types of classification problems: movie_reviews. This corpus contains numerous film reviews in which there is text of a discrete length together with another field that specifies whether the criticism is positive or negative. Therefore, it serves as great learning material.

The purpose of this tutorial is to find the words that recur most in negative documents, or words that recur more in positive ones, so as to focus on the keywords related to an opinion. This evaluation will be carried out through a Naïve Bayes Classification integrated into NLTK.

First of all, the corpus called movie_reviews is important.nltk.download('movie_reviews')

Then you build the training set from the corpus obtained, creating an array of element pairs called documents . This array contains in the first field the text of the single review, and in the second field the negative or positive evaluation. At the end, you will mix all the elements of the array in random order.import random

reviews = nltk.corpus.movie_reviews

documents = [(list(reviews.words(fileid)), category)

for category in reviews.categories()

for fileid in reviews.fileids(category)]

random.shuffle(documents)

To better understand, see the contents of documents in detail. The first element contains two fields; the first is the review containing all the words used.first_review = ' '.join(documents[0][0])

print(first_review)

topless women talk about their lives falls into that category that i mentioned in the devil ' s advocate : movies that have a brilliant beginning but don ' t know how to end . it begins by introducing us to a selection of characters who all know each other . there is liz , who oversleeps and so is running late for her appointment , prue who is getting married ,...

The second field instead contains the evaluation of the review:documents[0][1]

'neg'

But the training set is not yet ready; in fact you have to create a frequency distribution of all the words in the corpus. This distribution will be converted into a casting list with the list() function .all_words = nltk.FreqDist(w.lower() for w in reviews.words())

word_features = list(all_words)

Then the next step is to define a function for the calculation of the features, i.e., words that are important enough to establish the opinion of a review.def document_features(document, word_features):

document_words = set(document)

features = {}

for word in word_features:

features ['{}'.format(word)] = (word in document_words)

return features

Once you have defined the document_features() function , you can create feature sets from documents.featuresets = [(document_features (d, c)) for (d, c) in documents]

The aim is to create a set of all the words contained in the whole movie corpus, analyze whether they are present (True or False) in each single review, and see how much they contribute to the positive or negative judgment of it. The more often a word is present in the negative reviews and the less often it’s present in the positive ones, the more it’s evaluated as a「bad」word. The opposite is true for a「good」word evaluation.

To determine how to subdivide this feature set for the training set and the testing set, you must first see how many elements it contains.len (featuresets)

2000

Then you use the first 1,500 elements of the set for the training set, and the last 500 items for the testing set, in order to evaluate the accuracy of the model.train_set, test_set = featuresets[1500:], featuresets[: 500]

Finally, you apply the Naïve Bayes classifier provided by the NLTK library to classify this problem. Then you calculate its accuracy, submitting the test set to the model.classifier = nltk.NaiveBayesClassifier.train(train_set)

print (nltk.classify.accuracy(classifier, test_set))

0.85

The accuracy is not as high as in the examples from the previous chapters, but we are working with words contained in text, and therefore it is very difficult to create accurate models relative to numerical problems.

Now that you have completed the analysis, you can see which words have the most weight in evaluating the negative or positive opinion of a review.classifier.show_most_informative_features(10)

Most Informative Features

badly = True neg : pos = 11.1 : 1.0

julie = True neg : pos = 9.5 : 1.0

finest = True pos : neg = 9.0 : 1.0

forgot = True neg : pos = 8.8 : 1.0

naked = True neg : pos = 8.8 : 1.0

refreshing = True pos : neg = 7.9 : 1.0

stolen = True pos : neg = 7.3 : 1.0

luckily = True pos : neg = 7.3 : 1.0

directs = True pos : neg = 7.3 : 1.0

rain = True neg : pos = 7.3 : 1.0

Looking at the results, you will not be surprised to find that the word「badly」is a bad opinion word and that「finest」is a good opinion word. The interesting thing here is that「julie」is a bad opinion word.

Conclusions

In this chapter, you took a small glimpse of the text analysis world. In fact, there are many other techniques and examples that could be discussed. However, at the end of this chapter, you should be familiar with this branch of analysis and especially have begun to learn about the NLTK (Natural Language Toolkit) library, a powerful tool for text analysis.

© Fabio Nelli 2018

Fabio NelliPython Data Analyticshttps://doi.org/10.1007/978-1-4842-3913-1_14


