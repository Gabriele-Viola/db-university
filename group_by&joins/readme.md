# Group by:
1. Contare quanti iscritti ci sono stati ogni anno

SELECT count(`id`), YEAR(`enrolment_date`)
FROM `students`
GROUP BY YEAR(`enrolment_date`)

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

SELECT count(`id`) AS `id_teacher`, `office_address`
FROM `teachers`
GROUP BY `office_address`

3. Calcolare la media dei voti di ogni appello d'esame

SELECT AVG(`vote`), `exam_id`
FROM `exam_student`
GROUP BY `exam_id`

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

SELECt COUNT(`id`), `degree_id`  
FROM `courses`
GROUP BY `degree_id`


# Joins:
1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT `students`.`id` AS `student_id`,
`students`.`name` AS `student_name`,
`degrees`.`id` AS `degree_id`,
`degrees`.`name` AS `degree_name`
FROM `students`
JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` =  'Corso di Laurea in Economia'

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

SELECT `degrees`.`id` AS `degree_id`, 
`degrees`.`name` AS `degree_name`,
`degrees`.`level`,
`departments`.`id` AS `department_id`,
`departments`.`name` AS `department_name`
FROM `degrees`
JOIN `departments`
ON `department_id` = `departments`.`id` 
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze'
AND `degrees`.`level` = 'Magistrale'


3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT `courses`.`id` AS `course_id`,
`courses`.`name` AS `course_name`,
`teachers`.`name`
from `courses`
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`
WHERE `teachers`.`id` = 44

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

SELECT `students`.`id` AS `student_id`,
`students`.`surname` AS `student_surname`,
`students`.`name` AS `student_name`,
`degrees`.`id` AS `degree_id`,
`degrees`.`name` AS `degree_name`,
`departments`.`id` AS `department_id`,
`departments`.`name` AS `department_name`
FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname`

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

SELECT `degrees`.`id` AS `degree_id`,
`degrees`.`name` AS `degree_name`,
`courses`.`id` AS `course_id`,
`courses`.`name` AS `course_name`,
`teachers`.`id` AS `teacher_id`,
`teachers`.`name` AS `teachers_name`
FROM `degrees` 
JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

SELECT DISTINCT `teachers`.`id` AS `teacher_id`,
`teachers`.`name` AS `teacher_name`,
`departments`.`id` AS `departmente_id`,
`departments`.`name` AS `departmanet_name`
FROM `teachers`
JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id`
JOIN `departments` ON `departments`.`id` =  `degrees`.`department_id`
WHERE `departments`.`name` = 'Dipartimento di Matematica'

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

SELECT `student_id`, `exam_id`,
COUNT(*) AS `numb_of_try`,
MAX(vote) AS `max_vote`
FROM `exam_student`
WHERE `vote` >= 18 
GROUP BY `student_id`, `exam_id`
HAVING MIN(`vote`) <= 18