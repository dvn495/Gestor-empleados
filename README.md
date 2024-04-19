

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

    ```sql
    select id, substring(nif,1, length(nif)-1 ), substring(nif,-1)
    from empleado
    +----+----------------------------------+-------------------+
    | id | substring(nif,1, length(nif)-1 ) | substring(nif,-1) |
    +----+----------------------------------+-------------------+
    |  1 | 32481596                         | F                 |
    |  2 | Y5575632                         | D                 |
    |  3 | R6970642                         | B                 |
    |  4 | 77705545                         | E                 |
    |  5 | 17087203                         | C                 |
    |  6 | 38382980                         | M                 |
    |  7 | 80576669                         | X                 |
    |  8 | 71651431                         | Z                 |
    |  9 | 56399183                         | D                 |
    | 10 | 46384486                         | H                 |
    | 11 | 67389283                         | A                 |
    | 12 | 41234836                         | R                 |
    | 13 | 82635162                         | B                 |
    +----+----------------------------------+-------------------+
    ```

    

11. Lista el nombre de cada departamento y el valor del presupuesto actual del que dispone. Para calcular este dato tendrá que restar al valor del presupuesto inicial (columna presupuesto) los gastos que se han generado (columna gastos). Tenga en cuenta que en algunos casos pueden existir valores negativos. Utilice un alias apropiado para la nueva columna columna que está calculando.

    ```sql
    select nombre, (presupuesto-gastos) as presupuesto_actual
    from departamento
    +------------------+--------------------+
    | nombre           | presupuesto_actual |
    +------------------+--------------------+
    | Desarrollo       |             114000 |
    | Sistemas         |             129000 |
    | Recursos Humanos |             255000 |
    | Contabilidad     |             107000 |
    | I+D              |              -5000 |
    | Proyectos        |                  0 |
    | Publicidad       |              -1000 |
    +------------------+--------------------+
    ```

    

12. Lista el nombre de los departamentos y el valor del presupuesto actual ordenado de forma ascendente.

    ```sql
    select nombre, (presupuesto-gastos) as presupuesto_actual
    from departamento
    order by presupuesto_actual asc
    +------------------+--------------------+
    | nombre           | presupuesto_actual |
    +------------------+--------------------+
    | I+D              |              -5000 |
    | Publicidad       |              -1000 |
    | Proyectos        |                  0 |
    | Contabilidad     |             107000 |
    | Desarrollo       |             114000 |
    | Sistemas         |             129000 |
    | Recursos Humanos |             255000 |
    +------------------+--------------------+
    ```

    

13. Lista el nombre de todos los departamentos ordenados de forma ascendente.

    ```sql
    select nombre
    from departamento
    order by nombre asc
    +------------------+
    | nombre           |
    +------------------+
    | Contabilidad     |
    | Desarrollo       |
    | I+D              |
    | Proyectos        |
    | Publicidad       |
    | Recursos Humanos |
    | Sistemas         |
    +------------------+
    ```

    

14. Lista el nombre de todos los departamentos ordenados de forma descendente.

    ```sql
    select nombre
    from departamento
    order by nombre desc
    +------------------+
    | nombre           |
    +------------------+
    | Sistemas         |
    | Recursos Humanos |
    | Publicidad       |
    | Proyectos        |
    | I+D              |
    | Desarrollo       |
    | Contabilidad     |
    +------------------+
    ```

    

15. Lista los apellidos y el nombre de todos los empleados, ordenados de forma alfabética tendiendo en cuenta en primer lugar sus apellidos y luego su nombre.

    ```sql
    select apellido1, apellido2, nombre 
    from empleado
    order by apellido1 asc
    +-----------+-----------+--------------+
    | apellido1 | apellido2 | nombre       |
    +-----------+-----------+--------------+
    | Flores    | Salas     | Diego        |
    | Gómez     | López     | Juan         |
    | Herrera   | Gil       | Marta        |
    | Loyola    | Méndez    | Marcos       |
    | Rivero    | Gómez     | Aarón        |
    | Rubio     | Flores    | Adolfo       |
    | Ruiz      | NULL      | Pilar        |
    | Ruiz      | Santana   | Pepe         |
    | Sáez      | Guerrero  | Juan Antonio |
    | Salas     | Díaz      | Adela        |
    | Salas     | Flores    | Irene        |
    | Santana   | Moreno    | María        |
    | Suárez    | NULL      | Adrián       |
    +-----------+-----------+--------------+
    ```

    

16. Devuelve una lista con el nombre y el presupuesto, de los 3 departamentos que tienen mayor presupuesto.

    ```sql
    select nombre, presupuesto
    from departamento 
    order by presupuesto desc
    limit 0,3
    +------------------+-------------+
    | nombre           | presupuesto |
    +------------------+-------------+
    | I+D              |      375000 |
    | Recursos Humanos |      280000 |
    | Sistemas         |      150000 |
    +------------------+-------------+
    ```

    

17. Devuelve una lista con el nombre y el presupuesto, de los 3 departamentos que tienen menor presupuesto.

    ```sql
    select nombre, presupuesto
    from departamento 
    order by presupuesto asc
    limit 0,3
    +--------------+-------------+
    | nombre       | presupuesto |
    +--------------+-------------+
    | Proyectos    |           0 |
    | Publicidad   |           0 |
    | Contabilidad |      110000 |
    +--------------+-------------+
    ```

    

18. Devuelve una lista con el nombre y el gasto, de los 2 departamentos que tienen mayor gasto.

    ```sql
    select nombre, gastos
    from departamento 
    order by gastos desc
    limit 0,2
    +------------------+--------+
    | nombre           | gastos |
    +------------------+--------+
    | I+D              | 380000 |
    | Recursos Humanos |  25000 |
    +------------------+--------+
    ```

    

19. Devuelve una lista con el nombre y el gasto, de los 2 departamentos que tienen menor gasto.

    ```sql
    select nombre, gastos
    from departamento 
    order by gastos asc
    limit 0,2
    +------------+--------+
    | nombre     | gastos |
    +------------+--------+
    | Proyectos  |      0 |
    | Publicidad |   1000 |
    +------------+--------+
    ```

    

20. Devuelve una lista con 5 filas a partir de la tercera fila de la tabla empleado. La tercera fila se debe incluir en la respuesta. La respuesta debe incluir todas las columnas de la tabla empleado.

    ```sql
    select id, nif, nombre, apellido1, apellido2, codigo_departamento
    from empleado
    limit 2,5
    +----+-----------+---------+-----------+-----------+---------------------+
    | id | nif       | nombre  | apellido1 | apellido2 | codigo_departamento |
    +----+-----------+---------+-----------+-----------+---------------------+
    |  3 | R6970642B | Adolfo  | Rubio     | Flores    |                   3 |
    |  4 | 77705545E | Adrián  | Suárez    | NULL      |                   4 |
    |  5 | 17087203C | Marcos  | Loyola    | Méndez    |                   5 |
    |  6 | 38382980M | María   | Santana   | Moreno    |                   1 |
    |  7 | 80576669X | Pilar   | Ruiz      | NULL      |                   2 |
    +----+-----------+---------+-----------+-----------+---------------------+
    ```

    

21. Devuelve una lista con el nombre de los departamentos y el presupuesto, de aquellos que tienen un presupuesto mayor o igual a 150000 euros.

    ```sql
    select nombre, presupuesto
    from departamento
    where presupuesto >= 150000
    +------------------+-------------+
    | nombre           | presupuesto |
    +------------------+-------------+
    | Sistemas         |      150000 |
    | Recursos Humanos |      280000 |
    | I+D              |      375000 |
    +------------------+-------------+
    ```

    

22. Devuelve una lista con el nombre de los departamentos y el gasto, de aquellos que tienen menos de 5000 euros de gastos.

    ```sql
    select nombre, gastos
    from departamento
    where gastos < 5000
    +--------------+--------+
    | nombre       | gastos |
    +--------------+--------+
    | Contabilidad |   3000 |
    | Proyectos    |      0 |
    | Publicidad   |   1000 |
    +--------------+--------+
    ```

    

23. Devuelve una lista con el nombre de los departamentos y el presupuesto, de aquellos que tienen un presupuesto entre 100000 y 200000 euros. Sin utilizar el operador BETWEEN.

    ```sql
    select nombre, presupuesto
    from departamento
    where presupuesto >= 100000 and presupuesto <= 200000
    +--------------+-------------+
    | nombre       | presupuesto |
    +--------------+-------------+
    | Desarrollo   |      120000 |
    | Sistemas     |      150000 |
    | Contabilidad |      110000 |
    +--------------+-------------+
    ```

    

24. Devuelve una lista con el nombre de los departamentos que no tienen un presupuesto entre 100000 y 200000 euros. Sin utilizar el operador BETWEEN.

    ```sql
    select nombre, presupuesto
    from departamento
    where presupuesto <= 100000 or presupuesto >= 200000
    
    -- alternativa:
    -- select nombre, presupuesto
    -- from departamento
    -- where not presupuesto >= 100000 or not presupuesto <= 200000
    
    +------------------+-------------+
    | nombre           | presupuesto |
    +------------------+-------------+
    | Recursos Humanos |      280000 |
    | I+D              |      375000 |
    | Proyectos        |           0 |
    | Publicidad       |           0 |
    +------------------+-------------+
    ```

    

25. Devuelve una lista con el nombre de los departamentos que tienen un presupuesto entre 100000 y 200000 euros. Utilizando el operador BETWEEN.

    ```sql
    select nombre, presupuesto
    from departamento
    where presupuesto between 100000 and 200000
    +--------------+-------------+
    | nombre       | presupuesto |
    +--------------+-------------+
    | Desarrollo   |      120000 |
    | Sistemas     |      150000 |
    | Contabilidad |      110000 |
    +--------------+-------------+
    ```

    

26. Devuelve una lista con el nombre de los departamentos que no tienen un presupuesto entre 100000 y 200000 euros. Utilizando el operador BETWEEN.

    ```sql
    select nombre, presupuesto
    from departamento
    where presupuesto not between 100000 and 200000
    +------------------+-------------+
    | nombre           | presupuesto |
    +------------------+-------------+
    | Recursos Humanos |      280000 |
    | I+D              |      375000 |
    | Proyectos        |           0 |
    | Publicidad       |           0 |
    +------------------+-------------+
    ```

    

27. Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean mayores que el presupuesto del que disponen.

    ```sql
    select nombre, gastos, presupuesto
    from departamento
    where gastos > presupuesto
    +------------+--------+-------------+
    | nombre     | gastos | presupuesto |
    +------------+--------+-------------+
    | I+D        | 380000 |      375000 |
    | Publicidad |   1000 |           0 |
    +------------+--------+-------------+
    ```

    

28. Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean menores que el presupuesto del que disponen.

    ```sql
    select nombre, gastos, presupuesto
    from departamento
    where gastos < presupuesto
    +------------------+--------+-------------+
    | nombre           | gastos | presupuesto |
    +------------------+--------+-------------+
    | Desarrollo       |   6000 |      120000 |
    | Sistemas         |  21000 |      150000 |
    | Recursos Humanos |  25000 |      280000 |
    | Contabilidad     |   3000 |      110000 |
    +------------------+--------+-------------+
    ```

    

29. Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean iguales al presupuesto del que disponen.

    ```sql
    select nombre, gastos, presupuesto
    from departamento
    where gastos = presupuesto
    +-----------+--------+-------------+
    | nombre    | gastos | presupuesto |
    +-----------+--------+-------------+
    | Proyectos |      0 |           0 |
    +-----------+--------+-------------+
    ```

    

30. Lista todos los datos de los empleados cuyo segundo apellido sea NULL.

    ```sql
    select id, nif, nombre, apellido1, apellido2, codigo_departamento
    from empleado
    where apellido2 is NULL
    +----+-----------+---------+-----------+-----------+---------------------+
    | id | nif       | nombre  | apellido1 | apellido2 | codigo_departamento |
    +----+-----------+---------+-----------+-----------+---------------------+
    |  4 | 77705545E | Adrián  | Suárez    | NULL      |                   4 |
    |  7 | 80576669X | Pilar   | Ruiz      | NULL      |                   2 |
    +----+-----------+---------+-----------+-----------+---------------------+
    ```

    

31. Lista todos los datos de los empleados cuyo segundo apellido no sea NULL.

    ```sql
    select id, nif, nombre, apellido1, apellido2, codigo_departamento
    from empleado
    where apellido2 is not NULL;
    +----+-----------+--------------+-----------+-----------+---------------------+
    | id | nif       | nombre       | apellido1 | apellido2 | codigo_departamento |
    +----+-----------+--------------+-----------+-----------+---------------------+
    |  1 | 32481596F | Aarón        | Rivero    | Gómez     |                   1 |
    |  2 | Y5575632D | Adela        | Salas     | Díaz      |                   2 |
    |  3 | R6970642B | Adolfo       | Rubio     | Flores    |                   3 |
    |  5 | 17087203C | Marcos       | Loyola    | Méndez    |                   5 |
    |  6 | 38382980M | María        | Santana   | Moreno    |                   1 |
    |  8 | 71651431Z | Pepe         | Ruiz      | Santana   |                   3 |
    |  9 | 56399183D | Juan         | Gómez     | López     |                   2 |
    | 10 | 46384486H | Diego        | Flores    | Salas     |                   5 |
    | 11 | 67389283A | Marta        | Herrera   | Gil       |                   1 |
    | 12 | 41234836R | Irene        | Salas     | Flores    |                NULL |
    | 13 | 82635162B | Juan Antonio | Sáez      | Guerrero  |                NULL |
    +----+-----------+--------------+-----------+-----------+---------------------+
    ```

    

32. Lista todos los datos de los empleados cuyo segundo apellido sea López.

    ```sql
    select id, nif, nombre, apellido1, apellido2, codigo_departamento
    from empleado
    where apellido2 = 'López';
    +----+-----------+--------+-----------+-----------+---------------------+
    | id | nif       | nombre | apellido1 | apellido2 | codigo_departamento |
    +----+-----------+--------+-----------+-----------+---------------------+
    |  9 | 56399183D | Juan   | Gómez     | López     |                   2 |
    +----+-----------+--------+-----------+-----------+---------------------+
    ```

    

33. Lista todos los datos de los empleados cuyo segundo apellido sea Díaz o Moreno. Sin utilizar el operador IN.

    ```sql
    select id, nif, nombre, apellido1, apellido2, codigo_departamento
    from empleado
    where apellido2 = 'Díaz' or apellido2 = 'Moreno';
    +----+-----------+--------+-----------+-----------+---------------------+
    | id | nif       | nombre | apellido1 | apellido2 | codigo_departamento |
    +----+-----------+--------+-----------+-----------+---------------------+
    |  2 | Y5575632D | Adela  | Salas     | Díaz      |                   2 |
    |  6 | 38382980M | María  | Santana   | Moreno    |                   1 |
    +----+-----------+--------+-----------+-----------+---------------------+
    ```

    

34. Lista todos los datos de los empleados cuyo segundo apellido sea Díaz o Moreno. Utilizando el operador IN.

    ```sql
    select id, nif, nombre, apellido1, apellido2, codigo_departamento
    from empleado
    where apellido2 in ('Díaz', 'Moreno')
    +----+-----------+--------+-----------+-----------+---------------------+
    | id | nif       | nombre | apellido1 | apellido2 | codigo_departamento |
    +----+-----------+--------+-----------+-----------+---------------------+
    |  2 | Y5575632D | Adela  | Salas     | Díaz      |                   2 |
    |  6 | 38382980M | María  | Santana   | Moreno    |                   1 |
    +----+-----------+--------+-----------+-----------+---------------------+
    ```

    

35. Lista los nombres, apellidos y nif de los empleados que trabajan en el departamento 3.

    ```sql
    select nombre, apellido1, apellido2,nif
    from empleado
    where codigo_departamento = 3
    +--------+-----------+-----------+-----------+
    | nombre | apellido1 | apellido2 | nif       |
    +--------+-----------+-----------+-----------+
    | Adolfo | Rubio     | Flores    | R6970642B |
    | Pepe   | Ruiz      | Santana   | 71651431Z |
    +--------+-----------+-----------+-----------+
    ```

    

36. Lista los nombres, apellidos y nif de los empleados que trabajan en los departamentos 2, 4 o 5.

    ```sql
    select nombre, apellido1, apellido2,nif
    from empleado
    where codigo_departamento in (2,4,5)
    +---------+-----------+-----------+-----------+
    | nombre  | apellido1 | apellido2 | nif       |
    +---------+-----------+-----------+-----------+
    | Adela   | Salas     | Díaz      | Y5575632D |
    | Pilar   | Ruiz      | NULL      | 80576669X |
    | Juan    | Gómez     | López     | 56399183D |
    | Adrián  | Suárez    | NULL      | 77705545E |
    | Marcos  | Loyola    | Méndez    | 17087203C |
    | Diego   | Flores    | Salas     | 46384486H |
    +---------+-----------+-----------+-----------+
    ```

    

## **Consultas multitabla (Composición interna)**

**Resuelva todas las consultas utilizando la sintaxis de SQL1 y SQL2.**

1. Devuelve un listado con los empleados y los datos de los departamentos donde trabaja cada uno.

  ```sql
  select concat(e.nombre,' ',e.apellido1)as nombre_empleado, d.codigo, d.nombre, d.presupuesto, d.gastos
  from empleado as e, departamento as d
  where e.codigo_departamento = d.codigo
  +-----------------+--------+------------------+-------------+--------+
  | nombre_empleado | codigo | nombre           | presupuesto | gastos |
  +-----------------+--------+------------------+-------------+--------+
  | Aarón Rivero    |      1 | Desarrollo       |      120000 |   6000 |
  | María Santana   |      1 | Desarrollo       |      120000 |   6000 |
  | Marta Herrera   |      1 | Desarrollo       |      120000 |   6000 |
  | Adela Salas     |      2 | Sistemas         |      150000 |  21000 |
  | Pilar Ruiz      |      2 | Sistemas         |      150000 |  21000 |
  | Juan Gómez      |      2 | Sistemas         |      150000 |  21000 |
  | Adolfo Rubio    |      3 | Recursos Humanos |      280000 |  25000 |
  | Pepe Ruiz       |      3 | Recursos Humanos |      280000 |  25000 |
  | Adrián Suárez   |      4 | Contabilidad     |      110000 |   3000 |
  | Marcos Loyola   |      5 | I+D              |      375000 | 380000 |
  | Diego Flores    |      5 | I+D              |      375000 | 380000 |
  +-----------------+--------+------------------+-------------+--------+
  ```

  

2. Devuelve un listado con los empleados y los datos de los departamentos donde trabaja cada uno. Ordena el resultado, en primer lugar por el nombre del departamento (en orden alfabético) y en segundo lugar por los apellidos y el nombre de los empleados.

  ```sql
  select d.codigo, d.nombre, d.presupuesto, d.gastos, concat(e.nombre,' ',e.apellido1)as nombre_empleado
  from empleado as e, departamento as d
  where e.codigo_departamento = d.codigo
  order by d.nombre asc, nombre_empleado asc
  +--------+------------------+-------------+--------+-----------------+
  | codigo | nombre           | presupuesto | gastos | nombre_empleado |
  +--------+------------------+-------------+--------+-----------------+
  |      4 | Contabilidad     |      110000 |   3000 | Adrián Suárez   |
  |      1 | Desarrollo       |      120000 |   6000 | Aarón Rivero    |
  |      1 | Desarrollo       |      120000 |   6000 | María Santana   |
  |      1 | Desarrollo       |      120000 |   6000 | Marta Herrera   |
  |      5 | I+D              |      375000 | 380000 | Diego Flores    |
  |      5 | I+D              |      375000 | 380000 | Marcos Loyola   |
  |      3 | Recursos Humanos |      280000 |  25000 | Adolfo Rubio    |
  |      3 | Recursos Humanos |      280000 |  25000 | Pepe Ruiz       |
  |      2 | Sistemas         |      150000 |  21000 | Adela Salas     |
  |      2 | Sistemas         |      150000 |  21000 | Juan Gómez      |
  |      2 | Sistemas         |      150000 |  21000 | Pilar Ruiz      |
  +--------+------------------+-------------+--------+-----------------+
  ```

  

3. Devuelve un listado con el identificador y el nombre del departamento, solamente de aquellos departamentos que tienen empleados.

  ```sql
  select distinct d.codigo, d.nombre
  from empleado as e, departamento as d
  where e.codigo_departamento = d.codigo
  +--------+------------------+
  | codigo | nombre           |
  +--------+------------------+
  |      1 | Desarrollo       |
  |      2 | Sistemas         |
  |      3 | Recursos Humanos |
  |      4 | Contabilidad     |
  |      5 | I+D              |
  +--------+------------------+
  ```

  

4. Devuelve un listado con el identificador, el nombre del departamento y el valor del presupuesto actual del que dispone, solamente de aquellos departamentos que tienen empleados. El valor del presupuesto actual lo puede calcular restando al valor del presupuesto inicial (columna presupuesto) el valor de los gastos que ha generado (columna gastos).

  ```sql
  select distinct d.codigo, d.nombre, (presupuesto-gastos) as presupuesto_actual
  from empleado as e, departamento as d
  where e.codigo_departamento = d.codigo
  +--------+------------------+--------------------+
  | codigo | nombre           | presupuesto_actual |
  +--------+------------------+--------------------+
  |      1 | Desarrollo       |             114000 |
  |      2 | Sistemas         |             129000 |
  |      3 | Recursos Humanos |             255000 |
  |      4 | Contabilidad     |             107000 |
  |      5 | I+D              |              -5000 |
  +--------+------------------+--------------------+
  ```

  

5. Devuelve el nombre del departamento donde trabaja el empleado que tiene el nif 38382980M.

  ```sql
  select d.nombre as departamento
  from empleado as e, departamento as d
  where e.codigo_departamento = d.codigo and e.nif = '38382980M'
  +--------------+
  | departamento |
  +--------------+
  | Desarrollo   |
  +--------------+
  ```

  

6. Devuelve el nombre del departamento donde trabaja el empleado Pepe Ruiz Santana.

  ```sql
  select d.nombre as departamento
  from empleado as e, departamento as d
  where e.codigo_departamento = d.codigo and e.nombre = 'Pepe' and e.apellido1 ='Ruiz' and e.apellido2 = 'Sanatana';
  +------------------+
  | departamento     |
  +------------------+
  | Recursos Humanos |
  +------------------+
  ```

  

7. Devuelve un listado con los datos de los empleados que trabajan en el departamento de I+D. Ordena el resultado alfabéticamente.

  ```sql
  select e.id, e.nif, e.nombre, e.apellido1, e.apellido2, e.codigo_departamento
  from empleado as e, departamento as d
  where e.codigo_departamento = d.codigo and e.codigo_departamento = 5
  +----+-----------+--------+-----------+-----------+---------------------+
  | id | nif       | nombre | apellido1 | apellido2 | codigo_departamento |
  +----+-----------+--------+-----------+-----------+---------------------+
  |  5 | 17087203C | Marcos | Loyola    | Méndez    |                   5 |
  | 10 | 46384486H | Diego  | Flores    | Salas     |                   5 |
  +----+-----------+--------+-----------+-----------+---------------------+
  ```

  

1. Devuelve un listado con los datos de los empleados que trabajan en el departamento de Sistemas, Contabilidad o I+D. Ordena el resultado alfabéticamente.

```sql
 select e.id, e.nif, e.nombre, e.apellido1, e.apellido2, e.codigo_departamento
  from empleado as e, departamento as d
  where e.codigo_departamento = d.codigo and e.codigo_departamento in (2,4,5)
  order by e.nombre ASC
+----+-----------+---------+-----------+-----------+---------------------+
| id | nif       | nombre  | apellido1 | apellido2 | codigo_departamento |
+----+-----------+---------+-----------+-----------+---------------------+
|  2 | Y5575632D | Adela   | Salas     | Díaz      |                   2 |
|  4 | 77705545E | Adrián  | Suárez    | NULL      |                   4 |
| 10 | 46384486H | Diego   | Flores    | Salas     |                   5 |
|  9 | 56399183D | Juan    | Gómez     | López     |                   2 |
|  5 | 17087203C | Marcos  | Loyola    | Méndez    |                   5 |
|  7 | 80576669X | Pilar   | Ruiz      | NULL      |                   2 |
+----+-----------+---------+-----------+-----------+---------------------+
```

1. Devuelve una lista con el nombre de los empleados que tienen los departamentos que no tienen un presupuesto entre 100000 y 200000 euros.

```sql
  select e.nombre, e.apellido1, e.apellido2
  from empleado as e, departamento as d
  where e.codigo_departamento = d.codigo and d.presupuesto between 100000 and 200000
+---------+-----------+-----------+
| nombre  | apellido1 | apellido2 |
+---------+-----------+-----------+
| Aarón   | Rivero    | Gómez     |
| María   | Santana   | Moreno    |
| Marta   | Herrera   | Gil       |
| Adela   | Salas     | Díaz      |
| Pilar   | Ruiz      | NULL      |
| Juan    | Gómez     | López     |
| Adrián  | Suárez    | NULL      |
+---------+-----------+-----------+
```

1. Devuelve un listado con el nombre de los departamentos donde existe algún empleado cuyo segundo apellido sea NULL. Tenga en cuenta que no debe mostrar nombres de departamentos que estén repetidos.
    
    ```sql
    select distinct d.nombre
    from empleado as e, departamento as d
    where e.codigo_departamento = d.codigo and e.apellido2 is NULL
    +--------------+
    | nombre       |
    +--------------+
    | Contabilidad |
    | Sistemas     |
    +--------------+
    ```
    

## **Consultas multitabla (Composición externa)**

## **Resuelva todas las consultas utilizando las cláusulas LEFT JOIN y RIGHT JOIN.**

1. Devuelve un listado con todos los empleados junto con los datos de los departamentos donde trabajan. Este listado también debe incluir los empleados que no tienen ningún departamento asociado.

```sql
  select concat(e.nombre, ' ',e.apellido1) as empleado, d.codigo, d.nombre, d.presupuesto, d.gastos
  from empleado as e
  left join departamento as d
  on e.codigo_departamento = d.codigo
+--------------------+--------+------------------+-------------+--------+
| empleado           | codigo | nombre           | presupuesto | gastos |
+--------------------+--------+------------------+-------------+--------+
| Aarón Rivero       |      1 | Desarrollo       |      120000 |   6000 |
| Adela Salas        |      2 | Sistemas         |      150000 |  21000 |
| Adolfo Rubio       |      3 | Recursos Humanos |      280000 |  25000 |
| Adrián Suárez      |      4 | Contabilidad     |      110000 |   3000 |
| Marcos Loyola      |      5 | I+D              |      375000 | 380000 |
| María Santana      |      1 | Desarrollo       |      120000 |   6000 |
| Pilar Ruiz         |      2 | Sistemas         |      150000 |  21000 |
| Pepe Ruiz          |      3 | Recursos Humanos |      280000 |  25000 |
| Juan Gómez         |      2 | Sistemas         |      150000 |  21000 |
| Diego Flores       |      5 | I+D              |      375000 | 380000 |
| Marta Herrera      |      1 | Desarrollo       |      120000 |   6000 |
| Irene Salas        |   NULL | NULL             |        NULL |   NULL |
| Juan Antonio Sáez  |   NULL | NULL             |        NULL |   NULL |
+--------------------+--------+------------------+-------------+--------+
```

1. Devuelve un listado donde sólo aparezcan aquellos empleados que no tienen ningún departamento asociado.

```sql
  select concat(e.nombre, ' ',e.apellido1) as empleado, d.codigo, d.nombre, d.presupuesto, d.gastos
  from empleado as e
  left join departamento as d
  on e.codigo_departamento = d.codigo
  where e.codigo_departamento is NULL
+--------------------+--------+--------+-------------+--------+
| empleado           | codigo | nombre | presupuesto | gastos |
+--------------------+--------+--------+-------------+--------+
| Irene Salas        |   NULL | NULL   |        NULL |   NULL |
| Juan Antonio Sáez  |   NULL | NULL   |        NULL |   NULL |
+--------------------+--------+--------+-------------+--------+  
```

1. Devuelve un listado donde sólo aparezcan aquellos departamentos que no tienen ningún empleado asociado.

```sql
  select d.codigo, d.nombre, d.presupuesto, d.gastos
  from empleado as e
  right join departamento as d
  on e.codigo_departamento = d.codigo
  where e.codigo_departamento is NULL
+--------+------------+-------------+--------+
| codigo | nombre     | presupuesto | gastos |
+--------+------------+-------------+--------+
|      6 | Proyectos  |           0 |      0 |
|      7 | Publicidad |           0 |   1000 |
+--------+------------+-------------+--------+
```

1. Devuelve un listado con todos los empleados junto con los datos de los departamentos donde trabajan. El listado debe incluir los empleados que no tienen ningún departamento asociado y los departamentos que no tienen ningún empleado asociado. Ordene el listado alfabéticamente por el nombre del departamento.

```sql
select concat(e.nombre, ' ',e.apellido1) as empleado, d.codigo, d.nombre, d.presupuesto, d.gastos
from empleado as e
left join departamento as d
on e.codigo_departamento = d.codigo
order by d.nombre asc
+--------------------+--------+------------------+-------------+--------+
| empleado           | codigo | nombre           | presupuesto | gastos |
+--------------------+--------+------------------+-------------+--------+
| Irene Salas        |   NULL | NULL             |        NULL |   NULL |
| Juan Antonio Sáez  |   NULL | NULL             |        NULL |   NULL |
| Adrián Suárez      |      4 | Contabilidad     |      110000 |   3000 |
| Aarón Rivero       |      1 | Desarrollo       |      120000 |   6000 |
| María Santana      |      1 | Desarrollo       |      120000 |   6000 |
| Marta Herrera      |      1 | Desarrollo       |      120000 |   6000 |
| Marcos Loyola      |      5 | I+D              |      375000 | 380000 |
| Diego Flores       |      5 | I+D              |      375000 | 380000 |
| Adolfo Rubio       |      3 | Recursos Humanos |      280000 |  25000 |
| Pepe Ruiz          |      3 | Recursos Humanos |      280000 |  25000 |
| Adela Salas        |      2 | Sistemas         |      150000 |  21000 |
| Pilar Ruiz         |      2 | Sistemas         |      150000 |  21000 |
| Juan Gómez         |      2 | Sistemas         |      150000 |  21000 |
+--------------------+--------+------------------+-------------+--------+
```

1. Devuelve un listado con los empleados que no tienen ningún departamento asociado y los departamentos que no tienen ningún empleado asociado. Ordene el listado alfabéticamente por el nombre del departamento.

```sql
select concat(e.nombre, ' ',e.apellido1) as empleado, d.codigo, d.nombre, d.presupuesto, d.gastos
  from empleado as e
  left join departamento as d
  on e.codigo_departamento = d.codigo
  where e.codigo_departamento is NULL
  union
  select concat(e.nombre, ' ',e.apellido1) as empleado,d.codigo, d.nombre, d.presupuesto, d.gastos
  from empleado as e
  right join departamento as d
  on e.codigo_departamento = d.codigo
  where e.codigo_departamento is NULL
  +--------------------+--------+------------+-------------+--------+
| empleado           | codigo | nombre     | presupuesto | gastos |
+--------------------+--------+------------+-------------+--------+
| Irene Salas        |   NULL | NULL       |        NULL |   NULL |
| Juan Antonio Sáez  |   NULL | NULL       |        NULL |   NULL |
| NULL               |      6 | Proyectos  |           0 |      0 |
| NULL               |      7 | Publicidad |           0 |   1000 |
+--------------------+--------+------------+-------------+--------+
```

## **Consultas resumen**

1. Calcula la suma del presupuesto de todos los departamentos.

```sql
  select SUM(presupuesto)
  from departamento
+------------------+
| SUM(presupuesto) |
+------------------+
|          1035000 |
+------------------+
```

1. Calcula la media del presupuesto de todos los departamentos.

```sql
  select AVG(presupuesto)
  from departamento
+--------------------+
| AVG(presupuesto)   |
+--------------------+
| 147857.14285714287 |
+--------------------+
```

1. Calcula el valor mínimo del presupuesto de todos los departamentos.

```sql
  select MIN(presupuesto)
  from departamento
+------------------+
| MIN(presupuesto) |
+------------------+
|                0 |
+------------------+
```

1. Calcula el nombre del departamento y el presupuesto que tiene asignado, del departamento con menor presupuesto.

```sql
  select nombre, presupuesto
  from departamento
  order by presupuesto asc
  limit 1
 +-----------+-------------+
| nombre    | presupuesto |
+-----------+-------------+
| Proyectos |           0 |
+-----------+-------------+
```

1. Calcula el valor máximo del presupuesto de todos los departamentos.

```sql
select MAX(presupuesto)
from departamento
+------------------+
| MAX(presupuesto) |
+------------------+
|           375000 |
+------------------+
```

1. Calcula el nombre del departamento y el presupuesto que tiene asignado, del departamento con mayor presupuesto.

```sql
select nombre, presupuesto
from departamento
order by presupuesto desc
limit 1
+--------+-------------+
| nombre | presupuesto |
+--------+-------------+
| I+D    |      375000 |
+--------+-------------+
```

1. Calcula el número total de empleados que hay en la tabla empleado.

```sql
select count(id)
from empleado
+-----------+
| count(id) |
+-----------+
|        13 |
+-----------+
```

1. Calcula el número de empleados que no tienen NULL en su segundo apellido.

```sql
select count(id)
from empleado
where apellido2 is not NULL
+-----------+
| count(id) |
+-----------+
|        11 |
+-----------+
```

1. Calcula el número de empleados que hay en cada departamento. Tienes que devolver dos columnas, una con el nombre del departamento y otra con el número de empleados que tiene asignados.

```sql
select d.nombre,count(e.id) as 'numero de empleados'
from empleado as e, departamento as d
where e.codigo_departamento = d.codigo
group by d.nombre
+------------------+---------------------+
| nombre           | numero de empleados |
+------------------+---------------------+
| Desarrollo       |                   3 |
| Sistemas         |                   3 |
| Recursos Humanos |                   2 |
| Contabilidad     |                   1 |
| I+D              |                   2 |
+------------------+---------------------+
```

1. Calcula el nombre de los departamentos que tienen más de 2 empleados. El resultado debe tener dos columnas, una con el nombre del departamento y otra con el número de empleados que tiene asignados.

```sql
select d.nombre,count(e.id) as 'numero de empleados'
from empleado as e, departamento as d
where e.codigo_departamento = d.codigo
group by d.nombre
having count(e.id) > 2
+------------+---------------------+
| nombre     | numero de empleados |
+------------+---------------------+
| Desarrollo |                   3 |
| Sistemas   |                   3 |
+------------+---------------------+
```

1. Calcula el número de empleados que trabajan en cada uno de los departamentos. El resultado de esta consulta también tiene que incluir aquellos departamentos que no tienen ningún empleado asociado.

```sql
select d.nombre,count(e.id) as 'numero de empleados'
from empleado as e
right join departamento as d
on e.codigo_departamento = d.codigo
group by d.nombre
+------------------+---------------------+
| nombre           | numero de empleados |
+------------------+---------------------+
| Desarrollo       |                   3 |
| Sistemas         |                   3 |
| Recursos Humanos |                   2 |
| Contabilidad     |                   1 |
| I+D              |                   2 |
| Proyectos        |                   0 |
| Publicidad       |                   0 |
+------------------+---------------------+
```

1. Calcula el número de empleados que trabajan en cada unos de los departamentos que tienen un presupuesto mayor a 200000 euros.

```sql
select d.nombre,count(e.id) as 'numero de empleados'
from empleado as e
right join departamento as d
on e.codigo_departamento = d.codigo
where d.presupuesto >= 200000
group by d.nombre
+------------------+---------------------+
| nombre           | numero de empleados |
+------------------+---------------------+
| Recursos Humanos |                   2 |
| I+D              |                   2 |
+------------------+---------------------+
```

## **Subconsultas**

## **Con operadores básicos de comparación**

1. Devuelve un listado con todos los empleados que tiene el departamento de Sistemas. (Sin utilizar INNER JOIN).

```sql
select nombre
from empleado 
where codigo_departamento = (
  select codigo
  from departamento
  where nombre = 'Sistemas'
)
+--------+
| nombre |
+--------+
| Adela  |
| Pilar  |
| Juan   |
+--------+
```

1. Devuelve el nombre del departamento con mayor presupuesto y la cantidad que tiene asignada.

```sql
select nombre, presupuesto
from departamento
where presupuesto =(
  select max(presupuesto)
  from departamento
)
+--------+-------------+
| nombre | presupuesto |
+--------+-------------+
| I+D    |      375000 |
+--------+-------------+
```

1. Devuelve el nombre del departamento con menor presupuesto y la cantidad que tiene asignada.

```sql
select nombre, presupuesto
from departamento
where presupuesto =(
  select min(presupuesto)
  from departamento
)
limit 1
+-----------+-------------+
| nombre    | presupuesto |
+-----------+-------------+
| Proyectos |           0 |
+-----------+-------------+
```

 Subconsultas con ALL y ANY

1. Devuelve el nombre del departamento con mayor presupuesto y la cantidad que tiene asignada. Sin hacer uso de MAX, ORDER BY ni LIMIT.

```sql
select nombre, presupuesto
from departamento
where presupuesto >= ALL (
	select presupuesto 
	from departamento
)
+--------+-------------+
| nombre | presupuesto |
+--------+-------------+
| I+D    |      375000 |
+--------+-------------+
```

1. Devuelve el nombre del departamento con menor presupuesto y la cantidad que tiene asignada. Sin hacer uso de MIN, ORDER BY ni LIMIT.

```sql
select nombre, presupuesto
from departamento
where presupuesto <= ALL (
	select presupuesto 
	from departamento
)
limit 1
+-----------+-------------+
| nombre    | presupuesto |
+-----------+-------------+
| Proyectos |           0 |
+-----------+-------------+
```

1. Devuelve los nombres de los departamentos que tienen empleados asociados. (Utilizando ALL o ANY).

```sql
select nombre
from departamento
where codigo = ANY (
	select codigo_departamento
	from empleado
)
+------------------+
| nombre           |
+------------------+
| Desarrollo       |
| Sistemas         |
| Recursos Humanos |
| Contabilidad     |
| I+D              |
+------------------+
```

1. Devuelve los nombres de los departamentos que no tienen empleados asociados. (Utilizando ALL o ANY).

```sql
select nombre
from departamento
where codigo = ALL (
	select distinct codigo_departamento
	from empleado
);
```

 Subconsultas con IN y NOT IN

1. Devuelve los nombres de los departamentos que tienen empleados asociados. (Utilizando IN o NOT IN).

```sql
select nombre
from departamento
where codigo IN  (
	select codigo_departamento
	from empleado
);
+------------------+
| nombre           |
+------------------+
| Desarrollo       |
| Sistemas         |
| Recursos Humanos |
| Contabilidad     |
| I+D              |
+------------------+
```

1. Devuelve los nombres de los departamentos que no tienen empleados asociados. (Utilizando IN o NOT IN).

```sql

```

 Subconsultas con EXISTS y NOT EXISTS

1. Devuelve los nombres de los departamentos que tienen empleados asociados. (Utilizando EXISTS o NOT EXISTS).

```sql
select d.nombre
from departamento as d
where exists (
	select 1
	from empleado as e
	where e.codigo_departamento = d.codigo
);
+------------------+
| nombre           |
+------------------+
| Desarrollo       |
| Sistemas         |
| Recursos Humanos |
| Contabilidad     |
| I+D              |
+------------------+
```

1. Devuelve los nombres de los departamentos que tienen empleados asociados. (Utilizando EXISTS o NOT EXISTS).

```sql
select d.nombre
from departamento as d
where not exists (
	select 1
	from empleado as e
	where e.codigo_departamento = d.codigo
);
+------------+
| nombre     |
+------------+
| Proyectos  |
| Publicidad |
+------------+
```
