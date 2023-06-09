.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 20 - POO 2023
===================
(Fecha: 9 de junio)


Registro en video de algunos temas de la clase de hoy
=====================================================

`Herencia múltiple 2022 <https://youtu.be/67hIhqDpaGo>`_ 

`Herencia múltiple 2021 <https://youtu.be/N-oMfFPVrLs>`_ 

`inline 2021 <https://youtu.be/HbI7Dws-sYg>`_

`friend 2021 <https://youtu.be/zGcQ5n6vhrQ>`_



Herencia múltiple
^^^^^^^^^^^^^^^^^

- La clase derivada hereda todos los datos y funciones de todas las clases base
- Puede suceder que en la clases base existan funciones con igual nombre
- Los casos de ambigüedad se solucionan con el nombre completo
- Otra solución sería redefinir en la derivada la función ambigua.

.. code-block:: c	

	#include <QApplication>
	#include <QDebug>

	class ClaseA  {
	public:
	    ClaseA( int a ) : valorA( a )  {  }
	    int verValor()  {  return valorA;  }

	protected:
	    int valorA;
	};

.. code-block:: c	

	class ClaseB  {
	public:
	    ClaseB() : valorB( 20 )  {  }
	    int verValor()  {  return valorB;  }

	protected:
	    int valorB;
	};

.. code-block:: c	

	class ClaseC : public ClaseA, public ClaseB  {
	public:
	    ClaseC( int c ) : ClaseA( c ), ClaseB()  {  }
	    int verValor()  {  return ClaseA::verValor();  }
	};

.. code-block:: c	

	int main( int argc, char ** argv )  {
	    QApplication a( argc, argv );

	    ClaseC c( 10 );
	    qDebug() << c.verValor();  
	    qDebug() << c.ClaseB::verValor();  

	    return 0;
	}


**Ejemplo**

.. code-block:: c	

	class Persona  {
	private:
	    int edad;
	    int x, y;

	public:
	    Persona( int edad = 0 ) : edad( edad ), x( 0 ), y( 0 )  {  }

	    void move( int x, int y )  {
	        this->x = x;
	        this->y = y;
	    }
	};

	class Jugador : public Persona, public QWidget  {
	private:
	    int id;

	public:
	    Jugador() : Persona( 18 ), QWidget(), id( 0 )  {  }

	    void mudarse( int x, int y )  {
	        this->id++;
	        this->Persona::move( x, y );  // Se requiere especificar de esta manera
	    }
	};
	    


Funciones inline
================

- Cuando decimos que llamamos a una función es porque salta, ejecuta y retorna.
- Una función inline inserta su código.
- Ventaja de ejecutarse más rápidamente.
- Como desventaja tenemos un programa generado más extenso.

.. code-block:: c

	#include <QDebug>
	#include <QApplication>

	inline int calculo( int a, int b )  {
	    return a/2+b;
	}

	int main( int argc, char ** argv )  {
	    QApplication a( argc, argv );

	    int x=2, y=3, z=0;
	    z = calculo( x, y );

	    return 0;
	}

**Funciones miembro inline dentro de clases**

- Un método se declara dentro del cuerpo de la clase y se puede definir dentro o fuera
- Si se declara y define dentro, se denomina función inline. En este caso, no hace falta indicar con inline (está implícito).
- Si se define fuera, deberá indicar inline. De lo contrario será offline.
- Se recomienda usar funciones inline para funciones pequeñas y de uso frecuente.

.. code-block:: c

	#include <QDebug>
	#include <QApplication>

	class ClaseA  {
	private:
	    int x;
	    int y;

	public:
	    ClaseA() : x( 10 ), y( 20 )  {  }
	    int getX()  {  return x;  }     // inline implícito
	    int getY();
	};

	inline int ClaseA::getY()  {
	    return y;
	}

	int main( int argc, char ** argv )  {
	    QApplication a( argc, argv );

	    ClaseA cA;
	    qDebug() << cA.getX();
	    qDebug() << cA.getY();

	    return 0;
	}
	

Declaraciones friend
====================

- Miembros privados no son accesibles para funciones y clases externas
- Podemos usar friend en caso de necesitar acceder
- Se pueden aplicar a clases o métodos
- Inhabilitan el sistema de protección (protected o private)
- La amistad no es transferible

.. code-block:: c
	
	A es amigo de B     B amigo de C     No por eso A es amigo de C

- No se hereda

.. code-block:: c

	A amigo de B     C derivada de B     No por eso A es amigo de C

- No simétrica

.. code-block:: c

	A amigo de B     No por eso B es amigo de A

**Funciones amigas**

.. code-block:: c

	#include <iostream>
	using namespace std;

	class ClaseA  {
	public:
	    ClaseA( int i ) : a( i )  {  }
	    void verA()  {  cout << a << endl;  }

	protected:
	    int a;
	    friend void mostrarA( ClaseA );  // mostrarA es amiga de ClaseA
	};

	void mostrarA( ClaseA cA )  {  // Esta función no pertenece a ClaseA
	    cout << cA.a << endl;      // Pero al ser amiga puede acceder a 'a'
	}

	int main( int argc, char ** argv )  {
	    ClaseA objetoA( 10 );
	    mostrarA( objetoA );
	    objetoA.verA();

	    return 0;
	}
 
**Función amiga en otra clase**

.. code-block:: c

	#include <iostream>
	using namespace std;

	class ClaseA;	// Declaración

	class ClaseB  {
	public:
	    ClaseB( int i ) : b( i )  {  }
		
	    void ver()  {  cout << b << endl;  }
		
	    bool esMayor( ClaseA cA )  {  // Compara
	        return b > cA.a;
	    }
		
	private:
	    int b;
	};

	class ClaseA  {
	public:
	    ClaseA( int i ) : a( i )  {  }
	    void ver()  {  cout << a << endl;  }

	private:
	    friend bool ClaseB::esMayor( ClaseA );
	    int a;
	};

	int main( int argc, char ** argv )  {
	    ClaseA objetoA( 10 );
	    ClaseB objetoB( 2 );

	    objetoA.ver();	
	    objetoB.ver();

	    if ( objetoB.esMayor( objetoA ) )
	        cout << "objetoB > objetoA" << endl;
	    else
	        cout << "objetoB < objetoA" << endl;

	    return 0;
	}
	

Entrega Nro. 5 (última entrega)
===============================

- Es continuación de las entregas anteriores
- Para equipos de **2 estudiantes**, agregar lo que se indica en la sección Moodle.
- Para equipos de **3 estudiantes**, además de agregar la sección Moodle, agregar el parser.
- Las rúbricas de evaluación fueron publicadas en la `Clase 01 - POO 2023 <https://github.com/cosimani/Curso-POO-2023/blob/main/Clase01.rst>`_
- Son estas: `Rública Proyecto individual <https://docs.google.com/spreadsheets/d/1VZ3W91dbWRvWtav-Dr_NQjoCbTZx4DoiQCf9GN6OJX8/edit?usp=share_link>`_ y `Rúbrica Proyecto grupal <https://docs.google.com/spreadsheets/d/1hIZHseh0gT1SujRvPCBrctL8YzdA9tgLtqfP3rcKYeo/edit?usp=share_link>`_ 




