.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 19 - POO 2023
===================
(Fecha: 8 de junio)


Registro en video de algunos temas de la clase de hoy
=====================================================

`const 2021 <https://youtu.be/UqXE4GeFd_s>`_ 

`QFile 2021 <https://youtu.be/Zf-yAkNmqso>`_ 


const
=====

- Una variable definida como const no podrá ser modificada a lo largo del programa (se crea como sólo lectura)
- Se puede aplicar a cualquier tipo:

.. code-block:: c	

	const float pi = 3.14;
	const peso = 67;  // Si no se indica el tipo entonces es int
	                  // Aunque sólo en compiladores viejos



const con punteros
^^^^^^^^^^^^^^^^^^

.. code-block:: c	

	int x = 10;
	int * px = &x;  // normal

	const int y = 10;
	int * py = &y;  // El compilador dirá: "invalid conversion from const int*
	               // to int*". La inversa sí se permite

	int y = 10;
	const int * py = &y;  // permitido (pero el contenido es de sólo lectura)

	*py = 6;  // No permitido. El contenido apuntado es de sólo lectura


const en parámetros de funciones
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Cuando los parámetros son punteros, decimos que no podrá modificar los objetos referenciados

.. code-block:: c	

	int funcion( const char * ch )


- Lo mismo sucede con referencias

.. code-block:: c	

	int funcion( const char& ch )


const en clases
^^^^^^^^^^^^^^^

.. code-block:: c	

	class ClaseA  {
	    const int i;
	    int x;

	public:
	    int funcion( ClaseA cA, const ClaseA &c )  {
	        cA.x = 1;
	        cA.i = 2;  // No compila. i es de sólo lectura.
	        c.x = 3;   // No compila. El objeto c es de sólo lectura.

	        return cA.x;
	    }
	}; 


.. code-block:: c	

	// A la variable i sólo la puede inicializar el constructor y sólo con la forma:
	ClaseA() : i( 8 )  {  }   

	// Si en el cuerpo del constructor se hace:
	ClaseA()  { 
	    i = 8;  // Compila? i es de solo lectura o no
	}   


- Aplicado a métodos de una clase no permite modificar ninguna propiedad de la clase

.. code-block:: c	

	class ClaseB  {
	    int x;

	    void funcion( int i ) const  {
	        x = x + i;  // Compila?
	    }
	};


Clase QFile
^^^^^^^^^^^

- Permite leer y escribir en archivos. 
- Puede ser utilizado además con ``QTextStream`` o ``QDataStream``.

.. code-block:: c	

	QFile( const QString & name )
	viod setFile( const QString & name )

- Existe un archivo? y lo eliminamos.

.. code-block:: c	

	bool exists() const
	bool remove()

- Lectura de un archivo línea por línea:

.. code-block:: c	

	QFile file( "c:/in.txt" );
	if ( !file.open ( QIODevice::ReadOnly | QIODevice::Text ) )
	    return;

	while ( !file.atEnd() )  {
	    QByteArray linea = file.readLine();
	    qDebug() << linea;
	}



Clase QFileDialog
=================

- Permite abrir un cuadro de diálogo para buscar un archivo en disco

.. code-block:: c	

	QString file = QFileDialog::getOpenFileName( this, "Abrir", "./", "Imagen (*.png *.jpg)" );


Ejercicio 32
============

- Elegir un archivo de imagen del disco con ``QFileDialog`` y dibujar dos copias de esta imagen en un ``QWidget``.
- Deberá quedar como la siguiente figura:

.. figure:: imagenes/dos_imagenes.png  
 
- Al hacer click sobre una de estas dos imágenes, se deberá ocultar la imagen sobre la que se hizo click. 
- Cuando se hace click sobre la que quedó visible, se deberá hacerla rotar sobre su centro y que quede girando indefinidemente.


Ejercicio 33
============

- Crear un **parser** que pueda analizar cualquier html en busca de todas las URLs que encuentre
- Crear una GUI que permita al usuario ingresar un sitio web en un QLineEdit
- Que descargue en archivos todos los recursos de dicho sitio web
- Es decir, que busque en el html las imágenes, los css, los javascript y los descargue en archivos
- Que le permita al usuario indicar en qué directorio descargar los archivos


Entrega Nro. 5 (última entrega)
===============================

- Es continuación de las entregas anteriores
- Para equipos de **2 estudiantes**, agregar lo que se indica en la sección Moodle.
- Para equipos de **3 estudiantes**, además de agregar la sección Moodle, agregar el parser.
- Las rúbricas de evaluación fueron publicadas en la `Clase 01 - POO 2023 <https://github.com/cosimani/Curso-POO-2023/blob/main/Clase01.rst>`_
- Son estas: `Rública Proyecto individual <https://docs.google.com/spreadsheets/d/1VZ3W91dbWRvWtav-Dr_NQjoCbTZx4DoiQCf9GN6OJX8/edit?usp=share_link>`_ y `Rúbrica Proyecto grupal <https://docs.google.com/spreadsheets/d/1hIZHseh0gT1SujRvPCBrctL8YzdA9tgLtqfP3rcKYeo/edit?usp=share_link>`_ 



Moodle
======

- Incorporar a la base de datos en la API propia, la información del mail del usuario.
- Cuando un usuario se valide en la aplicación Qt, deberá mostrar la foto de perfil del usuario
- Esta foto de perfil está en la información de la cuenta de usuario en Moodle
- Esta foto de perfil se consulta con la siguiente URL:

https://campusvirtual.learningway.com.ar/webservice/rest/server.php?wstoken=aqui_va_el_token&wsfunction=core_user_get_users&moodlewsrestformat=json&criteria[0][key]=email&criteria[0][value]=cesarosimani@gmail.com

- Solicitar el token vía whatsapp


Ayuda para API de MercadoLibre
==============================

`API Mercado Libre. Crear aplicación, obtener token, peticiones usando Postman <https://www.youtube.com/watch?v=lvPAGzUFacE>`_ 




