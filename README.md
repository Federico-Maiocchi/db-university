1. Selezionare tutti gli studenti nati nel 1990 (160)

    -   SELECT * 
        FROM `students` 
        WHERE `date_of_birth` LIKE '1990-%';

    -   SELECT * 
        FROM `students` 
        WHERE `date_of_birth` 
        BETWEEN '1990-01-01' AND '1990-12-31';

    -   SELECT * 
        FROM `students` 
        WHERE YEAR(`date_of_birth`) = '1990';

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

    -   SELECT * 
        FROM `courses` 
        WHERE `cfu` >= 10;

    -   SELECT * 
        FROM `courses` 
        WHERE `cfu` >= 10 AND `cfu` <= 15;

3. Selezionare tutti gli studenti che hanno più di 30 anni

    -   SELECT * 
        FROM `students` 
        WHERE TIMESTAMPDIFF(YEAR, `date_of_birth`,CURRENT_DATE ) > 30;

    -   SELECT * , DATE_FORMAT(FROM_DAYS(DATEDIFF(NOW(), `date_of_birth`)),     '%Y') + 0 AS age 
        FROM `students` 
        WHERE DATE_FORMAT(FROM_DAYS(DATEDIFF(NOW(), `date_of_birth`)), '%Y') + 0 >= 30 
        ORDER BY `date_of_birth` DESC;

    - DATE_FORMAT(FROM_DAYS(DATEDIFF(NOW(),'DATE_OF_BIRTH')), '%Y').
        1. (NOW(), `date_of_birth`) = Restituisce data e ora correnti
        2. DATEDIFF() = Restituisce la differenza tra due valori di data, in anni
        3. FROM_DAYS() = Restituisce una data da una rappresentazione numerica del giorno
        4. DATE_FORMAT('%Y') = formatta una data come specificato, %Y  ANNO come valore numerico a 4 cifre

    

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

    -   SELECT * 
        FROM `courses` 
        WHERE `period` LIKE 'I semestre' 
        AND `year` LIKE 1;

    -   SELECT * 
        FROM `courses` 
        WHERE `period` = 'I semestre' 
        AND `year` = 1;

    -   SELECT * 
        FROM `courses` 
        WHERE `period` LIKE 'I%' 
        AND `year` = 1;

    -   SELECT * 
        FROM `courses` 
        WHERE `period` = 'I semestre' 
        AND `year` = '1';

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dop le 14) del 20/06/2020 (21)

    -   SELECT * 
        FROM `exams` 
        WHERE HOUR(`hour`) >= '14%' 
        AND `date` = '2020-06-20';

6. Selezionare tutti i corsi di laurea magistrale (38)

    -   SELECT * 
        FROM `degrees` 
        WHERE `level` = 'magistrale';   

7. Da quanti dipartimenti è composta l'università? (12)

    -   SELECT COUNT(`id`)   
        FROM `departments`;

    -   SELECT COUNT(*)  
        FROM `departments`;

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

    -   SELECT COUNT(*) 
        FROM `teachers` 
        WHERE `phone` IS NULL;

<!-- ////////////////////////////////////////////////////////////////////// -->

GROUP BY

1. Contare quanti iscritti ci sono stati ogni anno

    -   SELECT COUNT(*), YEAR(`enrolment_date`) AS `anno_iscrizione` 
        FROM `students`
        GROUP BY  YEAR(`enrolment_date`);

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

    -   SELECT COUNT(`id`) AS `insegnanti`,`office_address`  
        FROM `teachers`
        GROUP BY `office_address`
        <!-- HAVING COUNT(`id`) > 1; -->

3. Calcolare la media dei voti di ogni appello d'esame

    -   SELECT COUNT(`exam_id`), AVG(`vote`) AS `media_voto` 
        FROM `exam_student`
        GROUP BY `exam_id`;

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

    -   SELECT COUNT(`name`) AS `corsi_di_laurea`, `department_id`
        FROM `degrees`
        GROUP BY `department_id`;

<!-- ////////////////////////////////////////////////////////////////////// -->

INNER JOIN

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

    -   SELECT `students`.`name`,`students`.`surname`,`degrees`.`name` AS       `corse_name`
        FROM `students` 
        INNER JOIN `degrees`
        ON `degrees`.`id` = `students`.`degree_id`
        WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze

SELECT `degrees`.`level`, `departments`.`name` 
FROM `degrees`
INNER JOIN `departments`
ON `departments`.id = `degrees`.`department_id`
WHERE `degrees`.`level` = 'magistrale' 
AND `departments`.`name` = 'Dipartimento di Neuroscienze';

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

    -   SELECT `teachers`.`name`,`teachers`.`surname`, `courses`.`name` AS `courses` 
        FROM `teachers`
        INNER JOIN `course_teacher`
        ON `course_teacher`.`teacher_id` = `teachers`.`id`
        INNER JOIN `courses`
        ON `courses`.`id` = `course_teacher`.`course_id`
        WHERE `teachers`.`name` = 'Fulvio' AND `surname` = 'Amato';

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome

SELECT `students`.`surname`,`students`.`name`, `degrees`.`name`, `departments`.`name`
FROM `students`
INNER JOIN `degrees`
ON `degrees`.`id` = `students`.`degree_id`
INNER JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`
ORDER BY `students`.`surname`;

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18.


