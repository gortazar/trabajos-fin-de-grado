# Propuestas de Trabajos Fin de Grado 2016-2017

Aquí puedes encontrar mis propuestas de TFG para alumnos de la [URJC](http://www.urjc.es). Si te interesa alguna de ellas, ábreme un [issue](https://github.com/gortazar/tfgs/issues) indicándome porqué te interesa la propuesta, de qué titulación eres y en qué curso estás y me pondré en contacto contigo para comenzar.

Todos los proyectos serán publicados como software libre en esta misma plataforma. Por tanto, cojas el proyecto que cojas acabarás como mínimo aprendiendo Git y GitHub.

## Rendimiento de Kurento en múltiples infraestructuras

[Kurento](http://www.kurento.org) es un servidor de media compatible WebRTC que puede utilizarse para contruir aplicaciones de videoconferencia, clases online con vídeo y audio y aplicaciones de realidad aumentada.

El objetivo de este proyecto es estudiar la escalabilidad de Kurento en producción. Para ello, con la ayuda del tutor, se establecerán diferentes métricas para medir la calidad en gestión de media y se diseñarán varios escenarios (videoconferencia, transcodificación, etc) de prueba. Para cada escenario de prueba, se medirá la calidad en diferentes despliegues:

* Nativo (instalado directamente sobre un OS anfitrión corriendo en hardware físico)
* Virtualizado (instalado en una máquina virtual) en diferentes proveedores:
  * Amazon AWS
  * Azure
  * Openstack
* Corriendo en contenedores:
  * Docker sobre hardware real
  * Docker sobre máquina virtual
  * Docker en alguna infraestructura (Kubernetes, Amazon ECR, Azure Container Service o Apache Mesos a través de DCOS)

El proyecto incluye:

* Desarrollar el sw necesario de gestión de la configuración para poder automatizar los despliegues (no se harán despliegues a mano)
* Desarrollar los casos de test que se probarán a partir de casos que ya existen
* Ejecutar los escenarios
* Recoger los resultados
* Analizar los resultados obtenidos

**Competencias desarrolladas**: git, github, cloud, contenedores (Docker), testing, gestión de la configuración (devops)

## Comparativa de despliegue y autoescalado de contenedores Docker

[Docker](https://www.docker.com) permite empaquetar y ejecutar aplicaciones en un entorno aislado, permitiendo incluso limitar los recursos que dichas aplicaciones utilizan del SO anfitrión en el que se ejecutan. Es una tecnología similar en funcionalidades a la virtualización, pero no hay una máquina virtual, sino que todas las características de aislamiento las proporciona el propio sistema operativo. A este tipo de tecnología se la denomina genéricamente _contenedores_ y Docker es una de las implementaciones más exitosas y conocidas de este concepto (existen otras como rkt, lxc, OpenVZ, ...). El concepto de contenedor se ha extendido hasta el punto que los principales proveedores cloud proporcionan soporte para Docker de forma nativa (como Amazon AWS y Azure).

Se está hablando mucho de Docker para desplegar arquitecturas como Microservicios. Pero, ¿qué complicaciones implica desplegar un sistema compuesto de múltiples aplicaciones usando Docker?

El objetivo del proyecto es comparar diferentes infraestructuras que permiten desplegar servicios usando Docker. Se compararán al menos las siguientes infraestructuras:

* Docker Swarm: un cluster de máquinas virtuales corriendo Docker que permite desplegar aplicaciones distribuidas por el cluster
* Amazon ECR: el soporte para Docker de Amazon
* Azure Container Service: el soporte para Docker de Azure
* Kubernetes: un cluster para desplegar contenedores Docker que tiene sus propias herramientas para definir servicios y cómo interactúan entre ellos
* Mesos/DCOS: un sistema operativo distribuido para la nube

Se estudiarán y compararán características de cada uno de los sistemas probando a desplegar una aplicación compuesta de varios servicios. Entre otras, se medirán las siguientes características:

* Facilidad de puesta en marcha
* Compatibilidad con Docker Engine, Docker Compose y Docker Swarm
* Facilidad de despliegue de contenedores con puertos expuestos (apps web)
* Facilidad de despliegue de contenedores linkados (apps web + db)
* Facilidad de actualización de contenedores en runtime (actualizar la app web)
* Capacidad de gestionar persistencia (base de datos a disoc del host o similar)
* Soporte de grupos de autoescalado

**Competencias desarrolladas**: git, github, cloud, contenedores, Docker, sistemas distribuidos, gestión de la configuración, tecnologías relacionadas con Docker (Kubernetes, Mesos, Amazon ECR, Azure CS).

## Plugin de Jenkins para visualizar claramente las causas de fallo de los jobs

[Jenkins](https://jenkins.io) es probablemente el sistema de integración continua (CI) más conocido y utilizado. Es software libre y está escrito en Java. Jenkins se utiliza para construir proyectos, pasar tests y hacer despliegues. Cada una de estas tareas se define en lo que se denomina un _job_ o tarea.

El objetivo del proyecto es implementar un plugin de Jenkins que se integrará con la interfaz de usuario de Jenkins para visualizar claramente cuál es la causa de fallo de un job:

* Cuando falla un único test visualizar directamente el mensaje de error de dicho test
* Cuando fallan varios tests, agrupar errores y mostrar las causas agrupadas con el número de apariciones.  P.ej: NullPointerException(3), IndexOutOfBounds(2), assert failed (1)
* Poder asociar mediante expresiones regulares mensajes de error en la ejecución del job a mensajes a mostrar directamente en la página principal del job
* Proporcionar una nueva columna en la vista de tareas que indique la causa del fallo

**Competencias desarrolladas**: git, github, Java, Jenkins, testing, integración continua.

## Plugin de Jenkins para visualizar el estado general del entorno de integración continua

[Jenkins](https://jenkins.io) es probablemente el sistema de integración continua (CI) más conocido y utilizado. Es software libre y está escrito en Java. Jenkins se utiliza para construir proyectos, pasar tests y hacer despliegues. Cada una de estas tareas se define en lo que se denomina un _job_ o tarea.

Normalmente las tareas o jobs que ejecuta Jenkins se pueden dividir en categorías:

* Tareas que se ejecutan cada vez que los desarrolladores suben cambios al repositorio de código. Normalmente estas tareas deben durar poco.
* Tareas que se ejecutan cuando un cambio es aceptado y mezclado en la rama de desarrollo del proyecto. Estas tareas pueden ejecutar tests más exhaustivos.
* Tareas que se ejecutan cuando se quiere publicar una nueva release. Estas tareas normalmente publican los artefactos generados en algún repositorio de binarios.

El objetivo del proyecto es visualizar el estado de estas tareas. Para ello, se establecerán alarmas y se presentará un panel informativo con los problemas detectados:

* Jobs de cambios que empiezan a fallar sistemáticamente
* Jobs de release que fallan
* Artefactos resultado de los jobs que no están correctamente publicados

**Competencias desarrolladas**: git, github, Java, Jenkins, testing, integración continua

## Plugin de Jenkins para generar gráficas de rendimiento

[Jenkins](https://jenkins.io) es probablemente el sistema de integración continua (CI) más conocido y utilizado. Es software libre y está escrito en Java. Jenkins se utiliza para construir proyectos, pasar tests y hacer despliegues. Cada una de estas tareas se define en lo que se denomina un _job_ o tarea.

En ocasiones es necesario conocer el rendimiento de dichas tareas en términos de memoria, uso de CPU, etc. El objetivo de este proyecto es desarrollar un plugin para Jenkins que permita activar o desactivar estas medidas de rendimiento. Para ello, se introducirá un comando específico en el [pipeline de Docker](https://github.com/jenkinsci/docker-workflow-plugin) que el usuario podrá utilizar para indicar qué métricas de rendimiento desea tomar.

Las métricas se tomarán con perf, una herramienta Linux diseñada específicamente para ello y de sencillo uso, y posteriormente se transformarán en [Flame Graphs](http://www.brendangregg.com/flamegraphs.html) mediante la utilidad desarrollada por Brendan Gregg (Netflix). Dichos gráficos se mostrarán en la interfaz de la tarea Jenkins.

**Competencias desarrolladas**: git, github, Java, Jenkins, performance monitoring, devops, docker, flame graphs.

## Herramienta de chequeo de releases

Desarrollar una herramienta con Spring Boot y frontend Angular para chequear la validez de la publicación de las diferentes versiones de un proyecto. Normalmente cuando se construye un proyecto se generan múltiples artefactos (.jar, .war, ejecutables, ...) que hay que publicar en determinados sitios (Maven Central, un repositorio privado, ...) para que puedan ser desplegados en producción. Además, suele ser habitual marcar el código de la versión mediante un tag en el repositorio de código.

El objetivo del proyecto es construir una aplicación basada en Spring Boot con una interfaz web (en Angular) que permita:

* Dar de alta diferentes proyectos y sus artefactos asociados
* Debe soportar los siguientes tipos de artefactos:
 * Java: librerías publicadas en Maven Central o en un repositorio privado (Archiva)
 * Javascript: librerías publicadas en npm y en bower
 * Paquetes debian publicados en repositorios públicos
 * Tags en repositorios en GitHub
* Debe permitir verificar para las versiones que se especifiquen si todos los artefactos están disponibles en los sitios donde deben haber sido publicados

**Competencias desarrolladas**: git, GitHub, Java, Spring, Javascript, Angular, Jenkins, testing, REST

## Herramienta de análisis de log

Desarrollar un servicio web que permita entrenar una red neuronal para intentar determinar las causas de fallo de los jobs en Jenkins. Funcionalidades:

* Servicio web rest con frontend angular
* Posibilidad de configurar el servidor jenkins a interrogar
* Se recoge información de los jobs de Jenkins seleccionados
  * Si hay tests -> información de los tests (causa de fallo de cada test)
  * Si no hay resultados de tests -> Salida estándar
* La información se guarda en una bbdd
* El usuario puede asociar una causa concreta a cada job fallido. Puede hacerlo en cualquier momento
* Con la información de las causas de error de los jobs (de algunos de ellos, no necesariamente todos) se entrena una red neuronal
* Se probarán diferentes redes neuronales disponibles en Spark o en Deeplearning4Java (red neuronal, deep learning, recurrent network)
* Se harán iteraciones cortas y releases frecuentes. La app debe estar corriendo en todo momento en un servidor proporcionado por el profesor

**Competencias desarrolladas**: git, github, Java, ElasticSearch, Logstash, Jenkins, redes neuronales

## Construcción automática de EclipseGavab e incorporación de libs adicionales a Pascaline

* Construcción desatendida de EclipseGavab:
** Descarga de herramientas necearias (Ruby, Haskell, FreePascal, JRE, ...) en el caso de Win
** Construcción del IDE para las diferentes plataformas
* Ciclo de release: construcción y publicación en bintray automáticas
* IDEConfigurator: detectar en Linux herramientas que faltan y visualizar los comandos necesarios para instalarlas

## Eclipse Che

* Montar la infraestructura
* Estudiar diferentes despliegues
* Integración con git
* Proceso de desarrollo con Che (interacción del equipo, compartición de estilos entre workspaces, Jenkins...)

## Ejecutores Jenkins con monitorización (asignado)

## UI para monitorización (asignado)

## Análisis de logs Big Data con Spark+ES (asignado)
