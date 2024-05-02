
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
# Joins - Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
# Joins - Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
# Joins - Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
# Joins - Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
# Joins - Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
# Joins - BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.