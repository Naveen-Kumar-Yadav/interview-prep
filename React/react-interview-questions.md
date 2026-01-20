1️⃣ Why does React 18 run useEffect twice?

Answer:
React 18 StrictMode intentionally runs effects twice in development to detect side effects.
This does not happen in production.

2️⃣ Why state updates are batched in React?

Answer:
Batching improves performance by reducing re-renders.
React batches multiple setState calls into a single render.

3️⃣ Why does React.memo not stop re-render?

Answer:
Because props are compared using shallow comparison.
New object or function references cause re-renders.

4️⃣ Difference between useEffect and useLayoutEffect?

Answer:

useEffect runs after paint (non-blocking)

useLayoutEffect runs before paint (blocking, used for DOM measurements)

5️⃣ What is a stale closure in React?

Answer:
A stale closure happens when a function captures old state/props due to missing dependencies.

6️⃣ Why should we avoid index as key?

Answer:
Using index as key breaks reconciliation and causes UI bugs when list order changes.

7️⃣ How does React prevent XSS?

Answer:
React escapes values by default.
Only dangerouslySetInnerHTML can inject raw HTML.

8️⃣ What causes memory leaks in React?

Answer:

Uncleaned effects

Pending async operations

Subscriptions not removed on unmount

9️⃣ When should we use useReducer instead of useState?

Answer:

Complex state logic

Multiple related state updates

Predictable state transitions

🔟 What problem does useTransition solve?

Answer:
It marks updates as non-urgent, keeping UI responsive during heavy renders.

1️⃣1️⃣ Why Context API causes performance issues?

Answer:
Every context value change re-renders all consumers, even if they use only part of the value.

1️⃣2️⃣ What is reconciliation in React?

Answer:
It’s the process of comparing the previous and current virtual DOM to update the real DOM efficiently.

1️⃣3️⃣ What is React Fiber?

Answer:
Fiber is React’s new reconciliation engine that allows interruptible and prioritized rendering.

1️⃣4️⃣ How do you optimize large lists?

Answer:

Virtualization (react-window)

Memoization

Pagination

1️⃣5️⃣ What are Error Boundaries?

Answer:
They catch runtime errors in child components and prevent app crashes.
Only class components can implement them.
