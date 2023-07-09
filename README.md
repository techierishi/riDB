# Thread safe key value pair embedded NoSql database
NoSql Database in its simplest form

Steps to use the database:
```python
from ridb import RiDB
```

Create the database :
```python
ri_DB = RiDB('./mydb.json')
```
Storing simple data :
```python
ri_DB.set('name', 'John Doe')
ri_DB.set('version', 0.1)
ri_DB.set('author', 'John')
ri_DB.set('publised', False)
```
Getting the data:
```python
print(ri_DB.get('name'))
```

Pushing data in same array:
```python
 dictData = {'name': 'Rick', 'status': 'Y'}
 ri_DB.append('dictData', dictData)
 dictData2 = {'name': 'John', 'status': 'N'}
 ri_DB.append('dictData', dictData2)

 print(ri_DB.get('dictData'))
 ```
 Using in mulithreaded environment:
 ```python
 from ridb import RiDB
import threading

ri_DB = RiDB('./mydb.json')


def threadfunc():
    newData = {'name': 'Rick', 'status': 'Y'}
    ri_DB.append('newData', newData)
    ri_DB.set('name', 'John Doe')
    ri_DB.set('version', 0.1)
    ri_DB.set('publised', False)
    print(ri_DB.get('newData'))
    ri_DB.remove('name')


t1 = threading.Thread(target=threadfunc)
t2 = threading.Thread(target=threadfunc)

t1.start()
t2.start()
t1.join()
t2.join()
```
