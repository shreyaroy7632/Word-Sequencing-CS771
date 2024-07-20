Problem 1.1 (Word Sequencing). In the area of genetic research, a common task is to sequence
a genome i.e., find out the exact sequence of base pairs (ATCG) present in the DNA of an
organism. However, this is tricky to do directly. The DNA is seldom available in the form of a
single long chain that can be read end-to-end. Instead, the DNA is often broken up into short
strands each of which is sequenced to obtain the sequence of base pairs in those strands. The
whole genome is then using these partial sequences by exploiting the fact that these strands are
often overlapping.
Melbo is fascinated with genetics given its exciting applications such as synthetic biology, CRISPR etc that that have massive theraputic and industrial applications. Melbo wishes
to gain experience in this field by solving an NLP version of the sequencing problem. For
a string, a character bigram is simply a sequence of 2 characters that appear adjacent to
each other in that string. Consider the English word area – it has the following 3 bigrams
( ’ar’, ’re’, ’ea’ ). To take another example, the English word beside has the following
5 bigrams ( ’be’, ’es’, ’si’, ’id’, ’de’ )
Melbo wants to guess the word given only the bigrams that appear in that word. This
problem may appear straightforward if the bigrams are presented in the order in which they
appear in the word. However, similar to the DNA sequencing case, the bigrams are not available
in such neat order. Instead the following is done before handing the bigrams to Melbo:
1. The set of bigrams are calculated for a word.
2. Duplicates are removed i.e. if a bigram appears twice or more in a word, its duplicate
instances are removed.
3. The bigrams are sorted in lexicographic (alphabetically increasing) order.
4. Only the first 5 bigrams are retained and the rest are thrown away.
For example, for the English word optional, the entire list of bigrams is first created which
happens to be ( ’op’, ’pt’, ’ti’, ’io’, ’on’, ’na’, ’al’ ). These are then sorted in
lexicographic order to get ( ’al’, ’io’, ’na’, ’on’, ’op’, ’pt’, ’ti’ ). Then only the
first 5 bigrams are retained to get ( ’al’, ’io’, ’na’, ’on’, ’op’ ).
We note that it may not be possible to uniquely identify a word given its bigrams processed
as above. The process of sorting the bigrams, removing duplicates and retaining only 5 bigrams
can cause clashes.
1. Sorting introduces clashes: the above process will give the same set of bigrams ( ’ar’, ’ea’, ’re’ )
for the words area and rear since the bigrams are sorted
2. Neglecting duplicates introduces clashes: the above process will give the same set of
bigrams ( ’be’, ’de’, ’es’, ’id’, ’si’ ) for the words beside and besides since
we discard duplicate bigrams
3. Retaining only 5 bigrams introduces clashes: the above process will give the same set of bigrams ( ’al’, ’io’, ’na’, ’on’, ’op’ ) for the words optional and proportional
since we report only 5 bigrams
Still, it is assured that each bigram set corresponds to at most 5 words i.e. there is no 6-way
clash – the worst that can happen is that the above process generates the same set of bigrams
for 5 different words. An example of a 3-way clash is the following: the above process will give
the same set of bigrams ( ’ci’, ’en’, ’ff’, ’fi’, ’ic’ ) for the words insufficient,
sufficient, and sufficiently.
Melbo’s task is the following: given a list of bigrams as a Python tuple such that the tuple
contains 5 or less bigrams and the bigrams are sorted in lexicographic order, guess one or more
words that correspond to that list of bigrams. Melbo is allowed to make upto 5 guesses (since
there could potentially be a 5-way tie). Melbo returns these guesses in the form of a list of
words. If Melbo’s list contains more than 5 guesses, only the first 5 guesses will be considered.
If the correct word is present in Melbo’s guess list, Melbo gets a score of 1 divided by the number
of guesses Melbo made (thus, it is beneficial for Melbo to make as few guesses as possible). If
the correct word is not in Melbo’s guess list, Melbo gets a score of 0. This score is called the
precision of the output. The average precision across all test points is the final precision of the
model.
Your Data. We have provided you with a dictionary of N = 5167 words. Each word in the
dictionary is written using only lower-case Latin characters i.e. a - z. At test time, Melbo
will need to guess each word from the dictionary given its (deduplicated, sorted and truncated)
bigram list.
Your Task. You need to develop an ML algorithm (we recommend a decision tree but other
solutions are admissible as well) that can play this guessing game on words from the given
dictionary. However, note that your algorithm will be tested on a secret dictionary that we
have not revealed to you – more on this later. The following enumerates the 2 parts to the
question. Part 1 needs to be answered in the PDF file containing your report. Part 2 needs to
be answered in the Python file.
1. Give detailed calculations explaining the various design decisions you took to develop your
ML algorithm. For instance, if you did use a decision tree algorithm, this includes the
criterion to choose the splitting criterion at each internal node (e.g. if a certain bigram is
present in the bigram list or not), criterion to decide when to stop expanding the decision
tree and make the node a leaf, pruning strategies, hyperparameters etc. (10 marks)
2. Write code implementing your learning algorithm. You are allowed to use libraries such
as numpy, scikit-learn, scipy, skopt. You are also allowed to use the code that we used to
implement decision trees to play the Hangman game during the discussion hour in week 4
(code available on course website). However, you must ensure that you code does run on
our judge system. To ensure this, you must validate your code on Google Colab. Submit
code for your method in submit.py. Your code must implement a my_fit() method that
takes a dictionary as a list of words and returns a trained ML model. Your code must also
implement a my_predict() method that takes your learnt model and a tuple of bigrams
sorted in ascending order, and returns a list of guesses. The my_predict() must return a
list even if it is making only a single guess. If the list contains more than 5 guesses, only
the first 5 will be considered. We will evaluate your method on a different dictionary than
the one we have given you (see below for details). 
