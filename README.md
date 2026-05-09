A sus órdenes, mi xanxo. Aquí tienes la redacción del **README.md** técnica y profesional, estructurada específicamente para cumplir con los indicadores de evaluación **IE1, IE2, IE3, IE6 y IE8** que exige la pauta de Duoc UC.

Copia este contenido en un archivo llamado `README.md` en la raíz de cada repositorio (Frontend y Backend).

---

# Proyecto de Contenedorización y Despliegue Automatizado - Innovatech Chile

## 1. Descripción del Proyecto

Este repositorio forma parte de la Etapa 2 del proyecto de Innovatech Chile, enfocado en la contenedorización y despliegue automatizado de una solución de microservicios. El sistema consta de un Frontend y servicios de Backend (Ventas y Despachos) integrados en una arquitectura de contenedores desplegada en AWS.

## 2. Requerimientos Técnicos del Entorno

Para ejecutar este proyecto de forma local o en servidor, se requiere:

* 
**Docker & Docker Compose:** Para la orquestación de los servicios.


* 
**AWS EC2:** Instancia de ejecución para el entorno de producción.


* 
**GitHub Actions:** Para la ejecución del pipeline CI/CD.


* **Java 21 / Node.js 20:** Según el repositorio correspondiente (Backend/Frontend).

## 3. Estructura de Contenedorización (IE1 & IE6)

Se ha implementado una estrategia de contenedorización avanzada basada en las siguientes premisas técnicas:

* 
**Multi-stage Build:** Los Dockerfiles utilizan múltiples etapas para separar el entorno de compilación del entorno de ejecución, optimizando el tamaño de la imagen final y reduciendo la superficie de ataque.


* **Seguridad (Non-root user):** Los contenedores no se ejecutan con privilegios de administrador. Se han configurado usuarios específicos (springuser/nginx) para mitigar riesgos de seguridad en el sistema host.


* 
**Optimización de Capas:** Se han estructurado las instrucciones para aprovechar el sistema de caché de Docker y garantizar una limpieza efectiva de archivos temporales.



## 4. Orquestación y Persistencia (IE2 & IE3)

La gestión de los servicios se realiza mediante **Docker Compose**, el cual define la red interna y la interdependencia de los componentes.

* 
**Persistencia:** Se utilizan **Named Volumes** para garantizar que la información de la base de datos y logs críticos no se pierda ante reinicios o actualizaciones de los contenedores.


* 
**Justificación de Volumen:** Se optó por Named Volumes sobre Bind Mounts para asegurar una gestión nativa de Docker, mejorando la portabilidad y evitando conflictos de permisos con el sistema operativo de AWS EC2.


* 
**Healthchecks:** Se han implementado pruebas de estado para asegurar que los servicios de Backend solo inicien una vez que la base de datos esté plenamente operativa.



## 5. Pipeline CI/CD (IE7)

El flujo de entrega continua está automatizado mediante **GitHub Actions** y se rige por las siguientes reglas:

* 
**Triggers:** El pipeline se activa exclusivamente ante eventos de `push` en la rama **deploy**.


* 
**Flujo:** Build de imagen -> Push a Docker Hub -> Deploy SSH en AWS EC2.


* 
**Seguridad de Credenciales:** Toda la información sensible (IPs, llaves SSH, contraseñas de DB) se gestiona mediante **GitHub Secrets**, garantizando que no existan credenciales en texto plano dentro del código.



## 6. Instrucciones de Despliegue Local

1. Clonar el repositorio.
2. Configurar el archivo `.env` con las variables de base de datos requeridas.
3. Ejecutar el despliegue:
```bash
docker-compose up -d --build

```



## 7. Autores

* 
**Dupla:** Benjamín Ruz & Nathan Gutierrez.


* 
**Institución:** Duoc UC.



---

**Nota Táctica:** Recuerda que para la defensa oral (IE9), debes recalcar que la comunicación entre el Front y el Back respeta los Security Groups de AWS y que solo el puerto 80 es accesible desde el exterior. ¡Dale átomos con ese PDF, mi xanxo! 🏎️💨🏆
