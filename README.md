# Taller de FoxDot

Breve taller del entorno de livecoding FoxDot


## Iniciar Foxdot
En primer lugar, abrir SuperCollider y ejecutar.

```FoxDot.start```

Luego, escribir en la línea de comandos los siguiente.

```python -m FoxDot```


Este comando se puede guardar en un archivo foxdot.bat para iniciarlo con un doble click.

Para evaluar un bloque de código en FoxDot, pulsa Ctrl + Enter. Prueba con 
```python 
print(2+2)
```

Suficiente intro! Hagamos musica. 


## Sample Player

Primero el codigo, despues las explicaciones. Evalua el siguiente bloque de codigo:
```python 
d1 >> play('x-o-')
```

 * `d1` es el nombre de nuestro `Sample Player`. Los nombres de 2 caracteres ya estan definidos por comodidad y son los que se usan normalmente.
 * `>>` es sintaxis...de este modo se "asigna" en FoxDot un Player
 * `play()` es una funcion que crea un `Sample Player`
 * `x-o-` es un texto que se pasa como argumento a la funcion play, y cada caracter en este caso corresponde a un sample

Para detenerlo, evaluamos la funcion stop del Player:

```python 
d1.stop()
```

O alternativamente, `Ctrl + . ` detiene todo.

Puedo escribir cualquier cosa, y tendra como resultado algun ritmo. Probemos:

```python 
d1 >> play('hola a todos')
```


Para cambiar la duracion de cada golpe, que por defecto es `1`, podemos pasar la duracion como parametro a la funcion play

```python 
d1 >> play('x-o-', dur=2)
```

O incluso una secuencia:
```python 
d1 >> play('x-o-', dur=[1,2,0.5])
```

Dos atajos muy usados son la **alternancia** y la **subdivision**.


### Alternancia

Se indica encerrando entre parentesis los elementos que queremos alternar

```python 
d1 >> play('x-o(-=)')
```

Es una forma corta de escribir
```python 
d1 >> play('x-o-x-o=')
```

Puede usarse con mas de dos valores:
`play('x--(aeo)')` es igual a `play('x--ax--ex--o')`


### Subdivision

Si encerramos elementos entre corchetes duraran la misma unidad de tiempo que sus vecinos

```python 
d1 >> play('x[--]', dur=2)
```

Aca, tanto `x` como `--` duran lo mismo: `2`


Si queremos que suenen a la vez varios samples,  podemos crear dos `SamplePlayer`


```python 
d1 >> play('xo', dur=2)
hh >> play('--=-')
```


Ahora, podemos jugar con otros atributos aparte de secuencia de samples y duracion. Para ver cuales existen evaluamos este codigo

```python
>>> print(Player.get_attributes())
('degree', 'oct', 'dur', 'delay', 'blur', 'amplify', 'scale', 'bpm', 'sample', 'sus', 'fmod', 'pan', 'rate', 'amp', 'vib', 'vibdepth', 'slide', 'sus', 'slidedelay', 'slidefrom', 'bend', 'benddelay', 'coarse', 'striate', 'pshift', 'hpf', 'hpr', 'lpf', 'lpr', 'swell', 'bpf', 'bpr', 'bits', 'amp', 'crush', 'dist', 'chop', 'tremolo', 'echo', 'decay', 'spin', 'cut', 'room', 'mix', 'formant', 'shape')
```

Asi, podemos probar algo como:


```python 
d1 >> play('x-o-', sample=4, rate=0.65, coarse=20, amp=0.9, pan=0.5)
```

O, mas divertido, con secuencias:


```python 
d1 >> play('x-o-', sample=[4,3,6], rate=[0.65,1], coarse=[20,0,10,0,30], amp=0.9, pan=0.5)
```


## SynthDefs

Pasemos a algo mas melodico.
Para ver los sintes que vienen con FoxDot, 

```python 
print(SynthDefs)

['sawbass', 'karp', 'gong', 'varsaw', 'bell', 'feel', 'scratch', 'pulse', 'audioin', 'blip', 'pads', 'rave', 'donk', 'saw', 'orient', 'creep', 'growl', 'marimba', 'razz', 'dub', 'pasha', 'keys', 'arpy', 'zap', 'viola', 'piano', 'quin', 'ambi', 'dbass', 'crunch', 'noise', 'star', 'bass', 'dab', 'dirt', 'twang', 'swell', 'pluck', 'glass', 'soprano', 'charm', 'spark', 'bug', 'squish', 'sitar', 'snick', 'play2', 'play1', 'prophet', 'ripple', 'space', 'fuzz', 'lazer', 'klank', 'nylon', 'soft', 'scatter', 'loop']
```

Si elijo por ejemplo un pluck, puedo crearlo evaluando lo siguiente:

```python 
p1 >> pluck()
```

El primer argumento de un sinte no precisa ser nombrado y es la secuencia o pattern de notas. El resto deben ser parametros nombrados.

```python 
p1 >> pluck([0,2,4], dur=[1/4,1/2], amp=[1,0.9,0.8])
```

Si quiero mas de una nota a la vez, hago un grupo entre parentesis: `[0,2,(4,8)]`
Aca estamos hablando de grados de una escala ( por defecto, la escala mayor), y la secuencia anterior va a iterar entre tonica, tercera, quinta+novena.
(Notar que el primer grado es de indice 0)

Follow permite que un player *siga* a otro. Que siga las notas.


```python 
b1 >> bass([0,2,3,4], dur=4)
p1 >> piano(dur=1/2).follow(b1) + (0,2,4)
```


