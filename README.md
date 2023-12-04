1. Selezionare tutti gli studenti nati nel 1990 (160)

    - SELECT * FROM `students` WHERE `date_of_birth` LIKE '1990-%';
    - SELECT * FROM `students` WHERE `date_of_birth` BETWEEN '1990-01-01' AND '1990-12-31';
    - SELECT * FROM `students` WHERE YEAR(`date_of_birth`) = '1990';

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

    - SELECT * FROM `courses` WHERE `cfu` >= 10;
    - SELECT * FROM `courses` WHERE `cfu` >= 10 AND `cfu` <= 15;

3. Selezionare tutti gli studenti che hanno più di 30 anni

    - SELECT * , DATE_FORMAT(FROM_DAYS(DATEDIFF(NOW(), `date_of_birth`)), '%Y') + 0 AS age FROM `students` WHERE DATE_FORMAT(FROM_DAYS(DATEDIFF(NOW(), `date_of_birth`)), '%Y') + 0 >= 30 ORDER BY `date_of_birth` DESC;

    - DATE_FORMAT(FROM_DAYS(DATEDIFF(NOW(),'DATE_OF_BIRTH')), '%Y').
        1. (NOW(), `date_of_birth`) = Restituisce data e ora correnti
        2. DATEDIFF() = Restituisce la differenza tra due valori di data, in anni
        3. FROM_DAYS(), '%Y' = Restituisce una data da una rappresentazione numerica del giorno
        4. DATE_FORMAT('%Y') = formatta una data come specificato, %Y  ANNO come valore numerico a 4 cifre


4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dop le 14) del 20/06/2020 (21) 

6. Selezionare tutti i corsi di laurea magistrale (38)

7. Da quanti dipartimenti è composta l'università? (12)

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)