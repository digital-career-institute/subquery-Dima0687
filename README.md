# tables
Students Table:
course table

> I'm to tired now and hope that i understand the tasks right.

PRE:
```SQL
CREATE TABLE students ( 
	StudentID INT PRIMARY KEY,
	StudentName VARCHAR(50)
);
INSERT INTO students VALUES
(1, 'Alice'),
(2, 'Bob'),
(3, 'Charlie'),
(4, 'David');

CREATE TABLE courses (
	CourseID INT PRIMARY KEY,
	CourseName VARCHAR(50)
);
INSERT INTO courses VALUES
(101, 'Math'),
(102, 'English'),
(103, 'Science'),
(104, 'History');

CREATE TABLE enrollments ( 
	studentid INT,
	courseid INT
);

INSERT INTO enrollments VALUES
( 1, 101 ),
( 1, 102 ),
( 2, 101 ),
( 3, 102 ),
( 4, 103 );
```
## Write a query to retrieve the names of students who are enrolled in the 'Math' course.

```SQL
SELECT s.studentid, s.studentname
FROM students s
JOIN enrollments en ON s.studentid = en.studentid
WHERE en.courseid = 101;
```

## Write a query to find the names of students who are not enrolled in any course.

```SQL
SELECT 
	studentid, studentname
FROM students
WHERE NOT EXISTS (
	SELECT 1
	FROM enrollments
	WHERE enrollments.studentid = students.studentid
);
```

## Write a query to retrieve the names of students who are enrolled in both 'Math' and 'English' courses.

```SQ
SELECT s.studentid, s.studentname, c1.coursename
FROM students s
JOIN enrollments en1 ON s.studentid = en1.studentid
JOIN courses c1 ON en1.courseid = c1.courseid AND c1.coursename = 'Math'
JOIN enrollments en2 ON s.studentid = en2.studentid
JOIN courses c2 ON en2.courseid = c2.courseid AND c2.coursename = 'English';
```

## Write a query to find the names of students who are not enrolled in any course using the NOT IN clause.

```SQL
SELECT studentid, studentname
FROM students
WHERE studentid NOT IN (
	SELECT DISTINCT studentid
	FROM enrollments
);
```

## Write a query to retrieve the names of students who are enrolled in at least one course using the EXISTS clause.

```SQL
SELECT studentid, studentname
FROM students
WHERE EXISTS (
	SELECT 1
	FROM enrollments
	WHERE enrollments.studentid = students.studentid
);
```

## Write a query to find the names of students who are not enrolled in any course using the NOT EXISTS clause.
```SQL
SELECT studentid, studentname
FROM students
WHERE NOT EXISTS (
	SELECT 1
	FROM enrollments
	WHERE enrollments.studentid = students.studentid
);
```
