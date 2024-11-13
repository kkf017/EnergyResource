# Example of Django app

This app is an example of Django app (back-end) to manage Energy resources.

## Prerequisites
Make sure you have poetry:
```python
poetry --version
```

Make sure you have Django:
```python
pip3 install Django
```

Make sure you have rest_framework:
```python
pip3 install djangorestframework
pip3 install markdown       
pip3 install django-filter 
```

## Run the project
Run one of the following commands (in the /services/ directory):
```python
python3 manage.py runserver
```
```python
poetry run python3 manage.py runserver
```

## Home-made commands
To fill the database, one of the following commands can be used:
```python
python3 manage.py import_energy_data [filename]
```  
```python
poetry run python3 manage.py import_energy_data [filename]
``` 

To clear the database, one of the following commands can be used:
```python
python3 manage.py clear_data
```  
```python
poetry run python3 manage.py clear_data
``` 


## Examples of Requests

### Request GET

##### Display all Energy Resources
To display all Energy Ressources (in database), it is possible to go to http://127.0.0.1:8000/energy/ in your web browser, or use the following command in a terminal (Linux):
```sh
curl -X GET -H "Accept: application/json" http://127.0.0.1:8000/energy/
``` 
This command will return a json format with all the Energy Resources available in database.

##### Search request all Energy Resources
It is also possible to select Energy Resources, according to the following parameters:
- type: solar, wind, hydro, nuclear ...etc
- status: active, inactive, maintenance
- location: location of a ressource
- min, max: min and max value for capacity

These parameters can be combined in the url, as follows:
```sh
# Example of URL to select all the 'solar' ressources
curl -X GET -H "Accept: application/json" http://127.0.0.1:8000/energy/search?type=solar
``` 
```sh
# Example of URL to select all the 'solar' and 'active' ressources
curl -X GET -H "Accept: application/json" http://127.0.0.1:8000/energy/search?type=solar&status=active
```
```sh
# Example of URL to select all the ressources wiht capacity between 150 and 300
curl -X GET -H "Accept: application/json" http://127.0.0.1:8000/energy/search?min=150&max=300
```
```sh
# Example of URL to select all the 'active' ressources wiht capacity between 150 and 300
curl -X GET -H "Accept: application/json" http://127.0.0.1:8000/energy/search?status=active&min=150&max=300
```
It is also possible to go to the url with your web browser.

### Request POST
A new request can be created with the following request:
```sh
# Example of URL to create a ressource called "Biomass place 1"
curl -X POST -H "Content-Type: application/json" -d '{"name": "Biomass place 1", "type": "biomass", "capacity": "175", "location": "Location I", "status": "active"}' http://127.0.0.1:8000/new/
``` 
Or it is also possible to go to http://127.0.0.1:8000/new/ in your web browser and use the interface.


### Request DELETE
Finally, an Energy ressource can be deleted (using its id in table - eid) with the command:
```sh
# Example of URL to delete ressource with eid 4c7a2745227fd92f5381d4dfce69468e5df1c348
curl -X DELETE http://127.0.0.1:8000/close?eid=4c7a2745227fd92f5381d4dfce69468e5df1c348
``` 


