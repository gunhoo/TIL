# Priority Queue
## What is Priority Queue
```
A priority queue is an abstract data-type similar to a regular queue or stack data structure. Each element in a priority queue has an associated priority. In a priority queue, elements with high priority are served before elements with low priority.
```
Source: <i>Wikipedia</i>  


- Max Heap
    > Bigger elements have high priority.  
    So that ```poll``` function extracts an element with high priority.
    - In Java, you must use ```Collections.reverseOrder()``` to impelments Max Heap since it is not default
        ```java
        Queue<Integer> pq = new PriorityQueue<Integer>(Collections.reserveOrder());
        ```
- Min Heap
    > Smaller elements have high prioriy

## Compare to others
<table>
<tr>
    <th>Approach</th>
    <th>Time Complexity(insert)</th>
    <th>Time Complexit(extract)</th>
</tr>
<tr>
    <td>Disordered Array</td>
    <td>O(1)</td>
    <td>O(n)</td>
</tr>
<tr>
    <td>Disordered List</td>
    <td>O(1)</td>
    <td>O(n)</td>
</tr>
<tr>
    <td>Ordered Array</td>
    <td>O(n)</td>
    <td>O(1)</td>
</tr>
<tr>
    <td>Ordered List</td>
    <td>O(n)</td>
    <td>O(1)</td>
</tr>
<tr>
    <td>Heap</td>
    <td>O(logn)</td>
    <td>O(logn)</td>
</tr>
</table>

## Key Features
- <b>Priority-Based Ordering</b>: Elements in a `PriorityQueue` are ordered based on their natural order or according to a specified comparator. By default, it orders elements in <b>ascending order</b>
- <b>Binary Heap Implementation</b>: Internally, a `PriorityQueue` is implemented as a binary heap, which is a complete binary tree with the heap property. This allows for efficient addition(enqueue) and removal of elements(dequeue).
- <b>Automatic Sorting</b>: When elements are added to the `PriorityQueue`, they are automatically sorted based on their priority. The element with the highest priority(smallest value) is at the front.
- Efficient Access to Minimum(or Maximum) Element
- Flexible Ordering
- <b>Dynamic Size</b>
- <b>Support for Null Elements</b>
- <b>No Random Access</b>: Unlike some other collections like lists, `PriorityQueue` does not provide random access to elements. You can only access the front(highest priority) element.

## Examples
- Basic implements
    ```java
    import java.util.PriorityQueue;
    import java.util.Collections;

    public class PriorityQueueExample {
        
        public static void main(String[] args) {
            PriorityQueue<Integer> pq = new PriorityQueue<>();
            pq.add(11);
            pq.add(3);
            pq.add(1);
            pq.add(12);
            pq.add(5);

            while (!pq.isEmpty()) {
                System.out.print(pq.poll() + " "); // 1 3 5 11 12
            }
            System.out.println();

            pq = new PriorityQueue<>(Collections.reverseOrder());
            pq.add(11);
            pq.add(3);
            pq.add(1);
            pq.add(12);
            pq.add(5);

            while (!pq.isEmpty()) {
                System.out.print(pq.poll() + " "); // 12 11 5 3 1
            }
    }
    }
    ```
- Customized priority
    ```java
    import java.util.PriorityQueue;
    import java.util.Collections;
    import java.util.Comparator;

    public class PriorityQueueExample {
        
        public static void main(String[] args) {
            PriorityQueue<Student> pq = new PriorityQueue<>();

            pq.add(new Student(3, "Kate"));
            pq.add(new Student(19, "Hugo"));
            pq.add(new Student(1, "Anna"));

            while (!pq.isEmpty()) {
                System.out.print(pq.poll() + ", "); // [1, Anna], [3, Kate], [19, Hugo],
            }
            System.out.println();

            pq = new PriorityQueue<>(new Comparator<Student>() {
                @Override
                public int compare(Student s1, Student s2) {
                    return s1.name.compareTo(s2.name);
                }
            });
            // lamda expression
            // pq = new PriorityQueue<Student>((s1, s2) ->
            //    s1.name.compareTo(s2.name));
            pq.add(new Student(3, "Kate"));
            pq.add(new Student(19, "Hugo"));
            pq.add(new Student(1, "Anna"));
            while (!pq.isEmpty()) {
                System.out.print(pq.poll() + ", "); // [1, Anna], [19, Hugo], [3, Kate],
            }
        }
    }

    class Student implements Comparable<Student> {

        int studentId;
        String name;

        public Student(int studentId, String name) {
            this.studentId = studentId;
            this.name = name;
        }

        @Override
        public int compareTo(Student s) {
            return this.studentId - s.studentId; // ascending
            // return s.studentId - this.studentId; // descending
        }

        @Override
        public String toString() {
            return "[" + this.studentId + ", " + this.name + "]";
        }
    }
    ```
## Methods
<table>
<tr>
    <th>Modifier and Type</th>
    <th>Method</th>
    <th>Description</th>
</tr>
<tr>
    <td>boolean</td>
    <td>add(E e)</td>
    <td>Inserts element</td>
</tr>
<tr>
    <td>void</td>
    <td>clear()</td>
    <td>Removes all of the elements</td>
</tr>
<tr>
    <td>Comparator<? super E></td>
    <td>comparator()</td>
    <td>Returns the comparator</td>
</tr>
<tr>
    <td>boolean</td>
    <td>contains(Object o)</td>
    <td>Returns true if this queue contains the specified element</td>
</tr>
<tr>
    <td>Iterator&lt;E&gt;</td>
    <td>iterator()</td>
    <td>Returns an iterator</td>
</tr>
<tr>
    <td>boolean</td>
    <td>offer(E e)</td>
    <td>Inserts element</td>
</tr>
<tr>
    <td>E</td>
    <td>peek()</td>
    <td>Retrieves, but does not remove, or returns null if this queue is empty</td>
</tr>
<tr>
    <td>E</td>
    <td>poll()</td>
    <td>Retrieves and removes the head of this queue, or returns null if this queue is empty</td>
</tr>
<tr>
    <td>boolean</td>
    <td>remove(Object o)</td>
    <td>Removes a single instance of the specified element from this queue</td>
</tr>
<tr>
    <td>int</td>
    <td>size()</td>
    <td>Returns the number of elements</td>
</tr>
<tr>
    <td>Spliterator<E></td>
    <td>spliterator()</td>
    <td>Creates a late-binding and fail-fast Spliterator over the elements in this queue</td>
</tr>
<tr>
    <td>Object[]</td>
    <td>toArray()</td>
    <td>Returns an array containing all of the elements in this queue</td>
</tr>
<tr>
    <td>&lt;T&gt; T[]</td>
    <td>toArray(T[] a)</td>
    <td>Returns an array containing all of the elements in this queue</td>
</tr>
</table>


## References
- <a href="https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html">Oracle Docs</a>