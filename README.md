# Comentarios del Notebook 02_web_scrapping.ipynb
**Equipo:** grupo11 · **Integración GitHub:** @anmerinoto

Taller de Web Scraping en Python de D-Lab

[![Datahub](https://img.shields.io/badge/launch-datahub-blue)](https://dlab.datahub.berkeley.edu/hub/user-redirect/git-pull?repo=https%3A%2F%2Fgithub.com%2Fdlab-berkeley%2FPython-Web-Scraping&urlpath=lab%2Ftree%2FPython-Web-Scraping%2F&branch=main)
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/dlab-berkeley/Python-Web-Scraping/HEAD)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

Este repositorio contiene los materiales para el taller de raspado web de Python de D-Lab.

## Requisitos previos

Recomendamos asistir a [Fundamentos de Python](https://github.com/dlab-berkeley/python-fundamentals) y [Organización de datos de Python](https://github.com/dlab-berkeley/Python-Data-Wrangling/) antes de este taller. Además, recomendamos una comprensión básica de HTML y CSS.

Consulte el [Catálogo de talleres] (https://dlab-berkeley.github.io/dlab-workshops/) de D-Lab para explorar todos los talleres, ver lo que se está ejecutando ahora y revisar los requisitos previos.

## Objetivos del taller

En este taller, cubrimos cómo extraer datos de la web usando Python. 
El raspado implica descargar el código fuente de una página web y examinar el archivo material para extraer los datos deseados.

El Web Scraping generalmente solo se realiza cuando las API web no están disponibles. Plataformas como Twitter, Reddit o The New York Times ofrecen API para recuperar datos. Si usted desea aprender a usar las API web en Python, consulte [Python Web APIs](https://github.com/dlab-berkeley/Python-Web-APIs).

## Instrucciones de instalación

Anaconda es un útil software de gestión de paquetes que permite ejecutar Python
y cuadernos Jupyter fácilmente. Instalar Anaconda es la forma más fácil de hacer
Seguro que tienes todo el software necesario para ejecutar los materiales para este taller. Si desea ejecutar Python en su propia computadora, complete lo siguiente

Pasos previos al taller:

1. [Descargue e instale Anaconda (Python 3.9
distribución)](https://www.anaconda.com/products/individual). Haga clic en el icono
Botón "Descargar".

2. Descargue el [taller] Python Web Scraping
materiales](https://github.com/dlab-berkeley/Python-Web-Scraping):

   - Haga clic en el botón verde "Código" en la parte superior derecha del repositorio
información.
   - Haga clic en "Descargar Zip".
   - Extraiga este archivo a una carpeta en su computadora donde pueda fácilmente
acceder a él (recomendamos Escritorio).

3. Opcional: si estás familiarizado con 'git', puedes clonarlo
repositorio abriendo una terminal e ingresando el comando 'git clone
git@github.com:dlab-berkeley/Python-Web-Scraping.git'.

## ¿Python no funciona en su computadora?

Si no tiene Anaconda instalada y los materiales cargados en su taller
para cuando comience,  recomendamos *encarecidamente* usar el centro de datos de UC Berkeley para ejecutar los materiales para estas lecciones. Puede acceder al DataHub haciendo clic en este botón: 

[![ Centro de datos](https://img.shields.io/badge/launch-datahub-blue)](https://dlab.datahub.berkeley.edu/hub/user-redirect/git-pull?repo=https%3A%2F%2Fgithub.com%2Fdlab-berkeley%2FPython-Web-Scraping&urlpath=lab%2Ftree%2FPython-Web-Scraping%2F&branch=main)

El DataHub descarga este repositorio, junto con los paquetes necesarios, y
le permite ejecutar los materiales en un cuaderno de Jupyter que se almacena en UC de los servidores de Berkeley. No es necesaria ninguna instalación por su parte, solo necesita un navegador de Internet y una identificación de CalNet para iniciar sesión. Al usar DataHub, puede Guarde su trabajo y vuelva a él en cualquier momento. Cuando quieras volver a tu trabajo guardado, simplemente vaya directamente a [DataHub] (https://datahub.berkeley.edu), firme y haga clic en la  carpeta 'Python-Web-Scraping'.

Si no tiene una identificación de Berkeley CalNet, aún puede ejecutar estas lecciones en el cloud, haciendo clic en este botón:

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/dlab-berkeley/Python-Web-Scraping/HEAD)

Sin embargo, al usar este botón, no puede guardar su trabajo.

## Ejecuta el código

1. Abra la aplicación Anaconda Navigator. Deberías ver el logotipo de la serpiente verde en tu pantalla. Tenga en cuenta que esto puede tardar unos minutos en cargar el archivo primera vez. 

2. Haga clic en el botón "Iniciar" debajo de "Jupyter Notebooks" y navegue por su
 sistema de archivos a la  carpeta 'Python-Web-Scraping' que descargó anteriormente.  Nota que, si descarga los materiales de GitHub, el nombre de la carpeta puede en su lugar ser 'Python-Text-Analysis-main'.

3. Abra la  carpeta 'lecciones' y haga clic en '01_introduction.md' para comenzar.

4. Presione Mayús + Entrar (o Ctrl + Entrar) para ejecutar una celda.

5. Por defecto, los paquetes necesarios para este taller ya deberían estar
Instalado. Puede instalarlos en el cuaderno de Jupyter Notebook ejecutando el comando siguiente línea en su propia celda:

> '''%pip install -r requirements.txt'''

Tenga en cuenta que todos los pasos anteriores se pueden ejecutar desde la terminal, si está familiarizado con cómo interactuar con Anaconda de esa manera. Sin embargo, el uso de Anaconda Navigator es la forma más fácil de comenzar si es tu primera vez trabajando con Anaconda.

# Acerca del D-Lab de UC Berkeley

D-Lab trabaja con profesores, personal de investigación y estudiantes de Berkeley para avanzar investigación intensiva en ciencias sociales y humanidades con uso intensivo de datos. Nuestro objetivo en D-Lab es proporcionar capacitación práctica, apoyo del personal, recursos y espacio para permitirle
use R para sus propias aplicaciones de investigación. Nuestros servicios se adaptan a todos los niveles de habilidad y no se necesitan antecedentes en programación, estadística o informática.
Ofrecemos estos servicios en forma de talleres, consultoría personalizada y
grupos de trabajo que cubren una variedad de temas de investigación, herramientas digitales y lenguajes de programación.

Visite la [página de inicio de D-Lab](https://dlab.berkeley.edu/) para obtener más información sobre nosotros. Puede ver nuestro [calendario](https://dlab.berkeley.edu/events/calendar) para
próximos eventos, aprenda cómo utilizar nuestros
[consultoría](https://dlab.berkeley.edu/consulting) y [datos
servicios](https://dlab.berkeley.edu/data), y echa un vistazo a los próximos
[talleres](https://dlab.berkeley.edu/events/workshops). Suscríbete a nuestro
[newsletter](https://dlab.berkeley.edu/news/weekly-newsletter) para mantenerse al día fecha en eventos, servicios y oportunidades de D-Lab.

# Otros talleres de D-Lab Python

D-Lab ofrece una variedad de talleres de Python, dirigidos a diferentes niveles de pericia.

## Talleres introductorios

- [Fundamentos de Python](https://github.com/dlab-berkeley/Python-Fundamentals)
- [Manejo de datos de Python](https://github.com/dlab-berkeley/Python-Data-Wrangling)
- [Visualización de datos de Python](https://github.com/dlab-berkeley/Python-Data-Visualization)

## Talleres intermedios y avanzados

- [Fundamentos geoespaciales de Python](https://github.com/dlab-berkeley/Geospatial-Data-and-Mapping-in-Python)
- [Raspado web y API de Python](https://github.com/dlab-berkeley/Python-Web-Scraping)
- [Aprendizaje automático de Python](https://github.com/dlab-berkeley/Python-Machine-Learning)
- [Análisis de texto de Python](https://github.com/dlab-berkeley/Python-Text-Analysis)
- [Aprendizaje profundo de Python](https://github.com/dlab-berkeley/Python-Deep-Learning)

# Colaboradores

* [Rochelle Terman](https://github.com/rochelleterman)
* [George McIntire](https://github.com/GeorgeMcIntire)
* [Pratik Sachdeva](https://github.com/pssachdeva)
* [Tom van Nuenen](https://github.com/tomvannuenen)
