.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 09 - POO 2023
===================
(Fecha: 27 de abril)


Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`QGroupBox - QString number 2021 <https://www.youtube.com/watch?v=c7_axxXbphU>`_


`Sutileza con punteros - octal - arrays como parámetros 2021 <https://www.youtube.com/watch?v=XQOBvBVkffM>`_



QGroupBox
^^^^^^^^^ 

.. figure:: imagenes/qgroupbox.png

.. code-block:: c

	QGroupBox * grupo = new QGroupBox( "Texto" );
	QGridLayout * layout = new QGridLayout;
	
	layout->addWidget( label, 0, 0 );
	layout->addWidget( usuario, 1, 0, 1, 2 );
	layout->addWidget( clave, 2, 0, 1, 2 );
	
	grupo->setLayout( layout );



Sutilezas con punteros
^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	char cadena[ 10 ] = "hola";  
	// Funciona? sí. Qué hace con el sobrante?
	// Los completa a todos con \000

	char cadena[ 4 ] = "hola";   // Por qué no compila?

	char cadena[ 5 ] = "hola";   // Y por qué esto sí compila?

	// Porque la última posición se usa para el carácter nulo que el
	// compilador lo agrega (si tiene lugar).

	//    \000  (octal)
	//    \x0   (hexadecimal)    

Usando puntero para cadenas
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	char * cadena = "hola";      // el compilador agrega \000
	char * cadena = "ho\000la";  // Imprime  ho

- Asignamos memoria dinámicamente.
- No necesitamos especificar la longitud máxima.

Notación octal y hexadecimal
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	cout << 3 + 4 + 11;      // Imprime 18
	cout << 3 + 4 + 011;     // ?

	//    octal    hexadecimal    decimal
	//    0121     0x51           81
	//    011      0x9            9
	//    '\000'   '\x0'          nulo
	//    '\063'   '\x33'         carácter 3

Punteros a punteros
^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	char cadena[ 2 ][ 3 ];
	cadena[ 0 ][ 0 ] = 'f';
	cadena[ 0 ][ 1 ] = 'u';
	cadena[ 0 ][ 2 ] = 'e';
	cadena[ 1 ][ 0 ] = 'f';
	cadena[ 1 ][ 1 ] = 'u';
	cadena[ 1 ][ 2 ] = 'i';

	//    Mejor así

	char cadena[ 2 ][ 3 ];
	cadena[ 0 ][ 0 ] = 's';
	cadena[ 0 ][ 1 ] = 'i';
	cadena[ 0 ][ 2 ] = '\000';
	cadena[ 1 ][ 0 ] = 'n';
	cadena[ 1 ][ 1 ] = 'o';
	cadena[ 1 ][ 2 ] = '\000';
 
Array ≡ puntero
^^^^^^^^^^^^^^^

- Cuando declaramos un array
- Estamos declarando un puntero al primer elemento.

.. code-block:: c

	char arreglo[ 5 ];
	char * puntero;
	puntero = arreglo;  // Equivale a puntero = &arreglo[ 0 ];

Volviendo a puntero a puntero
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	char cadena[ 2 ][ 3 ] = { { 's', 'i', '\000' }, { 'n', 'o', '\000' } };
	// Y si fuera char cadena[ 2 ][ 3 ] = { { 's', 'i', '-' }, { 'n', 'o', '\000' } };
	char * p1;
	char * p2;

	p1 = cadena[ 0 ];   // p1 = &cadena[ 0 ][ 0 ];
	p2 = cadena[ 1 ];   // p2 = &cadena[ 1 ][ 0 ];

	cout << p1;  // si  
	cout << p2;  // no
	
	cout << *p1;  // ?
	cout << *p2;  // ?

	// Es decir:
	//    El identificador de un arreglo unidimensional 
	//    es considerado un puntero a su primer elemento.

**Ejemplo**

.. code-block:: c

	char p1[] = { 'a', 'b', 'c', 'd', 'e' };
	cout << "Letra " << *p1;   // Letra a
	cout << "Letra " << p1[ 0 ];   // Letra a

	char m2[][ 5 ] = { { 'a', 'b', 'c', 'd', 'e' }, { 'A', 'B', 'C', 'D', 'E' } };
	cout << "Letra " << **m2;          // Letra a
	cout << "Letra " << m2[ 0 ][ 0 ];      // Letra a
	cout << "Letra " << m2[ 1 ][ 3 ];      // Letra D
	cout << "Letra " << *( *( m2 + 1 ) + 3 );  // Letra D

**Extendiendo a arreglos de cualquier dimensión**

.. code-block:: c

	m[ a ] == *( m + a )
	m[ a ][ b ] == *( *( m + a ) + b )
	m[ a ][ b ][ c ] == *( *( *( m + a ) + b ) + c )

	//    Si nos referimos al primer elemento

	m[ 0 ] == *m
	m[ 0 ][ 0 ] == **m
	m[ 0 ][ 0 ][ 0 ] == ***m


**Array como parámetro en funciones**

.. code-block:: c

	#include <iostream>
	using namespace std;

	void funcion( int miArray[] );
	// Le estamos pasando un puntero al primer elemento del array.

	int main()  {
	    int miA[ 5 ] = { 0, 1, 2, 3, 4 };

	    funcion( miA );

	    cout << miA[ 0 ] << miA[ 1 ] << miA[ 2 ] << miA[ 3 ] << miA[ 4 ];
	}

	void funcion( int miArray[] )  {
	    miArray[ 0 ] = 5;  // Las modificaciones quedarán.

	    miArray[ 3 ] = 5; 
	} 



Parámetros desde la línea de comandos
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Escribir el siguiente programa y ejecutarlo desde la línea de comandos incluyendo parámetros:

.. code-block:: c

	#include <iostream>

	int main( int argc, char ** argv )  {
	    std::cout << "Hay " << argc << " argumentos:" << std::endl;
	    for ( int i = 0 ; i < argc ; ++i ) {
	        std::cout << argv[ i ] << std::endl;
	    }
	}



Ejercicio 15
============

- Tener disponible un web server con PHP, MySQL y phpmyadmin
- Diseñar una landing page personal, como estos ejemplos: `Ejemplo 1 <https://kawsar.design/>`_ o `Ejemplo 2 <https://alextass.com/>`_
- Buscar también ejemplos en: `https://dribbble.com/tags/personal_landing_page <https://dribbble.com/tags/personal_landing_page>`_ 
- Página para descargar íconos: `https://www.flaticon.es <https://www.flaticon.es/>`_
	

Ejercicio 16
============

- Crear en el web server una tabla usuarios con datos personales y credenciales de acceso
- Crear una API para loguear usuarios con el método GET de HTTP
- Que devuelva "denegado" o que devuelva "aceptado::Juan Carlos::Ponce::juncaponce@gmail.com"


Ejercicio 17
============

- Crear un login con un diseño que tenga de fondo una imagen
- Probar que si el usuario cambia el tamaño del login, que la imagen no se deforme


TG 1
====

- Colocar una palabra o frase en un QLineEdit
- En otro QLineEdit colocar el link a un video de Youtube
- Al pulsar un QPushButton que nos diga cuántas veces se dice esa palabra en el video.

TG 2
====

- En un QLineEdit colocar el link a un video de Youtube
- Usar `Embeddings de OpenAI <https://www.youtube.com/watch?v=-XVkdIdli0I>`_ para introducir el texto que se dice en el video
- En un QLineEdit hacerle una pregunta sobre el video


Entrega para el 4 de mayo
=========================

- Hacer el Ejercicio 16
- Crear una cuenta en GitHub para contener el trabajo práctico integrador y compartir el repositorio con el usuario ``cosimani``
- En POO 2023, hay tres equipos ya definidos. En estos tres casos, crear un único repositorio en donde el equipo pueda colaborar.
- Preparar la interfaz de un login de usuarios en Qt y subirlo al repositorio en una carpeta que se llame ``Qt``
- La API para loguear a los usuarios, programarla en PHP y subirlo al repositorio en una carpeta que se llame ``php``