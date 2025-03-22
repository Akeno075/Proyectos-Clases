# 📉 Actividades de PHP
----
## 📌 Proyecto Tabla Registro

Este proyecto consiste en la creación de una tabla en una base de datos MySQL donde se insertan datos de sensores y se muestran en una página web. Se utiliza **PHP** y **MySQL** para gestionar la base de datos y la visualización de los datos.

---

### 📖 Tecnologías Utilizadas

- **PHP** (para la conexión y manipulación de la base de datos)
- **MySQL** (para el almacenamiento de los datos)
- **HTML** (para la visualización de la tabla)
- **Servidor Web** (Apache o cualquier compatible con PHP y MySQL)

---


## 🛠 Configuración de la Base de Datos

Antes de ejecutar el proyecto, debes asegurarte de que la base de datos está configurada correctamente.

### 1️⃣ Crear la Base de Datos y la Tabla

Ejecuta el siguiente comando SQL en **phpMyAdmin** o en la consola de MySQL para crear la base de datos y la tabla:

    ```sql
    CREATE DATABASE base de datos;

    USE base de datos;

    CREATE TABLE registro (
        id INT AUTO_INCREMENT PRIMARY KEY,
        sensor VARCHAR(50) NOT NULL,
        fecha_hora TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        valor FLOAT NOT NULL
    );


### Archivos del Proyecto
#### 1️⃣ `db_config.php` - Configuración de la Conexión a la Base de Datos
Este archivo almacena la configuración de la conexión a MySQL.



    <?php
    $servername = "bjpgg.site";
    $username = "admin_shagy";
    $password = "Shagy123";
    $dbname = "admin_romerillo";

    // Crear conexión
    $conn = new mysqli($servername, $username, $password, $dbname);

    // Verificar conexión
    if ($conn->connect_error) {
        die("Connection failed: " . $conn->connect_error);
    }
    ?>

#### 2️⃣ `insert.php` - Insertar Datos en la Tabla
Este script permite insertar datos en la tabla registro desde PHP.

    <?php
    include 'db_config.php';

    $sql = "INSERT INTO registro (sensor, valor) VALUES ('temperatura', 22)";

    if ($conn->query($sql) === TRUE) {
        echo "Nuevo registro creado exitosamente";
    } else {
        echo "Error: " . $sql . "<br>" . $conn->error;
    }

    $conn->close();
    ?>

#### 3️⃣ `index.php` - Mostrar Datos en una Tabla
Este script obtiene y muestra los datos almacenados en la base de datos.

    <?php
    include 'db_config.php';

    $sql = "SELECT id, sensor, fecha_hora, valor FROM registro";
    $result = $conn->query($sql);

    echo "<h2>Registro de Sensores</h2>";
    echo "<table border='1'>
            <tr>
            <th>ID</th>
            <th>Sensor</th>
            <th>Fecha y Hora</th>
            <th>Valor</th>
            </tr>";

    if ($result->num_rows > 0) {
        while ($row = $result->fetch_assoc()) {
            echo "<tr>
                    <td>" . $row["id"] . "</td>
                    <td>" . $row["sensor"] . "</td>
                    <td>" . $row["fecha_hora"] . "</td>
                    <td>" . $row["valor"] . "</td>
                </tr>";
        }
        echo "</table>";
    } else {
        echo "No hay registros.";
    }

    $conn->close();
    ?>

----

# 📌 Proyecto Registro de Sensores

Este proyecto consiste en una API creada con PHP que recibe datos en formato **JSON** y los almacena en una base de datos MySQL. Es ideal para integrar con sistemas IoT o cualquier aplicación que requiera el almacenamiento de datos de sensores en tiempo real.

## 🛠 Configuración de la Base de Datos

Antes de ejecutar el proyecto, asegúrate de configurar correctamente la base de datos.

### 1️⃣ Crear la Base de Datos y la Tabla

Ejecuta el siguiente comando SQL en **phpMyAdmin** o en la consola de MySQL:

    
    CREATE DATABASE admin_romerillo;

    USE admin_romerillo;

    CREATE TABLE registro (
        id INT AUTO_INCREMENT PRIMARY KEY,
        sensor VARCHAR(50) NOT NULL,
        fecha_hora TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        valor FLOAT NOT NULL
    );
    
--- 
## 🚀 Archivos del Proyecto

### 1️⃣ `db_config.php` - Configuración de la Conexión a la Base de Datos

Este archivo se usa para conectar PHP con MySQL.

        <?php
        $servername = "pagina web";
        $username = "nombre de acceso";
        $password = "contraseña";
        $dbname = "nombre de la base de datos";

        // Crear conexión
        $conn = new mysqli($servername, $username, $password, $dbname);

        // Verificar conexión
        if ($conn->connect_error) {
            die("Conexión fallida: " . $conn->connect_error);
        }
        ?>

### 2️⃣ `recibir_datos.php` - Recibir Datos y Guardarlos
Este archivo recibe datos en formato JSON a través de una solicitud POST, los procesa y los guarda en la base de datos.

    <?php
    include 'db_config.php';

    // Verificar si la solicitud es POST
    if ($_SERVER['REQUEST_METHOD'] == 'POST') {
        // Obtener los datos JSON recibidos
        $datos = json_decode(file_get_contents('php://input'));

        if (isset($datos->sensor) && isset($datos->valor)) {
            $sensor = $conn->real_escape_string($datos->sensor);
            $valor = $conn->real_escape_string($datos->valor);

            // Insertar datos en la base de datos
            $sql = "INSERT INTO registro (sensor, valor) VALUES ('$sensor', '$valor')";

            if ($conn->query($sql) === TRUE) {
                echo json_encode(["mensaje" => "Nuevo registro creado exitosamente"]);
            } else {
                echo json_encode(["error" => "Error al insertar: " . $conn->error]);
            }
        } else {
            echo json_encode(["error" => "Datos incompletos"]);
        }
    }

    // Cerrar conexión
    $conn->close();
    ?>


-----

## 🛠 Cómo Ejecutar el Proyecto

#### 1️⃣ Subir los Archivos a un Servidor
- Puedes usar XAMPP, MAMP o un servidor web que soporte PHP y MySQL en este caso con el que adquirimos y de este mismo ejecutamos las pticiones con los datos directamente.

#### 2️⃣ Acceder desde el Navegador

- Para ver la tabla con los datos registrados, accede a:

https://bjpgg.site/tablas.php



### 📖 Recursos Adicionales
- 🔗 Guía Oficial de PHP y MySQL
- 🔗 XAMPP - Servidor Local
- 🔗 GitHub Pages
-----
##### 💡 Autor: [Juan Pablo Gonzalez Gasca]
##### 📆 Última actualización: [28/Marzo/2025]


