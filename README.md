# [Red neuronal recurrente](https://github.com/nanmon/rnn)

## Datasets
Los datasets estan disponibles en mi [google drive](https://drive.google.com/drive/folders/10xaxtz6KifCYOjg1p7o5RFjgJjgCJjnJ?usp=sharing)

## Municipios locos
Se creó una red neuronal que se entrenó con los nombres de los municipios de México,
para inventarse nombres de municipios

### Estructura del conjunto de entramiento
Se entrenó con secuencias de 25 caracteres, 68 caracteres distintos, generando del texto original 1421 secuencias. Por lo que las dimensiones del conjunto de aprendizaje es (1421, 25, 68)

### Arquitectura de la red
- Una capa LSTM con 250 neuronas y dropout de 30%
- Salida softmax
- Optimizador RMSPROP
- Función loss categorial_crossentropy
- Entrenamiento de 100 epochs con minibatches de 32

### Resultados
```
Matamoras
Matimol Martanterrosisio
Miguel de Altanoda
Ma Mileo
Mattián Moxiahia
San Mireo Tebasto
Sena Mintepec
Sititla
Matimár de Tatenaca
San Pedro de Sal Parto de Marta de Aruanda
San Pedro Jacantía de Samiapo
San Jerónimo Tilocuepo
Santiago Tomaconotuahicca
Santiago Sololtepec
San albo
Samadol
Santiago de Sal Pablo Atlapan
San Pedro Amiatlán
San Dien de la Solinar de lo SelosanoSan Parla del Protengo
San Pedro Mataparo de las Sinás
San Anto Tuiapan
San Anantan
Santa María de la Salina
Santa Laca Yuautlan
San Juan Atatinta Atalta
Santa Matía Mateneses Yitonas
Santa Catarina Tlaláxtla
Santiago Tlacotetlahca
Santa María Tlacotepec
Santa Tlamixtacan
Santiago Sochitlán
San Miguel de Siranto
San Pedro Totopen
San Pedro Toxtlahua
San Mateo Santo Do irba
Teoticao
Telima
Temimputitlán
Temotepec

Tamáx
Bampa
Vala
Mazapa
Matampa
Matampa
Ramarena
Ajacutli
Aoca
Atera
Atia
Migael de Altaa
Laringo Lavinho
Lagonis
Laginidado Loso Ma Matoa
Rosas Lo Panabaro
Lucabár
Puz
Dranisto Domisgo Ixtapata
Santa María
Inta Miual de Juárez
Sanaval
El Miguel Matapen
Sen Juan de  oringo Tepamueto
San Miruel de la Indenen
Sana Mirianga de Ateban
Santo Domingo Tlatopepo
Santiago Tltotepac
Santiago Tlamuzanatepec
Santiago Tlapatapuc
Santiago Tomaltepec
Santiago Tocutitlán
Santiago Tomatutlán
Santiago Tomaltepec
Santiago Tocatepec
Santiago Taxcuala
Santa Ana Tepatinahi
Santa Inis de la Indapende Santa de Ixiatepec
Santa María de lamaso Zimatlpec
Santa María Ototoneno
Santa María de lo Resososonasala
Santa La Ya Yelape
San Mateo Etelco
San Marton de  Orrdodo
San Pedro Martaner Tituitingo Tetlaxtepec
San Jemónimo Teotipac
Santiago Tompa
Timuatz
San Jimónimo Tlatocatepec
Tlaco
Tepachingo
Teatitlán
Temuitinggo
Teptitepec
Tetatipán
Toxtetla
Tutmayán
Tuxtitan
Tomititáá
Tochitlán
Totatimpe
Toatlás
Totatepec
Motta Motesoro
Ixcamuchiatlán
Ixtlalcha
tlala
Zepatla
Ixtapatlaho
Ixtatepec
Ixtatotlá
Mostarres
Moramo Mirtapa
Moteatla
Etlande
Etarango
Ixca
Ixian Migua Miria de la Indenenistis Mixaltepec
Satia
```

## El Hermanastro Grimm
Se creó una red neuronal que dado el libro de cuentos de los hermanos grimm, se inventa pequeños "relatos"

### Estructura del conjuto de entrenamiento
Es parecido al de municipios, ya que también se hizo por caracteres. Se usaron secuencias de 50 caracteres, 75 caracteres distintos, y 10352 secuencias. Las dimensiones del conjunto de aprendizaje es (10352, 50, 75)

### Arquitectura de la red
- Una capa LSTM con 700 neuronas y 30% dropout
- Otras dos capas LSTM con 700 neuronas, sin dropout
- Salida softmax
- Optimizador RMSPROP
- Función loss categorial_crossentropy
- Entrenamiento de 65 epochs con minibatches de 32

### Resultados
```
2 ‘What do you want here?--speak off!’ said the cat quite as my little mother
has come home, and has brought you her finger; but the wild man was standing at the hills, into the bed with the
eggs that sprinkled for joy. At last he could bear it no longer; so he gave him a needle, and drew the turnip to the court that was left all that sick up the castle was called Snow-white, and
the star-gazer took his glass, looked up, and said, ‘Now, my
godden a fellow who will see mine.’ Then the king and mo[...]
```

## Conclusiones
Municipios locos era una red muy sencilla, al principio me quise complicar con 3 capas LSTM, pero aparte de que copiaba, repetía el mismo hasta el infinito. No tuve muchas complicaciones con esta red porque entrenaba muy rapido, en menos de una hora ya llevaba 100 epochs.

El hermanastro Grimm dió mucha lata, primero dejé entrenando todo el día y al volver a mi casa estaba muerta la ejecución de python y olvidé guardar checkpoints. La segunda vez la dejé toda la noche (ahora si guardando checkpoints cada 5 epochs) y al amanecer me di cuenta que la compu se había reiniciado, y trágicamente mis checkpoints no sirvieron de nada porque el mapa de caracteres a indices generaba indices distintos en cada ejecución. Lo volví a correr el resto del día y el entrenamiento resultó bien, pero los resultados no eran muy convincentes, copiaba oraciones completas (sobreaprenzaje), así que reduje el tamaño de secuencia de 200 a 50 y lo dejé otra noche. Al amanecer vi que se había detenido a mitad de la noche porque no tenía suficiente espacio en disco para guardar el epoch #70, pero tenía el checkpoint del epoch 65 y al probarlo me gustaron los resultados, no tenía mucho sentido como un todo pero formaba oraciones con fragmentos de solo 2 a 4 palabras consecutivas del texto original.