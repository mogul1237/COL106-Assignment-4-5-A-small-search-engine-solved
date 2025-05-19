# COL106-Assignment-4-5-A-small-search-engine-solved

Download Here: [COL106 Assignment 4-5 A small search engine solved](https://jarviscodinghub.com/assignment/assignment-4-5-a-small-search-engine-solution/)

For Custom/Original Work email jarviscodinghub@gmail.com/whatsapp +1(541)423-7793

In this assignment we will build the basic data structure underlying search engines: an inverted index. We will use this inverted index to answer some simple search queries.
An inverted index for a set of webpages
Suppose we are given a set of webpages W. For our purposes, each webpage w ∈ W will be considered to be a sequence of words w1,w2,…wk. Another way of representing the webpage could be to maintain a list of words along with the position(s) of the words in the webpage. For example consider a web page with the following text:
Data structures is the study of structures for storing data.
This can be represented as {(data : 1,10),(structures : 2,7),(study : 5),(storing : 9)}. Note that the small connector words like “is”, “the”, “of”, “for” have not been stored. Words like this are referred to as stop words and are generally removed since they are very frequent and normally contain no information about the content of the webpage. This representation of the webpage is similar to the index we see at the back of many books which tell us the page numbers where certain important terms used in the book may be found. In fact, we can refer to this as an
1
index for the webpage. In mathematical notation we would say that given a webpage w = w1,w2,…,wk, the index of w is {(u : i1(u),…i`(u)) : wij(u) = u,1 ≤ j ≤ `}. An index is used to ﬁnd the location of a particular string (word) in a speciﬁc document or webpage, but when we move to a collection of webpages, we need to ﬁrst ﬁgure out which of the web pages contain the string. For this we store an inverted index. Let us try to deﬁne an inverted index formally. Let us suppose we are given a collection C of webpages. For each pagep ∈ C, let us denote by W(p) the set of all words (excluding stop words) that occur in p. Note that W(C) = [ p∈C W(p), is the set of all words in our collection. An inverted index for C will contain an entry for each word w ∈ W(C). This entry will contain tuples of the form (p,k) to indicate that w occurs in the kth position of page p ∈C. Using the notation that p[k] denotes the kth word of page p, we can say that the inverted index of C is deﬁned as Inv(C) = {(w : {(p,k) : p ∈C,p[k] = w}) : w ∈ W(C)}. For example, consider the following (small) collection of documents.
1: Data structures is the study of structures for storing data. 2: Structural engineers collect data about structures
The inverted index for this would be
{(data : {(1,1), (1,10), (2,4)}), (structures: {(1,2), (1,7), (2,6)}), (study : {(1,5)}), (storing : {(1,9)}), (structural : {(2,1)}), (engineers : {(2,2)}), (collect : {(2,3)}) }
2
The web search problem
The web search problem is deﬁned as follows: Given a collection of webpagesC and a sequence of words q1 …qk, ﬁnd the “most relevant” set of pages p1,p2,…p` that contain as many of q1 …qk as possible and return them in the order of decreasing “relevance.”
The question of how to measure the relevance of a webpage to a particular query is an involved question with no easy answers. However, for the purpose of this assignment we will work with a simple scoring function.
A scoring function for search term relevance
Given a word w and a webpage p, if w occurs ` times in positions k1,…,k`, the relevance score of the page p for the word w is deﬁned as
relevancew(p) =
` X i=1
1 k2 i
.
So, if we are given a search query that has a single term, say w, to return the webpages in order of relevance we have to ﬁrst extract the entry corresponding to w from Inv(C) and then calculate the relevance of each page and return the pages in decreasing order of relevance.
Compound searches
In this assignment we will answer three kinds of search queries: AND queries, OR queries and phrase queries. We now describe these three along with their scoring methodology. • OR queries: Given a search query q1 …qk, any page that contains any of the words q1 to qk is a valid answer. The relevance score of a page p is computed as
relevanceq1…qk(p) =
k X i=1
relevanceqi(p),
and pages are returned in decreasing order of relevance. Note that if some qi does not occur in page p the relevanceqi(p) = 0.
3
• AND queries: Given a search query q1 …qk, any page that contains all of the words q1 to qk is a valid answer. The relevance score of a page p is computed as
relevanceq1…qk(p) =
k X i=1
relevanceqi(p),
and pages are returned in decreasing order of relevance. • Phrase queries : Given a search query q1 …qk, any page that contains q1 in position `, q2 in position `+1 and so on till qk in position `+k−1 is said to contain the phrase q1 …qk at the position `. Suppose a webpage p contains the phrase q1 …qk at positions `1,`2,…`m then the relevance score of page p for this phrase is
relevanceq1…qk(p) =
m X i=1
1 `2 i
.
The programming assignment
The implementation of the search engine has been divided in to two assignments. You have been provided with separate folders for each assignment having their own webpages folder and actions.txt. In the ﬁrst assignment, Assignment 4, we will build the basic backbone of the search engine and answer single word search queries. Compound queries will be implemented in Assignment 5. Note that both the assignments have diﬀerent deadlines.
Assignment 4 [100 marks] Deadline: 11:55 PM, 3 October 2016
• Write a Java class MySet using Java generic’s (https://docs.oracle.com/javase/tutorial/java/generics/types.html). The class should be represented as MySet – void addElement(X element): Add element to the set. – MySet 4
– MySet – Position(PageEntry p, int wordIndex) Constructor method. – PageEntry getPageEntry() Return p – int getWordIndex() Return wordIndex • Write a Java class WordEntry. For a string str, this class stores the list of word indice’s where str is present in the document(s).
– WordEntry(String word): Constructor method. The argument is the word for which we are creating the word entry. – void addPosition(Position position): Add a position entry for str. – void addPositions(MyLinkedList – void addPositionForWord(String str, Position p): Add position p to the word-entry of str. If a word entry for str is already present in the page index, then add p to the word entry. Otherwise, create a new word-entry for str with just one position entry p. – LinkedList 5
– PageEntry(String pageName): Constructor method. The argument is the name of the document. Read this ﬁle, and create the page index. – PageIndex getPageIndex(): This method returns the page index of this web-page. • Write a Java class MyHashTable that implements the hashtable used by the InvertedPageIndex. It maps a word to its word-entry.
– private int getHashIndex(String str): Create a hash function which maps a string to the index of its word-entry in the hashtable. The implementation of hashtable should support chaining. – void addPositionsForWord(WordEntry w): This adds an entry to the hashtable: stringName(w) − positionList(w). If no wordentry exists, then create a new word entry. However, if a wordentry exists, then merge w with the existing word-entry. • Write a Java class InvertedPageIndex which contains the following methods:
– void addPage(PageEntry p): Add a new page entry p to the inverted page index. – MySet – SearchEngine(): This is the constructor method. It should create an empty InvertedPageIndex. – void performAction(String actionMessage): This the main stub method that you have to implement. It takes an action as a string. The list of actions, and their format will be described later.
Actions:
6
• addPage x Add webpage x to the search engine database. The contents of the webpage are stored in a ﬁle named x in the webpages folder. • queryFindPagesWhichContainWord x Print the name of the webpages which contain the word x. The list of webpage names should be comma separated. If the word is not found in any webpage, then print “No webpage contains word x” • queryFindPositionsOfWordInAPage x y Print the word indice’s where the word x is found in the document y. The word indices should be separated by a comma. If the word x is not found in webpage y, then print “Webpage y does not contain word x”.
Points to note: • Convert each word to lowercase. • Do not store the connector words in the search engine. However, consider them when you calculate the word indice’s. Here is a list of connector words: { a, an, the, they, these, this, for, is, are, was, of, or, and, does, will, whose }. • Replace the punctuation marks with a space. Here is a list of punctuations: {} [ ] < = ( ) . , ; ’ ” ? # ! – : • Plural and singular form: Assume that these words are same: (stack, stacks), (structure, structures), (application, applications). • We have given you a set of connector words, punctuation marks, and singular-plural entries. Consider these list of words as exhaustive. You do not need to make any more exceptions in your code.
Assignment 5 [100 marks] Deadline: 11:55 PM, 19 October 2016
In this assignment, we will complete the implementation of our search engine.
• Implement the following method in the InvertedPageIndex class.
7
– MySet<PageEntrygetPagesWhichContainPhrase(String str[]): Return a set of page-entries for webpages which contain a sequence of non-connector words (str[0] str[1] … str[str.len-1]). Assume a webpage which contains the following text: “Data structures is the study of structures for storing data.” This webpage contains the phrases: “Data structures”, “Data structures study”, and “Data structures study structures”.
• Implement the collection of position entries for the WordEntry class as an AVL-tree which is a height-balanced binary search tree. The data item for each node in the the tree is a position entry, and the ordering of the nodes in the tree is on the basis of the word index in the position entry. For phrase queries, you must use the AVL tree to ﬁnd the next word. • Implement the following method in the PageEntry class. – float getRelevanceOfPage(String str[ ], boolean doTheseWordsRepresentAPhrase): Return the relevance of the webpage for a group of words represented by the array str[ ]. If the ﬂag doTheseWordsRepresentAPhrase is true, it means that the words represent a phrase; otherwise the words are part of a complex query (AND/OR). • Write a Java class SearchResult which represents a tuple – public SearchResult(PageEntry p, float r): Constructor method. – public PageEntry getPageEntry(): Return p. – public float getRelevance(): Return r. – public int compareTo(SearchResult otherObject): Gives the ordering between the current object and the otherObject. • Write a Java class MySort to sort a list of Comparable objects. It must contain one method:
8
– ArrayList Actions: • queryFindPagesWhichContainAllWords x1 x2 .. xn: Print the name of the webpages which contain all the words x1, x2, .. xn. The words are separated by a space. • queryFindPagesWhichContainAnyOfTheseWords x1 x2 .. xn: Print the name of the webpages which contain at least one word from this set { x1, x2, .. xn }. • queryFindPagesWhichContainPhrase x1 x2 .. xn: Print the name of the webpages which contain the phrase x1 x2 .. xn. • queryFindPositionsOfWordInAPage x y Print the word indice’s where the word x is found in the document y. The word indices should be separated by a comma. If the word x is not found in webpage y, then print “Webpage y does not contain word x”.
Points to note: • The search engine should print the name of all the webpages which satisfy the given criteria. The list of webpages should be displayed in a sorted order. • Assume that the input to the search engine does not contain any punctuation mark or a connector word. • Actions available for assignment 4 should also be included in assignment 5
