** Ejercicio 1

# Crear una base de datos llamada call_list
'''
CREATE DATABASE call_list
'''
# En la base de datos recien creada, crear la tabla users con los campos id (clave primaria), first_name, email.
'''
CREATE TABLE users (id SERIAL PRIMARY KEY, first_name VARCHAR(50), email VARCHAR(50));
'''
# Ingresar un usuario, llamado Carlos (el resto de los datos deben inventarlos).
'''
INSERT INTO users (first_name, email) VALUES ('Carlos', 'carlos@gmail.com')
'''
# Ingresar un usuario, llamada Laura (el resto de los datos deben inventarlos).
'''
INSERT INTO users (name, email) VALUES ('Laura', 'laura@gmail.com')
'''
# Crear una tabla llamada calls con los campos id (clave primaria), phone, date, user_id (foreign key relacionado a users).
'''
CREATE TABLE calls (id SERIAL PRIMARY KEY, phone NUMERIC, date VARCHAR(50), user_id INT REFERENCES users(id));
'''
# Agregar a la tabla users el campo last_name.
'''
ALTER TABLE users ADD last_name VARCHAR(50);
'''
# Ingresar el apellido del usuario Carlos.
'''
UPDATE users SET last_name = 'Cortes' WHERE first_name = 'Carlos';
'''
# Ingresar el apellido del usuario Laura.
'''
UPDATE users SET last_name = 'Alarcon' WHERE first_name = 'Laura';
'''
# Ingresar 6 llamadas asociadas al usuario Laura.
'''
INSERT INTO calls (phone, date, user_id) VALUES ('+56922211', '10/3/18', '2');

INSERT INTO calls (phone, date, user_id) VALUES ('+5692222333', '9/3/18', '2');     

INSERT INTO calls (phone, date, user_id) VALUES ('+569333444', '10/3/18', '2');

INSERT INTO calls (phone, date, user_id) VALUES ('+569444555', '11/3/18', '2');

INSERT INTO calls (phone, date, user_id) VALUES ('+569555666', '21/3/18', '2');

INSERT INTO calls (phone, date, user_id) VALUES ('+569666777', '1/4/18', '2');
'''
# Ingresar 4 llamadas asociadas al usuario Carlos.
'''
INSERT INTO calls (phone, date, user_id) VALUES ('+56922211', '7/5/18', '1');

INSERT INTO calls (phone, date, user_id) VALUES ('+789123123', '3/5/18', '1');

INSERT INTO calls (phone, date, user_id) VALUES ('+123123123', '13/5/18', '1');

INSERT INTO calls (phone, date, user_id) VALUES ('+343434343', '7/6/18', '1');
'''
# Crear un nuevo usuario.
'''
INSERT INTO users (first_name, email, last_name) VALUES ('Katharina', 'Katharina@gmail.com', 'Elfert');
'''
# Seleccionar la cantidad de llamados de cada uno de los usuarios (nombre de usuario y cantidad de llamadas).
'''
SELECT COUNT(user_id), first_name FROM calls RIGHT JOIN users ON calls.user_id = users.id GROUP BY users.id;

 count | first_name 
-------+------------
     0 | Katharina
     6 | Laura
     4 | Carlos
(3 rows)
'''
# Seleccionar los llamados del usuario llamado Carlos ordenados por fecha en orden descendente.
'''
SELECT * FROM calls WHERE user_id  = 1 ORDER BY date_call DESC;

 id |   phone   | date_call | user_id 
----+-----------+-----------+---------
 10 | 343434343 | 7/6/18    |       1
  2 |  56922211 | 7/5/18    |       1
  8 | 789123123 | 3/5/18    |       1
  9 | 123123123 | 13/5/18   |       1
(4 rows)
'''
# Nuevos cambios solicitados por cliente.
#"Necesito agregar a la base una tabla de auditoría que registre el motivo del borrado de una llamada y el usuario que lo efectuó."
'''
CREATE TABLE log (id SERIAL PRIMARY KEY, user_id INT REFERENCES users(id),  call_id INT REFERENCES calls(id), reason VARCHAR(100), phone_deleted NUMERIC);

    Column     |          Type          | Collation | Nullable |             Default             
---------------+------------------------+-----------+----------+---------------------------------
 id            | integer                |           | not null | nextval('log_id_seq'::regclass)
 user_id       | integer                |           |          | 
 call_id       | integer                |           |          | 
 reason        | character varying(100) |           |          | 
 phone_deleted | numeric                |           |          | 
Indexes:
    "log_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "log_call_id_fkey" FOREIGN KEY (call_id) REFERENCES calls(id)
    "log_user_id_fkey" FOREIGN KEY (user_id) REFERENCES users(id)
'''
# A partir de la base anterior, agregar este requerimiento y modelar la base de datos (agregar print de pantalla [utilizar https://www.draw.io/]).

![My image](https://github.com/Ignaciooleac/S16A31/blob/master/db%20model.png)

Alumno : Ignacio Olea
