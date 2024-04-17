

```sql
CREATE TABLE departamento(
	codigo INT(10) PRIMARY KEY,
	nombre VARCHAR(100) NOT NULL,
	presupuesto DOUBLE NOT NULL,
	gastos DOUBLE NOT NULL
	);

CREATE TABLE empleado(
	id INT(10) PRIMARY KEY,
	nif VARCHAR(9) NOT NULL, 
	nombre VARCHAR(100) NOT NULL,
	apellido1 VARCHAR(100) NOT NULL,
	apellido2 VARCHAR(100),
	codigo_departamento INT(10),
	CONSTRAINT FK_departamento FOREIGN KEY (codigo_departamento) REFERENCES departamento(codigo)
	);
-- departamento
+-------------+--------------+------+-----+---------+-------+
| Field       | Type         | Null | Key | Default | Extra |
+-------------+--------------+------+-----+---------+-------+
| codigo      | int          | NO   | PRI | NULL    |       |
| nombre      | varchar(100) | NO   |     | NULL    |       |
| presupuesto | double       | NO   |     | NULL    |       |
| gastos      | double       | NO   |     | NULL    |       |
+-------------+--------------+------+-----+---------+-------+
-- empleado
+---------------------+--------------+------+-----+---------+-------+
| Field               | Type         | Null | Key | Default | Extra |
+---------------------+--------------+------+-----+---------+-------+
| id                  | int          | NO   | PRI | NULL    |       |
| nif                 | varchar(9)   | NO   |     | NULL    |       |
| nombre              | varchar(100) | NO   |     | NULL    |       |
| apellido1           | varchar(100) | NO   |     | NULL    |       |
| apellido2           | varchar(100) | YES  |     | NULL    |       |
| codigo_departamento | int          | YES  | MUL | NULL    |       |
+---------------------+--------------+------+-----+---------+-------+
```



## **Consultas sobre una tabla**

1. Lista el primer apellido de todos los empleados.

   ```sql
   select apellido1
   from empleado
   
   +-----------+
   | apellido1 |
   +-----------+
   | Rivero    |
   | Salas     |
   | Rubio     |
   | Suárez    |
   | Loyola    |
   | Santana   |
   | Ruiz      |
   | Ruiz      |
   | Gómez     |
   | Flores    |
   | Herrera   |
   | Salas     |
   | Sáez      |
   +-----------+
   ```

2. Lista el primer apellido de los empleados eliminando los apellidos que estén repetidos.

  ```sql
  select distinct apellido1
  from empleado
  +-----------+
  | apellido1 |
  +-----------+
  | Rivero    |
  | Salas     |
  | Rubio     |
  | Suárez    |
  | Loyola    |
  | Santana   |
  | Ruiz      |
  | Gómez     |
  | Flores    |
  | Herrera   |
  | Sáez      |
  +-----------+
  ```

  

3. Lista todas las columnas de la tabla empleado.

   ```sql
   select id, nif, nombre, apellido1, apellido2, codigo_departamento
   from empleado;	
   +----+-----------+--------------+-----------+-----------+---------------------+
   | id | nif       | nombre       | apellido1 | apellido2 | codigo_departamento |
   +----+-----------+--------------+-----------+-----------+---------------------+
   |  1 | 32481596F | Aarón        | Rivero    | Gómez     |                   1 |
   |  2 | Y5575632D | Adela        | Salas     | Díaz      |                   2 |
   |  3 | R6970642B | Adolfo       | Rubio     | Flores    |                   3 |
   |  4 | 77705545E | Adrián       | Suárez    | NULL      |                   4 |
   |  5 | 17087203C | Marcos       | Loyola    | Méndez    |                   5 |
   |  6 | 38382980M | María        | Santana   | Moreno    |                   1 |
   |  7 | 80576669X | Pilar        | Ruiz      | NULL      |                   2 |
   |  8 | 71651431Z | Pepe         | Ruiz      | Santana   |                   3 |
   |  9 | 56399183D | Juan         | Gómez     | López     |                   2 |
   | 10 | 46384486H | Diego        | Flores    | Salas     |                   5 |
   | 11 | 67389283A | Marta        | Herrera   | Gil       |                   1 |
   | 12 | 41234836R | Irene        | Salas     | Flores    |                NULL |
   | 13 | 82635162B | Juan Antonio | Sáez      | Guerrero  |                NULL |
   +----+-----------+--------------+-----------+-----------+---------------------+
   ```

   

4. Lista el nombre y los apellidos de todos los empleados.

   ```sql
   select nombre, apellido1, apellido2
   from empleado;	
   +--------------+-----------+-----------+
   | nombre       | apellido1 | apellido2 |
   +--------------+-----------+-----------+
   | Aarón        | Rivero    | Gómez     |
   | Adela        | Salas     | Díaz      |
   | Adolfo       | Rubio     | Flores    |
   | Adrián       | Suárez    | NULL      |
   | Marcos       | Loyola    | Méndez    |
   | María        | Santana   | Moreno    |
   | Pilar        | Ruiz      | NULL      |
   | Pepe         | Ruiz      | Santana   |
   | Juan         | Gómez     | López     |
   | Diego        | Flores    | Salas     |
   | Marta        | Herrera   | Gil       |
   | Irene        | Salas     | Flores    |
   | Juan Antonio | Sáez      | Guerrero  |
   +--------------+-----------+-----------+
   ```

   

5. Lista el identificador de los departamentos de los empleados que aparecen en la tabla empleado.

  ```sql
  select codigo_departamento
  from empleado;
  +---------------------+
  | codigo_departamento |
  +---------------------+
  |                NULL |
  |                NULL |
  |                   1 |
  |                   1 |
  |                   1 |
  |                   2 |
  |                   2 |
  |                   2 |
  |                   3 |
  |                   3 |
  |                   4 |
  |                   5 |
  |                   5 |
  +---------------------+
  ```

  

6. Lista el identificador de los departamentos de los empleados que aparecen en la tabla empleado, eliminando los identificadores que aparecen repetidos.

  ```sql
  select distinct codigo_departamento
  from empleado
  +---------------------+
  | codigo_departamento |
  +---------------------+
  |                NULL |
  |                   1 |
  |                   2 |
  |                   3 |
  |                   4 |
  |                   5 |
  +---------------------+
  ```

  

7. Lista el nombre y apellidos de los empleados en una única columna.

   ```sql
   select concat (nombre, ' ', apellido1) as nombre_completo
   from empleado
   +--------------------+
   | nombre_completo    |
   +--------------------+
   | Aarón Rivero       |
   | Adela Salas        |
   | Adolfo Rubio       |
   | Adrián Suárez      |
   | Marcos Loyola      |
   | María Santana      |
   | Pilar Ruiz         |
   | Pepe Ruiz          |
   | Juan Gómez         |
   | Diego Flores       |
   | Marta Herrera      |
   | Irene Salas        |
   | Juan Antonio Sáez  |
   +--------------------+
   ```

   

8. Lista el nombre y apellidos de los empleados en una única columna, convirtiendo todos los caracteres en mayúscula.

  ```sql
  select concat(upper(nombre), ' ', upper(apellido1)) as nombre_completo
  from empleado
  +--------------------+
  | nombre_completo    |
  +--------------------+
  | AARÓN RIVERO       |
  | ADELA SALAS        |
  | ADOLFO RUBIO       |
  | ADRIÁN SUÁREZ      |
  | MARCOS LOYOLA      |
  | MARÍA SANTANA      |
  | PILAR RUIZ         |
  | PEPE RUIZ          |
  | JUAN GÓMEZ         |
  | DIEGO FLORES       |
  | MARTA HERRERA      |
  | IRENE SALAS        |
  | JUAN ANTONIO SÁEZ  |
  +--------------------+
  ```

  

9. Lista el nombre y apellidos de los empleados en una única columna, convirtiendo todos los caracteres en minúscula.

  ```sql
  select concat(lower(nombre), ' ', lower(apellido1)) as nombre_completo
  from empleado
  +--------------------+
  | nombre_completo    |
  +--------------------+
  | aarón rivero       |
  | adela salas        |
  | adolfo rubio       |
  | adrián suárez      |
  | marcos loyola      |
  | maría santana      |
  | pilar ruiz         |
  | pepe ruiz          |
  | juan gómez         |
  | diego flores       |
  | marta herrera      |
  | irene salas        |
  | juan antonio sáez  |
  +--------------------+
  ```

  

10. Lista el identificador de los empleados junto al nif, pero el nif deberá aparecer en dos columnas, una mostrará únicamente los dígitos del nif y la otra la letra.

    ```
    
    ```

    

11. Lista el nombre de cada departamento y el valor del presupuesto actual del que dispone. Para calcular este dato tendrá que restar al valor del presupuesto inicial (columna presupuesto) los gastos que se han generado (columna gastos). Tenga en cuenta que en algunos casos pueden existir valores negativos. Utilice un alias apropiado para la nueva columna columna que está calculando.

12. Lista el nombre de los departamentos y el valor del presupuesto actual ordenado de forma ascendente.

13. Lista el nombre de todos los departamentos ordenados de forma ascendente.

14. Lista el nombre de todos los departamentos ordenados de forma descendente.

15. Lista los apellidos y el nombre de todos los empleados, ordenados de forma alfabética tendiendo en cuenta en primer lugar sus apellidos y luego su nombre.

16. Devuelve una lista con el nombre y el presupuesto, de los 3 departamentos que tienen mayor presupuesto.

17. Devuelve una lista con el nombre y el presupuesto, de los 3 departamentos que tienen menor presupuesto.

18. Devuelve una lista con el nombre y el gasto, de los 2 departamentos que tienen mayor gasto.

19. Devuelve una lista con el nombre y el gasto, de los 2 departamentos que tienen menor gasto.

20. Devuelve una lista con 5 filas a partir de la tercera fila de la tabla empleado. La tercera fila se debe incluir en la respuesta. La respuesta debe incluir todas las columnas de la tabla empleado.

21. Devuelve una lista con el nombre de los departamentos y el presupuesto, de aquellos que tienen un presupuesto mayor o igual a 150000 euros.

22. Devuelve una lista con el nombre de los departamentos y el gasto, de aquellos que tienen menos de 5000 euros de gastos.

23. Devuelve una lista con el nombre de los departamentos y el presupuesto, de aquellos que tienen un presupuesto entre 100000 y 200000 euros. Sin utilizar el operador BETWEEN.

24. Devuelve una lista con el nombre de los departamentos que no tienen un presupuesto entre 100000 y 200000 euros. Sin utilizar el operador BETWEEN.

25. Devuelve una lista con el nombre de los departamentos que tienen un presupuesto entre 100000 y 200000 euros. Utilizando el operador BETWEEN.

26. Devuelve una lista con el nombre de los departamentos que no tienen un presupuesto entre 100000 y 200000 euros. Utilizando el operador BETWEEN.

27. Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean mayores que el presupuesto del que disponen.

28. Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean menores que el presupuesto del que disponen.

29. Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean iguales al presupuesto del que disponen.

30. Lista todos los datos de los empleados cuyo segundo apellido sea NULL.

31. Lista todos los datos de los empleados cuyo segundo apellido no sea NULL.

32. Lista todos los datos de los empleados cuyo segundo apellido sea López.

33. Lista todos los datos de los empleados cuyo segundo apellido sea Díaz o Moreno. Sin utilizar el operador IN.

34. Lista todos los datos de los empleados cuyo segundo apellido sea Díaz o Moreno. Utilizando el operador IN.

35. Lista los nombres, apellidos y nif de los empleados que trabajan en el departamento 3.

36. Lista los nombres, apellidos y nif de los empleados que trabajan en los departamentos 2, 4 o 5.

Consultas multitabla (Composición interna)
Resuelva todas las consultas utilizando la sintaxis de SQL1 y SQL2.
1. Devuelve un listado con los empleados y los datos de los departamentos
donde trabaja cada uno.
2. Devuelve un listado con los empleados y los datos de los departamentos
donde trabaja cada uno. Ordena el resultado, en primer lugar por el nombre
del departamento (en orden alfabético) y en segundo lugar por los apellidos
y el nombre de los empleados.
3. Devuelve un listado con el identificador y el nombre del departamento,
solamente de aquellos departamentos que tienen empleados.
4. Devuelve un listado con el identificador, el nombre del departamento y el
valor del presupuesto actual del que dispone, solamente de aquellos
departamentos que tienen empleados. El valor del presupuesto actual lo
puede calcular restando al valor del presupuesto inicial
(columna presupuesto) el valor de los gastos que ha generado
(columna gastos).
5. Devuelve el nombre del departamento donde trabaja el empleado que tiene
el nif 38382980M.

6. Devuelve el nombre del departamento donde trabaja el empleado Pepe Ruiz
Santana.
7. Devuelve un listado con los datos de los empleados que trabajan en el
departamento de I+D. Ordena el resultado alfabéticamente.
8. Devuelve un listado con los datos de los empleados que trabajan en el
departamento de Sistemas, Contabilidad o I+D. Ordena el resultado
alfabéticamente.
9. Devuelve una lista con el nombre de los empleados que tienen los
departamentos que no tienen un presupuesto entre 100000 y 200000 euros.
10. Devuelve un listado con el nombre de los departamentos donde existe
algún empleado cuyo segundo apellido sea NULL. Tenga en cuenta que no
debe mostrar nombres de departamentos que estén repetidos.

Consultas multitabla (Composición externa)
Resuelva todas las consultas utilizando las cláusulas LEFT JOIN y RIGHT JOIN.
1. Devuelve un listado con todos los empleados junto con los datos de los
departamentos donde trabajan. Este listado también debe incluir los
empleados que no tienen ningún departamento asociado.
2. Devuelve un listado donde sólo aparezcan aquellos empleados que no
tienen ningún departamento asociado.
3. Devuelve un listado donde sólo aparezcan aquellos departamentos que no
tienen ningún empleado asociado.
4. Devuelve un listado con todos los empleados junto con los datos de los
departamentos donde trabajan. El listado debe incluir los empleados que no
tienen ningún departamento asociado y los departamentos que no tienen
ningún empleado asociado. Ordene el listado alfabéticamente por el
nombre del departamento.
5. Devuelve un listado con los empleados que no tienen ningún departamento
asociado y los departamentos que no tienen ningún empleado asociado.
Ordene el listado alfabéticamente por el nombre del departamento.

Consultas resumen
1. Calcula la suma del presupuesto de todos los departamentos.
2. Calcula la media del presupuesto de todos los departamentos.
3. Calcula el valor mínimo del presupuesto de todos los departamentos.
4. Calcula el nombre del departamento y el presupuesto que tiene asignado,
del departamento con menor presupuesto.
5. Calcula el valor máximo del presupuesto de todos los departamentos.
6. Calcula el nombre del departamento y el presupuesto que tiene asignado,
del departamento con mayor presupuesto.
7. Calcula el número total de empleados que hay en la tabla empleado.
8. Calcula el número de empleados que no tienen NULL en su segundo
apellido.
9. Calcula el número de empleados que hay en cada departamento. Tienes que
devolver dos columnas, una con el nombre del departamento y otra con el
número de empleados que tiene asignados.
10. Calcula el nombre de los departamentos que tienen más de 2 empleados. El
resultado debe tener dos columnas, una con el nombre del departamento y
otra con el número de empleados que tiene asignados.
11. Calcula el número de empleados que trabajan en cada uno de los
departamentos. El resultado de esta consulta también tiene que incluir
aquellos departamentos que no tienen ningún empleado asociado.
12. Calcula el número de empleados que trabajan en cada unos de los
departamentos que tienen un presupuesto mayor a 200000 euros.

Subconsultas
Con operadores básicos de comparación
1. Devuelve un listado con todos los empleados que tiene el departamento
de Sistemas. (Sin utilizar INNER JOIN).
2. Devuelve el nombre del departamento con mayor presupuesto y la cantidad
que tiene asignada.
3. Devuelve el nombre del departamento con menor presupuesto y la cantidad
que tiene asignada.
Subconsultas con ALL y ANY
4. Devuelve el nombre del departamento con mayor presupuesto y la cantidad
que tiene asignada. Sin hacer uso de MAX, ORDER BY ni LIMIT.
5. Devuelve el nombre del departamento con menor presupuesto y la cantidad
que tiene asignada. Sin hacer uso de MIN, ORDER BY ni LIMIT.
6. Devuelve los nombres de los departamentos que tienen empleados
asociados. (Utilizando ALL o ANY).
7. Devuelve los nombres de los departamentos que no tienen empleados
asociados. (Utilizando ALL o ANY).
Subconsultas con IN y NOT IN
8. Devuelve los nombres de los departamentos que tienen empleados
asociados. (Utilizando IN o NOT IN).
9. Devuelve los nombres de los departamentos que no tienen empleados
asociados. (Utilizando IN o NOT IN).
Subconsultas con EXISTS y NOT EXISTS
10. Devuelve los nombres de los departamentos que tienen empleados
asociados. (Utilizando EXISTS o NOT EXISTS).
11. Devuelve los nombres de los departamentos que tienen empleados
asociados. (Utilizando EXISTS o NOT EXISTS).

