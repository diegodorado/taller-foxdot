# Taller de FoxDot

Breve taller del entorno de livecoding FoxDot


## Iniciar Foxdot
En primer lugar, abrir SuperCollider y ejecutar.

```FoxDot.start```

Luego, escribir en la línea de comandos los siguiente.

```python -m FoxDot```


Este comando se puede guardar en un archivo foxdot.bat para iniciarlo con un doble click.

Para evaluar un bloque de código en FoxDot, pulsa Ctrl + Enter. Prueba con 


Suficiente intro! Hagamos musica. 


Sample Player

Primero el codigo, despues las explicaciones. Evalua el siguiente bloque de codigo:



d1 es el nombre de nuestro “Sample Player”. Los nombres de 2 caracteres ya estan definidos por comodidad y son los que se usan normalmente.
>> es sintaxis...de este modo se asigna en FoxDot un Player
play() es una funcion que crea un ‘Sample Player’
‘x-o-’ es un texto que se pasa como argumento a la funcion play, y cada caracter en este caso corresponde a un sample

Para detenerlo, evaluamos la funcion stop del Player:


O alternativamente, “Ctrl + . “ detiene todo.

Puedo escribir cualquier cosa, y tendra como resultado algun ritmo. Probemos:


Para cambiar la duracion de cada golpe, que por defecto es 1, podemos pasar la duracion como parametro a la funcion play



O incluso una secuencia: dur=[1,2,0.5]


Dos atajos muy usados son la alternancia y la subdivision.


Alternancia

Se indica encerrando entre parentesis los elementos que queremos alternar


Es una forma corta de escribir ‘x-o-x-o=’

Puede usarse con mas de dos valores:
play(‘x--(aeo)’) es igual a play(‘x--ax--ex--o’)


Subdivision

Si encerramos elementos entre corchetes duraran la misma unidad de tiempo que sus vecinos



Aca, tanto ‘x’ como ‘--’ duran lo mismo: 2


Si queremos que suenen a la vez varios samples,  podemos crear dos Sample Player



Ahora, podemos jugar con otros atributos aparte de secuencia de samples y duracion. Para ver cuales existen evaluamos este codigo

>>> print(Player.get_attributes())
('degree', 'oct', 'dur', 'delay', 'blur', 'amplify', 'scale', 'bpm', 'sample', 'sus', 'fmod', 'pan', 'rate', 'amp', 'vib', 'vibdepth', 'slide', 'sus', 'slidedelay', 'slidefrom', 'bend', 'benddelay', 'coarse', 'striate', 'pshift', 'hpf', 'hpr', 'lpf', 'lpr', 'swell', 'bpf', 'bpr', 'bits', 'amp', 'crush', 'dist', 'chop', 'tremolo', 'echo', 'decay', 'spin', 'cut', 'room', 'mix', 'formant', 'shape')

Asi, podemos probar algo como:



O, mas divertido, con secuencias:




SynthDefs

Pasemos a algo mas melodico.
Para ver los sintes que vienen con FoxDot, 


['sawbass', 'karp', 'gong', 'varsaw', 'bell', 'feel', 'scratch', 'pulse', 'audioin', 'blip', 'pads', 'rave', 'donk', 'saw', 'orient', 'creep', 'growl', 'marimba', 'razz', 'dub', 'pasha', 'keys', 'arpy', 'zap', 'viola', 'piano', 'quin', 'ambi', 'dbass', 'crunch', 'noise', 'star', 'bass', 'dab', 'dirt', 'twang', 'swell', 'pluck', 'glass', 'soprano', 'charm', 'spark', 'bug', 'squish', 'sitar', 'snick', 'play2', 'play1', 'prophet', 'ripple', 'space', 'fuzz', 'lazer', 'klank', 'nylon', 'soft', 'scatter', 'loop']

Si elijo por ejemplo un pluck, puedo crearlo evaluando lo siguiente:


El primer argumento de un sinte no precisa ser nombrado y es la secuencia o pattern de notas. El resto deben ser parametros nombrados.


Si quiero mas de una nota a la vez, hago un grupo entre parentesis: [0,2,(4,8)]
Aca estamos hablando de grados de una escala ( por defecto, la escala mayor), y la secuencia anterior va a iterar entre tonica, tercera, quinta+novena.
(Notar que el primer grado es de indice 0)

Follow permite que un player “siga” a otro. Que siga las notas.

