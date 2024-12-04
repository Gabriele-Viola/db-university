1. Selezionare tutti gli studenti nati nel 1990 (160)

SELECT *
FROM univesity_db.students
WHERE YEAR(date_of_birth) = 1990;

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

SELECT * FROM univesity_db.courses
WHERE cfu > 10;

3. Selezionare tutti gli studenti che hanno più di 30 anni

SELECT * FROM univesity_db.students
WHERE year(date_of_birth) <= 2024-30
and month(date_of_birth) < 12
and day(date_of_birth) < 4;

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

SELECT * FROM univesity_db.courses
where `period` = 'I semestre'
And `year` = 1;

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

SELECT * FROM univesity_db.exams
where `date` = '2020-06-20'
and `hour` > '14:00:00';

6. Selezionare tutti i corsi di laurea magistrale (38)

SELECT * FROM univesity_db.degrees
where `level` = 'magistrale';

7. Da quanti dipartimenti è composta l'università? (12)

SELECT COUNT(`id`) FROM univesity_db.departments;

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

SELECT * FROM univesity_db.teachers
Where isnull(phone);

9. Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo degree_id, inserire un valore casuale)

insert into univesity_db.students (`degree_id`, `name`, `surname`, `date_of_birth`, `fiscal_code`, `enrolment_date`, `registration_number`, `email`)
value(33, 'Gabriele', 'Viola', '1993-02-02', 'ABCCBA34N25H100P', '2024-08-28', 123456, 'GIOVA@GIOVA.IT');

10. Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126

UPDATE univesity_db.teachers 
set `office_number` = '126'
where `id` = 58;

11. Eliminare dalla tabella studenti il record creato precedentemente al punto 9

delete from univesity_db.students
where `id` = 5002;