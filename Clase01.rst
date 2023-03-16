.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 01 - POO 2023
===================
(Fecha: 16 de marzo)


:Autor: César Osimani
:Correo: cesarosimani@gmail.com

:Temas principales: 
		- Espacio de nombres
		- inline y const
		- std, vector, string
		- Aritmética de punteros
		- Funciones genéricas
		- Herencia y herencia múltiple
		- Polimorfismo
		- Funciones virtuales
		- Clases abstractas
		- Modificador friend
		- Biblioteca Qt
			- Uso de documentación
			- slots y signals
			- QtNetwork
			- Interfaz gráfica de usuario (widgets, layouts, etc.)
			- QPainter y captura de eventos del teclado y del mouse
			- QTimer
			- QtDesigner
		- OpenGL (glOrtho, gluPerspective, glLookAt, rotación, traslación, texturas, ...)
		- Base de datos (SELECT e INSERT).
		- Resolver los problemas consultando documentación técnica de distintas fuentes


Instalación de herramientas
===========================

:QtCreator: 
	- Si hay instaladas versiones anteriores de Qt, desinstalarlas ejecutando C:\\Qt\\MaintenanceTool.exe y tildando Uninstall only 
	- Descargar el `Instalador Online <https://www.qt.io/download-thank-you?hsLang=en>`_
	- Se recomienda este instalador Offline: `https://download.qt.io/archive/qt/5.14/5.14.1 <https://download.qt.io/archive/qt/5.14/5.14.1>`_
	- Importante la instalación de: 'Biblioteca Qt 5.14.1'  'Qt Creator'  'MinGW 7.3.0 64-bit'

:OpenSSL: 
	- Descargar instalador desde la `Página de descarga <https://slproweb.com/products/Win32OpenSSL.html>`_
	- Seleccionar el instalador `Win64 OpenSSL v3.1.0 <https://slproweb.com/download/Win64OpenSSL-3_1_0.exe>`_

:OBS Studio: 
	- Descargar instalador desde la `Página de descarga <https://obsproject.com/es>`_ e instalar


Metodología didáctica
=====================

- A continuación se resume el conjunto de estrategias, procedimientos y acciones para facilitar el aprendizaje y el logro de nuestros objetivos. 

:Teoría: 
	- En la primer parte de cada clase se expondrán los contenidos teóricos.
	- Este contenido también está disponible en grabaciones de años anteriores, cuyos links se colocarán en a medida que se avance en las clases.

:Práctica: 
	- La segunda parte de cada clase estará destinado a la resolución de ejercicios e incorporación de esos contenidos a un trabajo práctico que corresponde al segundo parcial.

:Regularidad, promoción y examen final: 
	- Primer parcial: Trabajo práctico individual para resolver en 2 horas
	- Segundo parcial: Entrega de un trabajo práctico integrador. El enunciado de este trabajo se entregará durante el primer mes de clases.
	- La materia se promociona bajo la modalidad de la UBP.
	- Para el trabajo práctico integrador, se puede elegir individual o grupal de hasta 3 estudiantes. Mientras más estudiantes formen el equipo, más características y complejidad tendrá el trabajo.
	- Hasta el viernes 31 de marzo se debe comunicar si se desea realizar el trabajo práctico integrador de manera individual o grupal. Por defecto, el trabajo es indiviudal.
	- Para acceder a la promoción se pide mucha participación durante clases, principalmente durante la parte práctica.
	- Las rúbricas de evaluación están en: `Rública Proyecto individual <https://docs.google.com/spreadsheets/d/1VZ3W91dbWRvWtav-Dr_NQjoCbTZx4DoiQCf9GN6OJX8/edit?usp=share_link>`_ y `Rúbrica Proyecto grupal <https://docs.google.com/spreadsheets/d/1hIZHseh0gT1SujRvPCBrctL8YzdA9tgLtqfP3rcKYeo/edit?usp=share_link>`_ 
	- El examen final tiene una modalidad distinta. El examen final se divide en dos partes: teórico y práctico (cada parte equivale al 50% del examen).
	- La parte práctica es la resolución de un desafío y la parte teórica es un tema particular de la material. Ver desafíos y temas en este github.

Ejercicio 1:
============

- Instalar Qt. Lo cual incluye las herramientas de compilación C++, la biblioteca Qt y Qt Creator.
- Crear un primer programa que muestre por la consola de QtCreator 10 números aleatorios en el intervalo [ 1, 2 )
- Cada vez que se ejecute el programa, los números deber´´an ser aleatorios.


Ejercicio 2:
============

- Explicar qué se entiende y para qué sirven: biblioteca, librería, library y archivos dll.
- Para qué sirve la variable de entorno PATH



