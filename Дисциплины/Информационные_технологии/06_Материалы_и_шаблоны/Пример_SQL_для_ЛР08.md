# Пример SQL для лабораторной работы № 8

Учебный пример для локальной SQLite. Выполняется в консоли sqlite3 или DB Browser for SQLite. Включение внешних ключей выполняется на каждом соединении.

```sql
PRAGMA foreign_keys = ON;
CREATE TABLE Students (
  student_id INTEGER PRIMARY KEY,
  full_name TEXT NOT NULL
);
CREATE TABLE Courses (
  course_id INTEGER PRIMARY KEY,
  title TEXT NOT NULL
);
CREATE TABLE Enrollments (
  student_id INTEGER NOT NULL,
  course_id INTEGER NOT NULL,
  registered_at TEXT NOT NULL,
  PRIMARY KEY (student_id, course_id),
  FOREIGN KEY (student_id) REFERENCES Students(student_id),
  FOREIGN KEY (course_id) REFERENCES Courses(course_id)
);
INSERT INTO Students VALUES (1,'Ученик 1'),(2,'Ученик 2'),(3,'Ученик 3');
INSERT INTO Courses VALUES (1,'Python'),(2,'SQL'),(3,'Аналитика');
INSERT INTO Enrollments VALUES
  (1,1,'2026-09-01'),(1,2,'2026-09-02'),
  (2,1,'2026-09-03'),(3,3,'2026-09-04'),(3,1,'2026-09-05');
SELECT c.title, COUNT(*) AS registrations
FROM Courses c LEFT JOIN Enrollments e ON c.course_id = e.course_id
GROUP BY c.course_id, c.title
ORDER BY registrations DESC, c.title;
```

**Самостоятельно:** расширьте Students и Courses минимум до пяти записей каждую, создайте дополнительное зачисление и независимо проверьте агрегированный результат. Данные о людях в примере синтетические.
