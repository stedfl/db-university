<h1 style="text-align: center;">Query db-university</h1>

### 1. Contare quanti iscritti ci sono stati ogni anno:
``` sql
SELECT COUNT(*) AS `total_enrolled_students`, YEAR(`enrolment_date`) AS `year_of_enrolment`
FROM `students`
GROUP BY `year_of_enrolment`;
```

### 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio:
``` sql
SELECT COUNT(*) AS `total_teachers`, `office_address`
FROM `teachers`
GROUP BY `office_address`;
```

### 3. Calcolare la media dei voti di ogni appello d'esame:
``` sql
SELECT AVG(`vote`) AS `average_votes`, `exam_id` AS `exam`
FROM `exam_student`
GROUP BY `exam_id`;
```

### 4. Contare quanti corsi di laurea ci sono per ogni dipartimento:
``` sql
SELECT COUNT(*) AS `total_degrees`, `department_id`
FROM `degrees`
GROUP BY `department_id`;
```
