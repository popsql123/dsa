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

---
