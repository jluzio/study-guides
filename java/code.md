# String.format
~~~
%[argument_index$][flags][width][.precision]conversion
- argument_index: position of the argument in the argument list (starts with 1)
- flags: set of characters that modify the output (depends on the conversion)
- width: positive integer indicating the minimum number of characters to be written to the output
- precision: non-negative integer used to restrict the number of characters
- conversion: character indicating how the argument should be formatted
  - b: boolean
  - h: hex string
  - x: hex int
  - c: char
  - s: toString or implemented Formattable.formatTo
  - d: decimal int
  - o: oct int
  - e: scientific notation
  - f: floating point number
  - t: date/time
  - n: line separator
~~~

# Pattern
- +: 1+
- *: 0+
- ?: 0 or 1
- ^: start
- $: end
- X{n}: x exacly n times
- X{n,m}: x n to m times
- \<class>: class of values
  - d: digit
  - D: non-digit
  - s: whitespace char
  - S: non-whitespace char
  - w: word char
  - W
  - t: tab
  - n: new line
- [abc]: a, b or c
- [^abc]: not a, not b and not c
- [a-z]: range
- [a-z&&[def]]: union
- [a-d[m-p]]: or. equals to [a-dm-p]

# ArrayList vs LinkedList
Key Difference Between ArrayList vs LinkedList ArrayList uses an array, which allows for fast random access but slow insertion and deletion. While LinkedList uses a doubly linked list, which allows for fast insertion and deletion but slow random access. Also one of the major difference lies in the access time.

# LinkedHashSet vs HashSet
Difference between HashSet and LinkedHashSet HashSet is an unordered & unsorted collection of the data set, whereas the LinkedHashSet is an ordered and sorted collection of HashSet. HashSet does not provide any method to maintain the insertion order.

# List vs Set
In Java, a set is a collection that does not allow duplicate elements and has no guaranteed order for its elements. In Java, when comparing “list vs set” a list supports ordered collections and allows duplicates, whereas a set emphasizes uniqueness without any specific order.

# Matrix multiply
~~~
[1 2 3] x [10 11] = [1*10+2*20+3*30  1*11+2*21+3*31]
[4 5 6]   [20 21]   [4*10+5*20+6*30  4*11+5*21+6*31]
          [30 31]
~~~
