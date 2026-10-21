# Base de Datos de Albergues do Camiño de Santiago

## Como arrancar o proxecto

1. Clona este repositorio na túa máquina.
2. Crea unha copia do ficheiro de variables de contorno:
   `cp .env.example .env`
3. Edita o ficheiro `.env` e configura un contrasinal real.
4. Levanta os contedores co comando:
   `docker compose up -d`
5. Accede a Adminer a través de `http://localhost:8080`. (O servidor por defecto é `db`).

## Proba de Persistencia

| Paso | Comando | Resultado obtido |
|---|---|---|
| 1 | `docker compose up -d` | Os contedores créanse e inícianse. Execútanse os scripts SQL ao ser a primeira vez. |
| 2 | Inserir un albergue novo desde Adminer | O albergue gárdase correctamente na base de datos. |
| 3 | `docker compose down` e `docker compose up -d` | Os contedores destrúense e vólvense a crear. Ao entrar en Adminer, **o albergue novo segue aí** porque o volume conservou os datos. |
| 4 | `docker compose down -v` e `docker compose up -d` | Os contedores e os volumes destrúense. Ao volver levantar o proxecto, **o albergue novo xa non está**. A base de datos restaurouse ao seu estado inicial cos 8 albergues por defecto. |

### Explicación do Paso 4
No paso 4, engadir o *flag* `-v` ao comando `docker compose down` indica a Docker que elimine tamén os volumes nomeados asociados aos servizos (neste caso, `db_data`). Ao eliminar o volume, pérdese calquera modificación feita nos datos. Cando volvemos facer `up -d`, créase un volume totalmente novo e baleiro, o que provoca que a imaxe de PostgreSQL volva a executar os scripts de inicialización de `initdb/`, deixando a base de datos exactamente como estaba ao principio.