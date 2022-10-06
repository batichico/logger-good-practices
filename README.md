# Buenas prácticas a la hora de crear logs:
```
user = "Michael"
# 1.- Case
logger.debug("%s has connected", user)
# 2.- Case
logger.debug(f"{user} has connected")
# 3.- Case
logger.debug("%s has connected" %user)
# 4.- Case
logger.debug("{} has connected".format(user))
```
## El primer caso a la hora de generar un log es el correcto, dado que solo se genera si realmente si pasa por la casuística del log. En el resto de casos en cambio se haría  el formateo de string, pase o no la condición.

# Además de eso en el caso de logger.exception :

## En el caso de %s , formatea el string del valor
```
import logging
logger = logging.getLogger('msd')
lst_services = {
  'free': {
    "id": 1
  },
  'vip': {
    "id": 2
  },
  'premium': {
    "id": 3
  }
}
try:
  service_type = 'all_payed'
  print(f"{service_type} service id: {lst_services[service_type]['id']}" )
except Exception as e:
  logger.exception("An error ocurred: %s", e)
``` 
```
An error ocurred: 'all_payed'
Traceback (most recent call last):
  File "main.py", line 16, in <module>
    print(f"{service_type} service id: {lst_services[service_type]['id']}" )
KeyError: 'all_payed'
``` 

## En el caso de %r , se usa para formatear el repr, que suele tener más información. En el caso de las excepciones, suele tener el nombre de la excepción.
```
import logging
logger = logging.getLogger('msd')
lst_services = {
  'free': {
    "id": 1
  },
  'vip': {
    "id": 2
  },
  'premium': {
    "id": 3
  }
}
try:
  service_type = 'all_payed'
  print(f"{service_type} service id: {lst_services[service_type]['id']}" )
except Exception as e:
  logger.exception("An error ocurred: %r", e)
```
```
An error ocurred: KeyError('all_payed')
Traceback (most recent call last):
  File "main.py", line 16, in <module>
    print(f"{service_type} service id: {lst_services[service_type]['id']}" )
KeyError: 'all_payed'
``` 

