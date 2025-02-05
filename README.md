# SXE-Tarea12

## Índice  
1. [Enunciado](#1-enunciado)  
2. [Preparación](#2-preparación)  
3. [Apartado 1: Crear tabla EmpresasFCT](#3-apartado-1)  
4. [Apartado 2: Insertar registros](#4-apartado-2)  
5. [Apartado 3: Consultar EmpresasFCT](#5-apartado-3)  
6. [Apartado 4: Listar contactos de Tracy](#6-apartado-4)  
7. [Apartado 5: Empresas proveedoras con reembolsos](#7-apartado-5)  
8. [Apartado 6: Clientes con más de dos facturas](#8-apartado-6)  
9. [Apartado 7: Actualizar correos](#9-apartado-7)  
10. [Apartado 8: Eliminar contactos de Ready Mat](#10-apartado-8)  

---------------------------------------------

## 1) Enunciado:  
Introducción  
Este ejercicio consiste en realizar una serie de operaciones sobre la base de datos  
de una instalación de odoo. Si bien, es cierto que no es algo que se produzca  
habitualmente, como hemos visto anteriormente, existen ocasiones en las que  
puede ser necesario realizar este tipo de acciones.  
La tarea se realizará en un repositorio en vuestra cuenta de github (no hace falta  
que sea privado). En el aula virtual escribid el enlace a vuestro repositorio.  

-----------------------------------------------

## 2) Preparación:  
### Creo nueva base de datos con los archivos de demo:  
![sxe-1](https://github.com/user-attachments/assets/c9f8b2c9-8991-4996-829d-ab991e6e6a2f)

### Añado las aplicaciones de Contactos y Facturación comprobando que estan los demos
![sxe-2](https://github.com/user-attachments/assets/7bdaddfd-45af-4283-b899-9b0c1dee9edf)

**Apunte: para llevar a cabo los ejercicios hemos de ir PGAdmin, en mi caso: http://192.168.1.134:5050/ y comprobar que conecto nuestra base de datos.**

------------------------------------------------

## 3) Apartado 1  
Como mencionamos en clase, aunque no es recomendable, en ocasiones puede ser necesario crear tablas ajenas a Odoo dentro de su base de datos (integración con sistemas externos, almacenamiento de históricos, datos temporales…). Mediante la herramienta PgAdmin u otro método que estimes oportuno, elabora y ejecuta una sentencia que cree una tabla llamada “EmpresasFCT“con los siguientes campos:  
● idEmpresa: autonumérico. Este campo será la clave primaria. 
● nombre: Texto con tamaño máximo de 40 caracteres.  
● -useChatgpt: booleano, por defecto a true  
● quiereAlumnos: Booleano.  
● numAlumnos: número entero.  
● fechaContacto: tipo fecha  

Para ello nos situamos en nuestra base de datos click derecho -> Query Tool
![sxe-3](https://github.com/user-attachments/assets/9e997c34-04b5-4417-9767-f45cf4728271)

Y lanzamos la siguiente sentencia:
<details><summary>🔍 SPOILER:</summary>  

  ```bash
  CREATE TABLE EmpresasFCT (
      idEmpresa SERIAL PRIMARY KEY,
      nombre VARCHAR(40) NOT NULL,
      quiereAlumnos BOOLEAN,
      numAlumnos INTEGER,
      fechaContacto DATE
  );
```

</details>

![sxe-4](https://github.com/user-attachments/assets/2be4b1ec-5e57-4625-a0de-473c1ef38db0)  
Comprobamos que nos ha creado las tablas:  
![sxe-5](https://github.com/user-attachments/assets/f42c0bdf-7df6-4003-a321-79822a30c74f)  

------------------------------------------------

## 4) Apartado 2  
Inserta 5 registros inventados en la tabla a través de una sentencia SQL.  

Volvemos al query:
<details><summary>🔍 SPOILER:</summary>  

  ```bash
INSERT INTO EmpresasFCT (nombre, quiereAlumnos, numAlumnos, fechaContacto)
VALUES
    ('Empresa A', TRUE, 5, '2024-02-01'),
    ('Empresa B', FALSE, 0, '2024-01-15'),
    ('Empresa C', TRUE, 2, '2024-02-10'),
    ('Empresa D', FALSE, 0, '2024-03-05'),
    ('Empresa E', TRUE, 10, '2024-01-25');
```

</details>

![sxe-6](https://github.com/user-attachments/assets/eb836c17-5eb9-4d24-a463-82a10a376e86)  

Le damos a View/Edit data:  
![sxe-7](https://github.com/user-attachments/assets/b4f9e837-0fb0-41ae-96c2-75e60f99fca6)  

Y comprobamos:  
![sxe-8](https://github.com/user-attachments/assets/3f39e3c5-ec98-471d-89a0-9b43e0ef676c)  

------------------------------------------------

## 5) Apartado 3 
Realiza una consulta donde se muestren todos los datos de la tabla EmpresasFCT 
ordenados por fechaContacto, de modo que en la primera fila salga el que tenga la 
fecha más reciente. 

<details><summary>🔍 SPOILER:</summary>  

  ```bash
SELECT * FROM empresasfct ORDER BY fechacontacto DESC; 
```

</details>

![sxe-9](https://github.com/user-attachments/assets/1c425962-add1-4eb3-9269-a15f942eb2d3)

------------------------------------------------

## 6) Apartado 4  
Realiza una consulta que permita obtener un listado de todos los contactos de Odoo (no empresas) con la siguiente información:  
- Nombre  
- Cuya ciudad sea Tracy, y código postal 95304  
- Nombre comercial de la empresa  
ordenados alfabéticamente por el nombre comercial de la empresa,
<details><summary>🔍 SPOILER:</summary>  

  ```bash
SELECT name, city, zip, commercial_company_name
FROM res_partner
WHERE city = 'Tracy' AND zip = '95304'
ORDER BY commercial_company_name;
  ```

</details>

![sxe-10](https://github.com/user-attachments/assets/a359d9eb-1b5e-4b8c-bde0-23146cb2a1e6)

------------------------------------------------

## 7) Apartado 5 
Utilizando las tablas de odoo, obtén un listado de empresas proveedoras, que han emitido algún reembolso (facturas rectificativas de proveedor)  
- Nombre de la empresa  
- Número de factura  
- Fecha de la factura  
- total de factura con impuestos  
- Total factura SIN mpuestos  
Ordenadas por fecha de factura de modo que la primera sea la más reciente.

<details><summary>🔍 SPOILER:</summary>  

  ```bash
SELECT rp.name AS empresa, am.name AS numero_factura, am.invoice_date AS fecha,
       am.amount_total AS total_con_impuestos, am.amount_untaxed AS total_sin_impuestos
FROM account_move am
JOIN res_partner rp ON am.partner_id = rp.id
WHERE am.move_type = 'in_refund'
ORDER BY am.invoice_date DESC;
  ```

</details>

![sxe-11](https://github.com/user-attachments/assets/434d11e8-9a33-44be-898b-47ff1dfc601a)

------------------------------------------------

## 8) Apartado 6  
Utilizando las tablas de odoo, obtén un listado de empresas clientes, a las que se les ha emitido más de dos facturas de venta (solo venta) confirmadas, mostrando los siguientes datos:  
- Nombre de la empresa  
- Número de facturas  
- Total de factura con impuestos  
- Total facturado SIN IMPUESTOS

<details><summary>🔍 SPOILER:</summary>  

  ```bash
SELECT rp.name AS empresa, COUNT(am.id) AS num_facturas,
       SUM(am.amount_total) AS total_con_impuestos,
       SUM(am.amount_untaxed) AS total_sin_impuestos
FROM account_move am
JOIN res_partner rp ON am.partner_id = rp.id
WHERE am.move_type = 'out_invoice' AND am.state = 'posted'
GROUP BY rp.name
HAVING COUNT(am.id) > 2;
  ```

</details>

![sxe-12](https://github.com/user-attachments/assets/5b29076f-f5be-4cad-8235-8670af9d6129)

------------------------------------------------

## 9) Apartado 7  
Crea una sentencia que actualice el correo de los contactos cuyo dominio es @bilbao.example.com a @bilbao.bizkaia.eus 

Lanzamos la sentencia:

<details><summary>🔍 SPOILER:</summary>  

  ```bash
UPDATE res_partner SET email = '@bilbao.bizkaia.neus' WHERE email ='@bilbao.example.com';
  ```

</details>

Comprobamos:  
![sxe-13](https://github.com/user-attachments/assets/15804f25-2d93-4b3a-af16-5933b845ab59)

------------------------------------------------

## 10) Apartado 8  
La empresa Ready Mat ha hecho un ERE y ha despedido a todos los empleados que tenías como contacto. Crea una sentencia que elimine todos los contactos pertenecientes a la empresa “Ready Mat”, pero mantén la empresa. Añade una captura de pantalla de la sección de ontactos de odoo con Ready Mat antes y después.  

Captura de pantalla antes de eliminar los contactos:  
![sxe-14](https://github.com/user-attachments/assets/52a8c352-f9db-42d7-b69e-4571406af683)

Lanzamos la sentencia:

<details><summary>🔍 SPOILER:</summary>  

  ```bash
DELETE from res_partner where commercial_company_name = 'Ready Mat' and is_company = FALSE;
  ```

</details>

![sxe-15](https://github.com/user-attachments/assets/6f40159a-b012-4196-97d5-2ad2d4beb647)







