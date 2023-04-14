.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 07 - POO 2023
===================
(Fecha: 14 de abril)

Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`Help signal slot QSlider QSpinBox 2021 <https://www.youtube.com/watch?v=BHog8TPjnos>`_

`Help signal slot QSlider QSpinBox 2021 <https://www.youtube.com/watch?v=BHog8TPjnos>`_

`QGridLayout - Q_OBJECT - Archivos del Qt Project 2021 <https://www.youtube.com/watch?v=KwtBKCs4B1c>`_


Signals y slots
^^^^^^^^^^^^^^^

- signal y slot son funciones.
- Las signals de una clase se comunican con los slots de otra.
- Se deben conectar con la función connect de QObject.
- Un evento puede generar una signal.
- Los slots reciben estas signals.
- SIGNAL() y SLOT() son macros (convierten a cadena).
- emisor y receptor son punteros a QObject


.. code-block:: c

	QObject::connect( emisor, SIGNAL( signal ), receptor, SLOT( slot ) );
	
- Se puede remover la conexión:

.. code-block:: c

	QObject::disconnect( emisor, SIGNAL( signal ), receptor, SLOT( slot ) );

**Ejemplo:** QPushButton para cerrar la aplicación.

.. code-block:: c

	#include <QApplication>
	#include <QPushButton>

	int main( int argc, char** argv )  {
	    QApplication a( argc, argv );
	    QPushButton* boton = new QPushButton( "Salir" );

	    QObject::connect( boton, SIGNAL( pressed() ), &a, SLOT( quit() ) );
	    boton->setVisible( true );
		
	    return a.exec();
	}

Macro Q_OBJECT
^^^^^^^^^^^^^^

- Convierte a una clase cualquiera en una clase Qt.
- Una clase Qt permitirá trabajar con signals y slots.
- Incluir la macro Q_OBJECT en la primer línea de la definición de la clase.

	
**Ejemplo:** Control de volumen

.. code-block:: c

	#include <QApplication>
	#include <QWidget>
	#include <QHBoxLayout>
	#include <QSlider>
	#include <QSpinBox>

	int main( int argc, char** argv )  {
	    QApplication a( argc, argv );

	    QWidget * ventana = new QWidget;  // Es la ventana padre (principal)
	    ventana->setWindowTitle( "Volumen" ); 
	    ventana->resize( 300, 50 );

	    QSpinBox * spinBox = new QSpinBox;
	    QSlider * slider = new QSlider( Qt::Horizontal );
	    spinBox->setRange( 0, 100 );
	    slider->setRange( 0, 100 );

	    QObject::connect( spinBox, SIGNAL( valueChanged( int ) ), slider, SLOT( setValue( int ) ) );
	    QObject::connect( slider, SIGNAL( valueChanged( int ) ),  spinBox, SLOT( setValue( int ) ) );

	    spinBox->setValue( 15 );

	    QHBoxLayout * layout = new QHBoxLayout;
	    layout->addWidget( spinBox );
	    layout->addWidget( slider );
	    ventana->setLayout( layout );
	    ventana->setVisible( true );	

	    return a.exec();
	}
	




Ejercicio 11
============

- Crear una aplicación Qt que inicie con un botón que diga "Mostrar segundo boton y label"
- Al hacer clic sobre este botón se deberá ocultar este botón, se visualizará un nuevo botón y un label
- El segundo botón dirá "Ocultar label y mostrar boton final"
- Al hacer clic en el segundo botón, se ocultará este y el label, para mostrar el último botón
- El último botón dirá "Cerrar aplicacion" y cerrará la aplicación al presionarlo


Ejercicio 12
============

- Teniendo el programa funcionando del entregable 6, modificarlo para que tenga el siguiente comportamiento
- Cuando inicie la aplicación, sólo el botón estará visible
- Al presionar el botón, se deberá visualizar el QLabel, el QWidget y el QLineEdit
- Cuando escribimos dentro del QLineEdit y se presiona Enter, en ese momento se deberá cerrar la aplicación

Ejercicio 13
============

- Punto de partida: Usar el código del ejemplo del control de volumen
- Cuando el valor del QSlider se modifique, colocar como título de la ventana el mismo valor que tiene el QSlider. 

