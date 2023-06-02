.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 18 - POO 2023
===================
(Fecha: 2 de junio)

Registro en video de algunos temas de la clase de hoy
=====================================================

`Enumeraciones - https://youtu.be/pD5sbMKiGSM <https://youtu.be/pD5sbMKiGSM>`_ 

`QTimer - https://youtu.be/3flYMoF0mNU <https://youtu.be/3flYMoF0mNU>`_ 

`logs y QTimer 2021 <https://youtu.be/Rh_NYJ42-Zw>`_ 

`Manager 2022 - https://youtu.be/smkrsoyeB68 <https://youtu.be/smkrsoyeB68>`_ 



Enumeraciones
=============

- Es un tipo especial de variable
- Sus valores son constantes enteras
- Estos valores pueden ser autogenerados (0, 1, 2, 3, ...)

.. code-block:: c	

	enum los_dias { DOM, LUN, MAR, MIE, JUE, VIE, SAB } dia;

	enum los_dias { DOM = 7, LUN = 1, MAR, MIE, JUE = 0, VIE, SAB };

- Las variables de este tipo pueden adoptar sólo valores DOM, LUN, ...
- Es decir, la variable "dia" puede tomar DOM o LUN o MAR ...
- Las enumeraciones declaradas dentro de una clase tiene la visibilidad de la clase

.. code-block:: c	

	class Dia  {
	public:
	    enum los_dias { LUN, MAR, MIE, JUE, VIE };
	    int un_dia;
	};

	int main( int argc, char ** argv )  {
	    Dia d1;
	    d1.un_dia = Dia::LUN;
	}


**Ejemplo**

.. code-block:: c	

	// figura.h
	class Figura : public QWidget  {
	    Q_OBJECT

	public:
	    enum Forma { CIRCULO, CUADRADO };

	    Figura( QWidget * parent = 0 );

	    void dibujar( Forma forma );

	protected:
	    void paintEvent( QPaintEvent * );

	private:
	    Forma forma;
	};


	// figura.cpp
	Figura::Figura( QWidget * parent ) : QWidget( parent ), forma( CIRCULO )  {  }

	void Figura::dibujar( Forma forma )  {
	    this->forma = forma;
	    this->repaint();
	}

	void Figura::paintEvent( QPaintEvent * )  {
	    QPainter pincel( this );
	    
	    switch( forma )  {
	    case CIRCULO:
	        // dibujar circulo
	        break;

	    case CUADRADO:
	        // dibujar cuadrado
	        break;

	    default:;
	    }
	}

	// main.cpp
	int main( int argc, char ** argv )  {
	    QApplication a( argc, argv );

	    Figura figura;
	    figura.dibujar( Figura::CUADRADO );
	    figura.show();

	    return a.exec();
	}






Clase QTimer
^^^^^^^^^^^^

- Permite programar tareas de una sola ejecución o tareas repetitivas. 
- Conectamos la señal ``timeout()`` con algún slot.
- Con ``start()`` comenzamos y la señal ``timeout()`` se emitirá al terminar.


**Ejemplo (repetitivo):** Temporizador que cada 1000 mseg llamará a ``slot_update()``


.. code-block:: c

	QTimer * timer = new QTimer( this );
	connect( timer, SIGNAL( timeout() ), this, SLOT( slot_update() ) );
	timer->start( 1000 );
 

**Para una sola ejecución**

- Para temporizador de una sola ejecución usar ``setSingleShot(true)``
- El método estático ``QTimer::singleShot()`` nos permite la ejecución.


**Ejemplo:** Luego de 200 mseg se llamará a ``slot_update()``:


.. code-block:: c

	QTimer::singleShot( 200, this, SLOT( slot_update() ) );
	// donde this es el objeto que tiene definido el slot_update().
	

Uso de una clase propia con QtDesigner
======================================

- Deben heredar de algún QWidget
- Colocamos el widget (clase base) con QtDesigner
- Clic derecho "Promote to"

.. figure:: imagenes/qtdesigner.png
					 
- Base class name: QLabel
- Promoted class name: MiLabel
- Header file: miLabel.h
- Add (y con esto queda disponible para promover)
- La clase MiLabel deberá heredar de QLabel
- El constructor debe tener como parámetro:


.. code-block::

	MiLabel( QWidget * parent = 0 );  // Esto en miLabel.h

	MiLabel::MiLabel( QWidget * parent ) : QLabel( parent )  {  // Esto en miLabel.cpp
	
	}



Clase Manager
=============

- Encargada de administrar las conexiones principales y la visualización de todas las ventanas de la aplicación




Ejercicio 28
============

- Usar QtDesigner
- Definir la clase Ventana que herede de QWidget
- Buscar una imagen de un fútbol con formato PNG (para usar transparencias).
- Ventana tendrá un formulario que pide al usuario:
	- Diámetro del fútbol (píxeles):
	- Velocidad (mseg para ir de lado a lado):
	- QPushButton para actualizar el estado.
- El fútbol irá golpeando de izquierda a derecha en Ventana.


Ejercicio 29
============
 
- Crear un proyecto Qt Widget Application con un QWidget que sea la clase Ventana
- Crear una clase Boton que hereda de QWidget
- Redefinir paintEvent en Boton y usar fillRect para dibujarlo de algún color
- Definir el siguiente método en Boton:

.. code-block:: c

	Boton * boton = new Boton;
	boton->colorear( Boton::Azul );

	// Este método recibe como parámetro una enumeración que puede ser:
	// Boton::Azul  Boton::Verde  Boton::Magenta

- Usar QtDesigner para Ventana y Boton. Es decir, Designer Form Class
- Definir la enumeración en Boton
- Abrir el designer de Ventana y agregar 5 botones (objetos de la clase Boton). Promocionarlos
- Que esta Ventana con botones quede lo más parecido a la siguiente imagen:

.. figure:: imagenes/botones.png

- Usar para Ventana grid layout, usar espaciadores y usar todos los recursos posibles del QtDesigner
- Dibujar un fondo agradable con paintEvent y drawImage
- Que Boton tenga la señal signal_clic()



Ejercicio 30
============

- Definir dos QWidgets (una clase Login y una clase Ventana).
- El Login validará al usuario contra una base SQLite
- La Ventana sólo mostrará un QPushButton para "Volver" al login.
- Crear solamente un objeto de Ventana y uno solo de Login.
- Analizar el problema que sucede con la compilación (respetar el enunciado).
- Solucionar ese problema y ver la alternativa de hacerlo con Manager.



Ejercicio 31
============

- Crear una clase base llamada Instrumento y las clases derivadas Guitarra, Bateria y Teclado.  
- La clase base tiene una función virtual pura llamada ``sonar()``. 
- Defina una función virtual ``verlo()`` que publique la marca del instrumento. Por defecto todos los instrumentos son de la marca Yamaha. 
- Utilice en la función ``main()`` un ``std::vector`` para almacenar punteros a objetos del tipo Instrumento. Instancie 5 objetos y agréguelos al ``std::vector``.
- Publique la marca de cada instrumento recorriendo el vector.
- En las clases derivadas agregue los datos miembro "``int cuerdas``", "``int teclas``" e "``int tambores``" según corresponda. Por defecto, guitarra con 6 cuerdas, teclado con 61 teclas y batería con 5 tambores.
- Haga que la clase ``Teclado`` tenga herencia múltiple, heredando además de una nueva clase ``Electrico``. Todos los equipos del tipo "``Electrico``" tienen por defecto un voltaje de 220 volts. Esta clase deberá tener un destructor que al destruirse publique la leyenda "Desenchufado".
- Al llamar a la función ``sonar()``, se deberá publicar "Guitarra suena...", "Teclado suena..." o "Batería suena..." según corresponda.
- Incluya los métodos ``get`` y ``set`` que crea convenientes.
