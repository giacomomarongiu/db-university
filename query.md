# Selezionare tutti gli studenti nati nel 1990 (160)
`` - SELECT * FROM `students` WHERE date_of_birth LIKE '1990-%';``  
- (LIKE è più comunemente usato con le stringhe)  
`` - SELECT * FROM `students` WHERE YEAR(date_of_birth) = 1990;``  
- (YEAR è una funzione che mi rende l'anno della data)  
`` - SELECT * FROM `students` WHERE EXTRACT(YEAR FROM date_of_birth) = 1990;``  
- (Mi permette di estrarre una 'part' della data con questa sintassi: EXTRACT(part FROM date))      

# Selezionare tutti i corsi che valgono più di 10 crediti (479)
`` - SELECT 'cfu' FROM `courses` WHERE cfu > 10;    ``

# Selezionare tutti gli studenti che hanno più di 30 anni
`` - SELECT * FROM `students` WHERE date_of_birth <= '1994-04-24'; ``(3702)  
- (Soluzione valida ma potrebbe capitare che la mia colonna non sia in formato DATE)  
`` - SELECT * FROM `students` WHERE CONVERT(date_of_birth, DATE) <= '1994-04-24';``
- (Qui converto il mio dato in formato DATE e poi lo confornto)  
`` - SELECT * FROM `students` WHERE date_of_birth <= DATE_SUB(NOW(), INTERVAL 30 YEAR);``  
- (Soluzione interessante che mi permette di ottenere un risultato costante nel tempo:  
 La funzione NOW mi restituisce la data corrente  
 La funzione DATE_SUB mi permette di definire un intervallo di tempo fisso (30 anni in questo caso))      

# Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)
`` - SELECT * FROM `courses`WHERE period = 'I semestre' and year = 1;``  
- (Modo valido, ma online consigliano molto le "tuple")  
`` - SELECT * FROM `courses` WHERE (period, year) = ('I semestre', 1);``  
- (Costruisci una 'tupla'(mini-riga?) dove inserisco solo period e year)  
- (Confronto poi la mia mini-riga con i valori che desidero e mi renderà solo le righe in cui le condizioni sono entrambe vere)     

# Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)
`` - SELECT * FROM `exams` WHERE hour >= '14:00:00' and date = '2020-06-20';  ``    

# Selezionare tutti i corsi di laurea magistrale (38)
`` - SELECT * FROM `degrees` WHERE level = 'magistrale';``  
`` - SELECT * FROM degrees WHERE level IN ('magistrale');``  
- (Soluzioni simili, IN è utile perché permette di cercare più di un valore ('stringa1'.'stringa2',...n))      

# Da quanti dipartimenti è composta l'università? (12)
`` - SELECT COUNT(*) as numer_of_departments FROM `departments`;``  
- (Da non confondere con l'id, che potrebbe coincidere essendo AI, ma non sempre (es. rimozione di una riga))    

# Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
`` - SELECT * FROM `teachers` WHERE phone is NULL;  ``   

# BONUS Contare quanti corsi "magistrale" e quanti "triennale" ci sono
`` - SELECT 'level', COUNT(*) AS degrees_quantity FROM `degrees` WHERE level IN ('magistrale', 'triennale') GROUP BY level;   ``   
- (Sto dicendo di:   
 selezionare la colonna level all'interno della tabella degrees  
 all'interno della colonna contare tutti gli elementi definiti come degrees_quantity  
 Torna utile IN in quanto voglio contare non una, ma due stringhe  
 con l'istruzione GROUP BY posso raggruppare le righe che hanno gli stessi valori in righe di riepilogo  
 Se cancello il GRUOP BY quello che ottengo è il conteggio dei degrees che hanno come valore ('magistrale', 'triennale'), in questo caso, tutti)      




 # Live 02/05 - Selezionare tutti i corsi del Corso di Laurea in Informatica
 ``SELECT `courses`.`name`,`courses`.`year` AS `degree_name` FROM `courses` JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id` WHERE `degrees`.`name` = 'Corso di Laurea in Informatica';``

 # Live 02/05 -  Selezionare le informazioni sul corso con id = 144, con tutti i relativi appelli d’esame
``SELECT courses. id, e tutte le proprietà che vuoi exams.id FROM courses JOIN exams ON courses.id = exams.course_id WHERE courses.id=144``

# Live 02/05 - Selezionare a quale dipartimento appartiene il Corso di Laurea in Diritto dell'Economia (Dipartimento di Scienze politiche, giuridiche e studi internazionali)
``SELECT * FROM `departments` JOIN `degrees` ON `degrees`.`department_id`= `departments`.`id` WHERE `degrees`.`name` = "Corso di Laurea in Diritto dell'Economia";``



