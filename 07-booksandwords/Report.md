#### Question 1. What is your hash function like for hash table solution (if you implemented hash table) ：

    private int hashCode(K key) {
        int hash = 0;
        String keyString = key.toString();
            for (int i = 0; i < keyString.length(); i++) {
            hash = 31 * hash + keyString.charAt(i);
        }
        return hash;
    }

#### Question 2. For binary search trees (if you implemented it), how does your implementation get the top-100 list? :

First, call the toSortedArray() method in KeyValueBSearchTree to sort the binary tree in ascending order, then call the reverse() method to reverse it,

    sorted = words.toSortedArray();
    Algorithms.reverse(sorted);

and the first 100 elements are the ones required for printing. So print out them
    
    for (int index = 0; index < 100 && index<sorted.length; index++) {
        String word = String.format("%-20s",sorted[index].getKey()).replace(' ', '.');
        System.out.format("%4d. %s %6d%n", index + 1, word, sorted[index].getValue());
    }

#### Question 3. What can you say about the correctness of your implementation? Any issues, bugs or problems you couldn't solve? Any idea why the problem persists and what could perhaps be the solution? :

In this exercise, I encountered two issues:

The first issue was that we initially set the specific word as the key of the Pair instance, and the occurrence count as the value of the Pair instance. Since this assignment required outputting the top 100 most frequent words, it was necessary to compare the values of each Pair instance for sorting. Previously, the key in Pair inherited from Comparable, so it was necessary to change a series of implementations and interfaces to make the value inherit from Comparable, allowing for comparison.

The second issue was with the implementation of the hash table. I discovered that it was running very slowly during the initial execution, taking about 3-4 minutes. Later, I found that the problem was with the getIndexByHC() called in the find method. After calculating the hash value, it failed to check whether the index was already occupied, leading to the program automatically traversing the entire hash table once if no value was found at that position, causing a significant time loss. Furthermore, I also improved the quicksort algorithm by using Hoare's version of quicksort to speed up the execution.

#### Question 4. What can you say about the time complexity of your implementation? How efficient is the code in reading and managing the words and their counts? How efficient is your code in getting the top-100 list? Which sorting algorithm are you using? What is the time complexity of that algorithm? :

 Efficiently manage word counts, with the average case for insert and search operations being O(1) both for hashTableImplementation and BSTImplementation.The sorting of words to retrieve the top-100 list implies a time complexity that likely averages O(n log n). I use the hoare quick sort

#### Question 5. What did you find the most difficult things to understand and implement in this programming task? Why?:

In my opinion, the most challenging part consists of two aspects. The first part was initially understanding the code, where `countUniqueWords()` was the main method undergoing changes. I needed to carefully study this method, and its call to `addToWords()` method, which is the core of the code. After delving deeper, I also had to make judgments on how to implement the specific addition operations, especially considering what data specifically corresponds to the key and value in Pair, which required careful thought. Then, when checking for issues, I found that the implementation of the hash table was very slow. This problem troubled me for several days. By carefully examining the runtime of each method through profiling features, I finally pinpointed that the issue was with `KeyValueHashTable`, and eventually, I resolved this problem. These two aspects were, in my view, the most challenging parts of this exercise.

#### Question 6. What did you learn doing this? :

I needed to use some tools to investigate where my code had issues on my own, such as using profiling to observe the runtime of different parts. This process led to a deeper understanding of hash tables and binary search trees. At the same time, I also learned a new quicksort algorithm.