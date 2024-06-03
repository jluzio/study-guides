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

# DateTimeFormatter pattern
- G: era (text / e.g.: AD; Anno Domini; A)
- u: year (year / e.g.: 2004; 04)
- y: year-of-era (year / e.g.: 2004; 04)
- D: day-of-year (number / e.g.: 189)
- M/L: month-of-year (number/ text / e.g.: 7; 07; Jul; July; J)
- d: day-of-month (number / e.g.: 10)
- g: modified-julian-day (number / e.g.: 2451334)
- Q/q: quarter-of-year (number/ text / e.g.: 3; 03; Q3; 3rd quarter)
- Y: week-based-year (year / e.g.: 1996; 96)
- w: week-of-week-based-year (number / e.g.: 27)
- W: week-of-month (number / e.g.: 4)
- E: day-of-week (text / e.g.: Tue; Tuesday; T)
- e/c: localized day-of-week (number/ text / e.g.: 2; 02; Tue; Tuesday; T)
- F: aligned-week-of-month (number / e.g.: 3)
- a: am-pm-of-day (text / e.g.: PM)
- B: period-of-day (text / e.g.: in the morning)
- h: clock-hour-of-am-pm (1-12) (number / e.g.: 12)
- K: hour-of-am-pm (0-11) (number / e.g.: 0)
- k: clock-hour-of-day (1-24) (number / e.g.: 24)
- H: hour-of-day (0-23) (number / e.g.: 0)
- m: minute-of-hour (number / e.g.: 30)
- s: second-of-minute (number / e.g.: 55)
- S: fraction-of-second (fraction / e.g.: 978)
- A: milli-of-day (number / e.g.: 1234)
- n: nano-of-second (number / e.g.: 987654321)
- N: nano-of-day (number / e.g.: 1234000000)
- V: time-zone ID (zone-id / e.g.: America/ Los_Angeles; Z; -08:30)
- v: generic time-zone name (zone-name / e.g.: Pacific Time; PT)
- z: time-zone name (zone-name / e.g.: Pacific Standard Time; PST)
- O: localized zone-offset (offset-O / e.g.: GMT+8; GMT+08:00; UTC-08:00)
- X: zone-offset 'Z' for zero (offset-X / e.g.: Z; -08; -0830; -08:30; -083015; -08:30:15)
- x: zone-offset (offset-x / e.g.: +0000; -08; -0830; -08:30; -083015; -08:30:15)
- Z: zone-offset (offset-Z / e.g.: +0000; -0800; -08:00)
- p: pad next (pad modifier / e.g.: 1)
- ': escape for text
- '': single quote

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
