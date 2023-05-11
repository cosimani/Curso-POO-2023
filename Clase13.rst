.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 13 - POO 2023
===================
(Fecha: 6 de mayo)


Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`webservice network QIODevice QUrl 2021 <https://youtu.be/gX-DEWwXvh4>`_

`QNetworkAccessManager imagen de internet 2021 <https://youtu.be/JtENM7t2zxE>`_



Web Service
^^^^^^^^^^^

- Para intercambiar datos entre aplicaciones
- Generalmente a través del protocolo HTTP
- La info puede viajar en XML, JSON, etc.
- Fomenta y facilita el uso y desarrollo de APIs Web
- https://es.wikipedia.org/wiki/Servicio_web

**Algunas APIs disponibles**

- Twitter - https://dev.twitter.com
- Facebook - https://developers.facebook.com
- Amazon - https://developer.amazonservices.es
- Spotify - https://developer.spotify.com/web-api
- MercadoLibre - http://developers.mercadolibre.com
- Google - https://developers.google.com
	- Youtube
	- Traductor
	- Google+
	- Maps
	- Street View

QUrl
^^^^

- Para manipular una url ingresada por el usuario 

.. code-block:: c
	
	// URL ejemplo: http://www.yahoo.com.ar/documento/info.html
		
	// El método path() devuelve /documento/info.html
	// El método host() devuelve www.yahoo.com.ar
	
	QUrl url( "http://www.yahoo.com.ar/documento/info.html" );
	qDebug() << url.host();
	qDebug() << url.path();




QByteArray
^^^^^^^^^^

- Se podría decir que es administrador de un char*
- Se puede usar el operador []
- Almacena \\000 al final de cada objeto QByteArray




Clase QNetworkAccessManager
^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Permite enviar y recibir solicitudes a la red
- Se obtiene un objeto ``QNetworkReply`` con toda la información recibida

.. code-block:: c

	QNetworkAccessManager * manager = new QNetworkAccessManager;

	connect( manager, SIGNAL( finished( QNetworkReply * ) ), this, SLOT( slot_respuesta( QNetworkReply * ) ) );

	manager->get( QNetworkRequest( QUrl( http://mi.ubp.edu.ar" ) ) );

- Para poder utilizar las clases de network hay que agregar en el .pro

.. code-block:: c

	QT += network  // Esto agrega al proyecto el módulo network

- Por defecto, el módulo 'gui' y el módulo 'core' están incluidos.
- Para utilizar HTTPS, Qt utiliza OpenSSL https://www.openssl.org/source
	- Se puede descargar desde https://slproweb.com/products/Win32OpenSSL.html
	- Por ejemplo, para 64 bits elegir `Win64 OpenSSL v1.1.1g <https://slproweb.com/download/Win64OpenSSL-1_1_1g.exe>`_

Clase QIODevice
^^^^^^^^^^^^^^^

.. figure:: imagenes/qiodevice.png 

- Clase base de los dispositivos de I/O
- Algunos métodos:

.. code-block:: c

	QByteArray readAll()  		   // Lee todos los datos disponibles.
	QByteArray read( qint64 max )  // Lee hasta max datos disponibles.
	QByteArray readLine()  		   // Lee una linea.


		
Clase QNetworkReply
^^^^^^^^^^^^^^^^^^^

- Contiene los datos y encabezado de una respuesta
- Una vez leídos los datos, ya no quedarán disponibles.
- Para controlar los bytes que se van descargando usar la señal:

.. code-block:: c

	void downloadProgress( qint64 bytesRecibidos, qint64 bytesTotal )


Clase QNetworkRequest
^^^^^^^^^^^^^^^^^^^^^

- Contiene la información que se envían en la petición
- Seteamos algún campo de la cabecera con:

.. code-block:: c

	void setRawHeader( const QByteArray &nombre, const QByteArray & valor )

	QNetworkRequest request;
	request.setUrl( QUrl( ui->le->text() ) );
	request.setRawHeader( "User-Agent", "MiNavegador 1.0" );


Clase QNetworkProxyFactory
^^^^^^^^^^^^^^^^^^^^^^^^^^

- Permite configurar un servidor proxy a nuestra aplicación Qt.
- Lo siguiente utiliza la configuración del sistema (Chrome y IE, no Firefox).

.. code-block:: c

	#include <QApplication>
	#include "principal.h"
	#include <QNetworkProxyFactory>

	int main( int argc, char ** argv )  {
	    QApplication a( argc, argv );

	    QNetworkProxyFactory::setUseSystemConfiguration( true );

	    Principal w;
	    w.showMaximized();

	    return a.exec();
	}




Algunas particularidades de QNetworkReply y QNetworkRequest
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Para controlar los bytes que se van descargando se puede usar la señal de ``QNetworkReply``:

.. code-block:: c

	void downloadProgress( qint64 bytesRecibidos, qint64 bytesTotal )

- Los campos de la cabecera HTTP se pueden setear con el método de ``QNetworkRequest``:

.. code-block:: c

	void setRawHeader( const QByteArray & nombre, const QByteArray & valor )

	QNetworkRequest request;
	request.setUrl( QUrl( this->le->text() ) );
	request.setRawHeader( "User-Agent", "MiNavegador 1.0" );



Obtener una imagen desde internet
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	void Principal::slot_descargaFinalizada( QNetworkReply * reply )  {
	    QImage image = QImage::fromData( reply->readAll() );
	}



Ejercicio 21
============

- Readaptar el Ejercicio 19, para que la imagen centrada sea una que se descargue de internet.



Entrega Nro. 3 (para el 18 y/o 19 de mayo)
==========================================

- Es continuación de la entrega nro. 2
- Publicar en la ventana de Login, la temperatura actual en la Ciudad de Córdoba.
- Cuando un usuario se loguee con éxito, en lugar de mostrar la ventana realizado en la Entrega Nro. 2, que se muestre una ventana que tenga un QLineEdit que permita ingresar el nombre de un producto que se desee comprar. Esto consultará a MercadoLibre y traerá los 5 resultados más económicos.
- Utilizar los recursos que crea necesario para lograr una agradable visualización de estos 5 resultados.
- Luego, cuando el usuario cierre la aplicación, esta búsqueda deberá quedar almacenada. Entonces, la próxima vez que ingrese deberá mostrarle nuevamente los 5 resultados más económicos. Estos resultados deberán ser consultados nuevamente a MercadoLibre, es decir, deberán estar con los precios actualizados.



