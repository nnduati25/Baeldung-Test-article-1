# Creating a Deep vs Shallow Copy of an Object in Java
In the field of Java Programming, Deep and Shallow copying are two main ways that objects are copied. In this article we are going to check the ways in which objects are duplicated using the two copying steps. Shallow and deep copying are both related to object copying. Buty what's an Object? objects are physical entities in programming that are used to represent real-world. An object copy also referred as clone, is usually created if you want to move or modify an object while still preserving tyhe state of the original object.

### Prerequisite
In order to understand the concept of `Shallow` and `Deep` copying is advicsble to have fondation on the following topics.
* Basic Java Syntax and concept
* Object oriented Programming (OOP)
* Undersatnding reference and reference types
* Cloneable Interface and `clone()` Method

## Shallow Copying
Shallow Copying is a process of copying an object where new object gets its own copy of the original object. Shallow copying stores the reference of object to the original object address. The object will have a similar copy of all the entities of source object inlcuding the primitive and object reference.

### Code Snippet for Shallow Copying 

```java
// Define Student Class
class Student{

// constructor for course
course(String courseName){
    this.type=courseName;
 }
}
// defining public student Class 
 public class student {
    String name;
    Course course;

    //Constructor for student
public Student(String name, Course course) {
        this.name = name;
        this.course = course; 
 }
  // Overriding the clone() method to create a shallow copy
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone(); // Shallow copy
    }

    // Main method to demonstrate shallow copy
    public static void main(String[] args) {
        try {
            // Create an original Course object
            Course course = new Course("java");
            
            // Create an original Student object
            Student student1 = new Student("Martin", course);

            // Create a shallow copy of student1
            Student student2 = (Student) student1.clone();

            // Print details of original and copied students
            System.out.println("Original Student: " + student1.name + ", " + student1.course.courseName);
            System.out.println("Shallow Copy: " + student2.name + ", " + student2.course.courseName);

            // Modify the course name of the copied student
            student2.course.courseName = "Programming";

            // Print details after modification
            System.out.println("\nAfter modification:");
            System.out.println("Original Student: " + student1.course.courseName); // Output will be "programming"
            System.out.println("Shallow Copy: " + student2.course.courseName);   // Output will be "programming"
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
    }
}
```

### Output

```yaml
Original Student: Martin, Java
Shallow Copy: Martin, Java

After modification:
Original Student: Programming
Shallow Copy: Programmig
```

## Deep Copy
Deep copy of an object creates an exact copy of the same object. In deep copy both source and replica objects are independent. A change in source object will not affect the replica object. By invoking the `clone()` method or using other techniques, deep copying ensures that both primitive fields and object references are entirely replicated, preserving the complete state of the original object.

### Code Snippet for Shallow Copying 
``` java
// Define the Course class
class Course {
    String courseName;

    // Constructor for Course
    Course(String courseName) {
        this.courseName = courseName;
    }

    // Copy constructor for deep copy
    public Course(Course original) {
        this.courseName = original.courseName;
    }
}

// Define the Student class
public class Student {
    String name;
    Course course;

    // Constructor for Student
    public Student(String name, Course course) {
        this.name = name;
        this.course = course;
    }

    // Copy constructor for deep copy
    public Student(Student original) {
        this.name = original.name;
        // Create a new Course object to ensure deep copy
        this.course = new Course(original.course);
    }

    public static void main(String[] args) {
        // Create an original Course object
        Course course = new Course("Programming");

        // Create an original Student object
        Student student1 = new Student("Martin", course);

        // Create a deep copy of student1 using the copy constructor
        Student student2 = new Student(student1);

        // Print details of original and copied students
        System.out.println("Original Student: " + student1.name + ", " + student1.course.courseName);
        System.out.println("Deep Copy: " + student2.name + ", " + student2.course.courseName);

        // Modify the course name of the copied student
        student2.course.courseName = "Java";

        // Print details after modification
        System.out.println("\nAfter modification:");
        System.out.println("Original Student: " + student1.course.courseName); // Output will be "Programming"
        System.out.println("Deep Copy: " + student2.course.courseName);   // Output will be "Java"
    }
}
```yaml
Original Student: Martin, Programming
Deep Copy: Martin, Programming

After modification:
Original Student: Programming
Deep Copy: Java

```
According to the output before mofication both student had  the `courseName` as "Programming" because the deep copy constructor creates a new `Course` object with the same `courseName`. 
After mofification changing the `courseName` in `student2` to "Java" does not affect student1, because student1 and student2 have separate Course objects.

## Differences between Shallow and Deep Copy
* Definition:
Shallow Copy: Produces a fresh object without making duplicates of nested objects. References to those nested objects are instead copied.
Deep Copy: Constructs a new object and duplicates every object—including nested objects—found inside the old object recursively.
* Managing References:
Shallow Copy: The original nested objects are still referenced by the nested objects.
Deep Copy: All nested items are completely replicated without making any reference to the source objects.
* Memory Utilization:
Shallow Copy: Since nested objects are not duplicated, it usually consumes less memory.
Deep Copy: Since every item is duplicated, it requires more memory.
* Achievement:
Shallow Copy: Since it simply needs to copy references, it is typically quicker.
Deep Copy: Takes longer because all nested items and their child objects must be copied.

