1. Selezionare tutti gli studenti nati nel 1990 (160)
    - SELECT * FROM `students` WHERE `date_of_birth` LIKE '1990-%';
    - SELECT * FROM `students` WHERE `date_of_birth` BETWEEN '1990-01-01' AND '1990-12-31';
    - SELECT * FROM `students` WHERE YEAR(`date_of_birth`) = '1990';

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
    - SELECT * FROM `courses` WHERE `cfu` >= 10;
    - SELECT * FROM `courses` WHERE `cfu` >= 10 AND `cfu` <= 15;

3. Selezionare tutti gli studenti che hanno più di 30 anni 

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dop le 14) del 20/06/2020 (21) 