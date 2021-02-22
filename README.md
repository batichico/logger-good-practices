# Buenas prácticas a la hora de crear logs:
```
name1 = "samuel"
# 1.- Caso
logger.debug("%s se ha conectado", name1)
# 2.- Caso
logger.debug(f"{name1} se ha conectado")
# 3.- Caso
logger.debug("%s se ha conectado " %name1)
# 4.- Caso
logger.debug("{} se ha conectado".format(name1)) 
```
## El primer caso a la hora de generar un log es el correcto, dado que solo se genera si realmente si pasa por la casuística del log. En el resto de casos en cambio se haría  el formateo de string pase o no la condición.

# Además de eso en el caso de logger.exception :

## En el caso de %s , formatea el string del valor
```
import logging
logger = logging.getLogger('msd')
lst_names = {
  'samuel': {
    "name": "samuel"
  },
  'marta': {
    "name": "marta"
  },
  'maria': {
    "name": "maria"
  }
} 
try:
  print(f"hola que tal {lst_names['raul']}" )
except Exception as e:
  logger.exception("An error ocurred: %s", e)
``` 
```
An error ocurred: 'raul'
Traceback (most recent call last):
  File "main.py", line 18, in <module>
    print(f"hola que tal {lst_names['raul']}" )
KeyError: 'raul'
``` 

## En el caso de %r , se usa para formatear el repr, que suele tener más información. En el caso de las excepciones, suele tener el nombre de la excepción.
```
import logging
logger = logging.getLogger('msd')
lst_names = {
  'samuel': {
    "name": "samuel"
  },
  'marta': {
    "name": "marta"
  },
  'maria': {
    "name": "maria"
  }
} 
try:
  print(f"hola que tal {lst_names['raul']}" )
except Exception as e:
  logger.exception("An error ocurred: %r", e)
```
```
An error ocurred: KeyError('raul')
Traceback (most recent call last):
  File "main.py", line 18, in <module>
    print(f"hola que tal {lst_names['raul']}" )
KeyError: 'raul'
``` 

