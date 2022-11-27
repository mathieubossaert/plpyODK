# pyODK in PostgreSQL with plpython3 extension

## install plpython
```bash
apt-get update && apt-get install postgresql-plpython3-12
```
## pip install (if not yet)
```bash
apt install python3-pip
```
## pyODK install
```
pip install pyodk
```

## Connecting to the database
### plpython3 installation

```sql
CREATE OR REPLACE PROCEDURAL LANGUAGE plpython3u
    HANDLER plpython3_call_handler
    INLINE plpython3_inline_handler
    VALIDATOR plpython3_validator;
```

### First try : project_list
```sql
CREATE OR REPLACE FUNCTION client_project_list()
RETURNS TEXT
AS $$
	from pyodk.client import Client

	client = Client()
	client.open()
	json_value = client.projects.list()
	return json_value
$$
LANGUAGE 'plpython3u';

SELECT client_project_list();
```