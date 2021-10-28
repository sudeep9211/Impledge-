Approach :

For example, if the input list is: ['cat', 'cats', 'catsdogcats', 'catxdogcatsrat', 'dog', 'dogcatsdog', 'hippopotamuses', 'rat', 'ratcat', 'ratcatdog', 'ratcatdogcat']. Then the longest compounded word is 'ratcatdogcat' with 12 letters.
The basic algorithm for searching for compound words is to iterate over the target words from longest to shortest and for each target word iterate over word list (again from longest to shortest) attempting to match if the target word "starts with" the match word.
 If the target word starts with the match word then recursively attempt to search the "tail" of the target word for matches. If any combination of words make up the target word it is considered a compound words and added to the result set and no longer processed (i.e. some of the words can be formed using different combinations of sub words, but for this exercise once a word is considered a compound word it doesn't matter or count if it can be formed multiple ways)
The datastructure we are going to use is Trie and Queue.
Let’s illustrate the process with an example, the first word is cat and we add it to the trie. Since it doesn’t have a prefix, we continue. Second word is cats, we add it to the trie and check whether it has a prefix, and yes it does, the word cat. So we append the pair <’cats’, ‘s’> to the queue, which is the current word and the suffix. The third word is catsdogcats, we again insert it to the trie and see that it has 2 prefixes, cat and cats. So we add 2 pairs <’catsdogcats’, ‘sdogcats’> and <’catsdogcats’, ‘dogcats’> where the former suffix correspond to the prefix cat and the latter to cats. We continue like this by adding <’catxdogcatsrat’, ‘xdogcatsrat’> to the queue and so on. And here’s the trie formed by adding example the words in the problem definition:
After building the trie and the queue, then we start processing the queue by popping a pair from the beginning. We check whether the suffix is a valid or compound word. If it’s a valid word and the original word is the longest up to now, we store the result. Otherwise we discard the pair. The suffix may be a compound word itself, so we check if the it has any prefixes. If it does, then we apply the above procedure by adding the original word and the new suffix to the queue. If the suffix of the original popped pair is neither a valid word nor has a prefix, we simply discard that pair.
