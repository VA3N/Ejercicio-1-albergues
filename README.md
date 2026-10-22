**Ejercicio 1**
**Autor:Marco**



**Cómo arrancar el proyecto**
1. Clona este repositorio en tu equipo.
2. Haz una copia del archivo de variables de entorno:
   cp .env.example .env
3. Abre el .env y ponle la contraseña que prefieras.
4. Levanta todo ejecutando el comando:
   **docker compose up -d**
5. Entra en http://localhost:8080. Para iniciar sesión, el servidor que tienes que indicar es db.

**Prueba de persistencia**

| Paso | Comando | Resultado obtenido |
|---|---|---|
| 1 | **docker compose up -d* | Todo arranca bien y se crean los 8 albergues que metí en los scripts de inicio. |
| 2 | Insertar en Adminer | Guardé un albergue inventado desde la web sin problemas. |
| 3 | **docker compose down** y luego **docker compose up -d** | Mi albergue inventado(Albergue O corgo) sigue ahí, no se perdió nada|
| 4 | **docker compose down -v** y luego **docker compose up -d** | Mi albergue desapareció y la base de datos volvió al estado original |

**Porque el paso 4 es distinto**
Básicamente porque al usar el parámetro "-v" estamos diciéndole a Docker que destruya también el volumen donde se están guardando los datos permanentemente. Al volver a levantar el proyecto con "up", Docker se encuentra sin datos, crea un volumen completamente nuevo y vacío, y eso provoca que los scripts SQL del principio se vuelvan a ejecutar desde cero.