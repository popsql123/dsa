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

