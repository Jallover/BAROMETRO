
______                                _              ______          _        _            
| ___ \                              | |             | ___ \        | |      | |           
| |_/ / __ _ _ __ ___  _ __ ___   ___| |_ _ __ ___   | |_/ /__  _ __| |_ __ _| | ___  ___  
| ___ \/ _` | '__/ _ \| '_ ` _ \ / _ \ __| '__/ _ \  |  __/ _ \| '__| __/ _` | |/ _ \/ __| 
| |_/ / (_| | | | (_) | | | | | |  __/ |_| | | (_) | | | | (_) | |  | || (_| | |  __/\__ \ 
\____/ \__,_|_|  \___/|_| |_| |_|\___|\__|_|  \___/  \_|  \___/|_|   \__\__,_|_|\___||___/ 
                                                                                           
                                                                                           
              ______      _               ___  _     _           _                         
              |  _  \    | |             / _ \| |   (_)         | |                        
              | | | |__ _| |_ ___  ___  / /_\ \ |__  _  ___ _ __| |_ ___  ___              
              | | | / _` | __/ _ \/ __| |  _  | '_ \| |/ _ \ '__| __/ _ \/ __|             
              | |/ / (_| | || (_) \__ \ | | | | |_) | |  __/ |  | || (_) \__ \             
              |___/ \__,_|\__\___/|___/ \_| |_/_.__/|_|\___|_|   \__\___/|___/    

		   JAVIER LLOPIS VERT - UNIVERSITAT POLITÉCNICA DE VALENCIA
			      ANÁLISIS DEL SECTOR INFOMEDIARIO
____________________________________________________________________________________________________
____________________________________________________________________________________________________
____________________________________________________________________________________________________
                                                                                           
INDICE
---------------------------------------------------------------------------------------------------- 
1. Introducción. 
2. Descripción de la solución planteada.
3. Metodología.
4. Resultados.
5. Guía de uso.
6. Términos de uso.
____________________________________________________________________________________________________

1. INTRODUCCIÓN
----------------------------------------------------------------------------------------------------
El objetivo de este proyecto es de tratar valorar y mostrar el estado de los portales de trasparencia
y datos abiertos de 7 ciudades españolas: Valencia, Barcelona, Madrid, Sevilla, Bilbao, Santander y
Zaragoza. Observando una serie características como la cantidad de conjuntos de datos que posee el
portal, en que formatos se encuentran y los periodos de tiempo en los que se actualizan.

Estos datos son extraídos a través de los catálogos de los portales en formato rdf-dcat, catálogos que
en algunos portales no está disponible y por lo que no son participes en este proyecto. Algunos
catálogos son distintos de otros, y cada uno muestra la información que el responsable de cada portal
decide mostrar. Esto se ve reflejado en ausencia de datos, o presencia de datos de dudosa veracidad.


2. DESCRIPCIÓN DE LA SOLUCIÓN PLANTEADA
----------------------------------------------------------------------------------------------------
A la hora de abordar la cuestión de cómo generar un documento que muestre la información que agrupan 
los más de 1400 conjuntos de datos, se ha optado por utilizar una visualización mediante cuadros de 
mando utilizando el software Tableau Desktop. 

Y a partir de toda la información extraída de los catálogos de datos y de cada portal, evaluando 
distintos factores se trata de dar una valoración con una nota sobre 10 a cada portal de datos. 
Con el objetivo de identificar portales de datos con necesidad de mejoras.

Este proyecto está basado o inspirado en el barómetro de opendata producido por la Fundación World 
Wide Web en colaboración con la Red de Desarrollo de Datos Abiertos (OD4D) https://opendatabarometer.org
pero simplemente evaluando la implementación de los conjuntos de datos.


3. METODOLOGÍA
----------------------------------------------------------------------------------------------------
Primero se procedió a identificar los portales que serían analizados. La idea inicial era analizar
los portales de transparencia y datos abiertos de las Comunidades Autónomas, pero se encontró el 
problema de que muchos portales no disponían de su catálogo en formato rdf o en otro formato.
Se solicitó la incorporación de dichos catálogos o su acceso por vía e-mail o desde la sección de 
comunicación que los portales disponían para solicitudes o sugerencias ( http://prntscr.com/j7b758 ).

Ya que se disponía de un plazo corto de tiempo para la realización de este proyecto, se decidió cambiar
de analizar los portales de datos de las Comunidades Autónomas, a analizar los portales de sus capitales
ya que estos sí que disponían del catálogo de datos en el formato requerido o al menos la mayoría de ellos.

				CATÁLOGOS DE DATOS OBTENIDOS
				_____________________________

			Andalucía 		--> 	Sevilla
			Aragón 			--> 	Zaragoza
			Cantabria 		--> 	Santander
			Cataluña 		--> 	Barcelona
			Comunidad de Madrid 	--> 	Madrid
			Comunidad Valenciana 	--> 	Valencia
			País Vasco 		-->	Bilbao

Además, con la intención de disponer del catálogo de datos en la versión más actual posible, se programó
mediante la herramienta wget, un servidor local que descarga automáticamente los 7 catálogos (al 
proporcionarle los respectivos links de descarga de los portales) cada día 21 de cada mes.

Una vez finalizada la fase de obtención de datos se procede a la conformación de un dataset que agrupe
la información de las distintas ciudades para servir como base a Tableau para la realización de una 
visualización utilizando cuadros de mando. Este dataset contiene información sobre:
 
	- Ciudad (char - Rol Geográfico)
	- Número Total de Documentos que ese portal tiene a su disposición (Núm)
	- Fecha en la que se creó el catálogo (date)
	- Fecha en la que se actualizó por última vez el catálogo (date)
	- Tipo de Licencia (char)
	- El conjunto de datos se permite compartir (Boolean)
	- El conjunto de datos se permite transformar (Boolean)
	- Se permite usar el conjunto de datos con fines comerciales (Boolean)
	- El acceso al conjunto de datos es gratuito (Boolean)
	- Fecha en la que se actualizó por última vez el conjunto de datos (Date)
	- Formatos legibles por máquina (1-0)
	- Formatos Mapa (1-0)
	- Sin Formato (1-0)
	- Categoría a la que pertenece el conjunto de datos (char)
	- Nombre de conjunto de datos (char)
	- % de presencia en el total de documentos de la Categoría (Núm)
	- Fecha de Incorporación del conjunto de datos (date)
	- Frecuencia de actualización (char)

Para obtener esta información y en un formato que pueda leer Tableau Desktop de una forma rápida se ha 
hecho uso del catálogo de datos en formato csv en caso de disponerlo y el software Open Refine leyendo
de las etiquetas del catálogo:

	-<dct:SizeOrDuration>: Número de documentos del catálogo
	-<dct:issued*: Fecha de creación
	-<dct:modified*: Fecha de modificación
	-<dct:license rdf:resource=*: Licencia de uso
	-<dct:title xml:lang="ca">: Nombre del conjunto de datos
	-<dct:Frequency>: Frecuencia de actualización
	-<dct:format>: Formato

Una vez conformado el dataset, uniendo el de cada ciudad y ordenándolo por categorías, se realizó una 
fase de verificación en la que se identificaron datos nulos, fechas que no son correctas o que el número 
de documentos del catálogo no se corresponde con el que decía al inicio de su correspondiente documento
en algunos casos.

Utilizando como base el dataset creado durante la fase anterior se procede a realizar la creación de 
los siguientes cuadros de mando mediante Tableau, mostrando la información a día 17/04/2018:

	- Mapa Geográfico por ciudades que sirve como filtro interactivo:
		- La información se muestra al pasar el ratón por encima de la zona
		- Número total de documentos disponibles
		- Número de Registros en categoría seleccionada
		- Filtro Año
		- Filtro Categoría
		- Leyenda Ciudad

	- Mapa en Árbol (Tamaño Num_Registros Categoría):
		- Para cada Ciudad, dividida por categorías que clasifican los conjuntos de datos.
		- % que representa la categoría en el catálogo
		- Número de registros (Emergente)
		- Gama de colores para Categorías
		- Filtro Ciudad (Lista)
		- Leyenda Categoría

	- Barras Apiladas
		- Columnas = Ciudad
		- Datos = Conteo Formatos Máquina-Mapa
		- Filtro Ciudad
		- Filtro Categoría

	- Tablas de Texto
		- Nota de cada Portal

	- Barras Verticales
		- Columnas = Ciudad
		- Datos = Número de Registros actualizados entre 2017 y 2018
		- Filtro Ciudad
		- Filtro Categoría

	- FILTROS
		- Ciudad
		- Categoría

Para el cálculo de la nota de cada portal lo que se ha hecho ha sido calcular una nota sobre 10
para cada categoría en cada portal. Puntuándolas en función de 9 características que son:

	-Existen datos de esa característica (Hay datos = 1'11 puntos || No hay datos = 0)

	-Del total de conjuntos de datos de cada categoría cuántos de ellos están en cualquier formato
  	 (100% de sus documentos en cualquier formato = 1'11 puntos)

	-Cuantos documentos de cada categoría tienen formato legible por máquina (CSV, JSON, GEOJSON...) 
  	 (100%=1'11puntos)

	-Cuantos documentos de cada categoría tienen formato mapa (WFS,WSD,SHP...) (100%=1'11puntos)

	-La licencia del conjunto de datos permite el acceso de forma gratuita (100%=1,11 puntos)

	-La licencia del conjunto de datos permite trabajar con esos datos (100%=1,11 puntos)

	-Cuántos datos son fáciles de acceder (Dificultad para acceder a un conjunto de datos) 
	 (100%=1,11 puntos)

	-Cuántos conjuntos de datos se han actualizado entre 2017-2018 (100%=1,11)

	-El número de conjuntos de datos de la categoría está por encima o es igual a la media global de 
 	 documentos en esa categoría. (Llegar a la media equivale al 100% de la puntuación = 1'11 puntos)

Así, cada categoría en cada portal recibe una nota sobre 9'99 que se redondea a 10, obteniendo un total 
de quince notas para cada categoría:

	- Medio Ambiente	- Hacienda
	- Urbanismo		- Seguridad
	- Cultura y Ocio	- Sociedad y bienestar
	- Economía		- Turismo
	- Educación		- Comercio
	- Transporte		- Ciencia y Tecnología
	- Salud			- Vivienda
	- Sector Público

A estas quince notas, se le suma una más en función de si el número total de documentos de un portal
es igual o superior a la media de documentos total de todos los portales examinados. Siendo 210
el número de documentos que otorgaría la máxima nota.
De estas 16 notas se calcula su media sobre 10 y esa es la nota resultante para cada portal.

Se utiliza una hoja de cálculo en excel para realizar las valoraciones, la cual se usará como fuente 
de datos al libro de Tableau para generar un cuadro de mando comparando las notas de cada portal.
En el caso de que haya datos nulos, o que no figuren dentro del catálogo como, por ejemplo, la fecha 
de actualización de cada conjunto de datos en el portal de Barcelona, se entenderá como que el dato no 
ha sido actualizado.

De esta forma se obtiene el cuadro de mando listo y completamente funcional desde Tableu Public.

4. RESULTADOS
----------------------------------------------------------------------------------------------------

**Número de Documentos del portal vs Número de Registros:
	-Valencia 	--> 118 Documentos --> 158 Registros
	-Barcelona 	--> 463 Documentos --> 345 Registros
	-Bilbao 	--> 189 Documentos --> 222 Registros
	-Santander 	--> 88 Documentos  --> 71 Registros
	-Madrid 	--> 323 Documentos --> 300 Registros
	-Sevilla 	--> 147 Documentos --> 202 Registros
	-Zaragoza 	--> 145 Documentos --> 145 Registros

	*Puede darse el caso de que haya más registros que documentos debido a que un conjunto de
	datos se encuentre clasificado en varias categorías. Pero es anómalo que se encuentran menos
	registros que documentos dice tener el catálogo.

**Número de Conjuntos de Datos por Categoría y Ciudad y % de presencia en su catálogo:
	- Medio Ambiente:			- Urbanismo:
	· Valencia  	--> 	37 - 31,4%	|	· Valencia 	--> 	20 - 16,9%
	· Barcelona 	--> 	14 - 3%		|	· Barcelona 	--> 	59 - 12,7%
	· Bilbao 	--> 	5 - 2,6%	|	· Bilbao 	--> 	11 - 5,8%
	· Santander 	--> 	7 - 29,5%	|	· Santander 	--> 	19 - 21,6%
	· Madrid 	--> 	35 - 10,8%	|	· Madrid 	--> 	29 - 9%
	· Sevilla 	--> 	3 - 2%		|	· Sevilla 	--> 	7 - 4,8%
	· Zaragoza 	-->	15 - 10,3%	|	· Zaragoza 	--> 	19 - 13,1%
		
	- Cultura y Ocio:				- Economía:
	· Valencia 	--> 	5 - 4,2%	|	· Valencia 	--> 	3 - 2,5%
	· Barcelona 	--> 	51 - 11%	|	· Barcelona 	--> 	15 - 3,2%
	· Bilbao 	--> 	2 - 1,1%	|	· Bilbao 	--> 	47 - 24,9%
	· Santander 	--> 	7 - 8%		|	· Santander 	--> 	0 - 0%
	· Madrid 	--> 	20 - 6,2%	|	· Madrid 	--> 	8 - 2,5%
	· Sevilla 	--> 	19 - 12,9%	|	· Sevilla 	--> 	60 - 44,9%
	· Zaragoza 	--> 	10 - 6,9%	|	· Zaragoza 	--> 	13 - 9%
	
	- Educación:					- Transporte:
	· Valencia 	--> 	1 - 0,8%	|	· Valencia 	--> 	27 - 22,9%
	· Barcelona 	--> 	1 - 0,2%	|	· Barcelona 	--> 	45 - 9,7%
	· Bilbao 	--> 	0 - 0%		|	· Bilbao 	--> 	30 - 15,9%
	· Santander 	--> 	0 - 0%		|	· Santander 	--> 	26 - 29,5%
	· Madrid 	--> 	7 - 2,2%	|	· Madrid 	--> 	57 - 17,6%
	· Sevilla 	--> 	2 - 1,4%	|	· Sevilla 	--> 	21 - 14,2%
	· Zaragoza 	--> 	3 - 2,1%	|	· Zaragoza 	--> 	17 - 11,7%
		
	- Salud:					- Sector Público:
	· Valencia 	--> 	15 - 12,7%	|	· Valencia 	--> 	5 - 4,2%
	· Barcelona	--> 	0 - 0%		|	· Barcelona 	--> 	65 - 14%
	· Bilbao 	--> 	0 - 0%		|	· Bilbao 	--> 	120 - 63,5%
	· Santander 	--> 	0 - 0%		|	· Santander 	--> 	0 - 0%
	· Madrid 	--> 	16 - 5%		|	· Madrid 	--> 	56 - 17,3%
	· Sevilla 	--> 	0 - 0%		|	· Sevilla 	--> 	75 - 51,7%
	· Zaragoza 	--> 	3 - 2,1%	|	· Zaragoza 	--> 	20 - 13,8%
		
	- Hacienda:					- Seguridad:
	· Valencia 	--> 	3 - 2,5%	|	· Valencia 	--> 	1 - 0,8%
	· Barcelona 	--> 	7 - 1,5%	|	· Barcelona 	--> 	6 - 1,3%
	· Bilbao 	--> 	0 - 0%		|	· Bilbao 	--> 	0 - 0%
	· Santander 	--> 	0 - 0%		|	· Santander 	--> 	0 - 0%
	· Madrid 	--> 	17 - 5,3%	|	· Madrid 	--> 	10 - 3,1%
	· Sevilla 	--> 	0 - 0%		|	· Sevilla 	--> 	2 - 1,4%
	· Zaragoza 	--> 	11 - 7,6%	|	· Zaragoza 	--> 	4 - 2,8%
	
	- Sociedad y bienestar:				- Turismo:
	· Valencia 	--> 	26 - 22%	|	· Valencia 	--> 	10 - 8,5%
	· Barcelona 	--> 	10 - 2,2%	|	· Barcelona 	--> 	3 - 0,6%
	· Bilbao 	--> 	5 - 2,6%	|	· Bilbao 	--> 	1 - 0,5%
	· Santander 	--> 	6 - 6,8%	|	· Santander 	--> 	0 - 0%
	· Madrid 	--> 	26 - 8%		|	· Madrid 	--> 	10 - 3,1%
	· Sevilla 	--> 	3 - 2%		|	· Sevilla 	--> 	6 - 4,1%
	· Zaragoza 	--> 	15 - 10,3%	|	· Zaragoza 	--> 	6 - 4,1%

	- Comercio:					- Ciencia y Tecnología:
	· Valencia 	--> 	3 - 2,5%	|	· Valencia 	--> 	1 - 0,8%
	· Barcelona 	--> 	8 - 1,7%	|	· Barcelona 	--> 	2 - 0,4%
	· Bilbao 	--> 	0 - 0%		|	· Bilbao 	--> 	1 - 0,5%
	· Santander 	--> 	0 - 0%		|	· Santander 	--> 	6 - 6,8%
	· Madrid 	--> 	5 - 1,5%	|	· Madrid 	--> 	3 - 0,9%
	· Sevilla 	--> 	2 - 1,4%	|	· Sevilla 	--> 	2 - 1,4%
	· Zaragoza 	--> 	3 - 2,1%	|	· Zaragoza 	--> 	6 - 4,1%

	- Vivienda:				|
	· Valencia 	--> 	1 - 0,8%	|
	· Barcelona 	--> 	59 - 12,7%	|
	· Bilbao 	--> 	0 - 0%		|
	· Santander 	--> 	0 - 0%		|
	· Madrid 	--> 	1 - 0,3%	|
	· Sevilla 	--> 	0 - 0%		|
	· Zaragoza 	--> 	1 0,7%		|


**Número de Registros Actualizados 2017-2018
	· Valencia 	--> 	53 / 158
	· Barcelona 	--> 	*La Fecha de actualización de los conjuntos no figura*
	· Bilbao 	--> 	124 / 222
	· Santander 	--> 	6 / 71
	· Madrid 	--> 	217 / 300
	· Sevilla 	--> 	71 / 202
	· Zaragoza 	--> 	43 / 145


**Registros Formato Máquina
	· Valencia 	--> 	144 / 158
	· Barcelona 	--> 	244 / 345
	· Bilbao 	--> 	165 / 222
	· Santander 	--> 	66 / 71
	· Madrid 	--> 	207 / 300
	· Sevilla 	--> 	186 / 202
	· Zaragoza 	--> 	109 / 145

**Registros Formato Mapa
	· Valencia 	--> 	135 / 158
	· Barcelona 	--> 	50 / 345
	· Bilbao 	--> 	18 / 222
	· Santander 	--> 	10 / 71
	· Madrid 	--> 	112 / 300
	· Sevilla 	--> 	46 / 202
	· Zaragoza 	--> 	42 / 145

**Registros Sin Formato
	· Valencia 	--> 	3 / 158
	· Barcelona 	--> 	51 / 345
	· Bilbao 	--> 	42 / 222
	· Santander 	--> 	2 / 71
	· Madrid 	--> 	73 / 300
	· Sevilla 	--> 	5 / 202
	· Zaragoza 	--> 	25 / 145

**Notas Portales (El cálculo de la nota puede verse el documento del repositorio GitHub)
	· Valencia 	--> 	8'1 / 10
	· Barcelona 	--> 	7 / 10
	· Bilbao 	--> 	5'1 / 10
	· Santander 	--> 	3'1 / 10
	· Madrid 	--> 	8'7 / 10
	· Sevilla 	--> 	6'4 / 10
	· Zaragoza 	--> 	7'9 / 10

5. GUÍA DE USO
----------------------------------------------------------------------------------------------------

Para el uso del cuadro de mando basta con acceder desde Tableu Public y una vez abierto
hacer click izquierdo sobre cualquier nombre de ciudad, categoría o formato para resaltarlo. Una 
vez resaltado, si elegimos la opción "Mantener solamente" los gráficos únicamente mostraran los datos 
seleccionados. Para volver al estado anterior deberá elegir la opción deshacer o Control+Z y el cuadro 
de mando volverá a mostrar los datos para todas las ciudades evaluadas.

También se puede hacer uso de los filtros de la parte izquierda para Ciudad y Categoría.
El mapa geográfico de la parte izquierda es completamente interactivo y clickando en una provincia
actuará como filtro para el resto de gráficos. Los datos mostrados son a día 17/04/2018.

6. TERMINOS DE USO
----------------------------------------------------------------------------------------------------

Los conjuntos de datos de los portales de datos abiertos de las ciudades examinadas están bajo una
licencia Pública Internacional Creative Commons Attribution 4.0. 
https://creativecommons.org/licenses/by/4.0/legalcode


Esto es un resumen inteligible para humanos (y no un sustituto) de la licencia.

Usted es libre de:

	-Compartir — copiar y redistribuir el material en cualquier medio o formato.

	-Adaptar, remezclar, transformar y crear a partir del material para cualquier finalidad, 
	incluso comercial.
 	-Esta licencia está aceptada para Obras Culturales Libres.

	-El licenciador no puede revocar estas libertades mientras cumpla con los términos de la 
	licencia.

Bajo las condiciones siguientes:

	-Reconocimiento
	Debe reconocer adecuadamente la autoría, proporcionar un enlace a la licencia e indicar si 
	se han realizado cambios <Puede hacerlo de cualquier manera razonable, pero no de una manera 
	que sugiera que tiene el apoyo del licenciador o lo recibe por el uso que hace>.

	-No hay restricciones adicionales 
	No puede aplicar términos legales o medidas tecnológicas que legalmente restrinjan realizar 
	aquello que la licencia permite.
Avisos:
	-No tiene que cumplir con la licencia para aquellos elementos del material en el dominio público 
	o cuando su utilización esté permitida por la aplicación de una excepción o un límite.

	-No se dan garantías. 
	La licencia puede no ofrecer todos los permisos necesarios para la utilización prevista. 
	Por ejemplo, otros derechos como los de publicidad, privacidad, o los derechos morales pueden 
	limitar el uso del material.


_______________________________________________________________________________________________________
Creative Commons Attribution 4.0 International Public License
By exercising the Licensed Rights (defined below), You accept and agree to be bound by the terms and conditions of this Creative Commons Attribution 4.0 International Public License ("Public License"). To the extent this Public License may be interpreted as a contract, You are granted the Licensed Rights in consideration of Your acceptance of these terms and conditions, and the Licensor grants You such rights in consideration of benefits the Licensor receives from making the Licensed Material available under these terms and conditions.

Section 1 – Definitions.

Adapted Material means material subject to Copyright and Similar Rights that is derived from or based upon the Licensed Material and in which the Licensed Material is translated, altered, arranged, transformed, or otherwise modified in a manner requiring permission under the Copyright and Similar Rights held by the Licensor. For purposes of this Public License, where the Licensed Material is a musical work, performance, or sound recording, Adapted Material is always produced where the Licensed Material is synched in timed relation with a moving image.
Adapter's License means the license You apply to Your Copyright and Similar Rights in Your contributions to Adapted Material in accordance with the terms and conditions of this Public License.
Copyright and Similar Rights means copyright and/or similar rights closely related to copyright including, without limitation, performance, broadcast, sound recording, and Sui Generis Database Rights, without regard to how the rights are labeled or categorized. For purposes of this Public License, the rights specified in Section 2(b)(1)-(2) are not Copyright and Similar Rights.
Effective Technological Measures means those measures that, in the absence of proper authority, may not be circumvented under laws fulfilling obligations under Article 11 of the WIPO Copyright Treaty adopted on December 20, 1996, and/or similar international agreements.
Exceptions and Limitations means fair use, fair dealing, and/or any other exception or limitation to Copyright and Similar Rights that applies to Your use of the Licensed Material.
Licensed Material means the artistic or literary work, database, or other material to which the Licensor applied this Public License.
Licensed Rights means the rights granted to You subject to the terms and conditions of this Public License, which are limited to all Copyright and Similar Rights that apply to Your use of the Licensed Material and that the Licensor has authority to license.
Licensor means the individual(s) or entity(ies) granting rights under this Public License.
Share means to provide material to the public by any means or process that requires permission under the Licensed Rights, such as reproduction, public display, public performance, distribution, dissemination, communication, or importation, and to make material available to the public including in ways that members of the public may access the material from a place and at a time individually chosen by them.
Sui Generis Database Rights means rights other than copyright resulting from Directive 96/9/EC of the European Parliament and of the Council of 11 March 1996 on the legal protection of databases, as amended and/or succeeded, as well as other essentially equivalent rights anywhere in the world.
You means the individual or entity exercising the Licensed Rights under this Public License. Your has a corresponding meaning.
Section 2 – Scope.

License grant.
Subject to the terms and conditions of this Public License, the Licensor hereby grants You a worldwide, royalty-free, non-sublicensable, non-exclusive, irrevocable license to exercise the Licensed Rights in the Licensed Material to:
reproduce and Share the Licensed Material, in whole or in part; and
produce, reproduce, and Share Adapted Material.
Exceptions and Limitations. For the avoidance of doubt, where Exceptions and Limitations apply to Your use, this Public License does not apply, and You do not need to comply with its terms and conditions.
Term. The term of this Public License is specified in Section 6(a).
Media and formats; technical modifications allowed. The Licensor authorizes You to exercise the Licensed Rights in all media and formats whether now known or hereafter created, and to make technical modifications necessary to do so. The Licensor waives and/or agrees not to assert any right or authority to forbid You from making technical modifications necessary to exercise the Licensed Rights, including technical modifications necessary to circumvent Effective Technological Measures. For purposes of this Public License, simply making modifications authorized by this Section 2(a)(4) never produces Adapted Material.
Downstream recipients.
Offer from the Licensor – Licensed Material. Every recipient of the Licensed Material automatically receives an offer from the Licensor to exercise the Licensed Rights under the terms and conditions of this Public License.
No downstream restrictions. You may not offer or impose any additional or different terms or conditions on, or apply any Effective Technological Measures to, the Licensed Material if doing so restricts exercise of the Licensed Rights by any recipient of the Licensed Material.
No endorsement. Nothing in this Public License constitutes or may be construed as permission to assert or imply that You are, or that Your use of the Licensed Material is, connected with, or sponsored, endorsed, or granted official status by, the Licensor or others designated to receive attribution as provided in Section 3(a)(1)(A)(i).
Other rights.

Moral rights, such as the right of integrity, are not licensed under this Public License, nor are publicity, privacy, and/or other similar personality rights; however, to the extent possible, the Licensor waives and/or agrees not to assert any such rights held by the Licensor to the limited extent necessary to allow You to exercise the Licensed Rights, but not otherwise.
Patent and trademark rights are not licensed under this Public License.
To the extent possible, the Licensor waives any right to collect royalties from You for the exercise of the Licensed Rights, whether directly or through a collecting society under any voluntary or waivable statutory or compulsory licensing scheme. In all other cases the Licensor expressly reserves any right to collect such royalties.
Section 3 – License Conditions.

Your exercise of the Licensed Rights is expressly made subject to the following conditions.

Attribution.

If You Share the Licensed Material (including in modified form), You must:

retain the following if it is supplied by the Licensor with the Licensed Material:
identification of the creator(s) of the Licensed Material and any others designated to receive attribution, in any reasonable manner requested by the Licensor (including by pseudonym if designated);
a copyright notice;
a notice that refers to this Public License;
a notice that refers to the disclaimer of warranties;
a URI or hyperlink to the Licensed Material to the extent reasonably practicable;
indicate if You modified the Licensed Material and retain an indication of any previous modifications; and
indicate the Licensed Material is licensed under this Public License, and include the text of, or the URI or hyperlink to, this Public License.
You may satisfy the conditions in Section 3(a)(1) in any reasonable manner based on the medium, means, and context in which You Share the Licensed Material. For example, it may be reasonable to satisfy the conditions by providing a URI or hyperlink to a resource that includes the required information.
If requested by the Licensor, You must remove any of the information required by Section 3(a)(1)(A) to the extent reasonably practicable.
If You Share Adapted Material You produce, the Adapter's License You apply must not prevent recipients of the Adapted Material from complying with this Public License.
Section 4 – Sui Generis Database Rights.

Where the Licensed Rights include Sui Generis Database Rights that apply to Your use of the Licensed Material:

for the avoidance of doubt, Section 2(a)(1) grants You the right to extract, reuse, reproduce, and Share all or a substantial portion of the contents of the database;
if You include all or a substantial portion of the database contents in a database in which You have Sui Generis Database Rights, then the database in which You have Sui Generis Database Rights (but not its individual contents) is Adapted Material; and
You must comply with the conditions in Section 3(a) if You Share all or a substantial portion of the contents of the database.
For the avoidance of doubt, this Section 4 supplements and does not replace Your obligations under this Public License where the Licensed Rights include other Copyright and Similar Rights.
Section 5 – Disclaimer of Warranties and Limitation of Liability.

Unless otherwise separately undertaken by the Licensor, to the extent possible, the Licensor offers the Licensed Material as-is and as-available, and makes no representations or warranties of any kind concerning the Licensed Material, whether express, implied, statutory, or other. This includes, without limitation, warranties of title, merchantability, fitness for a particular purpose, non-infringement, absence of latent or other defects, accuracy, or the presence or absence of errors, whether or not known or discoverable. Where disclaimers of warranties are not allowed in full or in part, this disclaimer may not apply to You.
To the extent possible, in no event will the Licensor be liable to You on any legal theory (including, without limitation, negligence) or otherwise for any direct, special, indirect, incidental, consequential, punitive, exemplary, or other losses, costs, expenses, or damages arising out of this Public License or use of the Licensed Material, even if the Licensor has been advised of the possibility of such losses, costs, expenses, or damages. Where a limitation of liability is not allowed in full or in part, this limitation may not apply to You.
The disclaimer of warranties and limitation of liability provided above shall be interpreted in a manner that, to the extent possible, most closely approximates an absolute disclaimer and waiver of all liability.
Section 6 – Term and Termination.

This Public License applies for the term of the Copyright and Similar Rights licensed here. However, if You fail to comply with this Public License, then Your rights under this Public License terminate automatically.
Where Your right to use the Licensed Material has terminated under Section 6(a), it reinstates:

automatically as of the date the violation is cured, provided it is cured within 30 days of Your discovery of the violation; or
upon express reinstatement by the Licensor.
For the avoidance of doubt, this Section 6(b) does not affect any right the Licensor may have to seek remedies for Your violations of this Public License.
For the avoidance of doubt, the Licensor may also offer the Licensed Material under separate terms or conditions or stop distributing the Licensed Material at any time; however, doing so will not terminate this Public License.
Sections 1, 5, 6, 7, and 8 survive termination of this Public License.
Section 7 – Other Terms and Conditions.

The Licensor shall not be bound by any additional or different terms or conditions communicated by You unless expressly agreed.
Any arrangements, understandings, or agreements regarding the Licensed Material not stated herein are separate from and independent of the terms and conditions of this Public License.
Section 8 – Interpretation.

For the avoidance of doubt, this Public License does not, and shall not be interpreted to, reduce, limit, restrict, or impose conditions on any use of the Licensed Material that could lawfully be made without permission under this Public License.
To the extent possible, if any provision of this Public License is deemed unenforceable, it shall be automatically reformed to the minimum extent necessary to make it enforceable. If the provision cannot be reformed, it shall be severed from this Public License without affecting the enforceability of the remaining terms and conditions.
No term or condition of this Public License will be waived and no failure to comply consented to unless expressly agreed to by the Licensor.
Nothing in this Public License constitutes or may be interpreted as a limitation upon, or waiver of, any privileges and immunities that apply to the Licensor or You, including from the legal processes of any jurisdiction or authority.
Creative Commons is not a party to its public licenses. Notwithstanding, Creative Commons may elect to apply one of its public licenses to material it publishes and in those instances will be considered the “Licensor.” The text of the Creative Commons public licenses is dedicated to the public domain under the CC0 Public Domain Dedication. Except for the limited purpose of indicating that material is shared under a Creative Commons public license or as otherwise permitted by the Creative Commons policies published at creativecommons.org/policies, Creative Commons does not authorize the use of the trademark “Creative Commons” or any other trademark or logo of Creative Commons without its prior written consent including, without limitation, in connection with any unauthorized modifications to any of its public licenses or any other arrangements, understandings, or agreements concerning use of licensed material. For the avoidance of doubt, this paragraph does not form part of the public licenses.

Creative Commons may be contacted at creativecommons.org.
___________________________________________________________________________________________________


