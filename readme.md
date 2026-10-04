# Simulador de Azure Cloud Shell · Terminal de Buses Costa Azul

Simulador web de la consola de Azure, desarrollado como recurso de aprendizaje para la asignatura
**Gestión de Seguridad de la Información (TI3V62)**, INACAP Valparaíso, segundo semestre de 2026.

## Propósito

La actividad práctica de las unidades 2 y 3 exige configurar y auditar controles de identidad y
acceso en un entorno de nube: protección de datos, identidades nominativas, grupos por función,
roles con mínimo privilegio, segundo factor de autenticación, pruebas de acceso y revisión de
registros de auditoría. Para desarrollarla en Microsoft Azure, cada estudiante requiere una cuenta
con privilegios de administración sobre un directorio de Microsoft Entra ID, condición que las
cuentas institucionales no cumplen por diseño.

El simulador resuelve esa restricción: reproduce el comportamiento de Azure Cloud Shell sobre un
entorno ficticio —el sistema de encomiendas del Terminal de Buses Costa Azul— y permite ejecutar el
procedimiento completo de la guía de laboratorio sin cuenta, sin costo y sin conexión a servicios
externos. La restricción encontrada no se oculta: forma parte del análisis que el estudiante
desarrolla, porque ilustra el principio de mínimo privilegio aplicado por una organización real.

## Alcance funcional

| Ámbito | Comportamiento simulado |
|---|---|
| Recursos | Grupos de recursos, cuentas de almacenamiento, contenedores y blobs |
| Protección de datos | Cifrado en tránsito, versión mínima de TLS y acceso anónimo; la lectura sin credencial responde 200 o 409 según la configuración |
| Identidades | Usuarios, grupos y membresías en Microsoft Entra ID; cambio de contraseña obligatorio en el primer ingreso |
| Control de acceso | Asignación y retiro de roles de Azure RBAC con evaluación de alcance y herencia; las operaciones no autorizadas se rechazan con el mensaje que emite Azure |
| Autenticación | Valores predeterminados de seguridad y registro de un segundo factor con una aplicación autenticadora simulada; rechazo de cuentas deshabilitadas |
| Auditoría | Registro de actividad de Azure y registros de auditoría e inicio de sesión de Microsoft Entra, generados a partir de las acciones del propio estudiante |
| Evidencia | Descarga de la transcripción completa de la sesión en texto plano |

Los comandos se escriben tal como figuran en la guía de laboratorio: el simulador interpreta
variables de entorno, sustitución de comandos, continuación de línea, tuberías y redirección, y
admite los parámetros `--query` y `--output` de la interfaz de línea de comandos de Azure.

## Arquitectura

Aplicación estática de un solo archivo (`index.html`), escrita en HTML, CSS y JavaScript sin
dependencias. Se compone de dos partes:

- **Motor de simulación.** Mantiene el estado del entorno, interpreta la línea de comandos, evalúa
  los permisos de cada identidad según sus roles y su alcance, y produce las salidas en los formatos
  `json`, `table` y `tsv`. Incluye un subconjunto de JMESPath suficiente para las consultas de la
  actividad.
- **Interfaz.** Consola interactiva con historial, pegado de bloques de varias líneas, panel de
  instrucciones y descarga de la transcripción.

El avance de cada estudiante se conserva en el almacenamiento local de su navegador. No existe
servidor, base de datos ni transmisión de información: el simulador no recopila datos personales.

## Uso

Abra `index.html` en un navegador actualizado, o acceda a la versión publicada. Desarrolle los
Pasos A0 a A3 de la guía de laboratorio en el orden indicado y descargue la transcripción al
término de cada paso. El panel de instrucciones indica cómo ejecutar en la consola las acciones
que la guía describe en el portal de Azure.

## Limitaciones

El simulador reproduce el comportamiento necesario para la actividad; no es una implementación de
Azure. Responde solo los comandos y las consultas de Microsoft Graph que el procedimiento utiliza,
los cambios surten efecto de inmediato —sin los tiempos de propagación de la plataforma real— y el
acceso condicional, que requiere la licencia Microsoft Entra ID P1, no forma parte del alcance.

## Referencias

- Microsoft. (2025). *Azure command-line interface (CLI) documentation*. Microsoft Learn.
- Microsoft. (2025). *Azure role-based access control (Azure RBAC) documentation*. Microsoft Learn.
- Microsoft. (2025). *Security defaults in Microsoft Entra ID*. Microsoft Learn.
- National Institute of Standards and Technology. (2020). *Security and privacy controls for
  information systems and organizations* (NIST Special Publication 800-53, Rev. 5).

## Autoría

Rubén Schnettler Lucero · Ingeniero Civil Industrial, Magíster en Gestión Empresarial · docente de
INACAP Valparaíso.
