

#### 1. Abstract Classes and Interfaces
**Question:** Which statement correctly differentiates abstract classes from interfaces in Java?
   - A) Abstract classes can have multiple methods, but interfaces can only have one.
   - B) Interfaces can have default methods with implementations, whereas abstract classes cannot.
   - C) Abstract classes can have constructor methods, but interfaces cannot.
   - D) Only abstract classes can have public methods.
   - **Correct Answer:** C

#### 2. Polymorphism
**Question:** What is the output of the following Java code?

   ```java
   class A {
       String show() { return "A"; }
   }

   class B extends A {
       String show() { return "B"; }
   }

   public class Test {
       public static void main(String args[]) {
           A obj = new B();
           System.out.println(obj.show());
       }
   }
   ```
   - A) A
   - B) B
   - C) Compilation Error
   - D) Runtime Error
   - **Correct Answer:** B

#### 3. Enumerations
**Question:** Which of these is a valid use of an enumeration in Java?
   - A) To define a set of constants representing days of the week.
   - B) To create a collection of objects.
   - C) To declare a method within a class.
   - D) To initialize thread states.
   - **Correct Answer:** A

#### 4. Generic Types
**Question:** What does the following Java generic class definition specify?

   ```java
   public class Box<T extends Number> { ... }
   ```
   - A) The Box class can only hold objects of type Number.
   - B) The Box class can hold any type of object.
   - C) The Box class can hold objects of Number type or its subclasses.
   - D) The Box class is a type of Number.
   - **Correct Answer:** C

#### 5. Collections
**Question:** In Java Collections Framework, which of the following is true about `ArrayList` and `LinkedList`?
   - A) `ArrayList` and `LinkedList` both use a dynamic array to store elements.
   - B) `ArrayList` provides faster insertion and removal operations than `LinkedList`.
   - C) `LinkedList` provides faster random access of elements than `ArrayList`.
   - D) `LinkedList` consumes less memory than `ArrayList` for large lists.
   - **Correct Answer:** D

#### 6. Inner Classes
**Question:** What is a characteristic of a static inner class in Java?
   - A) It can access non-static members of the outer class.
   - B) It requires an instance of the outer class to be instantiated.
   - C) It can only be declared within a static method.
   - D) It does not require an outer class instance to be instantiated.
   - **Correct Answer:** D

#### 7. Exceptions
**Question:** Consider the following Java code snippet:

   ```java
   try {
       // Code that may throw an exception
   } catch (Exception e) {
       System.out.println("Exception caught");
   } finally {
       System.out.println("Finally block executed");
   }
   ```

   **What is true about the 'finally' block?**
   - A) It is executed only if an exception is thrown.
   - B) It is not executed if an exception is caught in the 'catch' block.
   - C) It is executed regardless of whether an exception is thrown or caught.
   - D) It will not execute if the 'catch' block contains a return statement.
   - **Correct Answer:** C

#### 8. Annotations
**Question:** What is the primary use of the `@Deprecated` annotation in Java?
   - A) To mark a method or class that should not be used anymore.
   - B) To indicate that a method or class is going to be removed in future versions.
   - C) To automatically document methods or classes.
   - D) To prevent a method or class from being serialized.
   - **Correct Answer:** A

#### 9. Reflection
   - A) It allows an application to observe and modify its own behavior at runtime.
   - B) Reflection can only be used to inspect objects, not modify them.
   - C) Using Reflection significantly improves the performance of the application.
   - D) Reflection is primarily used for compile-time type checking.
   - **Correct Answer:** A

#### 10. Encapsulation
**Question:** What encapsulation property is violated if a class has public data fields?
   - A) Data Hiding
   - B) Inheritance
   - C) Polymorphism
   - D) Abstraction
   - **Correct Answer:** A

#### 11. Inheritance
**Question:** What happens when a subclass in Java has a method with the same signature as a method in the superclass?
   - A) The method in the subclass is hidden.
   - B) The method in the superclass is overridden.
   - C) A compilation error occurs.
   - D) The method in the superclass is overloaded.
   - **Correct Answer:** B

#### 12. Abstract Classes
**Question:** Which statement is true about abstract classes in Java?
   - A) An abstract class can have both abstract and non-abstract methods.
   - B) If a class has at least one abstract method, it must be declared abstract.
   - C) An abstract class cannot have a constructor.
   - D) Both A and B.
   - **Correct Answer:** D

#### 13. Generic Types
**Question:** What is the purpose of wildcards (`?`) in Java generics?
   - A) To specify an unknown type.
   - B) To enforce type safety.
   - C) To allow the creation of generic instances.
   - D) To restrict a type to a specific class hierarchy.
   - **Correct Answer:** A

#### 14. Collections Framework
**Question:** In the Java Collections Framework, which is a true statement about the `HashSet` and `TreeSet` classes?
   - A) `HashSet` maintains elements in sorted order, while `TreeSet` does not.
   - B) `TreeSet` allows duplicate elements, but `HashSet` does not.
   - C) `HashSet` offers constant time performance for basic operations, while `TreeSet` does not.
   - D) Both `HashSet` and `TreeSet` are synchronized.
   - **Correct Answer:** C

### Java Annotations and Reflection Quiz

**1. What is the primary use of annotations in Java?**
   - A) To change the behavior of a method at runtime
   - B) To provide metadata about the code
   - C) To optimize the code during compilation
   - D) To allocate memory during runtime
   - **Correct Answer:** B

**2. Which of these is not a built-in annotation in Java?**
   - A) `@Deprecated`
   - B) `@Override`
   - C) `@FunctionalInterface`
   - D) `@MemoryManagement`
   - **Correct Answer:** D

**3. What is Reflection used for in Java?**
   - A) To create new instances of classes at runtime
   - B) To inspect classes, methods, and fields at runtime
   - C) To enhance the performance of the application
   - D) Both A and B
   - **Correct Answer:** D

**4. Which method is used to obtain the `Class` object of a class in Java?**
   - A) `getClass()`
   - B) `getType()`
   - C) `instanceOf()`
   - D) `forName()`
   - **Correct Answer:** A

**5. Which of these is a correct way to access a private field of a class using Reflection?**
   - A) Using `getField()` method of the `Class` class
   - B) Using `getDeclaredField()` method of the `Class` class and setting it accessible
   - C) Directly accessing the field as Reflection bypasses access control
   - D) Using `getPrivateField()` method of the `Class` class
   - **Correct Answer:** B

**6. What does the `@Override` annotation indicate?**
   - A) The annotated method is overriding a method in a superclass.
   - B) The annotated method should be executed over other methods.
   - C) The annotated method will replace a method in a superclass.
   - D) The annotated method cannot be overridden by any subclass.
   - **Correct Answer:** A

**7. When using Reflection, how do you invoke a private method of a class?**
   - A) By directly calling the method, as Reflection bypasses method visibility
   - B) By getting the method with `getMethod()` and invoking it
   - C) By getting the method with `getDeclaredMethod()`, setting it accessible, and then invoking it
   - D) Private methods cannot be invoked using Reflection
   - **Correct Answer:** C

**8. Which of these is true about the `@FunctionalInterface` annotation?**
   - A) It is used to mark interfaces that have exactly one abstract method.
   - B) It is used to create anonymous classes.
   - C) It indicates that the interface will be automatically implemented by the Java compiler.
   - D) It is used to mark all interfaces that are functional.
   - **Correct Answer:** A

**9. How is Reflection commonly used?**
   - A) To increase the efficiency of code execution
   - B) For serialization and deserialization of objects
   - C) In high-performance critical applications
   - D) To create plug-in architectures
   - **Correct Answer:** D

**10. What is the potential downside of using Reflection in Java?**
    - A) It makes the code more readable and maintainable
    - B) It can lead to performance overhead
    - C) It is not supported in newer versions of Java
    - D) It automatically optimizes the code
    - **Correct Answer:** B
### Java Threading Quiz

**1. What is the purpose of the `wait()` method in Java's object threading?**
   - A) To send the current thread into a waiting state until another thread calls `notify()`
   - B) To permanently stop the execution of the current thread
   - C) To pause the thread for a specific period
   - D) To check if a thread is waiting
   - **Correct Answer:** A

**2. Which of the following is true about the `synchronized` keyword in Java?**
   - A) It is used to start a thread
   - B) It can be applied to variables
   - C) It allows only one thread to access a method or block at a time
   - D) It makes the class thread-safe automatically
   - **Correct Answer:** C

**3. What is the main difference between the `Thread` class and the `Runnable` interface in Java?**
   - A) `Thread` is a class, `Runnable` is an interface
   - B) `Runnable` can start a thread, `Thread` cannot
   - C) `Thread` has a `run()` method, `Runnable` does not
   - D) `Runnable` has a `start()` method, `Thread` does not
   - **Correct Answer:** A

**4. What is a daemon thread in Java?**
   - A) A high-priority thread
   - B) A thread that does garbage collection
   - C) A thread that runs in the background
   - D) The only thread that can access the main method
   - **Correct Answer:** C

**5. Which method would change the name of a thread?**
   - A) `setName()`
   - B) `changeName()`
   - C) `renameThread()`
   - D) `updateName()`
   - **Correct Answer:** A

**6. What happens when the `join()` method is called on a thread?**
   - A) The current thread pauses its execution until the thread it joins completes
   - B) The thread immediately stops executing
   - C) The runtime joins two threads into one
   - D) The thread execution is permanently joined to the main thread
   - **Correct Answer:** A

**7. How do you ensure that a resource is accessed by only one thread at a time?**
   - A) By using the `volatile` keyword
   - B) By using the `synchronized` keyword
   - C) By using the `static` keyword
   - D) By using the `final` keyword
   - **Correct Answer:** B

**8. In Java, which of these is a correct way to create a new thread?**
   - A) `new Thread(new Runnable()).start();`
   - B) `new Runnable().start();`
   - C) `Thread.start(new Runnable());`
   - D) `Runnable.start(new Thread());`
   - **Correct Answer:** A

**9. What is the use of the `interrupt()` method in thread handling in Java?**
   - A) To permanently stop a thread
   - B) To request a thread to stop its current work and do something else
   - C) To combine two threads
   - D) To pause a thread temporarily
   - **Correct Answer:** B

**10. Which method checks if a thread has been interrupted?**
    - A) `isInterrupted()`
    - B) `checkInterrupt()`
    - C) `hasInterrupted()`
    - D) `getInterruptStatus()`
    - **Correct Answer:** A
    
### Java I/O Quiz

**1. Which of these classes is used to read character files in Java?**
   - A) `FileOutputStream`
   - B) `FileReader`
   - C) `BufferedOutputStream`
   - D) `InputStreamReader`
   - **Correct Answer:** B

**2. In Java, what is the purpose of the `BufferedReader` class?**
   - A) To write text to a character-output stream
   - B) To read text from a character-input stream, buffering characters for efficient reading
   - C) To handle binary data instead of text data
   - D) To send output to the console
   - **Correct Answer:** B

**3. What does the `File` class in Java represent?**
   - A) A file in the file system
   - B) The contents of a file
   - C) A file output stream
   - D) A network connection
   - **Correct Answer:** A

**4. Which class would you use for file input using bytes in Java?**
   - A) `FileReader`
   - B) `FileInputStream`
   - C) `BufferedReader`
   - D) `FileWriter`
   - **Correct Answer:** B

**5. How do you append data to a file instead of overwriting it in Java?**
   - A) Use `FileWriter` with the append flag set to true
   - B) Use `FileOutputStream` in append mode
   - C) Use `BufferedWriter` with a special append method
   - D) Both A and B
   - **Correct Answer:** D

**6. What is the purpose of the `PrintWriter` class in Java?**
   - A) To read printed text from a file
   - B) To write formatted text to a file
   - C) To print text to the console only
   - D) To handle raw binary data
   - **Correct Answer:** B

**7. What exception is commonly thrown when dealing with I/O operations in Java?**
   - A) `NullPointerException`
   - B) `IOException`
   - C) `ArithmeticException`
   - D) `IndexOutOfBoundsException`
   - **Correct Answer:** B

**8. Which statement is true about the `RandomAccessFile` class in Java?**
   - A) It is used only to read from files.
   - B) It supports both reading and writing to a random access file.
   - C) It cannot write to files.
   - D) It is part of the Java Collections Framework.
   - **Correct Answer:** B

**9. In Java, what is the purpose of the `ObjectOutputStream` class?**
   - A) To write primitive data types to an OutputStream
   - B) To write objects to an OutputStream
   - C) To serialize objects to a file
   - D) Both B and C
   - **Correct Answer:** D

**10. What is a `Stream` in Java I/O?**
    - A) A sequence of data
    - B) A type of file
    - C) A memory management unit
    - D) A protocol for data transmission
    - **Correct Answer:** A
