# Política de seguridad

## Qué es SafeDrop

Una caja fuerte local de contraseñas con sincronización P2P en red local. Todo
ocurre en tu equipo: no hay servidores, ni cuentas, ni telemetría. La
sincronización solo funciona dentro de tu red local y solo con códigos QR que
generas tú.

## Versiones con soporte

`1.0.0-beta` es una beta. Recibe correcciones de seguridad hasta que salga la
1.0.0 estable.

## Cómo reportar un fallo

Abre un issue privado con [GitHub Security Advisories](https://github.com/VinekROG/safedrop-releases/security/advisories/new).

Incluye, si puedes:

- Versión (el `About` del panel la muestra)
- Pasos para reproducir
- Qué esperabas y qué pasó
- Si el fallo expone claves, bóvedas o el token de sesión, dilo explícitamente

**No abras un issue público** para un fallo que comprometa datos, aunque creas
que ya está corregido. Un issue público con los detalles llega a cualquiera
antes de que haya un parche.

## Qué considerate fallo de seguridad

- Que la bóveda se pueda descifrar sin la contraseña maestra
- Que el token de sesión del panel se pueda adivinar, filtrar o reutilizar desde
  otro origen
- Que la sincronización acepte a un tercero que no tenga el token
- Que se acepte una IP pública en la sincronización, o se transmita a otra
  máquina por una vía no prevista
- Que una credencial o una nota aparezcan en el listado, en un log o en una
  respuesta del panel
- Que un `.exe` alterado pase la verificación del instalador

## Fuera de alcance

- Que alguien con acceso a tu cuenta de Windows lea `%LOCALAPPDATA%\SafeDrop`.
  La protección ahí viene de las ACL del usuario, no de SafeDrop.
- Que el binario no esté firmado y SmartScreen avise. Es lo esperado.
- Que se pierda la contraseña maestra. No hay recuperación por diseño.
- Debilidades en las dependencias de terceros que no sean explotables en el uso
  real de la aplicación.

## Sobre el código fuente

Aquí solo se publican binarios. Si un fallo necesita inspección del código,
indícalo en el reporte y se coordina en privado.
