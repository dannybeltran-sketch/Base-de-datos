
# 📘 Ejercicios Propuestos: Modelado de Bases de Datos

## 📘 Ejercicio 1: Sistema de Biblioteca

Una biblioteca registra libros y autores. Un libro puede tener varios autores y un autor varios libros. Los socios toman libros prestados; de cada préstamo interesan la fecha de retiro y la de devolución.

🔗 [Enlace del Ejercicio 5](https://drive.google.com/file/d/1X5RGjOL7AcUuNdaMs1bUGXvV7UJoxNuN/view?usp=sharing)

## Modelo SQL

```
create table Autor (
    id_autor varchar(20) primary key,
    nombre varchar(20) not null
);

create table Libro (
    id_libro varchar(20) primary key,
    titulo varchar(100) not null,
    isbn varchar(20)
);

create table Socio (
    id_socio varchar(20) primary key,
    nombre varchar(20) not null,
    telefono varchar(10)
);

create table Libro_Autor (
    id_libro varchar(20),
    id_autor varchar(20),
    primary key (id_libro, id_autor),
    foreign key (id_libro) references Libro(id_libro),
    foreign key (id_autor) references Autor(id_autor)
);

create table Prestamo (
    id_prestamo varchar(20) primary key,
    fecha_retiro date not null,
    fecha_devolucion date not null,
    id_socio varchar(20) not null,
    id_libro varchar(20) not null,
    foreign key (id_socio) references Socio(id_socio),
    foreign key (id_libro) references Libro(id_libro)
);
```
---

## 📘 Ejercicio 2: Pedidos de Restaurante

Los clientes realizan pedidos que contienen varios platos con distinta cantidad. Los platos se agrupan en categorías. Cada pedido lo atiende un único mesero. El precio del plato debe registrarse tal como estaba al momento del pedido, aunque luego cambie.

🔗 [Enlace del Ejercicio 6](https://drive.google.com/file/d/1449k2nFVMDzpS83Vm4jB4GBV86DKsNid/view?usp=sharing)

## Modelo SQL

```
```
---

## 📘 Ejercicio 3: Clínica Médica

Los pacientes solicitan citas; cada cita la atiende un médico a un paciente en fecha, hora y consultorio. De algunas citas se genera una receta que incluye medicamentos con dosis y duración. Cada médico pertenece a una especialidad.

🔗 [Enlace del Ejercicio 7](https://drive.google.com/file/d/1IYEsMan6NHrXKY7JFPAh5xhLzup-tXh5/view?usp=sharing)

## Modelo SQL

```
```
---

## 📘 Ejercicio 4: Sistema de Aerolínea

Una aerolínea opera vuelos (cada uno con número, fecha, origen y destino), cada vuelo lo realiza un avión. Los pasajeros realizan reservas para un vuelo específico, indicando asiento y tarifa pagada en el momento de la reserva.

🔗 [Enlace del Ejercicio 8](https://drive.google.com/file/d/1qab-sqrWSFkJrjVkPFZVbBP4fD6BjR2n/view?usp=sharing)

## Modelo SQL

```
```
---

## 📘 Ejercicio 5: Empresa Discográfica

Una empresa discográfica necesita modelar los datos sobre sus diferentes recursos según las siguientes características:

- **Manager:** de cada mánager se almacena un identificador de manager y su nombre. Un manager representa a una serie de artistas.
- **Artista:** un artista es representado por un manager. De los artistas se almacena su nombre completo (usando un único atributo) y su NIF.
- **Evento de promoción:** los artistas participan en eventos de promoción para dar a conocer sus trabajos. En un evento de promoción pueden participar varios artistas. De un evento se almacena un identificador único, la fecha de celebración y el número de asistentes.

🔗 [Enlace del Ejercicio 9](https://drive.google.com/file/d/1rz7aHzC8aZ1_kyCsp1NAqNyw8S5AXsIU/view?usp=sharing)

## Modelo SQL

```
```
---

## 📘 Ejercicio 6: Tienda Informática

Se desea crear una aplicación para la gestión de una tienda informática. La tienda dispone de una serie de productos que se venden a los clientes. De cada producto informático se desea guardar el código, descripción, precio y número de existencias. De cada cliente se desea guardar el código, nombre, apellidos, dirección y número telefónico. Un cliente puede comprar varios productos en la tienda y un mismo producto puede ser comprado por varios clientes. Cada vez que se compre un artículo quedará registrada la compra en la base de datos junto con la fecha en la que se compró el artículo. La tienda tiene contactos con varios proveedores que son los que suministran los productos. Un mismo producto puede ser suministrado por varios proveedores. De cada proveedor se desea guardar el código, nombres, apellidos, dirección, provincia y número de teléfono.

🔗 [Enlace del Ejercicio 10](https://drive.google.com/file/d/1KS3dyAlMtWwXKQrA7DpE6R_zKvzOlbh2/view?usp=sharing)

## Modelo SQL

```
```
---

## 📘 Ejercicio 7: Discos Musicales

- La tienda vende discos de diferentes géneros musicales y cantantes.
- Cada género musical tiene un identificador.
- Cada disco tiene título, género musical, precio y cantante.
- De un cantante se registra el nombre y su país. Todo disco pertenece a un cantante y un cantante puede tener muchos discos. Además, un disco tiene un conjunto de canciones (identificador y título).
- Un disco tiene muchas canciones y una canción puede estar en varios discos. Interesa conocer la posición de una canción en un determinado disco.

🔗 [Enlace del Ejercicio 11](https://drive.google.com/file/d/1pjODzEzoVxXz-tit61jDsbqyIF8e4Ryb/view?usp=sharing)

## Modelo SQL

```
```
---

## 📘 Ejercicio 8: Camiones

Se desea informatizar la gestión de una empresa de transporte que reparte paquetes por toda España. Los encargados de llevar los paquetes son los camioneros, de los que se quiere guardar la cédula, nombre, teléfono, dirección, salario y población en que vive. De los paquetes transportados interesa conocer el código del paquete, descripción, destinatario y dirección del destinatario.

Un camionero distribuye muchos paquetes, y un paquete sólo puede ser distribuido por un camionero. De las provincias a las que llegan los paquetes interesa guardar el código de provincia y el nombre. Un paquete sólo puede llegar a una provincia. Sin embargo, a una provincia pueden llegar varios paquetes.

De los camiones que llevan los camioneros, interesa conocer la matrícula, modelo, tipo y potencia. Un camionero puede conducir diferentes camiones en fechas diferentes, y un camión puede ser conducido por varios camioneros.

🔗 [Enlace del Ejercicio 12](https://drive.google.com/file/d/18QR0joCmPk_V-HuVbGeWiad6jFG-YyWr/view?usp=sharing)

## Modelo SQL

```
```
---

## 📘 Ejercicio 9: Veterinaria

- **Del propietario** interesa: cédula, apellidos, nombres, dirección, teléfonos.
- **De la mascota** interesa: identificador, nombre, fecha de nacimiento, tipo.
- Un propietario puede llevar una o varias mascotas.
- Una mascota la lleva uno y solo un propietario.
- **Del personal de la clínica veterinaria** interesa un código, la cédula y el nombre.
- Entre el personal de la clínica se distingue a los veterinarios y los auxiliares, pudiendo haber otros tipos:
  - **Del veterinario** se guarda además su fecha_alta y especialidad.
  - **De los auxiliares** interesa su base de cotización.
- **Las mascotas pasan consulta con los veterinarios.** De manera que:
  - Un veterinario puede pasar consulta a ninguna o a varias mascotas.
  - Una misma mascota de la clínica ha pasado consulta una o más veces en fechas diferentes con varios veterinarios.
  - Al pasar consulta se realiza un diagnóstico.
- **Cada propietario tiene un familiar de contacto para casos de emergencia.**
  - De este familiar interesa la cédula, nombre y teléfono.
  - Si el propietario se da de alta en la clínica veterinaria, el familiar ya no interesa.
  - El familiar es contacto de un solo propietario.

🔗 [Enlace del Ejercicio 13](https://drive.google.com/file/d/1LUyu-VZxACpIXxiZmrVeo5GXwdSlqWpe/view?usp=sharing)

## Modelo SQL

```
```
