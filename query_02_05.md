
# Group by - Contare quanti iscritti ci sono stati ogni anno
``SELECT YEAR(`enrolment_date`) AS enrolment_year, COUNT(*) AS subs_quantity FROM `students` WHERE `enrolment_date` IS NOT NULL GROUP BY enrolment_year;``
- Seleziono gli ANNI della data di iscrizione degli students in una colonna enrolment_year
- Conto tutti gli studenti che non hanno una data di iscrizione nulla in un'altra colonna subs_quantity
- Gli ragruppo per enrolemnt_year

# Group by - Contare gli insegnanti che hanno l'ufficio nello stesso edificio
``SELECT `office_address`, COUNT(*) AS same_address_quantity FROM `teachers` WHERE `office_address` IS NOT NULL GROUP BY office_address;``
- Seleziono gli office_adress dei teachers in una colonna
- Conto tutti gli indirizzi che non sono null in un'altra colonna same_address_quantity
- Gli ragruppo per office_adress

``SELECT COUNT(`office_address`) AS same_address_quantity FROM `teachers` WHERE `office_address` IS NOT NULL GROUP BY office_address;``
-  da slides, può essere utile in alcuni casi (Non selezionando dei gli office adress ho solo i numeri delle quantità)

# Group by - Calcolare la media dei voti di ogni appello d'esame
``SELECT `exam_id`, AVG(`vote`) AS average_vote FROM `exam_student` GROUP BY `exam_id`;``
- Seleziono l'id degli esami (Non ho a disposizione il nome) e faccio la media dei voti di questo esame in una colonna average_vote
- Faccio la media dei voti di questo esame in una colonna average_vote
- Ragruppo per exam_id

# Group by - Contare quanti corsi di laurea ci sono per ogni dipartimento
``SELECT `department_id`, COUNT(*) AS degrees_per_department FROM `degrees` GROUP BY `department_id`;``
- Seleziono l'id dei departments in degrees
- Conto quanti corsi di laurea ci sono per ogni dipartimento i una colonna degrees_per_department
- Ragruppo per department_id


# Joins - Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
``SELECT * FROM `students` JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` AND `degrees`.`name`= "Corso di Laurea in Economia"; ``
- Per comodità seleziono tutto con *, ma potrei chiedere info specifiche con `students`.`name`
- Faccio un JOIN tra students e degrees coinvolgendo le colonne che stabiliscono il collegamento tra loro
- Aggiungo una condizone al Join (Posso farlo anche col Where? Dopo provo)

# Joins - Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
``SELECT * FROM `degrees` JOIN `departments` ON `degrees`.`department_id`= `departments`.`id` AND `departments`.`name` = "Dipartimento di Neuroscienze" AND `degrees`.`level`= "magistrale";``
- Logica molto simile alla precedente 

# Joins - Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
``SELECT `courses`.`name` AS course_name FROM `teachers` JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id` JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id` WHERE `teachers`.`id` = 44;``
- Soluzione leggermente più complessa in quanto bisogna fare due JOIN
- Una per fare un legame tra course_teacher e id teacher
- L'altra tra courses e course_teacher.course_id
- Utilizzo WHERE per filtrare solo dove id=44 per il signor Fulvio

# Joins - Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
``SELECT `students`.`id`, `students`.`surname`, `students`.`name`, `degrees`.`name`, `departments`.`name` FROM `students` JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` JOIN `departments` ON `departments`.`id` = `degrees`.`department_id` ORDER BY `students`.`surname` ASC, `students`.`name` ASC;``
- Seleziono nom e cognome degli studenti, nome del corso di laurea, relativo dipartimento
- Faccio due JOIN (Simile es precedente)
- Utilizzo Order BY per mettere in ordine alfabetico di cohnome e poi di nome

# Joins - Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
``SELECT `degrees`.`name`, `degrees`.`level`, `degrees`.`email`, `courses`.`name`, `courses`.`description`, `teachers`.`name`, `teachers`.`surname` ``
``FROM `degrees` ``
``JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id` ``
``JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id` ``
``JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`;``

- Logica simile alla precedente ma con più JOIN
- Con la prima collego Corsidi Laurea e Corsi
- COn la seconda ricavo un rapporto per stabilire i teacher
- Con la terza ricavo il noome del teacher

# Joins - Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
- Faccio riga per riga perché mi viene meglio ragionare

-Seleziono tutti i docenti
``SELECT DISTINCT `teachers`.`*` ``
``FROM `teachers` ``

- Seleziono i docenti che hanno dei corsi in course_teacher
``JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id` ``

- Aggiungo alla selezione i corsi presenti in course_teacher
``JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id` ``

- Per arrivare al dipartimento mi serve prima:
- Selezionare i Corsi di Laurea a cui fanno riferimento i corsi
``JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id` ``

- Adesso ho un collegamento tra insegnati e Dipartimenti
``JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` ``

- Pongo la mia condizione
``WHERE departments.`name` = 'Dipartimento di Matematica'; ``



#  BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.
- Prima di tutto conto i tentativi per studente con un GROUP BY 
