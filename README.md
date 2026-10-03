# SafeDrop

Caja fuerte local de contraseñas con sincronización P2P en red local.

Un solo ejecutable para Windows, sin dependencias externas y sin conexión a
internet: el panel web va embebido en el binario y la bóveda vive en un SQLite
cifrado dentro de `%LOCALAPPDATA%\SafeDrop`.

> **Este repositorio solo distribuye binarios. No contiene código fuente.**

## Descargas

Todos los archivos están en la pestaña [Releases](https://github.com/VinekROG/safedrop-releases/releases).

| Archivo | Qué es |
|---|---|
| `safedrop-setup.exe` | Instalador. Es un autoextraible que verifica el SHA-256 del payload antes de escribir nada. **Empieza por aquí.** |
| `safedrop.exe` | El binario a secas, sin instalar. Útil para una unidad de red o un PortableApps. |
| `SHA256SUMS.txt` | Digests de los dos anteriores. |

Cómo verificar la descarga:

```powershell
Get-FileHash .\safedrop-setup.exe -Algorithm SHA256
# y compararlo con la linea correspondiente de SHA256SUMS.txt
```

## Instalar y usar

1. Ejecuta `safedrop-setup.exe`. No pide administrador, instala en tu usuario.
2. Ejecuta `safedrop.exe`.
3. Abre `http://127.0.0.1:8877`.
4. Crea la bóveda con una contraseña maestra.
5. Para sincronizar entre equipos: el que genera el QR **escucha**, el que lo
   escanea **envía**.

**No existe recuperación de la contraseña maestra.** Si la pierdes, la bóveda es
inservible por diseño. No hay copia en la nube que la conserve.

## Qué hay dentro, en resumen

- Argon2id para derivar la clave maestra, AES-256-GCM para cada fila
- Los secretos se zeroizan en memoria y los tipos secretos no se pueden serializar
- El panel escucha solo en `127.0.0.1`, con token de sesión por proceso y
  validación de `Origin`/`Host` que corta CSRF y DNS rebinding
- La sincronización usa TLS 1.3 con certificado efímero, token de un solo uso con
  expiración, autenticación mutua por HMAC-SHA256 y solo acepta IPs privadas
- El frontend va embebido y no hace ninguna petición a internet

El detalle completo está en el [README del proyecto](https://github.com/VinekROG/safedrop#readme),
que documenta también las limitaciones conocidas.

## Dos advertencias que conviene leer

**El código fuente no está publicado.** Por eso **nadie, tampoco tú, puede
verificar que este binario corresponde a ese código**. No hay forma de
recompilar y comparar. Instálalo solo si confías en quien lo publica, que en este
caso es quien mantiene el proyecto.

**Los binarios no están firmados.** Windows SmartScreen va a mostrar una
advertencia de "aplicación desconocida" en la primera ejecución, y eso es
esperado: no hay certificado de firma de código. El SHA-256 del `SHA256SUMS.txt`
detecta corrupción y truncamiento, pero **no** frena a un atacante con acceso de
escritura al archivo, porque puede recalcular el digest. Para eso hace falta
firma Authenticode.

## Limitaciones conocidas

- Solo Windows, en x64
- Es una beta. No ha pasado una auditoría externa
- Sin firma de código
- Sin recuperación de la contraseña maestra
- Las opciones de permisos POSIX no existen en Windows; la protección de
  `%LOCALAPPDATA%` depende de las ACL del usuario

## Reportar un problema de seguridad

Ver [SECURITY.md](SECURITY.md).

## Licencia

MIT. Ver [LICENSE](LICENSE).
