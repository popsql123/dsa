<img width="1920" height="1080" alt="Screenshot 2026-03-11 140437" src="https://github.com/user-attachments/assets/7f54f7f7-0e5f-469c-94e6-02601a995aae" />




Below are **concise Java Collections Framework syntax revision notes** tailored for **DSA interviews (SDE-2 level)**.
Focus is on **syntax + commonly used methods + patterns used in coding interviews**.

---

# Java Collections Framework – Syntax Revision (DSA / SDE-2)

## 1. List Implementations

### ArrayList

**Use when:** fast random access, dynamic array

```java
List<Integer> list = new ArrayList<>();

// Add
list.add(10);
list.add(1, 20);     // insert at index
list.addAll(Arrays.asList(1,2,3));

// Access
int x = list.get(0);

// Update
list.set(0, 100);

// Remove
list.remove(0);              // by index
list.remove(Integer.valueOf(10)); // by value

// Size
int n = list.size();

// Iterate
for(int num : list) {}

for(int i = 0; i < list.size(); i++) {}

Iterator<Integer> it = list.iterator();
while(it.hasNext()) System.out.println(it.next());
```

**Complexity**

| Operation     | Time           |
| ------------- | -------------- |
| get           | O(1)           |
| add end       | O(1) amortized |
| insert middle | O(n)           |
| remove middle | O(n)           |

---

### LinkedList

**Use when:** frequent insertion/deletion

```java
LinkedList<Integer> list = new LinkedList<>();

list.addFirst(10);
list.addLast(20);

list.removeFirst();
list.removeLast();

list.getFirst();
list.getLast();
```

---

# 2. Stack

⚠️ Prefer **ArrayDeque instead of Stack**

### Using ArrayDeque as Stack

```java
Deque<Integer> stack = new ArrayDeque<>();

stack.push(10);
stack.push(20);

stack.pop();
stack.peek();
```

**Time:** O(1)

---

# 3. Queue

### Using LinkedList

```java
Queue<Integer> q = new LinkedList<>();

q.offer(10);
q.offer(20);

q.poll();
q.peek();
```

### Safe vs Exception Methods

| Safe    | Exception |
| ------- | --------- |
| offer() | add()     |
| poll()  | remove()  |
| peek()  | element() |

---

# 4. PriorityQueue (Heap)

### Min Heap (default)

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();

pq.offer(5);
pq.offer(1);
pq.offer(3);

pq.poll(); // smallest
pq.peek();
```

### Max Heap

```java
PriorityQueue<Integer> pq =
        new PriorityQueue<>(Comparator.reverseOrder());
```

### Custom Comparator

```java
PriorityQueue<int[]> pq =
        new PriorityQueue<>((a,b)->a[0]-b[0]);
```

**Complexity**

| Operation | Time     |
| --------- | -------- |
| insert    | O(log n) |
| remove    | O(log n) |
| peek      | O(1)     |

---

# 5. Deque (Double Ended Queue)

```java
Deque<Integer> dq = new ArrayDeque<>();

dq.offerFirst(1);
dq.offerLast(2);

dq.pollFirst();
dq.pollLast();

dq.peekFirst();
dq.peekLast();
```

**Used in:** Sliding window / monotonic queue problems.

---

# 6. Set Implementations

## HashSet

```java
Set<Integer> set = new HashSet<>();

set.add(10);
set.add(20);
set.contains(10);
set.remove(20);
```

**Properties**

* No duplicates
* No order

**Complexity:** O(1) average

---

## LinkedHashSet

```java
Set<Integer> set = new LinkedHashSet<>();
```

Maintains **insertion order**

---

## TreeSet

```java
Set<Integer> set = new TreeSet<>();

set.add(5);
set.add(1);
set.add(3);

System.out.println(set); // sorted
```

**Complexity:** O(log n)

---

# 7. Map Implementations

## HashMap

```java
Map<String,Integer> map = new HashMap<>();

map.put("a",1);
map.put("b",2);

map.get("a");
map.containsKey("a");

map.remove("a");

int size = map.size();
```

### Iteration

```java
for(Map.Entry<String,Integer> e : map.entrySet()){
    System.out.println(e.getKey()+" "+e.getValue());
}
```

or

```java
for(String key : map.keySet()){}
```

---

## TreeMap

```java
Map<Integer,String> map = new TreeMap<>();

map.put(3,"c");
map.put(1,"a");
map.put(2,"b");
```

Keys are **sorted**

**Time:** O(log n)

---

# 8. Arrays Utility (java.util.Arrays)

```java
int[] arr = {5,2,8,1};

Arrays.sort(arr);

Arrays.binarySearch(arr, 8);

Arrays.fill(arr, 0);

System.out.println(Arrays.toString(arr));

List<Integer> list = Arrays.asList(1,2,3);
```

---

# 9. Collections Utility

```java
Collections.sort(list);

Collections.sort(list, Comparator.reverseOrder());

Collections.reverse(list);

Collections.min(list);

Collections.max(list);

Collections.frequency(list, 2);

Collections.shuffle(list);
```

---

# 10. Comparator vs Comparable

### Comparable (inside class)

```java
class Student implements Comparable<Student>{
    int roll;

    public int compareTo(Student o){
        return this.roll - o.roll;
    }
}
```

### Comparator (outside class)

```java
Collections.sort(list, (a,b)->a.roll-b.roll);
```

---

# 11. StringBuilder

```java
StringBuilder sb = new StringBuilder();

sb.append("hello");
sb.append("world");

sb.reverse();

sb.toString();
```

---

# 12. Useful Interview Patterns

## Frequency Map

```java
Map<Integer,Integer> freq = new HashMap<>();

for(int num : arr){
    freq.put(num, freq.getOrDefault(num,0)+1);
}
```

---

## Top K Elements

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();

for(int num : arr){
    pq.offer(num);
    if(pq.size() > k)
        pq.poll();
}
```

---

## Sliding Window Maximum

```java
Deque<Integer> dq = new ArrayDeque<>();
```

(used for monotonic queue)

---

# 13. Time Complexity Quick Sheet

| Structure     | Insert   | Delete   | Search    |
| ------------- | -------- | -------- | --------- |
| ArrayList     | O(1)     | O(n)     | O(1)      |
| LinkedList    | O(1)     | O(1)     | O(n)      |
| HashSet       | O(1)     | O(1)     | O(1)      |
| TreeSet       | O(log n) | O(log n) | O(log n)  |
| HashMap       | O(1)     | O(1)     | O(1)      |
| TreeMap       | O(log n) | O(log n) | O(log n)  |
| PriorityQueue | O(log n) | O(log n) | O(1 peek) |

---

# 14. SDE-2 Interview Must-Know Tricks

1. `getOrDefault()` for frequency maps
2. `computeIfAbsent()` for grouping
3. `PriorityQueue` for **top K problems**
4. `Deque` for **monotonic queue**
5. `TreeMap` for **range queries**
6. `LinkedHashMap` for **LRU cache**








Below is a **concise SDE-2 Java Collections Interview Q&A sheet**.
Each answer is **structured for interviews**: *definition → key points → complexity/extra notes*.

---

# Java Collections Framework – Top Interview Q&A (SDE-2)

---

# 1. What is the Java Collections Framework?

**Answer**

Java Collections Framework (JCF) is a **set of interfaces, implementations, and algorithms** used to store and manipulate groups of objects.

**Components**

1. **Interfaces**

   * List
   * Set
   * Queue
   * Map

2. **Implementations**

   * ArrayList
   * HashSet
   * HashMap
   * TreeMap
   * PriorityQueue

3. **Algorithms**

   * Sorting
   * Searching
   * Shuffling

4. **Iterators**

   * Traverse collections

---

# 2. Difference between Collection and Collections

| Feature | Collection                  | Collections                     |
| ------- | --------------------------- | ------------------------------- |
| Type    | Interface                   | Utility class                   |
| Package | java.util                   | java.util                       |
| Purpose | Represents group of objects | Utility methods for collections |
| Example | List, Set                   | sort(), reverse(), min()        |

**Example**

```java
Collections.sort(list);
Collections.reverse(list);
```

---

# 3. Why is Map not part of Collection?

**Answer**

Map is separate because it stores **key-value pairs**, while Collection stores **only elements**.

**Key Difference**

```
Collection → [value]
Map → [key → value]
```

---

# 4. What is the difference between Iterable and Iterator?

| Feature | Iterable             | Iterator          |
| ------- | -------------------- | ----------------- |
| Purpose | Enables foreach loop | Iterates elements |
| Method  | iterator()           | hasNext(), next() |

**Example**

```java
Iterator<Integer> it = list.iterator();

while(it.hasNext()){
    System.out.println(it.next());
}
```

---

# 5. Difference between ArrayList and LinkedList

| Feature              | ArrayList     | LinkedList         |
| -------------------- | ------------- | ------------------ |
| Structure            | Dynamic array | Doubly linked list |
| Random access        | O(1)          | O(n)               |
| Insert/delete middle | O(n)          | O(1)               |
| Memory               | Less          | More               |

**Use case**

```
ArrayList → read-heavy
LinkedList → insert/delete-heavy
```

---

# 6. Why is ArrayDeque preferred over Stack?

**Answer**

Stack extends **Vector**, which is **synchronized and slower**.

ArrayDeque advantages:

* Not synchronized
* Faster operations
* Better memory locality

**Example**

```java
Deque<Integer> stack = new ArrayDeque<>();

stack.push(10);
stack.pop();
```

---

# 7. How does ArrayList grow internally?

**Answer**

When capacity is exceeded:

```
new capacity = old + (old / 2)
```

**Process**

1. Create new array
2. Copy elements
3. Replace old array

---

# 8. What are Fail-Fast and Fail-Safe iterators?

### Fail-Fast

* Throws `ConcurrentModificationException`
* Detects structural modification

Examples

```
ArrayList
HashMap
HashSet
```

### Fail-Safe

* Works on a **copy**
* No exception

Examples

```
CopyOnWriteArrayList
ConcurrentHashMap
```

---

# 9. Difference between HashSet, LinkedHashSet, TreeSet

| Feature    | HashSet | LinkedHashSet         | TreeSet        |
| ---------- | ------- | --------------------- | -------------- |
| Order      | None    | Insertion order       | Sorted         |
| Structure  | HashMap | HashMap + linked list | Red-Black tree |
| Complexity | O(1)    | O(1)                  | O(log n)       |

---

# 10. Why does HashSet not allow duplicates?

**Answer**

HashSet internally uses **HashMap**.

When inserting:

1. Compute `hashCode()`
2. Check bucket
3. Use `equals()` to verify duplicate

If duplicate found → insertion ignored.

---

# 11. What happens if equals() is overridden but hashCode() is not?

**Answer**

Hash-based collections break.

**Reason**

Objects may be equal but stored in **different hash buckets**.

Result:

```
HashSet may contain duplicates
HashMap lookups may fail
```

---

# 12. Difference between HashMap and TreeMap

| Feature    | HashMap    | TreeMap        |
| ---------- | ---------- | -------------- |
| Order      | None       | Sorted         |
| Structure  | Hash table | Red-Black tree |
| Complexity | O(1)       | O(log n)       |
| Null keys  | Allowed    | Not allowed    |

---

# 13. Difference between HashMap and Hashtable

| Feature        | HashMap | Hashtable   |
| -------------- | ------- | ----------- |
| Thread-safe    | No      | Yes         |
| Performance    | Faster  | Slower      |
| Null key/value | Allowed | Not allowed |
| Legacy         | No      | Yes         |

---

# 14. Why is HashMap not thread safe?

**Answer**

Multiple threads can modify buckets simultaneously.

Possible issues:

* Lost updates
* Data inconsistency
* Infinite loops during resizing (Java 7)

Solution:

```
ConcurrentHashMap
Collections.synchronizedMap()
```

---

# 15. Internal structure of HashMap (Java 8)

**Structure**

```
Array of buckets
       ↓
Linked List
       ↓
Red-Black Tree (if collisions > 8)
```

---

# 16. What is Treeification in HashMap?

When bucket size exceeds **8**, the linked list becomes a **Red-Black Tree**.

Benefits:

```
Search improves
O(n) → O(log n)
```

---

# 17. What is Load Factor?

**Definition**

Load factor determines **when resizing happens**.

Default:

```
0.75
```

Resize condition:

```
size > capacity × load factor
```

---

# 18. Difference between put() and putIfAbsent()

### put()

```
Always inserts
Overwrites existing value
```

### putIfAbsent()

```
Only inserts if key is absent
```

---

# 19. How does PriorityQueue work internally?

**Answer**

PriorityQueue is implemented using a **binary heap**.

Properties:

* Min heap by default
* Stored in array

Complexities

```
insert → O(log n)
remove → O(log n)
peek → O(1)
```

---

# 20. Why does PriorityQueue print unsorted elements?

Heap property guarantees:

```
Root is min/max
```

But rest of elements **are not sorted**.

---

# 21. What is ConcurrentHashMap?

Thread-safe alternative to HashMap.

Java 8 features:

* CAS operations
* synchronized buckets
* high concurrency

---

# 22. Difference between synchronizedMap and ConcurrentHashMap

| Feature     | synchronizedMap | ConcurrentHashMap |
| ----------- | --------------- | ----------------- |
| Locking     | Entire map      | Segment level     |
| Concurrency | Low             | High              |
| Performance | Slower          | Faster            |

---

# 23. What is CopyOnWriteArrayList?

Thread-safe list.

Mechanism:

```
Write → copy entire array
Read → no lock
```

Use case:

```
Read-heavy applications
```

---

# 24. Difference between Comparable and Comparator

| Feature  | Comparable   | Comparator     |
| -------- | ------------ | -------------- |
| Location | Inside class | External       |
| Method   | compareTo()  | compare()      |
| Sorting  | Single rule  | Multiple rules |

---

# 25. How does Collections.sort() work internally?

Java uses **TimSort**.

TimSort is a hybrid of:

```
Merge Sort
Insertion Sort
```

Complexity:

```
O(n log n)
```

---

# Quick Revision (Most Important Topics)

For **SDE-2 interviews focus on explaining internals of:**

```
HashMap
ConcurrentHashMap
ArrayList resizing
PriorityQueue heap
TreeMap red-black tree
```

Below are **20 very common SDE-2 coding interview problems where Java Collections are central to the solution**.
For each problem I include:

* **Problem**
* **Key collection(s) used**
* **Core idea**
* **Interview hint**

This format helps you **recognize patterns quickly during interviews**.

---

# Top 20 Java Collections Coding Questions (SDE-2)

---

# 1. Two Sum

**Problem**

Given an array, return indices of two numbers whose sum equals target.

**Collections Used**

* `HashMap`

**Core Idea**

Store `value → index`.

Check if `target - num` exists.

**Pattern**

```text
HashMap lookup O(1)
```

---

# 2. Group Anagrams

**Problem**

Group words that are anagrams.

**Collections Used**

* `HashMap`
* `ArrayList`

**Core Idea**

Sorted word → list of anagrams.

```text
key = sorted(word)
value = list of words
```

---

# 3. Top K Frequent Elements

**Problem**

Find K most frequent numbers.

**Collections Used**

* `HashMap`
* `PriorityQueue`

**Core Idea**

1. Count frequency
2. Maintain min heap of size K

---

# 4. LRU Cache

**Problem**

Design LRU cache with O(1) operations.

**Collections Used**

* `LinkedHashMap`
* `HashMap + Doubly Linked List`

**Core Idea**

Maintain insertion order with eviction.

---

# 5. Sliding Window Maximum

**Problem**

Find max in every window of size k.

**Collections Used**

* `Deque`

**Core Idea**

Maintain **monotonic decreasing deque**.

---

# 6. Merge Intervals

**Problem**

Merge overlapping intervals.

**Collections Used**

* `ArrayList`
* `Collections.sort()`

**Core Idea**

Sort by start time then merge.

---

# 7. K Closest Points to Origin

**Problem**

Return K closest points.

**Collections Used**

* `PriorityQueue`

**Core Idea**

Max heap of size K.

---

# 8. Subarray Sum Equals K

**Problem**

Count subarrays with sum = K.

**Collections Used**

* `HashMap`

**Core Idea**

Prefix sum frequency.

---

# 9. Find Duplicate Elements

**Problem**

Find duplicates in array.

**Collections Used**

* `HashSet`

**Core Idea**

If `set.add()` returns false → duplicate.

---

# 10. Intersection of Two Arrays

**Problem**

Find common elements.

**Collections Used**

* `HashSet`

**Core Idea**

Store elements of first array.

Check second array membership.

---

# 11. Design HashMap

**Problem**

Implement HashMap from scratch.

**Collections Concepts Tested**

* hashing
* collision handling
* buckets

---

# 12. Kth Largest Element

**Problem**

Find kth largest number.

**Collections Used**

* `PriorityQueue`

**Core Idea**

Min heap of size K.

---

# 13. Course Schedule (Topological Sort)

**Problem**

Detect if course schedule is possible.

**Collections Used**

* `HashMap`
* `Queue`

**Core Idea**

Kahn’s algorithm using queue.

---

# 14. Clone Graph

**Problem**

Clone graph nodes.

**Collections Used**

* `HashMap`
* `Queue`

**Core Idea**

Map original node → cloned node.

---

# 15. Word Frequency Counter

**Problem**

Find most frequent word.

**Collections Used**

* `HashMap`

**Core Idea**

Frequency map.

---

# 16. First Non-Repeating Character

**Problem**

Return first non repeating character.

**Collections Used**

* `LinkedHashMap`

**Core Idea**

Maintain insertion order.

---

# 17. Reorganize String

**Problem**

Rearrange string so no adjacent chars equal.

**Collections Used**

* `PriorityQueue`
* `HashMap`

**Core Idea**

Max heap of characters by frequency.

---

# 18. Find Median from Data Stream

**Problem**

Maintain median of stream.

**Collections Used**

* `PriorityQueue`

**Core Idea**

Two heaps

```text
max heap → left side
min heap → right side
```

---

# 19. Employee Free Time

**Problem**

Find free intervals.

**Collections Used**

* `PriorityQueue`
* `ArrayList`

**Core Idea**

Merge sorted intervals using heap.

---

# 20. K Frequent Words

**Problem**

Return top k frequent words.

**Collections Used**

* `HashMap`
* `PriorityQueue`

**Core Idea**

Heap sorted by

```text
frequency desc
word lexicographically
```

---

# Most Important Java Collections Patterns

These **patterns cover ~70-80% of problems**.

| Pattern             | Collection    |
| ------------------- | ------------- |
| Frequency count     | HashMap       |
| Duplicate detection | HashSet       |
| Top K problems      | PriorityQueue |
| Sliding window      | Deque         |
| Ordered map         | TreeMap       |
| LRU cache           | LinkedHashMap |

---

# Most Important Collections to Master for SDE-2

```text
HashMap
HashSet
PriorityQueue
Deque
TreeMap
LinkedHashMap
ArrayList
```

Below are **20 tricky Java Collections interview traps** that frequently appear in **SDE-2 interviews**.
Each includes:

* **Trap question**
* **Expected answer**
* **Why candidates get confused**

These are the kinds of questions interviewers use to check **deep understanding of Java Collections internals**.

---

# Top 20 Tricky Java Collections Interview Traps

---

# 1. Why does HashSet allow only unique elements?

**Answer**

HashSet internally uses **HashMap**.

When inserting:

1. `hashCode()` determines bucket
2. `equals()` checks duplicates

If both match → element rejected.

**Trap**

Candidates often say **HashSet checks equals only**, which is incomplete.

---

# 2. What happens if equals() is overridden but hashCode() is not?

**Answer**

Objects may go into **different hash buckets**, causing duplicates.

Example issue:

```text
HashSet may contain logically equal objects
```

**Rule**

```
If equals() is overridden → hashCode() must also be overridden
```

---

# 3. Can HashMap have null keys?

**Answer**

Yes.

```
1 null key
multiple null values
```

**Reason**

Null key always stored in **bucket 0**.

---

# 4. Why does TreeMap not allow null keys?

**Answer**

TreeMap uses **comparisons (compareTo / Comparator)**.

Null cannot be compared → throws **NullPointerException**.

---

# 5. Why does PriorityQueue print unsorted values?

Example:

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.add(5);
pq.add(1);
pq.add(10);

System.out.println(pq);
```

Output may be:

```
[1,5,10] or [1,10,5]
```

**Answer**

PriorityQueue is a **heap**, not a sorted structure.

Only guarantee:

```
peek() returns smallest element
```

---

# 6. Why is ArrayDeque preferred over Stack?

**Answer**

Stack extends **Vector**, which is:

* synchronized
* slower

ArrayDeque:

* faster
* non-synchronized
* better cache locality

---

# 7. Why does ConcurrentModificationException occur?

Example:

```java
for(Integer i : list){
    list.remove(i);
}
```

**Answer**

Collection modified during iteration.

Iterator is **fail-fast**.

Solution:

```
Use iterator.remove()
```

---

# 8. Difference between fail-fast and fail-safe iterator

| Type      | Behavior                               |
| --------- | -------------------------------------- |
| Fail-fast | Throws ConcurrentModificationException |
| Fail-safe | Iterates over copy                     |

Examples

```
ArrayList → fail-fast
CopyOnWriteArrayList → fail-safe
```

---

# 9. Why does HashMap become slow with many collisions?

Before Java 8:

```
Linked list per bucket
O(n)
```

Java 8 improvement:

```
Red-Black Tree
O(log n)
```

---

# 10. What is Treeification in HashMap?

When bucket size exceeds **8**, linked list converts to **Red-Black Tree**.

Improvement:

```
O(n) → O(log n)
```

---

# 11. Why is HashMap not thread safe?

Multiple threads modifying buckets simultaneously can cause:

```
data corruption
infinite loops (Java 7)
lost updates
```

Use:

```
ConcurrentHashMap
```

---

# 12. Why does Collections.sort() sometimes perform faster than expected?

Because Java uses **TimSort**, a hybrid algorithm:

```
Merge Sort + Insertion Sort
```

Optimized for **partially sorted data**.

---

# 13. Why does Arrays.asList() not allow add/remove?

Example:

```java
List<Integer> list = Arrays.asList(1,2,3);
list.add(4); // exception
```

**Answer**

Returns **fixed-size list backed by array**.

Unsupported operations:

```
add()
remove()
```

---

# 14. Why does modifying key after inserting into HashMap break retrieval?

Example:

```
Map<Key,Value>
```

If key fields change → `hashCode()` changes.

Result:

```
object stored in wrong bucket
lookup fails
```

---

# 15. Difference between HashMap and LinkedHashMap

| Feature   | HashMap    | LinkedHashMap                   |
| --------- | ---------- | ------------------------------- |
| Ordering  | None       | Insertion order                 |
| Structure | Hash table | Hash table + doubly linked list |

Used in:

```
LRU Cache
```

---

# 16. Why is TreeSet slower than HashSet?

TreeSet uses **Red-Black Tree**.

Complexity:

```
O(log n)
```

HashSet uses hashing:

```
O(1)
```

---

# 17. Why does PriorityQueue remove smallest element first?

Default implementation is **Min Heap**.

To get max heap:

```java
new PriorityQueue<>(Comparator.reverseOrder());
```

---

# 18. Why is HashMap resizing expensive?

When resizing occurs:

1. new bucket array created
2. all entries rehashed
3. elements redistributed

Cost:

```
O(n)
```

---

# 19. Why does CopyOnWriteArrayList perform poorly on writes?

Because every write operation:

```
creates new array copy
```

Good for:

```
read-heavy systems
```

---

# 20. Why should mutable objects not be used as HashMap keys?

Because changing fields affects:

```
hashCode()
equals()
```

Result:

```
map cannot find key anymore
```

---

# The 6 Most Dangerous Java Collections Interview Traps

These appear **very often in SDE-2 interviews**.

```
1 HashMap internal working
2 equals vs hashCode contract
3 PriorityQueue heap behavior
4 Arrays.asList fixed list
5 ConcurrentModificationException
6 mutable keys in HashMap
```

Below are **15 output-based Java Collections interview puzzles**.
These are **classic traps used in SDE-2 / FAANG interviews**. Try to **predict the output first** before reading the explanation.

---

# 1. HashSet Duplicate Trap

```java
Set<Integer> set = new HashSet<>();

set.add(10);
set.add(10);
set.add(new Integer(10));

System.out.println(set.size());
```

### Output

```
1
```

### Why

HashSet uses **hashCode + equals**, so duplicates are ignored.

---

# 2. Arrays.asList Trap

```java
List<Integer> list = Arrays.asList(1,2,3);
list.add(4);

System.out.println(list);
```

### Output

```
UnsupportedOperationException
```

### Why

`Arrays.asList()` returns **fixed-size list backed by array**.

---

# 3. PriorityQueue Ordering Trap

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();

pq.add(5);
pq.add(1);
pq.add(10);

System.out.println(pq);
```

### Possible Output

```
[1, 5, 10]
or
[1, 10, 5]
```

### Why

PriorityQueue is a **heap**, not sorted.

Only guarantee:

```
peek() → smallest element
```

---

# 4. HashMap Null Key Trap

```java
Map<String,Integer> map = new HashMap<>();

map.put(null,1);
map.put(null,2);

System.out.println(map.size());
System.out.println(map.get(null));
```

### Output

```
1
2
```

### Why

HashMap allows **only one null key**.

---

# 5. TreeMap Null Key Trap

```java
Map<String,Integer> map = new TreeMap<>();

map.put(null,1);
```

### Output

```
NullPointerException
```

### Why

TreeMap requires **comparable keys**.

---

# 6. Iterator Modification Trap

```java
List<Integer> list = new ArrayList<>();

list.add(1);
list.add(2);

for(Integer i : list){
    list.remove(i);
}
```

### Output

```
ConcurrentModificationException
```

### Why

Fail-fast iterator detects modification.

---

# 7. LinkedHashSet Order Trap

```java
Set<Integer> set = new LinkedHashSet<>();

set.add(5);
set.add(2);
set.add(10);

System.out.println(set);
```

### Output

```
[5, 2, 10]
```

### Why

LinkedHashSet preserves **insertion order**.

---

# 8. TreeSet Sorting Trap

```java
Set<Integer> set = new TreeSet<>();

set.add(5);
set.add(1);
set.add(10);

System.out.println(set);
```

### Output

```
[1, 5, 10]
```

### Why

TreeSet maintains **sorted order**.

---

# 9. Remove by Index vs Value Trap

```java
List<Integer> list = new ArrayList<>();

list.add(10);
list.add(20);
list.add(30);

list.remove(1);

System.out.println(list);
```

### Output

```
[10, 30]
```

### Why

`remove(int)` removes **index**, not value.

---

# 10. HashMap Overwrite Trap

```java
Map<Integer,String> map = new HashMap<>();

map.put(1,"A");
map.put(1,"B");

System.out.println(map.size());
```

### Output

```
1
```

### Why

Duplicate keys **overwrite values**.

---

# 11. PriorityQueue Poll Trap

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();

pq.add(3);
pq.add(1);
pq.add(2);

while(!pq.isEmpty()){
    System.out.print(pq.poll() + " ");
}
```

### Output

```
1 2 3
```

### Why

Polling returns elements in **heap order**.

---

# 12. HashSet Mutable Key Trap

```java
class Key{
    int id;
}

Set<Key> set = new HashSet<>();

Key k = new Key();
k.id = 1;

set.add(k);

k.id = 2;

System.out.println(set.contains(k));
```

### Output

```
false (possible)
```

### Why

Changing fields changes **hashCode bucket lookup**.

---

# 13. CopyOnWriteArrayList Trap

```java
List<Integer> list = new CopyOnWriteArrayList<>();

list.add(1);
list.add(2);

for(Integer i : list){
    list.add(3);
}

System.out.println(list);
```

### Output

```
[1, 2, 3, 3]
```

### Why

Iterator works on **snapshot copy**.

---

# 14. HashMap Iteration Order Trap

```java
Map<Integer,String> map = new HashMap<>();

map.put(3,"C");
map.put(1,"A");
map.put(2,"B");

System.out.println(map);
```

### Output

```
Order NOT guaranteed
```

Possible:

```
{1=A, 2=B, 3=C}
```

or any order.

---

# 15. Collections.sort Trap

```java
List<Integer> list = Arrays.asList(5,2,8);

Collections.sort(list);

System.out.println(list);
```

### Output

```
[2, 5, 8]
```

### Why

`Collections.sort()` uses **TimSort**.

---

# The 6 Most Important Output Questions Interviewers Love

Memorize these:

```
Arrays.asList() modification
HashMap null key behavior
PriorityQueue order
remove(index) vs remove(object)
ConcurrentModificationException
HashSet duplicate behavior
```


---
