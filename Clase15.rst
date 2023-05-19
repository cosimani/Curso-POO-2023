.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 15 - POO 2023
===================
(Fecha: 18 de mayo)


Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`Polimorfismo función virtual 2021 <https://youtu.be/wT_LfW-Ao0A>`_

`Polimorfismo - QtDesigner y métodos virtuales de QWidget 2023 <https://youtu.be/idc1aCpYUgg>`_






Vista obligatoria
^^^^^^^^^^^^^^^^^

`Funciones virtuales 2023 <https://youtu.be/a5-p12-jscc>`_




Polimorfismo
============

- Lo utilizamos con punteros.
- Nos permite acceder a objetos de la clase derivada usando un puntero a la clase base.
- Sin embargo, sólo podemos acceder a datos y funciones que existan en la clase base.
- Los datos y funciones propias de la derivada quedan inaccesibles.

.. code-block:: c

	class Persona  {
	public:
	    Persona( QString nombre ) : nombre( nombre )  {  }
	    QString verNombre()  {  return "Nombre: " + nombre;  }

	protected:  // Para acceso desde las clases derivadas
	    QString nombre;
	};

	class Empleado : public Persona  {
	public:
	    Empleado( QString nombre ) : Persona( nombre )  {  }
	    QString verNombre()  {  return "Empleado: " + nombre;  }
	    void mostrarAlgo()  {  qDebug() << "Algo";  }
	};

	class Estudiante : public Persona  {
	public:
	    Estudiante( QString nombre ) : Persona( nombre )  {  }
	    QString verNombre()  {  return "Estudiante: " + nombre;  }
	};


	#include <QApplication>
	#include "persona.h"
	#include <QDebug>

	int main( int argc, char** argv )  {
	    QApplication a(argc, argv);

	    {
	    Persona * jose = new Estudiante( "Jose" );
	    Persona * carlos = new Empleado( "Carlos" );

	    qDebug() << carlos->verNombre();
	    qDebug() << jose->verNombre();
	    carlos->mostrarAlgo();  // Muestra algo? 

	    delete jose;
	    delete carlos;
	    }

	    return a.exec();
	}
	


Funciones virtuales
===================

- Puede ser interesante llamar a la función de la derivada (en polimorfismo).
- Al declarar una función como virtual en la clase base, si se superpone en la derivada, al invocar usando el puntero a la clase base, se ejecuta la versión de la derivada.

.. code-block:: c

	class Persona  {
	public:
	    Persona( QString nombre ) : nombre( nombre )  {  }
	    virtual QString verNombre()  {  return "Persona: " + nombre;  }  // Y si no fuera virtual?

	protected:  
	    QString nombre;
	};

	class Empleado : public Persona  {
	public:
	    Empleado( QString nombre ) : Persona( nombre )  {  }
	    QString verNombre()  {  return "Empleado: " + nombre;  }
	};


	#include <QApplication>
	#include "personal.h"
	#include <QDebug>

	int main( int argc, char** argv )  {
	    QApplication a( argc, argv) ;

	    {
	    Persona *carlos = new Empleado( "Carlos" );

	    qDebug() << carlos->verNombre();  // Qué publica?

	    delete carlos;
	    }

	    return a.exec();
	}




Uso de Qt Designer
==================

- Nuevo proyecto -> Qt Widgets Application
- Utilizar el puntero ``ui`` para acceder a los objetos del diseño


**Ejemplo**

.. code-block:: c	
	
	// ventana.h
	#ifndef VENTANA_H
	#define VENTANA_H

	#include <QWidget>

	namespace Ui {
	    class Ventana;
	}

	class Ventana : public QWidget  {
	    Q_OBJECT

	public:
	    explicit Ventana( QWidget * parent = 0 );
	    ~Ventana();

	private:
	    Ui::Ventana *ui;
	};

	#endif // VENTANA_H

.. code-block:: c

	// ventana.cpp
	#include "ventana.h"
	#include "ui_ventana.h"

	Ventana::Ventana( QWidget * parent ) : QWidget( parent ), ui( new Ui::Ventana )  {
	    ui->setupUi( this );
	}

	Ventana::~Ventana()  {
	    delete ui;
	}


Métodos virtuales de QWidget para capturar eventos
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Estos métodos pueden ser reimplementados en una clase derivada para recibir los eventos.

.. code-block:: c

	virtual void mouseDoubleClickEvent( QMouseEvent * event );
	virtual void mouseMoveEvent( QMouseEvent * event );
	virtual void mousePressEvent( QMouseEvent * event );
	virtual void mouseReleaseEvent( QMouseEvent * event );
	virtual void keyPressEvent( QKeyEvent * event );
	virtual void keyReleaseEvent( QKeyEvent * event );
	virtual void resizeEvent( QResizeEvent * event );
	virtual void moveEvent( QMoveEvent * event );
	virtual void closeEvent( QCloseEvent * event );
	virtual void hideEvent( QHideEvent * event );
	virtual void showEvent( QShowEvent * event );
	virtual void paintEvent( QPaintEvent * event );



Entrega Nro. 4 (para el 1 y/o 2 de junio)
==========================================

- Es continuación de la entrega nro. 3
- Agregar un checkbox que agregue la funcionalidad de Recordarme. Con esta opción tildada, se deberá almacenar el usuario y clave en una base de datos local en SQLite. Cuando un usuario coloque su nombre de usuario, al salir de foco del QLineEdit del usuario, deberá completar automáticamente su contraseña, siempre y cuando, en un inicio de sesión anterior haya tildado el checkbox de Recordarme.
- Registrarse en el Moodle que se pasó en clases. Crear un usuario ahí, con su mail y completar correctamente sus datos. Importante subir una foto de perfil correcta.
- Agregar la funcionalidad en su aplicación Qt para registrar nuevos usuarios. En el momento de registro de un usuario en la Aplicación de Qt, deberá chequear que no exista un usuario con ese mail en moodle, en caso de existir, que automáticamente se cargue en el formulario de Qt, los datos que ya fueron cargados en el registro de Moodle.

 






