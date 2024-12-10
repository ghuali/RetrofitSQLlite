# Esquemas-Retrofit-y-SQLite
Para empazar a utilzar Retrofit en los proyectos hay que importar dos implementaciones en builds.gradle.kts:


Ejemplo de como se vería    
![image](https://github.com/user-attachments/assets/19a7cb2e-5095-4270-b286-4cde3cad1422)


Después de escribirlo hay que sincronizar el proyecto para que se guarden los cambios.

![image](https://github.com/user-attachments/assets/0b272e0b-f14f-47a5-8134-408a0df0c3d2)

Hay que selecionar la opción (Replace with existing version catalog reference "la opción a cambiar") y volver a sincronizar el proyecto.
![image](https://github.com/user-attachments/assets/08c48874-a568-482f-9ceb-9287254ff89f)

Pasos a seguir:
- Hay que importar retrofit2.Retrofit y retrofit2.converter.gson GsonConverterFactory
- Crear una constante con el enlace.
- Agrega un compilador de Retrofit justo debajo de esa constante para compilar y crear un objeto Retrofit.
- Llama a addConverterFactory() en el compilador con una instancia de ScalarsConverterFactory.
- Por último, llama a build() para crear el objeto Retrofit.

![image](https://github.com/user-attachments/assets/ce6b4d35-89be-46ba-8264-3d54babf7d79)

--------

# Esquema de Base de Datos SQLite
SQLite es una base de datos ligera integrada en Android que facilita el almacenamiento persistente de datos.

- Primero hay que importar módulos necesarios: Asegúrate de tener los módulos de SQLite en tu proyecto.

- Crear una clase de Helper: Esta clase ayudará a crear, abrir y gestionar la base de datos.

- Definir el esquema de la base de datos: Incluye los parámetros y las consultas necesarias.

- Métodos onCreate y onUpgrade: Implementa estos métodos en el Helper para gestionar la creación y actualización de la base de datos.

- Para más detalles sobre el uso de SQLite en Android, consulta la documentación oficial: Documentación de SQLite en Android:

https://developer.android.com/training/data-storage/sqlite?hl=es-419

Se muestra un ejemplo de los módulos necesarios, la clase, el objeto con los parámetros, Oncreate para crearla y OnUpgrade para actualizarla

![image](https://github.com/user-attachments/assets/a622a248-c254-4bc2-82fe-2ce3bd6efc94)

### Cómo ingresar información en una base de datos

```kotlin
val db = MyDatabaseHelper(context).writableDatabase
val values = ContentValues().apply {
    put("name", "Angel")
    put("age", 20)
}
db.insert("Users", null, values)
```

### Cómo leer información de una base de datos

```kotlin
val cursor = db.query("Users", null, null, null, null, null, null)
while (cursor.moveToNext()) {
    val name = cursor.getString(cursor.getColumnIndexOrThrow("name"))
    val age = cursor.getInt(cursor.getColumnIndexOrThrow("age"))
}
cursor.close()
```
### Cómo borrar información de una base de datos
```kotlin
db.delete("Users", "name = ?", arrayOf("Angel"))
```

### Cómo actualizar una base de datos
```kotlin
val values = ContentValues().apply {
    put("age", 21)
}
db.update("Users", values, "name = ?", arrayOf("Angel"))
```
