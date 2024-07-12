# JTask5
import java.util.ArrayList;
import java.util.List;

public class StudentRegistrationSystem {
    public static void main(String[] args) {
        // Creating courses
        Course c1 = new Course("CS101", "Introduction to Computer Science", "Basic concepts of programming", 30);
        Course c2 = new Course("ENG201", "English Literature", "Introduction to classic literature", 25);
        Course c3 = new Course("MATH301", "Calculus", "Fundamental principles of calculus", 40);

        // Creating students
        Student s1 = new Student(1, "Alice");
        Student s2 = new Student(2, "Bob");

        // Registering courses
        s1.registerCourse(c1);
        s1.registerCourse(c2);
        s2.registerCourse(c1);
        s2.registerCourse(c3);

        // Displaying registered courses for each student
        System.out.println(s1);
        s1.displayRegisteredCourses();

        System.out.println(s2);
        s2.displayRegisteredCourses();

        // Dropping a course
        s1.dropCourse(c2);

        // Displaying registered courses after dropping
        System.out.println("Courses after dropping for " + s1.getName() + ":");
        s1.displayRegisteredCourses();
    }
}

class Course {
    private String courseCode;
    private String title;
    private String description;
    private int capacity;
    private int currentEnrollment;

    public Course(String courseCode, String title, String description, int capacity) {
        this.courseCode = courseCode;
        this.title = title;
        this.description = description;
        this.capacity = capacity;
        this.currentEnrollment = 0;
    }

    public String getCourseCode() {
        return courseCode;
    }

    public String getTitle() {
        return title;
    }

    public String getDescription() {
        return description;
    }

    public int getCapacity() {
        return capacity;
    }

    public int getCurrentEnrollment() {
        return currentEnrollment;
    }

    public boolean enrollStudent() {
        if (currentEnrollment < capacity) {
            currentEnrollment++;
            return true;
        } else {
            return false; // course is full
        }
    }

    public void dropStudent() {
        if (currentEnrollment > 0) {
            currentEnrollment--;
        }
    }

    @Override
    public String toString() {
        return "Course Code: " + courseCode + "\n" +
               "Title: " + title + "\n" +
               "Description: " + description + "\n" +
               "Capacity: " + capacity + "\n" +
               "Current Enrollment: " + currentEnrollment + "\n";
    }
}

class Student {
    private int studentId;
    private String name;
    private List<Course> registeredCourses;

    public Student(int studentId, String name) {
        this.studentId = studentId;
        this.name = name;
        this.registeredCourses = new ArrayList<>();
    }

    public int getStudentId() {
        return studentId;
    }

    public String getName() {
        return name;
    }

    public List<Course> getRegisteredCourses() {
        return registeredCourses;
    }

    public void registerCourse(Course course) {
        if (course.enrollStudent()) {
            registeredCourses.add(course);
            System.out.println("Student " + name + " registered in course " + course.getCourseCode());
        } else {
            System.out.println("Course " + course.getCourseCode() + " is full. Registration failed.");
        }
    }

    public void dropCourse(Course course) {
        course.dropStudent();
        registeredCourses.remove(course);
        System.out.println("Student " + name + " dropped course " + course.getCourseCode());
    }

    public void displayRegisteredCourses() {
        System.out.println("Registered Courses for " + name + ":");
        for (Course course : registeredCourses) {
            System.out.println(course);
        }
        System.out.println();
    }

    @Override
    public String toString() {
        return "Student ID: " + studentId + "\n" +
               "Name: " + name + "\n" +
               "Registered Courses: " + registeredCourses.size() + "\n";
    }
}
