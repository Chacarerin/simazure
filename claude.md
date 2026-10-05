# Proyecto: simazure · Simulador de Azure Cloud Shell

**Objetivo:** simulador web de la consola de Azure para Gestión de Seguridad de la Información, INACAP
Valparaíso: la parte de nube del laboratorio de las unidades 2 y 3 (vespertino TI3V62 y diurno TI3062)
y la implementación del proyecto integrador de la Unidad 4. Se despliega en Vercel como sitio estático.

## Por qué existe

Las cuentas institucionales de los estudiantes no pueden crear usuarios en Microsoft Entra ID
(«Insufficient privileges») ni abrir su portal de administración (error 401), y Microsoft no permite
crear directorios desde suscripciones gratuitas o de prueba. La guía de laboratorio ya estaba
entregada y **no se modifica**: el simulador reproduce Azure para que los comandos de la guía se
ejecuten tal como están escritos.

## ⚠️ Lineamientos obligatorios para agentes

> [!IMPORTANT]
> Los commits y operaciones de Git **solo** pueden ser autorizados por el propietario del
> repositorio. No realizar `git add`, `git commit` ni `git push` sin autorización explícita.

> [!IMPORTANT]
> El despliegue es **100 % manual por el usuario**. La responsabilidad del agente termina en dejar
> el código listo para producción. No realizar despliegues automáticos.

- `bitacora.md` registra errores, soluciones, decisiones y grandes cambios. **No forma parte del
  repositorio** (está en `.gitignore`).
- `readme.md` sí forma parte del repositorio y se escribe en **tono académico**.
- Registro del material: español neutro y formal, sin coloquialismos, como todo el material del
  docente.

## Reglas del simulador

1. **La guía manda.** Todo comando que figure en las guías, en los enunciados o en las diapositivas
   (sets 5 a 7 y de evaluación) debe producir la salida que el material indica. Ante una diferencia, se
   corrige el simulador; la guía del vespertino ya se entregó y no se modifica.
1.b **Fiel a Azure, también en sus límites.** Lo que Azure no permite con Entra ID Free, el simulador
   tampoco: la lectura de inicios de sesión por API responde el error de licencia, y se consultan en el
   portal de Entra simulado. Un plan básico rechaza la redundancia de zona.
2. **Un solo archivo, sin dependencias.** `index.html` funciona sin conexión, abierto con doble
   clic. No se agregan bibliotecas externas, fuentes remotas ni procesos de compilación.
3. **Sin base de datos ni servidor.** El estado vive en `localStorage` de cada navegador. No se
   recopila información de los estudiantes.
4. **Errores realistas.** Un comando mal escrito responde con el mensaje que daría Azure.
5. **Fuente de verdad.** Este repositorio. La copia que se entrega en el aula virtual vive en
   `202602_clases_inacap/202602_gest_seg_info_lun_mie_TI3062DIEIN6P2/diapositivas_gest_seg_info/flex/GSI-TI3V62-Simulador-Azure.html`
   y se actualiza copiando `index.html` después de cada cambio.

## Cómo probar

El motor está en el bloque `<script id="motor">` y exporta `crearSimulador` para Node:

```bash
python3 -c "import re;s=open('index.html').read();open('/tmp/motor.js','w').write(re.search(r'<script id=\"motor\">(.*?)</script>',s,re.S).group(1))"
node -e "const {crearSimulador}=require('/tmp/motor.js'); const s=crearSimulador(); console.log(s.ejecutar('az account show -o table').out)"
```

Antes de publicar un cambio, recorrer la Parte A completa de la guía del vespertino (A0 a A3) y
verificar los cinco resultados de la Medida 4: dos accesos permitidos, dos denegados y el rechazo de
la cuenta compartida. Correr además los comandos de la guía del diurno con un caso A a D y la secuencia
del Paso 4 de los enunciados de la Unidad 4 con el caso Costa Azul.

## Despliegue continuo

⚠️ El proyecto de Vercel debe estar **conectado al repositorio** para que cada push publique. Si se
desplegó subiendo archivos, el push no se refleja y hay que conectar el repositorio o volver a
desplegar a mano.

## Despliegue

Ver [`docs/deploy.md`](docs/deploy.md).
