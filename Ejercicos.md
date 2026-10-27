
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
create table Cliente (
    id_cliente varchar(20) primary key,
    nombre varchar(20),
    telefono varchar(10)
);

create table Mesero (
    id_mesero varchar(20) primary key,
    nombre varchar(20) not null
);

create table Categoria (
    id_categoria varchar(20) primary key,
    nombre varchar(20) not null
);

create table Plato (
    id_plato varchar(20) primary key,
    nombre varchar(20) not null,
    precio_actual double not null,
    id_categoria varchar(20) not null,
    foreign key (id_categoria) references Categoria(id_categoria)
);

create table Pedido (
    id_pedido varchar(20) primary key,
    id_cliente varchar(20) not null,
    id_mesero varchar(20) not null,
    foreign key (id_cliente) references Cliente(id_cliente),
    foreign key (id_mesero) references Mesero(id_mesero)
);

create table Detalle_Pedido (
    id_pedido varchar(20),
    id_plato varchar(20),
    primary key (id_pedido, id_plato),
    foreign key (id_pedido) references Pedido(id_pedido),
    foreign key (id_plato) references Plato(id_plato)
);
```
---

## 📘 Ejercicio 3: Clínica Médica

Los pacientes solicitan citas; cada cita la atiende un médico a un paciente en fecha, hora y consultorio. De algunas citas se genera una receta que incluye medicamentos con dosis y duración. Cada médico pertenece a una especialidad.

🔗 [Enlace del Ejercicio 7](https://drive.google.com/file/d/1IYEsMan6NHrXKY7JFPAh5xhLzup-tXh5/view?usp=sharing)

## Modelo SQL

```
create table Paciente (
    id_paciente varchar(20) primary key,
    cedula varchar(10) unique not null,
    nombre varchar(20) not null
);

create table Especialidad (
    id_especialidad varchar(20) primary key,
    nombre varchar(20) not null
);

create table Medico (
    id_medico varchar(20) primary key,
    nombre varchar(20) not null,
    id_especialidad varchar(20),
    foreign key (id_especialidad) references Especialidad(id_especialidad)
);

create table Consultorio (
    id_consultorio varchar(20) primary key,
    numero int not null
);

create table Cita (
    id_cita varchar(20) primary key,
    fecha date not null,
    hora time not null,
    id_paciente varchar(20) not null,
    id_medico varchar(20) not null,
    id_consultorio varchar(20),
    foreign key (id_paciente) references Paciente(id_paciente),
    foreign key (id_medico) references Medico(id_medico),
    foreign key (id_consultorio) references Consultorio(id_consultorio)
);

create table Medicamento (
    id_medicamento varchar(20) primary key,
    nombre varchar(20) not null
);

create table Receta (
    id_receta varchar(20) primary key,
    id_cita varchar(20) not null,
    foreign key (id_cita) references Cita(id_cita)
);

create table Detalle_Receta (
    id_receta varchar(20),
    id_medicamento varchar(20) not null,
    dosis varchar(100),
    duracion varchar(100) not null,
    primary key (id_receta, id_medicamento),
    foreign key (id_receta) references Receta(id_receta),
    foreign key (id_medicamento) references Medicamento(id_medicamento)
);
```
---

## 📘 Ejercicio 4: Sistema de Aerolínea

Una aerolínea opera vuelos (cada uno con número, fecha, origen y destino), cada vuelo lo realiza un avión. Los pasajeros realizan reservas para un vuelo específico, indicando asiento y tarifa pagada en el momento de la reserva.

🔗 [Enlace del Ejercicio 8](https://drive.google.com/file/d/1qab-sqrWSFkJrjVkPFZVbBP4fD6BjR2n/view?usp=sharing)

## Modelo SQL

```
create table Avion (
    matricula varchar(10) primary key,
    modelo varchar(60) not null,
    capacidad int not null
);

create table Vuelo (
    num_vuelo varchar(10) primary key,
    fecha date not null,
    origen varchar(60) not null,
    destino varchar(60) not null,
    matricula varchar(10) not null,
    foreign key (matricula) references Avion(matricula)
);

create table Pasajero (
    id_pasajero int auto_increment primary key,
    documento varchar(20) unique not null,
    nombre varchar(100) not null
);

create table Reserva (
    id_reserva int auto_increment primary key,
    asiento varchar(5) not null,
    tarifa_pagada decimal(10,2) not null,
    num_vuelo varchar(10) not null,
    id_pasajero int not null,
    unique (num_vuelo, asiento),
    foreign key (num_vuelo) references Vuelo(num_vuelo),
    foreign key (id_pasajero) references Pasajero(id_pasajero)
);
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
create table Manager (
    id_manager int auto_increment primary key,
    nombre varchar(100) not null
);

create table Artista (
    nif varchar(9) primary key,
    nombre_completo varchar(150) not null,
    id_manager int not null,
    foreign key (id_manager) references Manager(id_manager)
);

create table Evento_Promocion (
    id_evento int auto_increment primary key,
    fecha date not null,
    num_asistentes int not null
);

create table Artista_Evento (
    nif varchar(9) not null,
    id_evento int not null,
    primary key (nif, id_evento),
    foreign key (nif) references Artista(nif),
    foreign key (id_evento) references Evento_Promocion(id_evento)
);
```
---

## 📘 Ejercicio 6: Tienda Informática

Se desea crear una aplicación para la gestión de una tienda informática. La tienda dispone de una serie de productos que se venden a los clientes. De cada producto informático se desea guardar el código, descripción, precio y número de existencias. De cada cliente se desea guardar el código, nombre, apellidos, dirección y número telefónico. Un cliente puede comprar varios productos en la tienda y un mismo producto puede ser comprado por varios clientes. Cada vez que se compre un artículo quedará registrada la compra en la base de datos junto con la fecha en la que se compró el artículo. La tienda tiene contactos con varios proveedores que son los que suministran los productos. Un mismo producto puede ser suministrado por varios proveedores. De cada proveedor se desea guardar el código, nombres, apellidos, dirección, provincia y número de teléfono.

🔗 [Enlace del Ejercicio 10](https://drive.google.com/file/d/1KS3dyAlMtWwXKQrA7DpE6R_zKvzOlbh2/view?usp=sharing)

## Modelo SQL

```
create table Cliente (
    cod_cliente int auto_increment primary key,
    nombre varchar(60) not null,
    apellidos varchar(60) not null,
    direccion varchar(150) not null,
    telefono varchar(15) not null
);

create table Producto (
    cod_producto int auto_increment primary key,
    descripcion varchar(150) not null,
    precio decimal(10,2) not null,
    existencias int not null
);

create table Proveedor (
    cod_proveedor int auto_increment primary key,
    nombres varchar(60) not null,
    apellidos varchar(60) not null,
    direccion varchar(150) not null,
    provincia varchar(60) not null,
    telefono varchar(15) not null
);

create table Compra (
    cod_cliente int not null,
    cod_producto int not null,
    fecha date not null,
    primary key (cod_cliente, cod_producto, fecha),
    foreign key (cod_cliente) references Cliente(cod_cliente),
    foreign key (cod_producto) references Producto(cod_producto)
);

create table Suministra (
    cod_proveedor int not null,
    cod_producto int not null,
    primary key (cod_proveedor, cod_producto),
    foreign key (cod_proveedor) references Proveedor(cod_proveedor),
    foreign key (cod_producto) references Producto(cod_producto)
);
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
create table Genero_Musical (
    id_genero int auto_increment primary key,
    nombre varchar(60) unique not null
);

create table Cantante (
    id_cantante int auto_increment primary key,
    nombre varchar(100) not null,
    pais varchar(60) not null
);

create table Disco (
    id_disco int auto_increment primary key,
    titulo varchar(150) not null,
    precio decimal(10,2) not null,
    id_genero int not null,
    id_cantante int not null,
    foreign key (id_genero) references Genero_Musical(id_genero),
    foreign key (id_cantante) references Cantante(id_cantante)
);

create table Cancion (
    id_cancion int auto_increment primary key,
    titulo varchar(150) not null
);

create table Disco_Cancion (
    id_disco int not null,
    id_cancion int not null,
    posicion int not null,
    primary key (id_disco, id_cancion),
    unique (id_disco, posicion),
    foreign key (id_disco) references Disco(id_disco),
    foreign key (id_cancion) references Cancion(id_cancion)
);
```
---

## 📘 Ejercicio 8: Camiones

Se desea informatizar la gestión de una empresa de transporte que reparte paquetes por toda España. Los encargados de llevar los paquetes son los camioneros, de los que se quiere guardar la cédula, nombre, teléfono, dirección, salario y población en que vive. De los paquetes transportados interesa conocer el código del paquete, descripción, destinatario y dirección del destinatario.

Un camionero distribuye muchos paquetes, y un paquete sólo puede ser distribuido por un camionero. De las provincias a las que llegan los paquetes interesa guardar el código de provincia y el nombre. Un paquete sólo puede llegar a una provincia. Sin embargo, a una provincia pueden llegar varios paquetes.

De los camiones que llevan los camioneros, interesa conocer la matrícula, modelo, tipo y potencia. Un camionero puede conducir diferentes camiones en fechas diferentes, y un camión puede ser conducido por varios camioneros.

🔗 [Enlace del Ejercicio 12](https://drive.google.com/file/d/18QR0joCmPk_V-HuVbGeWiad6jFG-YyWr/view?usp=sharing)

## Modelo SQL

```
create table Camionero (
    cedula varchar(10) primary key,
    nombre varchar(100) not null,
    telefono varchar(15) not null,
    direccion varchar(150) not null,
    salario decimal(10,2) not null,
    poblacion varchar(80) not null
);

create table Provincia (
    cod_provincia int primary key,
    nombre varchar(60) not null
);

create table Paquete (
    cod_paquete int auto_increment primary key,
    descripcion varchar(150) not null,
    destinatario varchar(100) not null,
    dir_destinatario varchar(150) not null,
    cedula_camionero varchar(10) not null,
    cod_provincia int not null,
    foreign key (cedula_camionero) references Camionero(cedula),
    foreign key (cod_provincia) references Provincia(cod_provincia)
);

create table Camion (
    matricula varchar(10) primary key,
    modelo varchar(60) not null,
    tipo varchar(40) not null,
    potencia int not null
);

create table Conduce (
    cedula varchar(10) not null,
    matricula varchar(10) not null,
    fecha date not null,
    primary key (cedula, matricula, fecha),
    foreign key (cedula) references Camionero(cedula),
    foreign key (matricula) references Camion(matricula)
);

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
create table Propietario (
    cedula varchar(10) primary key,
    apellidos varchar(80) not null,
    nombres varchar(80) not null,
    direccion varchar(150) not null
);

create table Telefono_Propietario (
    cedula varchar(10) not null,
    telefono varchar(15) not null,
    primary key (cedula, telefono),
    foreign key (cedula) references Propietario(cedula)
);

create table Familiar (
    cedula_propietario varchar(10) not null,
    cedula varchar(10) unique not null,
    nombre varchar(100) not null,
    telefono varchar(15) not null,
    primary key (cedula_propietario, cedula),
    foreign key (cedula_propietario) references Propietario(cedula)
);

create table Mascota (
    id_mascota int auto_increment primary key,
    nombre varchar(60) not null,
    fecha_nacimiento date not null,
    tipo varchar(40) not null,
    cedula_propietario varchar(10) not null,
    foreign key (cedula_propietario) references Propietario(cedula)
);

create table Personal (
    codigo varchar(10) primary key,
    cedula varchar(10) not null,
    nombre varchar(100) not null
);

create table Veterinario (
    codigo varchar(10) primary key,
    fecha_alta date not null,
    especialidad varchar(80) not null,
    foreign key (codigo) references Personal(codigo)
);

create table Auxiliar (
    codigo varchar(10) primary key,
    base_cotizacion decimal(10,2) not null,
    foreign key (codigo) references Personal(codigo)
);

create table Consulta (
    id_consulta int auto_increment primary key,
    fecha date not null,
    diagnostico text not null,
    id_mascota int not null,
    codigo_veterinario varchar(10) not null,
    foreign key (id_mascota) references Mascota(id_mascota),
    foreign key (codigo_veterinario) references Veterinario(codigo)
);
```
