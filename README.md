# nspyre
Networked Scientific Python Research Environment

## Installation
#### Install MongoDB
- Download mongodb v4.2.1 (or greater) from https://www.mongodb.com/download-center/community
- Install mongodb v4.2.1 using default options
- Put the bin to the path variable (in system environment variable).  
  For a standard install this will likelly be something like C:\Program Files\MongoDB\Server\4.2\bin
  This will allow you to call mongod from the command line. and is necessary for the install.bat script to work

#### Install NSpyre
Clone the repository
```
git clone git@github.com:AlexBourassa/nspyre.git nspyre
```

Configure and start the MongoDB server (this will start two mongo server in the same replica set (one primary and one secondary)). By default these are publicly accessible on ports 27017 and port 27018 so if you are not in a secured private network, make sure to add some security configurations
```
cd nspyre
install.bat
```

Now you need to initialize the replica set. To do so enter the mongo shell and input a rs.initiate command
```
mongo
rs.initiate({_id: "NSpyreSet", members:[{_id: 0, host: 'localhost:27017'},{_id: 1, host: 'localhost:27018'}]})
quit()
```

Finally you can create and configure a conda environment.  The pip command must be run from inside the nspyre folder (where the setup.py script is located). Additionally, some part of this install may require the shell to be started with admin rigths:
```
conda create -n nspyre python = 3
activate nspyre
conda install pyzmq
pip install -e .
pip install git+https://github.com/pyqtgraph/pyqtgraph.git
```

You will also need to make sure to install lantz (most likelly a local distribution)
