Estándars de Codificación
#########################

Los desarrolladores de CakePhp usarán los siguientes éstándars de codificación.

Se recomienda que otros desarrolladores de CakeIngredients sigan los mismos
estándars

Puedes usar el `CakePHP Code Sniffer
<https://github.com/cakephp/cakephp-codesniffer>`_ para comprobar que tu código
sigue los estándars requeridos.

Lenguaje
========

Todos el código y comentarios debería ser escrito en Inglés.

Añadiendo Nuevas Características
================================

Ninguna característica nueva debería ser añadida, sin tener sus propios test - 
los cuales deberían haber pasado antes de remitirlos al respositorio.

Indentación
===========

Se usará una tabulación para indentar.

Así que, la indentación debería tener este aspecto::

    // base level
        // level 1
            // level 2
        // level 1
    // base level

O::

    $booleanVariable = true;
    $stringVariable = 'moose';
    if ($booleanVariable) {
        echo 'Boolean value is true';
        if ($stringVariable === 'moose') {
            echo 'We have encountered a moose';
        }
    }

Longitud de Línea
=================

Se recomienda mantener las líneas de aproximadamente 100 caracteres de largo 
para una mejor lectura de código.
Las líneas no deberían ser mas largas de 120 caracteres.

En resumen:

* 100 caracteres es el límite suave.
* 120 caracteres es el límite duro.

Estructuras de Control
======================

Las estructuras de control son por ejemplo "``if``", "``for``", "``foreach``",
"``while``", "``switch``" etc. Debajo, un ejemplo con "``if``"::

    if ((expr_1) || (expr_2)) {
        // action_1;
    } elseif (!(expr_3) && (expr_4)) {
        // action_2;
    } else {
        // default_action;
    }

*  En las estructuras de control debería haber 1 (un) espacio antes del
   primer paréntesis y 1 (un) espacio entre el último paréntesis y
   la llave de apertura.
*  Siempre usar llaves en las estructuras de control, aunque no sean
   necesarios. Éstos incrementan la legibilidad del código, y te dan
   menos errores lógicos.
*  Las llaves de apertura deberían ponerse en la misma línea que
   la estructura de control. Las llaves de cierre deberían ponerse en una nueva
   línea, y deberían tener el mismo nivel de indentación que la estructura
   de control. La declaración incluída entre las llaves debería empezar en una
   nueva línea, y el código contenido en su interior debería ganar un nuevo nivel
   de indentación.   
*  Las asignaciones en la misma línea no deberían ser usadas dentro de las 
   estructuras de control.

::

    // wrong = no brackets, badly placed statement
    if (expr) statement;

    // wrong = no brackets
    if (expr)
        statement;

    // good
    if (expr) {
        statement;
    }

    // wrong = inline assignment
    if ($variable = Class::function()) {
        statement;
    }

    // good
    $variable = Class::function();
    if ($variable) {
        statement;
    }

Operador Ternario
-----------------

Los operadores ternario están permitidos cuando el operador entero cabe
en una línea. Operadores ternarios más largos deberían dividirse en sentencias
``if else``. Los operadores ternarios nunca deberían anidarse. Opcionalmente
se pueden usar paréntesis alrededor de la comprobación de una condición del 
operador ternario por claridad::

    // Good, simple and readable
    $variable = isset($options['variable']) ? $options['variable'] : true;

    // Nested ternaries are bad
    $variable = isset($options['variable']) ? isset($options['othervar']) ? true : false : false;


Archivos de Vista
-----------------

En los archivos de vista (archivos .ctp) los desarrolladores deberían usar 
palabras clave de estructuras de control. Las palabras clave de las estructuras
de control so más fáciles de leer en archivos de vista complejos. Estructuras
de control pueden también estár contenidas en un bloque PHP más grande, o en
etiquetas PHP separadas::

    <?php
    if ($isAdmin):
        echo '<p>You are the admin user.</p>';
    endif;
    ?>
    <p>The following is also acceptable:</p>
    <?php if ($isAdmin): ?>
        <p>You are the admin user.</p>
    <?php endif; ?>

We allow PHP closing tags (``?>``) at the end of .ctp files.
Permitimos etiquetas de cierre PHP (``?>``) al final de los archivos .ctp. 

Comparación
===========

Intenta ser siempre lo más estricto posible. Si se usa un test no estricto 
deliberadamente podría ser sensato comentarlo como tal para evitar confundirlo
por error.

Para evaluar si una variable es null, se recomienda usar una comprobación 
estricta::

    if ($value === null) {
    	  // ...
    }

El valor con el que comprobar debería situarse en el lado derecho::

    // not recommended
    if (null === $this->foo()) {
        // ...
    }

    // recommended
    if ($this->foo() === null) {
        // ...
    }

Llamada a Funciones
===================

Las funciones deberían ser llamadas sin espacios entre el nombre de la función
y el comienzo del paréntesis. Debería haber un espacio entre cada parámetro de 
una función llamada::

    $var = foo($bar, $bar2, $bar3);

Como puedes ver encima debería haber un espacio a ambos lados del signo
igual (=).

Definición de Métodos
=====================

Ejemplo de definición de un método::

    public function someFunction($arg1, $arg2 = '') {
        if (expr) {
            statement;
        }
        return $var;
    }

Los parámetros con un valor por defecto, deberían ponerse los últimos en la 
definición de la función. Intenta hacer funciones que devuelvan algo, al menos 
``true`` o ``false``, para que pueda determinarse cuándo la llamada a la 
función se realizó con éxtio::


    public function connection($dns, $persistent = false) {
        if (is_array($dns)) {
            $dnsInfo = $dns;
        } else {
            $dnsInfo = BD::parseDNS($dns);
        }

        if (!($dnsInfo) || !($dnsInfo['phpType'])) {
            return $this->addError();
        }
        return true;
    }

Hay espacios a ambos lados del signo igual.

Determinación de Tipos
----------------------

Los argumentos que esperan objetos o arrays pueden determinarse por tipo::

    /**
     * Some method description.
     *
     * @param Model $Model The model to use.
     * @param array $array Some array value.
     * @param bool $boolean Some boolean value.
     */
    public function foo(Model $Model, array $array, $boolean) {
    }

Aquí ``$Model`` deberá ser una instacia de ``Model`` y ``$array`` deberá ser 
un ``array``.


Nótese que si quieres permitir que ``$array`` sea también una instancia de 
``ArrayObject`` no deberías determinar el tipo como ``array`` aceptando sólo 
el tipo primitivo::

    /**
     * Some method description.
     *
     * @param array|ArrayObject $array Some array value.
     */
    public function foo($array) {
    }

Métodos Encadenados
===================

Los métodos encadenados deberían tener múltiples métodos desplegados a lo largo
de líneas separadas, e indentadas con una tabulación::

    $email->from('foo@example.com')
        ->to('bar@example.com')
        ->subject('A great message')
        ->send();

DocBlocks
=========

Todos los bloques de comentarios, a excepción del primer bloque de un archivo, 
deberían siempre estar precedidos por una nueva línea.

DocBlock de Cabecera de Archivo
-------------------------------

Todos los archivos PHP deberían contener un DocBlock en la cabecera del archivo
que tuviera una pinta similar a esta::

    <?php
    /**
    * CakePHP(tm) : Rapid Development Framework (http://cakephp.org)
    * Copyright (c) Cake Software Foundation, Inc. (http://cakefoundation.org)
    *
    * Licensed under The MIT License
    * For full copyright and license information, please see the LICENSE.txt
    * Redistributions of files must retain the above copyright notice.
    *
    * @copyright     Copyright (c) Cake Software Foundation, Inc. (http://cakefoundation.org)
    * @link          http://cakephp.org CakePHP(tm) Project
    * @since         X.Y.Z
    * @license       http://www.opensource.org/licenses/mit-license.php MIT License
    */

Las etiquetas `phpDocumentor <http://phpdoc.org>`_ incluídas son:

*  `@copyright <http://phpdoc.org/docs/latest/references/phpdoc/tags/copyright.html>`_
*  `@link <http://phpdoc.org/docs/latest/references/phpdoc/tags/link.html>`_
*  `@since <http://phpdoc.org/docs/latest/references/phpdoc/tags/since.html>`_
*  `@license <http://phpdoc.org/docs/latest/references/phpdoc/tags/license.html>`_

DocBlocks de Clase
------------------

Los DocBlocks de clase deberían ser como estos::

    /**
     * Short description of the class.
     *
     * Long description of class.
     * Can use multiple lines.
     *
     * @deprecated 3.0.0 Deprecated in 2.6.0. Will be removed in 3.0.0. Use Bar instead.
     * @see Bar
     * @link http://book.cakephp.org/2.0/en/foo.html
     */
    class Foo {

    }

Los DocBlocks de clase deberían contener las siguientes etiquetas `phpDocumentor <http://phpdoc.org>`_:

*  `@deprecated <http://phpdoc.org/docs/latest/references/phpdoc/tags/deprecated.html>`_
   Using the ``@version <vector> <description>`` format, where ``version`` and ``description`` are mandatory.
*  `@internal <http://phpdoc.org/docs/latest/references/phpdoc/tags/internal.html>`_
*  `@link <http://phpdoc.org/docs/latest/references/phpdoc/tags/link.html>`_
*  `@property <http://phpdoc.org/docs/latest/references/phpdoc/tags/property.html>`_
*  `@see <http://phpdoc.org/docs/latest/references/phpdoc/tags/see.html>`_
*  `@since <http://phpdoc.org/docs/latest/references/phpdoc/tags/since.html>`_
*  `@uses <http://phpdoc.org/docs/latest/references/phpdoc/tags/uses.html>`_

DocBlocks de Propiedades
------------------------

Los DocBlocks de propiedades deberían ser como estos::

    /**
     * @var string|null Description of property.
     *
     * @deprecated 3.0.0 Deprecated as of 2.5.0. Will be removed in 3.0.0. Use $_bla instead.
     * @see Bar::$_bla
     * @link http://book.cakephp.org/2.0/en/foo.html#properties
     */
    protected $_bar = null;

Los DocBlocks de propiedades deberían contener las siguientes etiquetas `phpDocumentor <http://phpdoc.org>`_:

*  `@deprecated <http://phpdoc.org/docs/latest/references/phpdoc/tags/deprecated.html>`_
   Using the ``@version <vector> <description>`` format, where ``version`` and ``description`` are mandatory.
*  `@internal <http://phpdoc.org/docs/latest/references/phpdoc/tags/internal.html>`_
*  `@link <http://phpdoc.org/docs/latest/references/phpdoc/tags/link.html>`_
*  `@see <http://phpdoc.org/docs/latest/references/phpdoc/tags/see.html>`_
*  `@since <http://phpdoc.org/docs/latest/references/phpdoc/tags/since.html>`_
*  `@var <http://phpdoc.org/docs/latest/references/phpdoc/tags/var.html>`_

DocBlocks de Método/Función
---------------------------

Los DocBlocks de método y funciones deberían parecerse a éstos:

    /**
     * Short description of the method.
     *
     * Long description of method.
     * Can use multiple lines.
     *
     * @param string $param2 first parameter.
     * @param array|null $param2 Second parameter.
     * @return array An array of cakes.
     * @throws Exception If something goes wrong.
     *
     * @link http://book.cakephp.org/2.0/en/foo.html#bar
     * @deprecated 3.0.0 Deprecated as of 2.5.0. Will be removed in 3.0.0. Use Bar::baz instead.
     * @see Bar::baz
     */
     public function bar($param1, $param2 = null) {
     }

Los DocBlocks de método y funciones deberían contener las siguientes etiquetas `phpDocumentor <http://phpdoc.org>`_:

*  `@deprecated <http://phpdoc.org/docs/latest/references/phpdoc/tags/deprecated.html>`_
   Using the ``@version <vector> <description>`` format, where ``version`` and ``description`` are mandatory.
*  `@internal <http://phpdoc.org/docs/latest/references/phpdoc/tags/internal.html>`_
*  `@link <http://phpdoc.org/docs/latest/references/phpdoc/tags/link.html>`_
*  `@param <http://phpdoc.org/docs/latest/references/phpdoc/tags/param.html>`_
*  `@return <http://phpdoc.org/docs/latest/references/phpdoc/tags/return.html>`_
*  `@throws <http://phpdoc.org/docs/latest/references/phpdoc/tags/throws.html>`_
*  `@see <http://phpdoc.org/docs/latest/references/phpdoc/tags/see.html>`_
*  `@since <http://phpdoc.org/docs/latest/references/phpdoc/tags/since.html>`_
*  `@uses <http://phpdoc.org/docs/latest/references/phpdoc/tags/uses.html>`_

Tipos de Variable
-----------------

Tipos de variable para usar en DocBlocks:

Tipo
    Descripción
mixed
    Una variable con tipo (o múltiples tipos) indefinidos.
int
    Tipo de variable entera (numero completo).
float
    Tipo float (número decimal).
bool
    Tipo lógico (true o false).
string
    Tipo cadena (cualquier valor entre " " o ' ').
null
    Tipo nulo. Normalmente usado junto con otro tipo.
array
    Tipo array (colección).
object
    Tipo objeto. Debería usarse un nombre de clase específico si fuera posible.
resource
    Tipo recurso (devuelto por por ejemplo mysql\_connect()).
    Recuerda que cuando especificas el tipo como mixed, deberías indicar
    si es desconocido, o qué posibles tipos son.
callable
    Funciones llamables.

También puedes combinar tipos usando el carácter de tubería::

    int|bool

Para más de dos tipos normalmente es mejor simplmente usar ``mixed``.

Cuando se devuelva el propio objeto, e.g. para encadenar, debería usarse 
``$this`` en su lugar::

    /**
     * Foo function.
     *
     * @return $this
     */
    public function foo() {
        return $this;
    }

Archivos de Inclusión
=====================

``include``, ``require``, ``include_once`` y ``require_once`` no tienen 
paréntesis::

    // wrong = parentheses
    require_once('ClassFileName.php');
    require_once ($class);

    // good = no parentheses
    require_once 'ClassFileName.php';
    require_once $class;

Cuando se incluyan archivos con clases o librerías, usar sólo y siempre la 
función require\_once <http://php.net/require_once>`_.

Etiquetas PHP
=============

Usar siempre las etiquetas largas (``<?php ?>``) En lugar de las 
cortas (``<? ?>``).

Nomenclatura
============

Funciones
---------

Escribe todas las funciones en notación camelBack::

    function longFunctionName() {
    }

Clases
-------

Los nombres de clase deberían ser escritos en CamelCase, por ejemplo::

    class ExampleClass {
    }

Variables
---------

Los nombres de variables deberían ser tan descriptivos como sea posible, pero 
también tan cortos como sea posible. Todas las variables deberían comenzar con 
una letra minúscula, y deberían ser escritas en camelBack en caso de contener 
varias palabras. Las variables que referencien objetos deberían estar asociadas
de alguna manera con la clase de  cuyo objeto es la variable. Ejemplo::

    $user = 'John';
    $users = array('John', 'Hans', 'Arne');

    $dispatcher = new Dispatcher();

Visibilidad de Miembros
-----------------------

Usa las palabras reservadas de PHP private y protected para métodos y 
variables. Adicionalmente, los nombres de métodos o variables protegidos 
deberían empezar con un carácter de subrayado (``_``). Ejemplo::

    class A {
        protected $_iAmAProtectedVariable;

        protected function _iAmAProtectedMethod() {
           /* ... */
        }
    }

Los nombres de métodos o variables deberían empezar con dos caracteres de 
subrayado (``__``). Ejemplo::

    class A {
        private $__iAmAPrivateVariable;

        private function __iAmAPrivateMethod() {
            /* ... */
        }
    }

Trata de evitar métodos o variables privados, en favor de los protegidos.
ÉStos últimos pueden ser accedidos o modificados por subclases, donde los 
privados previenen su ampliación o reutilización. La visibilidad privada 
también hacen el testeo mucho más difícil.

Ejempo de Direcciones
---------------------

Para todos los ejemplos de direcciones URL y de correo se usa "example.com",
"example.org" y "example.net", por ejemplo:

*  Email: someone@example.com
*  WWW: `http://www.example.com <http://www.example.com>`_
*  FTP: `ftp://ftp.example.com <ftp://ftp.example.com>`_

El nombre de dominio "example.com" ha sido reservado para esto 
(see :rfc:`2606`) y se recomienda para su uso en documentación o como ejemplos.

Archivos
-----

Los nombres de archivo que no contengan clases deberían estar en minúscula y 
con subrayados, por ejemplo::

    long_file_name.php

Casting
-------

Para el casting usamos:

Tipo
    Descripción
(bool)
		Conversión a boolean.
(int)
		Conversión a integer.
(float)
		Conversión a float.
(string)
		Conversión a string.
(array)
		Conversión a array.
(object)
		Conversión a object.

Por favor ``(int)$var`` en lugar de ``intval($var)`` y ``(float)$var`` en vez 
de ``floatval($var)`` cuando aplique.

Constantes
----------

Las constantes deberían definirse en letras mayúsculas::

    define('CONSTANT', 1);

Si un nombre de constante tiene varias palabras, deberían ser separadas
por un caracter de subrayado, por ejemplo::

    define('LONG_NAMED_CONSTANT', 2);


.. meta::
    :title lang=es: Estándars de Codificación
    :keywords lang=es: llaves,nivel de indentación,errores lógicos,estructuras de control,estructura de control,expr,estándar de codificación,paréntesis,foreach,legibilidad,moose,nuevas características,repositorio,desarrolladores
