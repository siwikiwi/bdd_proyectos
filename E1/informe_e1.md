# Informe Entrega 1 - Bases de datos IIC2413

### Datos del Alumno
| **Apellidos**       | **Nombres**          | **Número de Alumno** |
|---------------------|----------------------|----------------------|
|ULLOA       | VANIA |111111111111           |

### 1. Modelo Entidad-Relación (E/R)
<!-- Inserta aquí tu diagrama ER. Usa el formato svg para evitar la perdida de calidad. Reemplaza "diagrama.svg" por la ruta a tu archivo -->

![Diagrama E/R](diagrama_final.drawio.svg)

### 2. Entidades Débiles
identifiqué las siguientes entidades débiles: 
 - Receta 
 - Orden
 - Orden_examen
 - Orden_procedimiento

#### 2.1
#### Entidad_Receta
Se identifico **receta** como entidad débil porque su existencia depende directamente de consulta medica

#### Entidad_Orden
Se identifico **orden** como entidad débil porque su existencia depende directamente de consulta medica

#### Entidad_Orden_examen
Se identifico **orden_examen** como entidad débil porque su existencia depende directamente de orden

#### Entidad_Orden_procedimiento
Se identifico **Orden_procedimiento** como entidad débil porque su existencia depende directamente de orden



## 3.1 Llaves primarias simples

- **persona** PK : `id_persona`  
  La llave primaria de **persona** es (**id_persona**) porque identifica de forma única a cada persona del sistema.

- **paciente** PK :  `id_persona`  
  La llave primaria de **paciente** es (**id_persona**) porque es una subclase de persona y reutiliza el mismo identificador.

- **trabajador** PK :  `id_persona`  
  La llave primaria de **trabajador** es (**id_persona**) porque hereda directamente de persona y no requiere un id nuevo.

- **staff_medico** PK :  `id_persona`  
  La llave primaria de **staff_medico** es (**id_persona**) porque es una especialización de trabajador.

- **administrativo** PK : `id_persona`  
  La llave primaria de **administrativo** es (**id_persona**) porque es otra especialización de trabajador.

- **apoyo_medico** PK : `id_persona`  
  La llave primaria de **apoyo_medico** es (**id_persona**) porque es subclase de staff_medico.

- **medico**PK :  `id_persona`  
  La llave primaria de **medico** es (**id_persona**) porque es subclase de staff_medico y mantiene el mismo identificador.

- **consulta_medica** PK :  `id_consulta`  
  La llave primaria de **consulta_medica** es (**id_consulta**) porque cada atención se identifica con un número único de consulta.

- **farmacia** PK : `codigo`  
  La llave primaria de **farmacia** es (**codigo**) porque cada producto del catálogo se identifica con un código único.

- **catalogo_onu**PK : `codigo_onu`  
  La llave primaria de **catalogo_onu** es (**codigo_onu**) porque cada clasificación ONU tiene un código único.

- **institucion_salud** PK : `codigo_ministerial`  
  La llave primaria de **institucion_salud** es (**codigo_ministerial**) porque el registro ministerial identifica a cada institución.

- **isapre** PK : `codigo_ministerial`  
  La llave primaria de **isapre** es (**codigo_ministerial**) porque es subclase de institucion_salud y usa el mismo identificador.

- **fonasa** PK : `codigo_ministerial`  
  La llave primaria de **fonasa** es (**codigo_ministerial**) porque es subclase de institucion_salud y reutiliza ese id.

- **arancel_fonasa** PK : `codigo`  
  La llave primaria de **arancel_fonasa** es (**codigo**) porque cada prestación FONASA se codifica de forma única.

- **arancel_dcc** PK : `codigo_interno`  
  La llave primaria de **arancel_dcc** es (**codigo_interno**) porque en el arancel particular cada ítem se identifica por su código interno.


## 3.2 Llaves primarias compuestas

- **titular_de_prevision** PK : `(id_persona, cod_prevision)`  
La llave compuesta de **titular_de_prevision** es (**id_persona**, **cod_prevision**) porque una misma persona podría estar asociada a distintas instituciones en el tiempo y la combinación persona–previsión define el registro.

- **beneficiario** PK : `(id_persona, id_titular, cod_prevision)`  
La llave compuesta de **beneficiario** es (**id_persona**, **id_titular**, **cod_prevision**) porque el beneficiario queda determinado por la persona que usa la cobertura, el titular y la previsión específica de ese titular.

- **receta** PK : `(id_consulta, id_receta)`  
  La llave compuesta de **receta** es (**id_consulta**, **id_receta**) porque las recetas se numeran dentro de cada consulta y no globalmente.

- **receta_psicotropico**PK : `(id_consulta, id_receta)`  
  La llave compuesta de **receta_psicotropico** es (**id_consulta**, **id_receta**) porque hereda la identidad de la receta base y agrega atributos propios (como el código de autorización).

- **receta_no_psicotropico** PK :  `(id_consulta, id_receta)`  
  La llave compuesta de **receta_no_psicotropico** es (**id_consulta**, **id_receta**) porque también hereda la identidad de la receta base.

- **items** PK : `(id_consulta, id_receta, codigo)`  
  La llave compuesta de **items** es (**id_consulta**, **id_receta**, **codigo**) porque cada línea de receta se identifica por la receta a la que pertenece y el producto del catálogo.

- **orden**PK : `(id_consulta, id_orden)`  
  La llave compuesta de **orden** es (**id_consulta**, **id_orden**) porque las órdenes se numeran dentro de la consulta médica.

- **orden_examen** PK : `(id_consulta, id_orden, id_examen)`  
  La llave compuesta de **orden_examen** es (**id_consulta**, **id_orden**, **id_examen**) porque cada examen está ligado a una orden específica dentro de una consulta.

- **orden_procedimiento** PK :  `(id_consulta, id_orden, id_proced)`  
  La llave compuesta de **orden_procedimiento** es (**id_consulta**, **id_orden**, **id_proced**) porque cada procedimiento está ligado a una orden específica dentro de una consulta.

- **detalle_examen** PK`(id_consulta, id_orden, id_examen)`  
  La llave compuesta de **detalle_examen** es (**id_consulta**, **id_orden**, **id_examen**) porque detalla el cobro del examen asociado a esa orden en esa consulta.

- **detalle_procedimiento** PK`(id_consulta, id_orden, id_proced)`  
  La llave compuesta de **detalle_procedimiento** es (**id_consulta**, **id_orden**, **id_proced**) porque detalla el cobro del procedimiento asociado a esa orden en esa consulta.

- **bonificacion_grupo** PK`(codigo_ministerial, grupo)`  
  La llave compuesta de **bonificacion_grupo** es (**codigo_ministerial**, **grupo**) porque cada isapre define una bonificación por grupo FONASA, y la combinación institución–grupo es única.

## 4. Relaciones 

### Relación_EsBeneficiario
- Involucra a **Persona** con **TitularDePrevisión**, porque una persona puede ser beneficiaria o no de un titular, y cada titular puede tener asignado un beneficiario.  
- *Ejemplo*: pinocho puede ser beneficiario del titular geppetto, y gepetto puede tener afiliados a pinocho y a pepito grillo

### Relación_Afiliado
- Involucra a **Persona** con **InstituciónPrevisionalDeSalud**, porque cada persona está afiliada a una única institución previsional, y una institución puede tener muchos afiliados.  
- *Ejemplo*: El **Dr. Iván Goic**, como persona, está afiliado a FONASA y FONASA puede tener a Gepetto y Pinocho como afiliados.  

- Igual involucra a staff medico con las instituciones de salud, pues en el enunciado dice que un staff medico solo puede ser titular, entonces aqui los conecto directamente para que forzadamente esten afiliados a algun plan ellos directamente. 

### Relación_participan en consulta
- Involucra a **Médico** con **Consulta**, porque un médico puede realizar múltiples consultas médicas, y cada consulta está asociada a un único médico.  
- *Ejemplo*: El **Dr. Iván Goic** puede realizar 5 consultas médicas, y esas 5 están asociadas solo a él.  

### Relación_participan en consulta
- Involucra a **Paciente** con **Consulta**, porque un paciente puede asistir múltiples consultas médicas.
y n consultas medicas podrían estar asociados a un paciente.

- ejemplo: Gepetto asiste a 10 consultas medicas, y esas 10 consultas medicas están asociadas a Gepetto.

### Relación_Emite
- Involucra a **ConsultaMédica** con **Receta**, porque en una consulta se pueden emitir varias recetas.  
- Involucra a **ConsultaMédica** con **Orden**, porque en una consulta se pueden emitir múltiples órdenes médicas.  
- *Ejemplo*: En una consulta con el **Dr. Iván Goic**, se pueden emitir recetas para paracetamol, ibuprofeno y naproxeno (3 recetas distintas).  

### Relación_Indica
- Involucra a **Orden** con **OrdenExamen/OrdenProcedimiento**, porque una orden puede indicar múltiples exámenes o procedimientos médicos.  
- *Ejemplo*: El **Dr. Iván Goic** puede indicar en una sola orden que el paciente realice: hemograma, perfil lipídico, perfil bioquímico y glucosa en sangre. Es decir, 4 exámenes distintos en 1 orden.  

### Relación_detalle
- Involucra a **OrdenExamen/OrdenProcedimiento** con **ArancelDCC_Colita / ArancelFONASA / BonificaciónISAPRE**, porque un examen o procedimiento puede cobrarse como particular (precio original), por FONASA o por ISAPRE.  
- *Ejemplo*: Un hemograma puede cobrarse según el valor de FONASA, o bien según un arancel particular de DCC Olita.  

### Relación_bonifica
- Involucra a **ISAPRE** con **BONIFICACION_ISAPRE**, porque cada ISAPRE ofrece múltiples planes, y cada plan está ligado a una única ISAPRE.  
- *Ejemplo: ISAPRE Colmena tiene el Plan A y el Plan B; ambos provienen de Colmena.  


### Relación_Bonifica
- Involucra a **FONASA** con **Arancel_FONASA**, porque FONASA puede bonificar múltiples aranceles, y cada arancel pertenece a esa institución.  
- *Ejemplo*: FONASA bonifica los aranceles de procedimientos como consulta médica, hemograma o radiografía.  

### Relación_RecetaPsicotrópico: especifica
- Involucra a **RecetaPsicotrópico** con **ÍtemPsicotrópico**, porque cada receta psicotrópica está asociada a un único ítem psicotrópico.  
- *Ejemplo*: El **Dr. Iván Goic** emite una receta psicotrópica para clonazepam 434342mg, esa receta corresponde a un único ítem psicotrópico.  

### Relación_RecetaNoPsicotrópico: especifica
- Involucra a **RecetaNoPsicotrópico** con **Ítems**, porque una receta no psicotrópica puede contener varios ítems.  
- *Ejemplo*: El **Dr. Iván Goic** emite una receta no psicotrópica que incluye paracetamol e ibuprofeno, ambos como ítems distintos en una sola receta.   

### Relación_ContenidoEn
- Involucra a **Ítems** con **Farmacia**, porque los ítems deben estar contenidos en el inventario de una farmacia.  
- *Ejemplo*: El ítem “Ibuprofeno 400mg” está contenido en la **Farmacia Dr.Simi**.  

### Relación_RegistradosEn
- Involucra a **Farmacia** con **CatálogoONU_Fármacos**, porque los fármacos de la farmacia deben estar registrados en el catálogo de la ONU.  
- *Ejemplo*: El ítem “Morfina” de la farmacia está registrado en el **Catálogo ONU de Fármacos** 



### 5. Cardinalidades

### Relación_EsBeneficiario
- **Cardinalidad**:  
  - De **Persona** a **TitularDePrevisión**: N : 0 a 1  (n, 0 a 1)
  - De **TitularDePrevisión** a **Persona**: 1 : N  
- **Justificación**: Muchas personas pueden ser beneficiarias de un mismo titular, pero cada persona tiene como máximo un titular asignado.  
- *Ejemplo*: Pinocho puede ser beneficiario del titular Geppetto; Geppetto puede tener afiliados a Pinocho y Pepito Grillo.  


### Relación_Afiliado
- **Cardinalidad**:  
  - De **TITULAR DE PREVISION* a **InstituciónPrevisionalDeSalud**: N : 1  
  - De **InstituciónPrevisionalDeSalud** a **Persona**: 1 : N  
- **Justificación**: Cada persona está afiliada a una única institución previsional, pero una institución puede tener muchos afiliados.  
  - De **Staff medico** a **Institución de salud** 
    forzados porque el enunciado lo indica. 

- ej: El **Dr. Iván Goic** (del staff_medico), como persona, está afiliado a FONASA, y FONASA puede tener afiliados a Geppetto y Pinocho. 

También aplica a **StaffMédico**, ya que el enunciado indica que un staff médico solo puede ser titular, por lo que se fuerza a que estén afiliados directamente a una institución.  


### Relación_ParticipanEnConsulta (Médico–Consulta)
- **Cardinalidad**:  
  - De **Médico** a **Consulta**: 1 : N  
  - De **Consulta** a **Médico**: N : 1  
- **Justificación**: Un médico puede realizar muchas consultas, pero cada consulta médica es realizada por un único médico.  
- *Ejemplo*: El **Dr. Iván Goic** puede realizar 5 consultas médicas, y esas 5 están asociadas solo a él.  


### Relación_ParticipanEnConsulta (Paciente–Consulta)
- **Cardinalidad**:  
  - De **Paciente** a **Consulta**: 1 : N  
  - De **Consulta** a **Paciente**: N : 1  
- **Justificación**: Un paciente puede asistir a muchas consultas médicas, pero cada consulta está asociada a un único paciente.  
- *Ejemplo*: Geppetto asiste a 10 consultas médicas, y esas 10 consultas están asociadas solo a él.  

### Relación_Emite (Consulta–Receta / Orden)
- **Cardinalidad**:  
  - De **Consulta** a **Receta**: 0 a 1 : N  (0 a 1, n)
  - De **Receta** a **Consulta**: 0 a 1 : 1  (n,1)
  - De **Consulta** a **Orden**: 0 a 1 : N  (0 a 1, n)
  - De **Orden** a **Consulta**: N : 1  (n,1)
- **Justificación**: Una consulta puede emitir varias recetas y órdenes (o no emitir), pero cada receta u orden proviene de una sola consulta.  
- *Ejemplo*: En una consulta con el **Dr. Iván Goic**, se pueden emitir recetas para paracetamol, ibuprofeno y naproxeno (3 recetas distintas).  



### Relación_Indica (Orden–OrdenExamen/OrdenProcedimiento)
- **Cardinalidad**:  
  - De **Orden** a **OrdenExamen/OrdenProcedimiento**: 1 : N  (1,n)
  - De **OrdenExamen/OrdenProcedimiento** a **Orden**: N : 1   (n,1)
- **Justificación**: Una orden puede indicar muchos exámenes/procedimientos, pero cada examen/procedimiento pertenece a una sola orden.  


### Relación_Específica (RecetaPsicotrópico–ÍtemPsicotrópico)
- **Cardinalidad**:  
  - De **RecetaPsicotrópico** a **ÍtemPsicotrópico**: 1 : 1  
  - De **ÍtemPsicotrópico** a **RecetaPsicotrópico**: 1 : 1  
- **Justificación**: Cada receta psicotrópica corresponde a un único ítem, y cada ítem psicotrópico pertenece a una receta específica. 


### Relación_Específica (RecetaNoPsicotrópico–Ítems)
- **Cardinalidad**:  
  - De **RecetaNoPsicotrópico** a **Ítems**: 1 : N  
  - De **Ítems** a **RecetaNoPsicotrópico**: N : 1  
- **Justificación**: Una receta no psicotrópica puede incluir múltiples ítems, pero cada ítem está asociado a una receta.  

### Relación_ContenidoEn (Ítems–Farmacia)
- **Cardinalidad**:  
  - De **Farmacia** a **Ítems**: 1 : N  
  - De **Ítems** a **Farmacia**: N : 1  
- **Justificación**: Una farmacia puede tener muchos ítems en stock, pero cada ítem pertenece a una sola farmacia.  

### Relación_RegistradosEn (Farmacia–CatálogoONU_Fármacos)
- **Cardinalidad**:  
  - De **CatálogoONU_Fármacos** a **Farmacia**: 1 : N  
  - De **Farmacia** a **CatálogoONU_Fármacos**: N : 1  
- **Justificación**: Cada ítem farmacéutico está registrado en un único catálogo ONU, pero un catálogo puede agrupar muchos ítems de farmacias distintas.  

### Relación_Bonifica (Instituciones de Salud)
- **Cardinalidad**:  
  - De **FONASA** a **ArancelFONASA**: 1 : N  
  - De **ArancelFONASA** a **FONASA**: N : 1  
  - De **ISAPRE** a **BonificaciónISAPRE**: 1 : N  
  - De **BonificaciónISAPRE** a **ISAPRE**: N : 1  
- **Justificación**: Cada institución previsional (FONASA o ISAPRE) define muchos aranceles o bonificaciones, pero cada arancel o bonificación proviene de una sola institución. 

<!-- Identifica y justifica TODAS las jerarquías -->
#### 6.1 Entidad_Padre - Entidad_Hija1 - Entidad_Hija2

### ENTIDAD PADRE: **Persona**  
**ENTIDADES HIJAS:**  
- **Paciente**  
- **Trabajador**

**Justificación:**  
- Una persona puede ser paciente, trabajador, o ambas cosas.  
- Si se guardara el “rol” en un solo campo, se rompería 1NF y habría muchos nulos.  
- Con subclases, cada rol tiene solo los atributos que le aplican.

**Tipo de jerarquía:**  
- **Parcial**: no toda persona es paciente o trabajador.  
- **Superposición (overlap)**: una persona puede ser a la vez paciente y trabajador.


### ENTIDAD PADRE: **Trabajador**  
**ENTIDADES HIJAS:**  
- **Staff_Médico**  
- **Administrativo**

**Justificación:**  
- Algunos trabajadores realizan funciones clínicas y otros administrativas.  
- Evita guardar atributos clínicos en administrativos (nulos).

**Tipo de jerarquía:**  
- **Disjunta**: un trabajador no es a la vez staff médico y administrativo.  
- **Parcial**: podrían existir otros tipos de trabajador.

### ENTIDAD PADRE: **Staff_Médico**  
**ENTIDADES HIJAS:**  
- **Apoyo_Médico**  
- **Médico**

**Justificación:**  
- Dentro del staff hay roles distintos: médicos (atienden, firman recetas) y apoyo (asisten en procedimientos).  
- Refleja reglas de negocio: solo médicos pueden firmar recetas.

**Tipo de jerarquía:**  
- **Disjunta**: un staff no es médico y apoyo a la vez.  
- **Parcial**: podrían existir más roles clínicos.


### ENTIDAD PADRE: **Institucion_Salud**  
**ENTIDADES HIJAS:**  
- **FONASA**  
- **ISAPRE**

**Justificación:**  
- Son tipos diferentes de institución previsional.  
- Comparten atributos comunes (código, nombre) pero difieren en sus funciones.  
- Se evitan atributos “tipo” con valores múltiples.

**Tipo de jerarquía:**  
- **Disjunta**: una institución es FONASA o ISAPRE.  

### 7. Esquema Relacional
<!-- Construye el esquema relacional a partir de tu Modelo E/R -->

CREATE TABLE persona (
    id_persona INT NOT NULL,
    run TEXT NOT NULL,
    nombres TEXT NOT NULL,
    apellidos TEXT NOT NULL,
    direccion TEXT,
    correo TEXT,
    telefono TEXT,
    PRIMARY KEY (id_persona),
    UNIQUE (run)
);


----ahora las afiliaciones a alguna insti de salud las tiene directamente el paciente, que puede tener o no tener---

esta tabla sale de una relacion entre persona--es beneficiario---y entidad titular_de_prevision

luego, titular tiene solo la tabla de titulares

CREATE TABLE titular_de_prevision (
    id_persona    INT NOT NULL,  
    cod_prevision INT NOT NULL,  
    PRIMARY KEY (id_persona, cod_prevision),
    FOREIGN KEY (id_persona) REFERENCES persona(id_persona) ON DELETE CASCADE,
    FOREIGN KEY (cod_prevision) REFERENCES institucion_salud(codigo_ministerial)
);
CREATE TABLE beneficiario (
    id_persona    INT NOT NULL, 
    id_titular    INT NOT NULL, 
    cod_prevision INT NOT NULL,  
    PRIMARY KEY (id_persona, id_titular, cod_prevision),
    FOREIGN KEY (id_persona) REFERENCES persona(id_persona) ON DELETE CASCADE,
    FOREIGN KEY (id_titular, cod_prevision) 
        REFERENCES titular_de_prevision(id_persona, cod_prevision) ON DELETE CASCADE
);


---subclases de persona--
CREATE TABLE paciente (
    id_persona INT,
    PRIMARY KEY (id_persona),
    FOREIGN KEY (id_persona) REFERENCES persona(id_persona)
    ON DELETE CASCADE
); 

CREATE TABLE trabajador (
    id_persona INT,
    PRIMARY KEY (id_persona),
    FOREIGN KEY (id_persona) REFERENCES persona(id_persona)
    ON DELETE CASCADE
); 

--subclase de trabajador---
CREATE TABLE staff_medico (
    id_persona INT,
    profesion TEXT NOT NULL,
    PRIMARY KEY (id_persona),
    FOREIGN KEY (id_persona) REFERENCES trabajador(id_persona)
    ON DELETE CASCADE
); 


CREATE TABLE administrativo (
    id_persona INT,
    PRIMARY KEY (id_persona),
    FOREIGN KEY (id_persona) REFERENCES trabajador(id_persona)
    ON DELETE CASCADE
); 

--subclase de staff medico--

CREATE TABLE apoyo_medico (
    id_persona INT,
    PRIMARY KEY (id_persona),
    FOREIGN KEY (id_persona) REFERENCES staff_medico(id_persona)
    ON DELETE CASCADE
); 


CREATE TABLE medico (
    id_persona INT,
    PRIMARY KEY (id_persona),
    FOREIGN KEY (id_persona) REFERENCES staff_medico(id_persona)
    ON DELETE CASCADE
); 

CREATE TABLE consulta_medica (
    id_consulta INT NOT NULL,
    fecha DATE,
    id_paciente INT NOT NULL, 
    id_medico INT NOT NULL, 
    PRIMARY KEY (id_consulta),
    FOREIGN KEY (id_paciente) REFERENCES paciente(id_persona), 
    FOREIGN KEY (id_medico) REFERENCES medico(id_persona)
); 


-----recetas --- 
receta es entidad debil de consulta_medica, no puse el id_paciente y id_medico en receta porque ya estan en conuslta medica, y se pueden obtener mediante joins

SUPERCLASE receta: 

CREATE TABLE receta (
    id_consulta INT,
    id_receta INT,
    diagnostico TEXT,
    firma_medico TEXT NOT NULL,
    PRIMARY KEY (id_consulta, id_receta),
    FOREIGN KEY (id_consulta) REFERENCES consulta_medica(id_consulta)
    ON DELETE CASCADE
); 

subclases de recetas: 

CREATE TABLE receta_psicotropico(
    id_receta INT,
    id_consulta INT,
    cod_autorizacion VARCHAR(50) NOT NULL,
    PRIMARY KEY (id_receta, id_consulta),
    FOREIGN KEY(id_consulta, id_receta) REFERENCES receta(id_consulta, id_receta) 
    ON DELETE CASCADE,
    UNIQUE (cod_autorizacion)
); 

CREATE TABLE receta_no_psicotropico(
    id_receta INT,
    id_consulta INT,
    PRIMARY KEY (id_receta, id_consulta),
    FOREIGN KEY(id_consulta, id_receta) REFERENCES receta(id_consulta, id_receta) 
    ON DELETE CASCADE
); 

---cada una de estas recetas, se relacionan segun una relacion especifica---> items-- 
items, contiene de atributo las especificaciones de cada medicamento indicado en la receta medica. 
los items se encuentran contenidos en farmacia...


CREATE TABLE FARMACIA(
    codigo INT NOT NULL, 
    nombre TEXT NOT NULL, 
    descripcion TEXT,
    tipo TEXT, 
    valor INT, 
    PRIMARY KEY (codigo)
); 

CREATE TABLE items(
    id_consulta INT,
    id_receta INT,
    codigo INT,
    indicaciones TEXT,
    PRIMARY KEY (id_consulta, id_receta, codigo),
    FOREIGN KEY (id_consulta, id_receta) REFERENCES receta(id_consulta, id_receta)
    ON DELETE CASCADE, 
    FOREIGN KEY (codigo) REFERENCES farmacia(codigo)
); 

CREATE TABLE catalogo_onu(
    codigo_onu INT NOT NULL,
    clasificacion TEXT NOT NULL,
    PRIMARY KEY (codigo_onu)
); 


---aqui pongo las ordenes: proced/examen--

CREATE TABLE orden (
    id_consulta INT,
    id_orden INT,
    diagnostico TEXT,
    firma_medico TEXT NOT NULL,
    PRIMARY KEY (id_consulta, id_orden),
    FOREIGN KEY (id_consulta) REFERENCES consulta_medica(id_consulta)
        ON DELETE CASCADE
);

-- Cada orden puede indicar varios exámenes

CREATE TABLE orden_examen (
    id_consulta INT,
    id_orden INT
    id_examen TEXT NOT NULL,
    especialidad TEXT,
    PRIMARY KEY (id_consulta, id_orden, id_examen),
    FOREIGN KEY (id_consulta, id_orden) REFERENCES orden(id_consulta, id_orden)
        ON DELETE CASCADE
);

-- Y también varios procedimientos

CREATE TABLE orden_procedimiento (
    id_consulta INT,
    id_orden INT,
    id_proced TEXT NOT NULL,
    especialidad TEXT,
    PRIMARY KEY (id_consulta, id_orden, id_proced),
    FOREIGN KEY (id_consulta, id_orden) REFERENCES orden(id_consulta, id_orden)
        ON DELETE CASCADE
);

----luego, las ordenes, tienen un detalle para poder cobrar--- 

detalle es una relacion que se involucra directamente con orden_examen y orden_procedimiento, y se conectan estas dos con arancel_dcc (que es el arancel particular)... 

CREATE TABLE arancel_dcc (
    codigo_interno TEXT,
    codigo TEXT,
    valor_particular INT NOT NULL,
    PRIMARY KEY (codigo_interno),
    FOREIGN KEY (codigo) REFERENCES arancel_fonasa(codigo)
);

ENTONCES CREAMOS DETALLE PARA AMBOS...

CREATE TABLE detalle_examen (
    id_consulta INT,
    id_orden INT,
    id_examen TEXT,
    codigo_interno TEXT,   -- referencia al arancel particular
    PRIMARY KEY (id_consulta, id_orden, id_examen),
    FOREIGN KEY (id_consulta, id_orden, id_examen)
        REFERENCES orden_examen(id_consulta, id_orden, id_examen)
        ON DELETE CASCADE,
    FOREIGN KEY (codigo_interno)
        REFERENCES arancel_dcc(codigo_interno)
);

CREATE TABLE detalle_procedimiento (
    id_consulta INT,
    id_orden INT,
    id_proced TEXT,
    codigo_interno TEXT,   -- referencia al arancel particular
    PRIMARY KEY (id_consulta, id_orden, id_proced),
    FOREIGN KEY (id_consulta, id_orden, id_proced)
        REFERENCES orden_procedimiento(id_consulta, id_orden, id_proced)
        ON DELETE CASCADE,
    FOREIGN KEY (codigo_interno)
        REFERENCES arancel_dcc(codigo_interno)
);

---- INSTITUCIONES DE SALUD --- 

es una super clase institucion de salud 
-- Superclase
CREATE TABLE institucion_salud (
    codigo_ministerial INT NOT NULL,
    nombre TEXT NOT NULL,
    tipo TEXT,
    rut TEXT UNIQUE,
    enlace TEXT,
    PRIMARY KEY (codigo_ministerial)
);

-- Subclases simples
CREATE TABLE isapre (
    codigo_ministerial INT NOT NULL,
    PRIMARY KEY (codigo_ministerial),
    FOREIGN KEY (codigo_ministerial) REFERENCES institucion_salud(codigo_ministerial)
        ON DELETE CASCADE
);

CREATE TABLE fonasa (
    codigo_ministerial INT NOT NULL,
    PRIMARY KEY (codigo_ministerial),
    FOREIGN KEY (codigo_ministerial) REFERENCES institucion_salud(codigo_ministerial)
        ON DELETE CASCADE
);

-- Arancel FONASA (catálogo)
CREATE TABLE arancel_fonasa (
    codigo TEXT NOT NULL,     
    consulta TEXT,            
    grupo TEXT NOT NULL,      
    tipo TEXT,                
    valor_fonasa INT NOT NULL,
    PRIMARY KEY (codigo)
);
-- Bonificación por grupo (de la ISAPRE)
CREATE TABLE bonificacion_grupo (
    codigo_ministerial INT NOT NULL, 
    grupo TEXT NOT NULL,
    bonificacion INT NOT NULL,       
    PRIMARY KEY (codigo_ministerial, grupo),
    FOREIGN KEY (codigo_ministerial) REFERENCES isapre(codigo_ministerial)
        ON DELETE CASCADE
);


### 8. Consistencia y Normalización en BCNF

Partiendo por **persona**, en el archivo proporcionado se vio que los roles pueden ser múltiples, es decir, una persona puede ser trabajador y paciente al mismo tiempo. Esto rompe con 1NF si lo modelamos con un único atributo “rol”, entonces fue mejor diferenciar los roles mediante **jerarquías de subclases** (`paciente`, `trabajador`, etc.), de modo que cada rol hereda directamente de persona. Esto facilita las consultas y evita almacenar varios valores en un mismo campo.

Por otro lado, consideré mejor quitar atributos de **persona** tales como *isapre* (que lo puse como `cod_prevision` para que fuera más descriptivo), quité *tipo*, *titular*, y *profesión*. Esta última porque no necesariamente está indicada para todas las personas, solo para el **staff médico**. Con esto se logra que cada atributo esté en la tabla que realmente le corresponde, evitando valores nulos innecesarios y redundancia.

Proporcioné después la diferenciación entre **personas beneficiarias y titulares**, para facilitar las consultas: no todas las personas son titulares, y estos últimos son los que reciben las bonificaciones de sus órdenes médicas. Separar las tablas `titular_de_prevision` y `beneficiario` ayuda a expresar esa diferencia y a mantener integridad: solo los titulares pueden estar ligados directamente a una institución de salud, mientras que los beneficiarios dependen de un titular.

En **recetas**, identifiqué la diferencia entre distintos tipos para poder aislar los psicotrópicos en una subclase propia. Esto permite tener un control más claro sobre los campos adicionales, como el código de autorización, que aplica solo para ese caso.  
Además, me di cuenta de que una receta puede identificar varios medicamentos o fármacos (especialmente en las no psicotrópicas). Esto podría romper con 1NF, ya que si en una celda guardamos dos medicamentos con dos indicaciones, habría más de un dato por celda. Para solucionarlo, opté por crear la tabla **items**, donde cada fila identifica un medicamento específico asociado a una receta. De esta manera, cada fila almacena un solo dato por columna, cumpliendo con la forma normal.

En **farmacia**, los datos `codigo_onu` y `clasificacion_onu` no cumplían con BCNF, ya que se cumple la dependencia `codigo_onu → clasificacion_onu` pero `codigo_onu` no era llave primaria en farmacia. Para solucionarlo, opté por crear la entidad separada **catalogo_onu**, donde se puede consultar directamente sin romper la normalización y manteniendo las dependencias en su tabla correspondiente.

También, para las **órdenes médicas**, preferí separar exámenes y procedimientos en tablas distintas (`orden_examen` y `orden_procedimiento`), cada una con su PK compuesta. Esto mantiene la consistencia al no mezclar conceptos diferentes en una misma tabla. Los detalles de cobro se modelaron con tablas específicas (`detalle_examen` y `detalle_procedimiento`) que hacen referencia al arancel particular. Esta decisión elimina la necesidad de guardar múltiples precios o códigos en una sola celda, reforzando la 1NF y la consistencia general del modelo.


- **Consistencia:**  
  El modelo asegura consistencia porque:
  - Cada entidad tiene una clave primaria clara que la identifica sin ambigüedades.  
  - Las subclases heredan con PK = FK, lo que refleja correctamente jerarquías de especialización.  
  - Se evita la redundancia: atributos que no aplican a todas las personas se mueven a sus subclases; `id_paciente` e `id_medico` no se repiten en recetas porque ya están en `consulta_medica`.  
  - Se usan catálogos separados (`arancel_fonasa`, `arancel_dcc`, `farmacia`, `catalogo_onu`) para centralizar información que puede ser compartida por varias tablas, evitando duplicación y facilitando las actualizaciones.  
  - La relación entre titulares y beneficiarios asegura que solo personas válidas pueden estar afiliadas, y que los beneficiarios dependen siempre de un titular registrado.  
  - Con estas decisiones, se logra que cada tabla almacene datos consistentes y que las dependencias entre entidades estén claras y sin contradicciones.

- **Normalización en BCNF:**  
  Una tabla está en BCNF si toda dependencia funcional no trivial tiene como determinante una superclave. En este esquema:  
  - En tablas con PK simples (`persona`, `consulta_medica`, `farmacia`, `institucion_salud`, etc.), todos los atributos dependen solo de la PK, sin excepciones.  
  - En tablas con PK compuesta (`receta`, `orden`, `items`, `detalle_examen`, etc.), los atributos dependen de **toda la clave** y no de una parte. Por ejemplo, en `receta(id_consulta, id_receta)`, los atributos `diagnostico` y `firma_medico` dependen de la combinación completa.  
  - El caso de `beneficiario` se mantiene en BCNF bajo la suposición de que un titular puede estar asociado a más de una previsión. Si se asumiera que cada titular tiene una única previsión, entonces la dependencia `id_titular → cod_prevision` violaría BCNF y sería mejor sacar `cod_prevision` de esa tabla.  
  - El catálogo `catalogo_onu` se separó de `farmacia` justamente para cumplir BCNF, ya que `codigo_onu` determinaba `clasificacion_onu` pero no era clave en farmacia.  
  - No hay atributos multivaluados ni dependencias transitivas que obliguen a repetir información.  

En resumen, el modelo cumple con **BCNF** porque todas las dependencias funcionales importantes tienen como determinante una clave primaria, y los casos donde no se cumplía se corrigieron con la separación en entidades adicionales o subclases.
