<h1 style="text-align: center;">Query db-university</h1>

### 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia:
``` sql
SELECT `students`.*, `degrees`.`name` AS `degree_name`
FROM `students`
JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia'
ORDER BY `students`.`surname`, `students`.`name` ;
```

### 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze:
``` sql
SELECT `degrees`.*, `departments`.`name` AS `department_name`
FROM `degrees`
JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
WHERE `degrees`.`level` = 'magistrale'
AND `departments`.`name` = 'Dipartimento di Neuroscienze';
```
### 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44):
``` sql
SELECT `courses`.*, `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`
FROM `courses`
JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`
WHERE `teachers`.`id` = 44;
```

### 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome:
``` sql
SELECT `students`.`surname` AS `student_surname`, `students`.`name` AS `student_name`, `degrees`.`name` AS `degree`, `departments`.`name` AS `department`
FROM `students`
JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id`
JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
ORDER BY `students`.`surname`, `students`.`name`;
```

### 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti:
``` sql
SELECT DISTINCT `degrees`.`name` AS `degrees`, `courses`.`name` AS `courses`, `teachers`.`surname` AS `teacher_surname`,`teachers`.`name` AS `teachers_name`
FROM `degrees` JOIN `courses` ON `courses`.`degree_id` = `degrees`.`id`
JOIN `course_teacher` ON `course_teacher`.`course_id`
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`;
```

### 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54):
``` sql
SELECT DISTINCT `teachers`.*, `departments`.`name` AS `departments_name`
FROM `teachers`
JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id`
JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` =  'Dipartimento di Matematica'
ORDER BY `teachers`.`surname`, `teachers`.`name`;
```


### 7. BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami:
``` sql
SELECT `students`.`surname` AS `student_surname`, `students`.`name` AS `student_name`,
`courses`.`name` AS `course`, COUNT(*) AS `attempts`
FROM `exam_student`
JOIN `exams` ON `exams`.`id` = `exam_student`.`exam_id`
JOIN `students` ON `students`.`id` = `exam_student`.`student_id`
JOIN `courses` ON `courses`.`id` = `exams`.`course_id`
GROUP BY `exam_student`.`student_id`, `exams`.`course_id`
ORDER BY `students`.`surname`, `students`.`name`;
```

