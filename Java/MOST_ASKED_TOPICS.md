# Most Asked Java Interview Topics with Coding Examples

> Focus on these topics for maximum interview readiness (~5 years experience level)

---

## 1. Collections Framework (VERY COMMON)

### HashMap vs HashSet vs TreeMap

**Interview Question:** "Explain HashMap internals and when to use HashMap vs TreeSet?"

```java
// HashMap - key-value pairs, O(1) average lookup, unordered
HashMap<String, Integer> map = new HashMap<>();
map.put("apple", 5);
map.put("banana", 3);
System.out.println(map.get("apple")); // 5

// HashSet - unique elements only, no duplicates, O(1) lookup
HashSet<String> set = new HashSet<>();
set.add("apple");
set.add("apple"); // ignored, no duplicates
System.out.println(set.size()); // 1

// TreeMap - sorted by key, O(log n) lookup
TreeMap<String, Integer> treeMap = new TreeMap<>();
treeMap.put("banana", 3);
treeMap.put("apple", 5);
for (String key : treeMap.keySet()) {
    System.out.println(key); // apple, banana (sorted order)
}
```

### Find Duplicate Elements

**Interview Question:** "Find all duplicates in an array efficiently."

```java
public class FindDuplicates {
    // Approach 1: Using HashSet - O(n) time, O(n) space
    public static void findDuplicatesHashSet(int[] numbers) {
        Set<Integer> seen = new HashSet<>();
        for (int n : numbers) {
            if (!seen.add(n)) {
                System.out.println("Duplicate: " + n);
            }
        }
    }
    
    // Approach 2: Using Streams - O(n) time, O(n) space
    public static void findDuplicatesStream(int[] numbers) {
        Set<Integer> seen = new HashSet<>();
        Arrays.stream(numbers)
            .filter(n -> !seen.add(n))
            .distinct()
            .forEach(n -> System.out.println("Duplicate: " + n));
    }
    
    // Approach 3: Using HashMap with count - returns frequency
    public static Map<Integer, Integer> countDuplicates(int[] numbers) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int n : numbers) {
            map.put(n, map.getOrDefault(n, 0) + 1);
        }
        return map;
    }
}
```

### ArrayList vs LinkedList Performance

**Interview Question:** "When would you use ArrayList vs LinkedList?"

```java
public class ListPerformance {
    public static void main(String[] args) {
        ArrayList<Integer> arrayList = new ArrayList<>();
        LinkedList<Integer> linkedList = new LinkedList<>();
        
        // ArrayList: O(1) random access, O(n) insertion/deletion in middle
        arrayList.add(1);      // O(1) amortized
        arrayList.get(0);      // O(1) fast
        arrayList.add(0, 100); // O(n) slow if many elements
        
        // LinkedList: O(n) random access, O(1) insertion/deletion at ends
        linkedList.add(1);        // O(1)
        linkedList.get(0);        // O(n) slow
        linkedList.addFirst(100); // O(1) fast
        linkedList.remove();      // O(1) fast
    }
}
```

---

## 2. String & String Operations (VERY COMMON)

### String Reversal Variations

**Interview Question:** "Reverse a string in different ways."

```java
public class StringReversal {
    // Approach 1: Using StringBuilder - MOST COMMON
    public static String reverseUsingStringBuilder(String s) {
        return new StringBuilder(s).reverse().toString();
    }
    
    // Approach 2: Character array - efficient for interviews
    public static String reverseUsingCharArray(String s) {
        char[] chars = s.toCharArray();
        int left = 0, right = chars.length - 1;
        while (left < right) {
            char temp = chars[left];
            chars[left] = chars[right];
            chars[right] = temp;
            left++;
            right--;
        }
        return new String(chars);
    }
    
    // Approach 3: Recursion
    public static String reverseRecursive(String s) {
        if (s.isEmpty()) return s;
        return reverseRecursive(s.substring(1)) + s.charAt(0);
    }
}
```

### Check Palindrome

**Interview Question:** "Check if a string is a palindrome (ignoring spaces/case)."

```java
public class PalindromeCheck {
    // Approach 1: Two pointers - O(n) time, O(1) space
    public static boolean isPalindrome(String s) {
        String clean = s.replaceAll("[^a-zA-Z0-9]", "").toLowerCase();
        int left = 0, right = clean.length() - 1;
        while (left < right) {
            if (clean.charAt(left) != clean.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
    
    // Approach 2: Using StringBuilder
    public static boolean isPalindromeBuilder(String s) {
        String clean = s.replaceAll("[^a-zA-Z0-9]", "").toLowerCase();
        return clean.equals(new StringBuilder(clean).reverse().toString());
    }
}
```

---

## 3. Linked List Operations (COMMON IN CODING ROUNDS)

### Reverse a Linked List

**Interview Question:** "Reverse a linked list iteratively and recursively."

```java
public class Node {
    int data;
    Node next;
    Node(int data) { this.data = data; }
}

public class LinkedListReversal {
    // Approach 1: Iterative - PREFERRED
    public static Node reverseIterative(Node head) {
        Node prev = null;
        Node current = head;
        while (current != null) {
            Node next = current.next;
            current.next = prev;
            prev = current;
            current = next;
        }
        return prev;
    }
    
    // Approach 2: Recursive
    public static Node reverseRecursive(Node head) {
        if (head == null || head.next == null) return head;
        Node newHead = reverseRecursive(head.next);
        head.next.next = head;
        head.next = null;
        return newHead;
    }
    
    // Print list
    public static void printList(Node head) {
        while (head != null) {
            System.out.print(head.data + " -> ");
            head = head.next;
        }
        System.out.println("null");
    }
}
```

### Detect Cycle in Linked List (Floyd's Algorithm)

**Interview Question:** "How to detect if a linked list has a cycle?"

```java
public class CycleDetection {
    // Floyd's Cycle Detection Algorithm (Tortoise & Hare)
    public static boolean hasCycle(Node head) {
        if (head == null || head.next == null) return false;
        
        Node slow = head;
        Node fast = head;
        
        while (fast != null && fast.next != null) {
            slow = slow.next;           // move 1 step
            fast = fast.next.next;       // move 2 steps
            
            if (slow == fast) {
                return true; // cycle found
            }
        }
        return false; // no cycle
    }
    
    // Find cycle start node
    public static Node findCycleStart(Node head) {
        if (head == null) return null;
        
        Node slow = head, fast = head;
        
        // Find meeting point
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) break;
        }
        
        if (fast == null || fast.next == null) return null;
        
        // Find cycle start
        slow = head;
        while (slow != fast) {
            slow = slow.next;
            fast = fast.next;
        }
        return slow;
    }
}
```

### Merge Two Sorted Linked Lists

**Interview Question:** "Merge two sorted linked lists into one sorted list."

```java
public class MergeSortedLists {
    public static Node merge(Node l1, Node l2) {
        Node dummy = new Node(0);
        Node current = dummy;
        
        while (l1 != null && l2 != null) {
            if (l1.data <= l2.data) {
                current.next = l1;
                l1 = l1.next;
            } else {
                current.next = l2;
                l2 = l2.next;
            }
            current = current.next;
        }
        
        // Attach remaining nodes
        current.next = (l1 != null) ? l1 : l2;
        
        return dummy.next;
    }
}
```

---

## 4. Concurrency & Threading (COMMON)

### Thread-Safe Singleton (Double-Checked Locking)

**Interview Question:** "How to create a thread-safe singleton?"

```java
// BEST: Enum-based (thread-safe by default)
public enum SingletonEnum {
    INSTANCE;
    
    private String config;
    
    public void setConfig(String config) {
        this.config = config;
    }
}

// GOOD: Double-checked locking
public class DCLSingleton {
    private static volatile DCLSingleton instance;
    
    private DCLSingleton() {}
    
    public static DCLSingleton getInstance() {
        if (instance == null) {
            synchronized (DCLSingleton.class) {
                if (instance == null) {
                    instance = new DCLSingleton();
                }
            }
        }
        return instance;
    }
}

// Usage
SingletonEnum singleton = SingletonEnum.INSTANCE;
```

### Producer-Consumer Problem

**Interview Question:** "Implement producer-consumer using BlockingQueue."

```java
import java.util.concurrent.*;

public class ProducerConsumer {
    static class Producer implements Runnable {
        private BlockingQueue<String> queue;
        
        Producer(BlockingQueue<String> queue) {
            this.queue = queue;
        }
        
        @Override
        public void run() {
            try {
                for (int i = 0; i < 5; i++) {
                    String item = "Item-" + i;
                    queue.put(item);
                    System.out.println("Produced: " + item);
                    Thread.sleep(500);
                }
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        }
    }
    
    static class Consumer implements Runnable {
        private BlockingQueue<String> queue;
        
        Consumer(BlockingQueue<String> queue) {
            this.queue = queue;
        }
        
        @Override
        public void run() {
            try {
                while (true) {
                    String item = queue.take();
                    System.out.println("Consumed: " + item);
                    Thread.sleep(1000);
                }
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        }
    }
    
    public static void main(String[] args) {
        BlockingQueue<String> queue = new LinkedBlockingQueue<>(10);
        
        new Thread(new Producer(queue)).start();
        new Thread(new Consumer(queue)).start();
    }
}
```

### CompletableFuture (Async Programming)

**Interview Question:** "How to work with CompletableFuture for async operations?"

```java
import java.util.concurrent.*;

public class CompletableFutureExample {
    public static void main(String[] args) throws Exception {
        ExecutorService executor = Executors.newFixedThreadPool(2);
        
        // Example 1: Simple async computation
        CompletableFuture<Integer> future = CompletableFuture
            .supplyAsync(() -> {
                System.out.println("Computing...");
                return 42;
            }, executor)
            .thenApply(n -> n * 2)        // Transform result
            .thenApply(n -> n + 1);       // Chain operations
        
        System.out.println("Result: " + future.get()); // 85
        
        // Example 2: Combining multiple futures
        CompletableFuture<String> future1 = CompletableFuture
            .supplyAsync(() -> "Hello", executor);
        
        CompletableFuture<String> future2 = CompletableFuture
            .supplyAsync(() -> "World", executor);
        
        CompletableFuture<String> combined = future1
            .thenCombine(future2, (s1, s2) -> s1 + " " + s2);
        
        System.out.println(combined.get()); // Hello World
        
        executor.shutdown();
    }
}
```

---

## 5. Java 8+ Features (VERY COMMON)

### Lambda & Streams

**Interview Question:** "Explain Lambda expressions and Streams with examples."

```java
import java.util.*;
import java.util.stream.*;

public class LambdaAndStreams {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
        
        // Example 1: Filter + map + collect
        List<Integer> evenSquares = numbers.stream()
            .filter(n -> n % 2 == 0)           // Keep only even
            .map(n -> n * n)                   // Square each
            .collect(Collectors.toList());
        System.out.println(evenSquares); // [4, 16, 36, 64, 100]
        
        // Example 2: Reduce - sum all elements
        int sum = numbers.stream()
            .reduce(0, (a, b) -> a + b);
        System.out.println("Sum: " + sum);
        
        // Example 3: Group by
        Map<Boolean, List<Integer>> evenOdd = numbers.stream()
            .collect(Collectors.partitioningBy(n -> n % 2 == 0));
        System.out.println("Even: " + evenOdd.get(true));
        System.out.println("Odd: " + evenOdd.get(false));
        
        // Example 4: Method references
        List<String> strings = Arrays.asList("apple", "banana", "cherry");
        strings.forEach(System.out::println); // Method reference
    }
}
```

### Optional Handling

**Interview Question:** "How to properly use Optional?"

```java
import java.util.Optional;

public class OptionalExample {
    public static void main(String[] args) {
        Optional<String> value = Optional.of("Hello");
        Optional<String> empty = Optional.empty();
        
        // Using ifPresent
        value.ifPresent(v -> System.out.println("Value: " + v));
        
        // Using ifPresentOrElse (Java 9+)
        value.ifPresentOrElse(
            v -> System.out.println("Got: " + v),
            () -> System.out.println("Not present")
        );
        
        // Using orElse
        String result = empty.orElse("Default Value");
        System.out.println(result);
        
        // Using map
        Optional<Integer> length = value.map(String::length);
        System.out.println(length); // Optional[5]
        
        // Using filter
        Optional<String> filtered = value.filter(v -> v.length() > 3);
        System.out.println(filtered); // Optional[Hello]
    }
}
```

---

## 6. Exception Handling (COMMON)

### Custom Exceptions & Try-Catch-Finally

**Interview Question:** "Design a custom exception and show proper exception handling."

```java
// Custom exception
public class InsufficientFundsException extends Exception {
    public InsufficientFundsException(String message) {
        super(message);
    }
}

public class BankAccount {
    private double balance;
    
    public BankAccount(double initial) {
        this.balance = initial;
    }
    
    public void withdraw(double amount) throws InsufficientFundsException {
        if (amount > balance) {
            throw new InsufficientFundsException(
                "Insufficient funds. Balance: " + balance + ", Requested: " + amount
            );
        }
        balance -= amount;
    }
    
    public static void main(String[] args) {
        BankAccount account = new BankAccount(100);
        
        try {
            account.withdraw(150);
        } catch (InsufficientFundsException e) {
            System.err.println("Error: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Unexpected error: " + e);
        } finally {
            System.out.println("Transaction attempt completed");
        }
    }
}
```

---

## 7. Design Patterns (COMMON IN SENIOR INTERVIEWS)

### LRU Cache

**Interview Question:** "Implement an LRU Cache."

```java
import java.util.*;

public class LRUCache<K, V> extends LinkedHashMap<K, V> {
    private final int capacity;
    
    public LRUCache(int capacity) {
        super(capacity, 0.75f, true); // accessOrder = true
        this.capacity = capacity;
    }
    
    @Override
    protected boolean removeEldestEntry(Map.Entry<K, V> eldest) {
        return size() > capacity;
    }
    
    public static void main(String[] args) {
        LRUCache<String, Integer> cache = new LRUCache<>(3);
        
        cache.put("a", 1);
        cache.put("b", 2);
        cache.put("c", 3);
        System.out.println(cache); // {a=1, b=2, c=3}
        
        cache.get("a"); // Access 'a', moves to end
        cache.put("d", 4); // 'b' is removed (least recently used)
        System.out.println(cache); // {c=3, a=1, d=4}
    }
}
```

### Builder Pattern

**Interview Question:** "Implement Builder pattern for object creation."

```java
public class User {
    private final String name;
    private final String email;
    private final String phone;
    private final int age;
    
    // Private constructor
    private User(UserBuilder builder) {
        this.name = builder.name;
        this.email = builder.email;
        this.phone = builder.phone;
        this.age = builder.age;
    }
    
    public static class UserBuilder {
        private String name;
        private String email;
        private String phone = "N/A";
        private int age = 0;
        
        public UserBuilder name(String name) {
            this.name = name;
            return this;
        }
        
        public UserBuilder email(String email) {
            this.email = email;
            return this;
        }
        
        public UserBuilder phone(String phone) {
            this.phone = phone;
            return this;
        }
        
        public UserBuilder age(int age) {
            this.age = age;
            return this;
        }
        
        public User build() {
            return new User(this);
        }
    }
    
    @Override
    public String toString() {
        return "User{" + "name='" + name + "', email='" + email + 
               "', phone='" + phone + "', age=" + age + "}";
    }
    
    public static void main(String[] args) {
        User user = new User.UserBuilder()
            .name("John Doe")
            .email("john@example.com")
            .phone("9876543210")
            .age(25)
            .build();
        
        System.out.println(user);
    }
}
```

---

## 8. equals() & hashCode() Contract (IMPORTANT)

**Interview Question:** "Explain hashCode() and equals() contract."

```java
public class Student {
    private int id;
    private String name;
    
    public Student(int id, String name) {
        this.id = id;
        this.name = name;
    }
    
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        
        Student student = (Student) obj;
        return id == student.id && Objects.equals(name, student.name);
    }
    
    @Override
    public int hashCode() {
        return Objects.hash(id, name);
    }
    
    public static void main(String[] args) {
        Set<Student> set = new HashSet<>();
        Student s1 = new Student(1, "John");
        Student s2 = new Student(1, "John");
        
        set.add(s1);
        set.add(s2);
        System.out.println(set.size()); // 1 (both are equal and same hash)
    }
}
```

---

## 9. Array Problems (VERY COMMON)

### Two Sum Problem

**Interview Question:** "Find two numbers in array that add up to target."

```java
public class TwoSum {
    // Approach 1: HashSet - O(n) time, O(n) space
    public static boolean twoSum(int[] arr, int target) {
        Set<Integer> seen = new HashSet<>();
        for (int num : arr) {
            if (seen.contains(target - num)) {
                return true;
            }
            seen.add(num);
        }
        return false;
    }
    
    // Approach 2: Two pointers (sorted array) - O(n) time, O(1) space
    public static boolean twoSumSorted(int[] arr, int target) {
        Arrays.sort(arr);
        int left = 0, right = arr.length - 1;
        while (left < right) {
            int sum = arr[left] + arr[right];
            if (sum == target) return true;
            if (sum < target) left++;
            else right--;
        }
        return false;
    }
}
```

---

## Quick Reference: Time Complexity

| Operation | ArrayList | LinkedList | HashMap | TreeMap | HashSet |
|-----------|-----------|-----------|---------|---------|---------|
| Get       | O(1)      | O(n)      | O(1)    | O(log n)| O(1)    |
| Add       | O(1)*     | O(1)      | O(1)    | O(log n)| O(1)    |
| Remove    | O(n)      | O(1)      | O(1)    | O(log n)| O(1)    |
| Search    | O(n)      | O(n)      | O(1)    | O(log n)| O(1)    |

---

## Interview Preparation Checklist

- [ ] String reversal & manipulation (StringBuilder, two pointers)
- [ ] Linked list operations (reverse, cycle detection, merge)
- [ ] Collections (HashMap, HashSet, ArrayList, LinkedList)
- [ ] Concurrency basics (threads, synchronized, volatile)
- [ ] Lambda & Streams (filter, map, reduce, collect)
- [ ] Exception handling (custom exceptions, try-catch-finally)
- [ ] Design patterns (Singleton, Builder, Factory, Observer)
- [ ] equals() & hashCode() contract
- [ ] Array problems (two pointers, hash-based solutions)
- [ ] Optional usage (ifPresent, map, filter, orElse)

---

**Last Updated:** 2026-10-08  
**Focus Level:** 5 years experience  
**Estimated Study Time:** 3-4 weeks with daily 2-3 hour practice
