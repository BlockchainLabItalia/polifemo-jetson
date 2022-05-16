# Polifemo

Polifemo è un sistema di conteggio di elementi in movimento, in questo caso specifico di persone. 
Utilizza un hardware dalle capacità computazionali relativamente basse (come un Jetson Nano), una videocamera ed una connessione ad internet verso un DB per contare persone entranti o uscenti una determinata area.

In particolare dopo aver definito una linea immaginaria che divide in due la scena ripresa dalla videocamera, il sistema conta le persone che la attraversano in entrambe le direzioni e salva le informazioni sul DB.

### DB
Il DB utilizzato e InfluxDB. Dopo averlo creato i parametri di connessione vanno inseriti nel file [configuration.json](./configuration.json).

### DEFINIZIONE LINEA

Prima di eseguire il programma, va definita la linea immaginaria. Sempre all'interno del file [configuration.json](./configuration.json), vanno definite le caratteristiche della linea;
Ci sono 3 diverse possibilità

- "line_orientation":"vertical":
    
    "line_position" è un numero compreso tra 0 e 1 e definisce la posizione della linea verticale sull'asse delle ascisse (ad esempio se ["line_position": 0.5] allora la linea sarà posizionata a metà dell'inquadratura).

- "line_orientation":"horizzontal":
    
    "line_position" è un numero compreso tra 0 e 1 e definisce la posizione della linea verticale sull'asse delle ordinate.

- "line_orientation":"oblique": 
    
    "line_position" è un oggetto tipo:
    ```
    {
        "point1":{
            "x":,
            "y":
        },
        "point2":{
            "x":,
            "y":
        }
    }
    ``` 
    In cui poin1 e poin2 indicano due punti di una linea retta che in 2 il frame catturato dalla videocamera.


In caso di linea obliqua, per aiutarci ad ottenere i punti utili, è stato creato lo script [draw_line_on_capture_frame.py](./draw_line_on_capture_frame.py) che all'esecuzione mostra a schermo la scena ripresa dalla videocamera. a questo punto basterà cliccare su un punto dal quale desideriamo passi la linea e premere successivamente il tasto 'a' sulla tastiera; in questo modo sulla console verrano mostrate le coordinate del punto cliccato con il mouse.

> Nota: in caso dovessimo essere connessi al dispositivo via SSH avremo bisogno di una XSession ed in caso stiamo usando un terminale windows dovremmo installare XMing

### ESECUZIONE


```
python polifemo.py
```

