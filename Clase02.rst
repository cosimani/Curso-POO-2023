.. -*- coding: utf-8 -*-

.. _rcs_subversion:
  
Clase 02 - POO 2022
===================
(Fecha: 17 de marzo)


Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`Library, Librería, Biblioteca 2021 <https://www.youtube.com/watch?v=k9ZZSSWuX6E>`_ 

`std C y std C++ 2021 <https://www.youtube.com/watch?v=GrOLHLHcZqg>`_ 

`Espacio de nombres 2021 <https://www.youtube.com/watch?v=oUVACqK4ssg>`_ 



Instalación de herramientas
===========================

:QtCreator: 
	- Si hay instaladas versiones anteriores de Qt, desinstalarlas con C:\\Qt\\MaintenanceTool.exe y tildando Uninstall only 
	- Se recomienda este instalador Offline: `https://download.qt.io/archive/qt/5.14/5.14.1 <https://download.qt.io/archive/qt/5.14/5.14.1>`_
	- Importante la instalación de: 'Biblioteca Qt 5.14.1'  'Qt Creator'  'MinGW 7.3.0 64-bit'

:OpenSSL: 
	- Descargar instalador desde la `Página de descarga <https://slproweb.com/products/Win32OpenSSL.html>`_
	- Seleccionar el instalador `Win64 OpenSSL v3.1.0 <https://slproweb.com/download/Win64OpenSSL-3_1_0.exe>`_


Biblioteca estándar de C++
==========================

- Está en el espacio de nombres ``std``
- En la biblioteca estándar de C, los archivos de cabecera X.h se reemplazan por cX o X. Por ejemplo:

.. code-block:: c

	#include <stdlib.h>                   #include <cstdlib>    

	    int atoi( const char * )  // Convierte a int un número expresado en cadena
	    int abs( int )            // Devuleve el valor absoluto
	    int rand()                // Devuelve un número pseudo aleatorio entre 0 y 32767


	#include <stdio.h>                   #include <cstdio>    

	    // Borra un archivo. Devuelve 0 o un código de error.
	    int remove( const char * filename )

	    // Imprime por pantalla. Recibe un número indefinido de argumentos.
	    int printf( const char * format, ... )

	#include <iostream.h>                   #include <iostream>    

	    cout
	    cin
	    endl



Espacio de nombres (namespace)
==============================

- Permite agrupar declaraciones (de clases, funciones, etc.).
- Permite declarar identificadores (nombre de variables) sin que se solapen. Es decir, identificadores iguales en distinto namespace.
- Se pueden incluir las definiciones en un namespace pero mejor no.
- Un espacio de nombre es un ámbito.

Ejemplos con namespace
======================

**Ejemplo 1**

.. code-block:: c

	#include <iostream>
	using namespace std;

	namespace enteros  {
	    int var1 = 5;
	    int var2 = 7;
	}

	namespace con_decimales  {
	    float var1 = 5.14;
	    float var2 = 7.13;
	}

	int main()  {
	    cout << enteros::var1 << endl;
	    cout << con_decimales::var1 << endl;
	    return 0;
	}

- ¿Cuál es la salida por consola?

.. ..

 <!---  
 Publica:    5    5.14		(para ocultar requiere una primer linea con .. ..    Los que queremos ocultar debe tener el menos un espacio)
 --->

**Ejemplo 2**

.. code-block:: c

	#include <iostream>
	using namespace std;
	
	namespace enteros  {
	    int var1 = 5;
	    int var2 = 7;
	}
	
	namespace con_decimales  {
	    float var1 = 5.14;
	    float var2 = 7.13;
	}
	
	int main()  {
	    using enteros::var1;
	    using con_decimal::var2;

	    cout << var1 << endl;
	    cout << var2 << endl;
	    cout << enteros::var2 << endl;
	    cout << con_decimales::var1 << endl;

	    return 0;
	}

.. ..

 <!---  
 Publica:    5		7.13		7		5.14
 --->

**Ejemplo 3**

.. code-block:: c

	#include <iostream>
	using namespace std;

	namespace enteros  {
	    int var1 = 5;
	    int var2 = 7;
	}
	
	namespace con_decimales  {
	    float var1 = 5.14;
	    float var2 = 7.13;
	}

	int main()  {
	    using namespace enteros;

	    cout << var1 << endl;
	    cout << var2 << endl;
	    cout << con_decimales::var1 << endl;
	    cout << con_decimales::var2 << endl;

	    return 0;
	}

.. ..

 <!---  
 Publica:    5		7		5.14		7.13
 --->

**Ejemplo 4**

.. code-block:: c

	#include <iostream>
	using namespace std;

	namespace enteros  {
	    int var1 = 5;
	    int var2 = 7;
	}
	
	namespace con_decimales  {
	    float var1 = 5.14;
	    float var2 = 7.13;
	}
	
	int main()  {
	    {
	    using namespace enteros;
	    cout << var1 << endl;
	    }

	    {
	    using namespace con_decimales;
	    cout << var1 << endl;
	    }

	    return 0;
	}

.. ..

 <!---  
 Publica:    5		5.14
 --->



Ejercicio 1:
============

- Instalar Qt. Lo cual incluye las herramientas de compilación C++, la biblioteca Qt y Qt Creator.
- Crear un primer programa que muestre por la consola de QtCreator 10 números aleatorios en el intervalo [ 2, 20 ]
- Cada vez que se ejecute el programa, los números deberán ser aleatorios.


Ejercicio 2:
============

- Explicar qué se entiende y para qué sirven: biblioteca, librería, library y archivos dll.
- Para qué sirve la variable de entorno PATH

Ejercicio 3:
============

- Elija un nombre para su propio espacio de nombres
- La biblioteca estándar de C++ se llama ``std``, la biblioteca OpenCV para visión artificial se llama ``cv``, un grupo de desarrollo de realidad aumentada de la Universidad de Córdoba de España le puso como nombre ``aruco``. 
- El espacio de nombres del profesor de esta asignatura es ``osi``
- Luego de elegido el nombre para su namespace, defina una función dentro de ese namespace
- Esta función devolverá un único número que será aleatorio y estará dentro del intervalo indicado en los dos párámetros de la función. Por ejemplo:

.. code-block:: c

	int generarNumero( int limiteInferior, int limiteSuperior );

- Utilice esta función para generar 10 números y que sean publicados en consola


