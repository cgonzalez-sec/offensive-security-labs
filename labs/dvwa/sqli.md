# DVWA – SQL Injection

## Target
Damn Vulnerable Web Application (DVWA), SQL Injection module.  
Aplicación web vulnerable que consulta datos de usuarios a partir de un parámetro `id`.

## Scope
Entorno de laboratorio autorizado ejecutado localmente (DVWA).

## Recon
- El input recibe un `id` de usuario y devuelve:
  - ID
  - First Name
  - Surname
- Método HTTP: POST
- Parámetro vulnerable identificado:
  id=1&Submit=Submit
- Restricciones en el frontend (dropdown o input limitado), pero el backend procesa directamente el valor recibido.
- Peticiones interceptadas con Burp Suite.

## Vulnerability
La aplicación construye consultas SQL usando directamente el valor del parámetro `id` sin sanitización ni consultas preparadas.  
Esto permite modificar la lógica de la consulta SQL (SQL Injection).

## Exploitation

### Low
- El input no está filtrado.
- El backend interpreta el valor enviado directamente en la consulta SQL.
- Se observa que el servidor procesa el valor recibido sin validación estricta.
- Comportamientos anómalos confirman la inyección.

### Medium
- Existen restricciones en el frontend.
- El backend sigue siendo vulnerable.
- Manipulando la request POST es posible alterar el comportamiento de la consulta.

### High
- Se implementan controles adicionales.
- La inyección es más limitada.
- El backend muestra comportamientos consistentes con una mitigación parcial.

### Impossible
- El backend valida correctamente el input.
- Uso de consultas preparadas.
- No es posible alterar la consulta SQL.
- La aplicación se comporta de forma segura.

## Result
- Se confirmó la existencia de SQL Injection en los niveles Low, Medium y High.
- El nivel Impossible implementa correctamente las mitigaciones.
- Se comprendió la diferencia entre restricciones de frontend y seguridad real en el backend.

## Mitigation
- Uso de prepared statements (consultas parametrizadas).
- Validación estricta del input en el servidor.
- Nunca confiar en restricciones del frontend.

