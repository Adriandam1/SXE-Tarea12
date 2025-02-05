# SXE-Tarea12

## Enunciado:  
Introducción  
Este ejercicio consiste en realizar una serie de operaciones sobre la base de datos  
de una instalación de odoo. Si bien, es cierto que no es algo que se produzca  
habitualmente, como hemos visto anteriormente, existen ocasiones en las que  
puede ser necesario realizar este tipo de acciones.  
La tarea se realizará en un repositorio en vuestra cuenta de github (no hace falta  
que sea privado). En el aula virtual escribid el enlace a vuestro repositorio.  

## Preparación:  
### Creo nueva base de datos con los archivos de demo:  
![sxe-1](https://github.com/user-attachments/assets/c9f8b2c9-8991-4996-829d-ab991e6e6a2f)

### Añado las aplicaciones de Contactos y Facturación comprobando que estan los demos
![sxe-2](https://github.com/user-attachments/assets/7bdaddfd-45af-4283-b899-9b0c1dee9edf)

**Apunte: para llevar a cabo los ejercicios hemos de ir PGAdmin, en mi caso: http://192.168.1.134:5050/ y comprobar que conecto nuestra base de datos.**

## Apartado 1  
Como mencionamos en clase, aunque no es recomendable, en ocasiones puede ser necesario crear tablas ajenas a Odoo dentro de su base de datos (integración con sistemas externos, almacenamiento de históricos, datos temporales…). Mediante la herramienta PgAdmin u otro método que estimes oportuno, elabora y ejecuta una sentencia que cree una tabla llamada “EmpresasFCT“con los siguientes campos:  
● idEmpresa: autonumérico. Este campo será la clave primaria. 
● nombre: Texto con tamaño máximo de 40 caracteres.  
● -useChatgpt: booleano, por defecto a true  
● quiereAlumnos: Booleano.  
● numAlumnos: número entero.  
● fechaContacto: tipo fecha  
## Apartado 2 
Inserta 5 registros inventados en la tabla a través de una sentencia SQL.  
## Apartado 3 
Realiza una consulta donde se muestren todos los datos de la tabla EmpresasFCT 
ordenados por fechaContacto, de modo que en la primera fila salga el que tenga la 
fecha más reciente. 
## Apartado 4  
Realiza una consulta que permita obtener un listado de todos los contactos de Odoo (no empresas) con la siguiente información:  
- Nombre  
- Cuya ciudad sea Tracy, y código postal 95304  
- Nombre comercial de la empresa  
ordenados alfabéticamente por el nombre comercial de la empresa,  
## Apartado 5 
Utilizando las tablas de odoo, obtén un listado de empresas proveedoras, que han emitido algún reembolso (facturas rectificativas de proveedor)  
- Nombre de la empresa  
- Número de factura  
- Fecha de la factura  
- total de factura con impuestos  
- Total factura SIN mpuestos  
Ordenadas por fecha de factura de modo que la primera sea la más reciente.  
## Apartado 6  
Utilizando las tablas de odoo, obtén un listado de empresas clientes, a las que se les ha emitido más de dos facturas de venta (solo venta) confirmadas, mostrando los siguientes datos:  
- Nombre de la empresa  
- Número de facturas  
- Total de factura con impuestos  
- Total facturado SIN IMPUESTOS  
## Apartado 7  
Crea una sentencia que actualice el correo de los contactos cuyo dominio es @bilbao.example.com a @bilbao.bizkaia.eus 
## Apartado 8  
La empresa Ready Mat ha hecho un ERE y ha despedido a todos los empleados que tenías como contacto. Crea una sentencia que elimine todos los contactos pertenecientes a la empresa “Ready Mat”, pero mantén la empresa. Añade una captura de pantalla de la sección de ontactos de odoo con Ready Mat antes y después.  
