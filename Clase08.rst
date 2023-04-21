.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 08 - POO 2023
===================
(Fecha: 21 de abril)


Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`Dibujar a mano - QByteArray - Preprocesador 2021 <https://www.youtube.com/watch?v=8Gu5_ejipus>`_



QLineEdit
^^^^^^^^^

.. code-block:: c

	QLineEdit * le = new QLineEdit;
	le->setEchoMode( QLineEdit::Password );
	le->setEnabled( false );

	// QLineEdit::Normal  // Se visualizan al escribir
	// QLineEdit::NoEcho  // No se visualiza nada
	// QLineEdit::Password  // Se escribe como asteriscos
	// QLineEdit::PasswordEchoOnEdit  // Se escribe normal y al dejar de editar se convierten en asteriscos

**Señales**

.. code-block:: c

	// void returnPressed()  // Detecta cuando el usuario presiona Enter.

	// void editingFinished()  // Cuando pierde foco.

	// void textChanged( const QString & text )  // Texto modificado por código o por usuario desde la gui.

	// void textEdited( const QString & text )  // Sólo por el usuario.



Dibujar a mano sobre un QWidget
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	// mapa.h
	#include <QWidget>

	class Mapa : public QWidget  {
	    Q_OBJECT

	public:
	    Mapa()  {  }

	protected:
	    void paintEvent( QPaintEvent * );

	};

	// mapa.cpp
	#include "mapa.h"
	#include <QPainter>

	void Mapa::paintEvent( QPaintEvent * )  {
	    QPainter painter( this );
	    painter.drawLine( 0, 0, this->width(), this->height() );
	}

**Clase QPainter**

- Pinta a bajo nivel sobre widgets.
- Debe ser utilizado dentro del método ``paintEvent( QPaintEvent * )``.

.. code-block:: c

	void drawEllipse( int x, int y, int ancho, int alto );
	void drawImage( int x, int y, QImage & image );
	void drawLine( int x1, int y1, int x2, int y2 );
	void drawText( int x, int y, QString & text );
	void fillRect( int x, int y, int ancho, int alto );



¿Cómo entregar proyectos de Qt?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Luego de finalizar el desarrollo del programa, cerrar el proyecto de QtCreator.
- Eliminar el archivo .pro.user
- Comprimir la carpeta donde está el código fuente, no así la carpeta build- .


Ejercicio 13
============

- Utilizar un login diseñado anteriormente.
- Definir la clase Formulario que será un QWidget
- Formulario tendrá QLabels y QLineEdits para Legajo, Nombre y Apellido y un QPushButton
- Si la clave ingresada es admin:1111, se cierra Login y se muestra Formulario

Ejercicio 14
============

.. figure:: imagenes/ejercicio_captcha.jpg

Ejercicio 15
============

- Tener disponible un web server con PHP, MySQL y phpmyadmin
- Diseñar una landing page personal, como estos ejemplos: `Ejemplo 1 <https://kawsar.design/>`_ o `Ejemplo 2 <https://alextass.com/>`_
- Buscar también ejemplos en: `https://dribbble.com/tags/personal_landing_page <https://dribbble.com/tags/personal_landing_page>`_ 
- Página para descargar íconos: `https://www.flaticon.es <https://www.flaticon.es/>`_
	







