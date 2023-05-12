.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 14 - POO 2023
===================
(Fecha: 12 de mayo)


Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`Derivadas - Constructor explícito 2021 <https://www.youtube.com/watch?v=O2mCsBB_gro>`_



Clases derivadas 
^^^^^^^^^^^^^^^^

.. code-block:: c
 
	// personal.h
	#include <QString>

	class Personal  {
	public:
	    QString verEdad()  {  return "Edad: " + QString::number( edad );  }
	    QString verSalario()  {  return "Salario: " + QString::number( salario );  }

	protected:  // Para acceso desde las clases derivadas
	    int edad;
	    int salario;
	};

	// Modificadores de acceso para Herencia:
	//    public  ->  Mantiene los modificadores de acceso de la clase base
	//    private ->  Pasa todo a privado
	class Desarrollador : public Personal  {
	public:
	    Desarrollador( int edad )  {
	    salario = 2000;
	    this->edad = edad;
	}

	// Se podrá usar? 
	Desarrollador( int edad ) : salario( 2000 ), edad( edad )  {  }
	    // No. Sólo para miembros de la propia clase (no para heredados).
	};

	class Administrador : public Personal  {
	public:
	    Administrador()  {
	        salario = 2000;
	        edad = 30;
	    }
	};

	#include <QApplication>
	#include "personal.h"
	#include <QDebug>

	int main( int argc, char ** argv )  {
	    QApplication a( argc, argv );

	    Desarrollador juan( 20 );
	    Administrador marcos;

	    qDebug() << juan.verEdad();
	    qDebug() << juan.verSalario();

	    qDebug() << marcos.verEdad();
	    qDebug() << marcos.verSalario();

	    return a.exec();
	}

Constructor de la clase derivada
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	class Persona  {
	public:
	    Persona( int edad ) : edad( edad )  {  }
	    QString verEdad()  {  return "Edad: " + QString::number( edad );  }
	    void setEdad( int edad )  {  this->edad = edad;  }

	protected:
	    int edad;
	};

	class Empleado : public Persona  {
	public:
	    // Siempre primero se llama al constructor de la clase base
	    Empleado( int edad, int salario ) : Persona( edad ), salario( salario )  {  }
	    QString verSalario()  {  return "Salario: " + QString::number( salario );  }

	protected:
	    int salario;
	};

	#include <QApplication>
	#include "personal.h"
	#include <QDebug>

	int main( int argc, char ** argv )  {
	    QApplication a( argc, argv );

	    Persona carlos( 24 );
	    Empleado ale( 20, 2500 );

	    qDebug() << carlos.verEdad();
	    //    qDebug() << carlos.verSalario();  // No compila. No está en la clase base.

	    qDebug() << ale.verEdad();
	    qDebug() << ale.verSalario();

	    return a.exec();
	}



Destructor de la clase derivada
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	class ClaseA  {
	public:
	    ClaseA() : datoA(10)  {  qDebug() << "Constructor A";  }
	    ~ClaseA()  {  qDebug() << "Destructor A";  }
	    int verA()  {  return datoA;  }

	protected:
	    int datoA;
	};

	class ClaseB : public ClaseA  {
	public:
	    ClaseB() : datoB( 20 )  {  qDebug() << "Constructor B";  }
	    ~ClaseB()  {  qDebug() << "Destructor B";  }
	    int verB()  {  return datoB;  }

	protected:
	    int datoB;
	};

	#include <QApplication>
	#include "personal.h"
	#include <QDebug>

	int main( int argc, char ** argv )  {
	    QApplication a( argc, argv );

	    {
	    ClaseB objeto;
	    qDebug() << "a=" << objeto.verA() << ", b=" << objeto.verB();
	    }

	    return a.exec();
	}

	// Publica
	Constructor A
	Constructor B
	a=10, b=20
	Destructor B
	Destructor A



Constructor explícito
^^^^^^^^^^^^^^^^^^^^^

- En el siguiente ejemplo tenemos una clase con un constructor no explícito:

.. code-block:: c

	class Persona  {
	private:
	    int edad;

	public:
	    Persona( int edad = 0 ) : edad( edad )  {  }

	    int getEdad()  {  return edad;  }
	    void setEdad( int edad )  {  this->edad = edad;  }   
	};

- Lo que permite instanciar objetos de todas las siguientes maneras:

.. code-block:: c

	Persona carlos;
	Persona miguel( 25 );
	Persona * roman = new Persona;
	Persona * juan = new Persona( 18 );

	Persona roberto = 23;

- Llama la atención la última de las maneras. 
- En ese caso, el compilador permite la conversión, ya que se entiende que el programador quiere usar el constructor que recibe un int como parámetro.

- Si deseamos bloquear esta posibilidad, debemos indicar que el constructor sea explícito, de la siguiente manera:

.. code-block:: c

	class Persona  {
	private:
	    int edad;

	public:
	    explicit Persona( int edad = 0 ) : edad( edad )  {  }

	    int getEdad()  {  return edad;  }
	    void setEdad( int edad )  {  this->edad = edad;  }   
	};

- Cuando un constructor no explícito recibe dos variables:

.. code-block:: c

	class Persona  {
	private:
	    int edad;
	    int dni;

	public:
	    Persona( int edad = 0, int dni = 0 ) : edad( edad ), dni( dni )  {  }

	    int getEdad()  {  return edad;  }
	    void setEdad( int edad )  {  this->edad = edad;  }
	    int getDni()  {  return dni;  }
	    void setDni( int dni )  {  this->dni = dni;  }
	};

- Se puede hacer lo siguiente:

.. code-block:: c

	Persona roberto = { 23, 35876543 };

- Y tener en cuenta que también es posible lo siguiente:

.. code-block:: c

	// Cuando el constructor recibe 3 parámetros y de distintos tipos
	Persona( int edad = 0, int dni = 0, QString nombre = "" ) : edad( edad ),
	                                                            dni( dni ), 
	                                                            nombre( nombre )  {  
	}

	// Se puede instanciar un objeto así:
	Persona roberto = { 23, 35876543, "Roberto" };

- A continuación un ejemplo por Carlos Duarte para `Constructor explícito <https://www.youtube.com/watch?v=lsdC3F27lt0>`_



Ejercicio 22
============

- Crear una clase Barra para dar funcionalidad a una barra de progreso
- Que la barra tenga el siguiente aspecto:

.. figure:: imagenes/progressbar.png

- Debe tener métodos para setear su valor en porcentaje
- Usar la señal de ``downloadProgress`` de ``QNetworkReply``
- Crear una interfaz que tenga un ``QLineEdit`` para la URL y una Barra.
- Probarlo con alguna URL que pertenezca a un archivo de tamaño superior a 50MB


Ejercicio 23
============

- Crear la jerarquía de clases en donde la clase Persona sea la clase base.
- Cliente y Administrativo derivan de Persona.
- Oro y Platino heredan de Cliente.
- Coloque las características, atributos y métodos más comunes que deberían tener estas clases.
