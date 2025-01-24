# B2-TrabajoDeConsulta_2Conexi-nBaseDeDatosRelacional.

¡Entendido! Aquí tienes la misma explicación enfocada a un entorno de desarrollo con IntelliJ y cómo aprovecharlo al máximo para trabajar con JDBC:

---

### **JDBC (Java Database Connectivity)**
Es una API de Java que permite conectar aplicaciones Java con bases de datos relacionales. JDBC es parte del JDK estándar y proporciona una interfaz estándar para realizar operaciones como consultas, actualizaciones y transacciones en una base de datos.

---

### **Componentes principales de JDBC**
#### 1. **Driver JDBC**
Es un conjunto de clases que implementan la interfaz JDBC y traducen las solicitudes de la aplicación Java en comandos que la base de datos entiende. Los tipos más comunes son:

- **Tipo 4:** Controladores puros Java que interactúan directamente con el protocolo de la base de datos (como MySQL Connector/J).

#### 2. **DriverManager**
Es la clase que administra los controladores disponibles. Establece la conexión con la base de datos mediante:
```java
Connection connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/mi_base", "usuario", "contraseña");
```

#### 3. **Connection**
Representa la conexión activa con la base de datos. A través de este objeto se crean sentencias SQL, se gestionan transacciones y se configuran propiedades de conexión.

#### 4. **Statement**
Permite ejecutar comandos SQL. JDBC incluye tres tipos:
- **Statement:** Para consultas simples.
- **PreparedStatement:** Más eficiente y seguro, especialmente para consultas parametrizadas.
- **CallableStatement:** Diseñado para invocar procedimientos almacenados.

#### 5. **ResultSet**
Es el objeto que contiene los resultados de una consulta SQL. Proporciona métodos para navegar por las filas y columnas devueltas.

#### 6. **SQLException**
Maneja los errores relacionados con bases de datos en JDBC. Incluye detalles como el estado SQL, el código de error y el mensaje.

---

### **Flujo básico con IntelliJ**
#### 1. **Configurar el proyecto**
- **Dependencias:** Añade el controlador MySQL:
  - Ve a **File > Project Structure > Libraries**, haz clic en **+**, y selecciona **From Maven...**.
  - Busca y agrega:
    ```plaintext
    mysql:mysql-connector-java:8.0.33
    ```

#### 2. **Código de ejemplo**
Crea un archivo Java con el siguiente contenido:

```java
import java.sql.*;

public class EjemploJDBC {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/mi_base";
        String user = "root";
        String password = "tu_contraseña";

        try (Connection connection = DriverManager.getConnection(url, user, password)) {
            System.out.println("Conexión exitosa.");

            // Crear declaración y ejecutar consulta
            String query = "SELECT * FROM usuarios";
            try (Statement stmt = connection.createStatement();
                 ResultSet rs = stmt.executeQuery(query)) {

                // Procesar resultados
                while (rs.next()) {
                    System.out.println("ID: " + rs.getInt("id"));
                    System.out.println("Nombre: " + rs.getString("nombre"));
                    System.out.println("Correo: " + rs.getString("correo"));
                    System.out.println("---------------");
                }
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

---

### **Características adicionales usando IntelliJ**
1. **Database Tool Window:**
   - Conéctate a la base de datos directamente desde IntelliJ:
     - Ve a **View > Tool Windows > Database**.
     - Configura una nueva conexión seleccionando **+ > Data Source > MySQL**.
     - Ingresa los datos de conexión y verifica con **Test Connection**.

2. **Inspección del código:**
   - IntelliJ proporciona advertencias sobre conexiones no cerradas y ayuda a refactorizar el manejo de excepciones.

3. **Ejecución simplificada:**
   - Usa el atajo `Shift + F10` para compilar y ejecutar directamente tu clase principal.

4. **Autocompletado:**
   - IntelliJ sugiere métodos y parámetros mientras escribes, simplificando el trabajo con JDBC.

---

### **Beneficios de JDBC**
- Portabilidad: Funciona con cualquier base de datos que tenga un controlador compatible.
- Eficiencia: Optimiza las operaciones mediante el uso de conexiones parametrizadas y transacciones.
- Integración: Se puede combinar con herramientas avanzadas como Hibernate para facilitar el manejo de datos.

