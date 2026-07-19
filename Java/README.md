# Java Interview Prep (≈5 years experience)

A compact, practical collection of top Java interview questions, answers, and short code examples aimed at developers with roughly 5 years of experience. Use this as a study guide, flashcard source, or the basis for timed mock interviews.

## How to use
- Read the topic summaries to refresh concepts quickly.
- Practice the coding problems under "Practical Coding" with a 30–45 minute timer.
- Use the short code examples to remember idiomatic solutions.
- Convert sections into flashcards or a one-hour mock interview: 30–40 min coding + 15–20 min system/concurrency discussion.

## Contents
- Core Java fundamentals
- Collections & Data Structures
- Concurrency & Multithreading
- JVM Internals & Performance
- Java 8+ (Streams, Lambdas, Optional)
- Design Patterns & Architecture
- Spring & Ecosystem
- Databases, Serialization & Networking
- Practical coding problems and sample solutions
- Behavioral & system design prompts

---

## Core Java (language & basics)
- == vs equals(): `==` compares references (for objects) or values (primitives). `equals()` compares logical equality; override carefully.
- hashCode()/equals() contract: equal objects must have equal hashCodes — required for hash-based collections.
- Immutability: `final` class, `private final` fields, no setters, defensive copies for mutable fields.
- final vs finally vs finalize(): modifier vs cleanup block vs deprecated finalizer.
- Stack vs heap: primitives & references on stack; objects on heap. Escape analysis may allocate on stack.

## Collections & Data Structures
- ArrayList vs LinkedList vs Vector vs CopyOnWriteArrayList — pick based on read/write pattern, concurrency, and access requirements.
- HashMap internals: hash -> bucket -> chain/tree; resizing when load factor exceeded; Java 8+: treeify long chains.
- ConcurrentHashMap vs synchronizedMap — non-blocking reads and finer-grained concurrency vs single lock wrapper.
- Iterators: fail-fast behavior leads to ConcurrentModificationException on structural modifications.

## Concurrency & Multithreading
- synchronized vs ReentrantLock: ReentrantLock offers tryLock, lockInterruptibly, fairness and Conditions.
- volatile: visibility guarantee and ordering for single variables; not a substitute for atomic compound actions.
- happens-before relationships determine visibility and ordering.
- Executors: choose thread pool type based on task nature (CPU-bound vs IO-bound).
- Deadlock: avoid by consistent lock ordering, use timeouts or tryLock fallbacks.

Short snippet — CompletableFuture usage
```java
import java.util.concurrent.*;
public class CompletableFutureExample {
  public static void main(String[] args) throws Exception {
    ExecutorService ex = Executors.newFixedThreadPool(4);
    CompletableFuture<Integer> f = CompletableFuture.supplyAsync(() -> 21, ex)
      .thenApply(x -> x * 2)
      .thenCompose(x -> CompletableFuture.supplyAsync(() -> x + 1, ex));
    System.out.println(f.get()); // 43
    ex.shutdown();
  }
}
```

Double-checked locking (thread-safe singleton)
```java
public class DCLSingleton {
  private static volatile DCLSingleton instance;
  private DCLSingleton(){}
  public static DCLSingleton getInstance() {
    if (instance == null) {
      synchronized (DCLSingleton.class) {
        if (instance == null) instance = new DCLSingleton();
      }
    }
    return instance;
  }
}
```

## JVM Internals & Performance
- Class loading: bootstrap -> extension -> application; custom classloaders should respect parent delegation.
- GC overview: generational GC, G1, ZGC, Shenandoah; pick based on latency vs throughput needs.
- Metaspace replaced PermGen in Java 8.
- Memory leaks: long-lived static collections, unclosed listeners, thread-local misuse, classloader leaks.
- Profiling: JFR, Java Mission Control, async-profiler, VisualVM.

## Java 8+ (Streams, Lambdas, Optional)
- Streams: intermediate (lazy) vs terminal ops; beware shared mutable state in parallel streams.
- Optional: use as return type for absent values; avoid for fields/parameters usually.
- Method references and lambda capture: capturing lambdas may allocate; non-capturing can be optimized.

## Design Patterns & Architecture
- Common patterns: Singleton (enum or holder idiom), Factory, Builder, Strategy, Observer.
- LRU cache: LinkedHashMap(accessOrder=true) or use Caffeine/Guava for production.

LRU cache quick snippet:
```java
import java.util.*;
public class LRUCache<K,V> extends LinkedHashMap<K,V> {
  private final int capacity;
  public LRUCache(int capacity){ super(capacity, 0.75f, true); this.capacity = capacity; }
  @Override protected boolean removeEldestEntry(Map.Entry<K,V> eldest){ return size() > capacity; }
}
```

## Spring & Ecosystem
- DI: prefer constructor injection; understand bean scopes and ApplicationContext vs BeanFactory.
- Transactions: propagation, isolation, and self-invocation caveat (proxy bypass).
- Production concerns: health endpoints, metrics (Micrometer), tracing (OpenTelemetry), circuit breakers (Resilience4j).

## Databases, Serialization & Networking
- JDBC vs JPA: know when to use raw SQL; watch for N+1 selects and fix with fetch joins or batching.
- Java serialization: be careful with serialVersionUID and backward compatibility; prefer JSON/Protobuf for external interfaces.
- REST best practices: correct status codes, consistent error payloads, idempotency.

## Practical Coding / Algorithms (practice these)
- Linked list reversal (iterative & recursive)
- Merge two sorted lists
- Detect cycle in linked list (Floyd’s algorithm)
- In-memory rate limiter (token bucket or leaky bucket)
- Producer-consumer: prefer BlockingQueue
- Implement LRU cache

Suggested timed practice:
- 30–45 min: one medium coding problem (linked list/tree), write and test in-editor.
- 15 min: concurrency question + short code or design discussion.
- 15–20 min: system design / architecture mini-question.

## Behavioral & System Design Prompts
- Describe a production incident you handled (STAR): problem, actions, impact, lessons learned.
- How would you scale a Java microservice? Discuss state handling, caching, sharding, and resilience.

## Converting this content
If you want:
- Flashcards: Q/A pairs per question.
- Mock interview script: timed prompts with scoring rubric.
- Full sample solutions: step-by-step answers for 6–8 coding problems.
Tell me which format you prefer and I will generate it.

## Contributing
- PRs welcome. Add new questions, better explanations, or optimized code samples.
- Keep answers concise and tested where code is provided.

## License
Use, modify, and share — add a LICENSE file at repo root if you want a specific license.
