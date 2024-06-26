# FinallyDataLogger

FinallyDataLogger is a simple, lightweight data logging server and client package. Log, modify, and fetch data with ease!

## Features

- Log data from any Python script easily.
- Store scalar, textual, and binary blob data (currently numpy arrays).
- Fetch and modify data based on criteria.
- Local server setup for easy data storage and retrieval.

## Installation

```bash
pip install FinallyDataLogger
```

## Quick Start

### Starting the server

From the command line:

```bash
finallydatalogger --port 5000 --dir /path/to/storage/directory
# to make it visible on the network
finallydatalogger --host 0.0.0.0 --port 5000 --dir /path/to/storage/directory
```

### Using the client

In your Python script:

```python
import numpy as np
from finally_data_logger import DataLogger

logger = DataLogger(port=5000) #  DataLogger(server_url="http://192.168.x.x", port=5000)

# Log some data
img = np.random.rand(10,10)
# a packet of data is stored in the form of a dictionary
data = {
    "name": "test1",
    "duration": 0.3,
    "image": img
}
response = logger.log_data(data)
print(response)

# Fetch data
criteria = {'name': 'test*'}
results = logger.get_data(criteria, fetch_blob=True)
print(results)


#To delete specific data based on criteria:
criteria = {'name': 'test*'}
response = logger.delete_data(criteria)
print(response)

#To reset the entire database and remove all logged data:
logger.reset_database()


```


## API

### Server Endpoints

- `POST /log_data`: Log data to the server.
- `PUT /modify_data/<entry_id>`: Modify a data entry by its ID.
- `POST /get_data`: Fetch data based on criteria.
- `POST /delete_data`: Delete data from the server based on given criteria.
- `POST /reset_database`: Reset the entire database and remove all blobs.

### Client Methods

- `log_data(data)`: Log data to the server.
- `modify_data(entry_id, modifications)`: Modify a data entry by its ID.
- `get_data(criteria)`: Fetch data based on criteria.
- `delete_data(criteria)`: Delete data from the server based on given criteria.
- `reset_database()`: Reset the entire database and remove all blobs on the server.


## Contributing

Contributions are welcome! Please read the [CONTRIBUTING](CONTRIBUTING.md) guide for more information.

## License

[MIT License](LICENSE)

