# Sistema de Biblioteca Escolar

Evaluación Final Transversal de Desarrollo Orientado a Objetos II. 
Aplicación de escritorio en Java que permite administrar una biblioteca escolar, registrar préstamos y devoluciones y consultar reportes mediante una base de datos MySQL.

## Funcionalidades

### Bibliotecario

- Administración de libros, estudiantes, categorías y usuarios mediante operaciones CRUD.
- Registro de préstamos y devoluciones.
- Consulta de disponibilidad y actualización del stock.
- Cálculo automático de vencimientos y días de atraso.
- Reportes de libros más prestados, historial por estudiante y préstamos abiertos.

### Estudiante

- Consulta del catálogo.
- Solicitud de préstamos.
- Devolución de sus propios préstamos.
- Consulta de su historial.

Las cuentas estudiantiles se vinculan con los registros de estudiantes mediante el RUT.

## Diseño orientado a objetos

El proyecto implementa los siguientes principios y patrones:

- **Herencia y abstracción:** `Persona` y `Usuario` son clases abstractas que reúnen características comunes.
- **Polimorfismo:** las subclases `Bibliotecario` y `UsuarioEstudiante` implementan permisos diferentes mediante `puedeAdministrar()`.
- **Interfaces:** `Entidad` y `CrudDAO` definen contratos comunes.
- **MVC:** separación entre modelos, vistas y controladores.
- **DAO:** encapsulación de las operaciones de persistencia.
- **Singleton:** `DatabaseConnection` administra una única instancia de conexión JDBC.

## Concurrencia y consistencia

Las operaciones de acceso a datos se ejecutan mediante `SwingWorker` para mantener disponible la interfaz gráfica.

El servicio utiliza métodos `synchronized` en operaciones críticas. El registro del préstamo y la reducción del stock se realizan dentro de una transacción. El stock solo disminuye cuando existen ejemplares disponibles.

Las devoluciones utilizan bloqueo de filas para impedir que un mismo préstamo se devuelva dos veces. Si ocurre un error durante una transacción, sus cambios se revierten.

## Estructura del proyecto

```text
src/main/java/cl/eft/biblioteca/
├── model/
├── view/
├── controller/
├── service/
├── dao/
├── config/
└── util/

src/test/java/
sql/
config/
dist/
docs/
pom.xml
```

## Ejecución

Desde la carpeta raíz del proyecto, ejecutar:

```bat
ejecutar.bat
```

También es posible iniciar la aplicación con:

```bash
java -jar dist/biblioteca.jar
```

El JAR incluye el controlador JDBC. Para funcionar requiere un servidor MySQL disponible y la configuración local de conexión.

En IntelliJ IDEA, abrir `pom.xml`, cargar las dependencias Maven y ejecutar la clase:

```text
cl.eft.biblioteca.App
```

El directorio de trabajo debe ser la carpeta raíz del proyecto.

## Cuentas de demostración

Después de ejecutar el poblamiento oficial y convertir las contraseñas:

| Rol | Correo | Contraseña |
|---|---|---|
| Bibliotecario | antonia@correo.cl | clave123 |
| Estudiante | carlos@correo.cl | clave123 |
| Estudiante | maria@correo.cl | clave123 |

Estas cuentas corresponden a los datos de ejemplo de la actividad.

