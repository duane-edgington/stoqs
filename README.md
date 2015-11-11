Spatial Temporal Oceanographic Query System
-------------------------------------------

[![Build Status](https://travis-ci.org/stoqs/stoqs.svg)](https://travis-ci.org/stoqs/stoqs)
[![Coverage Status](https://coveralls.io/repos/stoqs/stoqs/badge.svg?branch=master&service=github)](https://coveralls.io/github/stoqs/stoqs?branch=master)
[![Requirements Status](https://requires.io/github/stoqs/stoqs/requirements.svg?branch=master)](https://requires.io/github/stoqs/stoqs/requirements/?branch=master)
[![Code Health](https://landscape.io/github/stoqs/stoqs/master/landscape.svg?style=flat)](https://landscape.io/github/stoqs/stoqs/master)

STOQS is a geospatial database and web application designed to give oceanographers
efficient integrated acccess to *in situ* measurement and *ex situ* sample data.
See http://www.stoqs.org.

##### Getting started with a STOQS development system 

First, install [Vagrant](https://www.vagrantup.com/) and and [VirtualBox](doc/instructions/VirtualBox.md)
&mdash; there are standard installers for Mac, Windows, and Linux. Then create an empty folder off your 
home directory such as `Vagrants/stoqsvm`, open a command prompt window, cd to that folder, and enter these 
commands:

    curl "https://raw.githubusercontent.com/stoqs/stoqs/master/Vagrantfile" -o Vagrantfile
    curl "https://raw.githubusercontent.com/stoqs/stoqs/master/provision.sh" -o provision.sh
    vagrant up --provider virtualbox

The `vagrant up` command takes a few hours to provision and setup a complete CentOS 7 
STOQS server that also includes all the data science tools bundled in packages such as
Anaconda.  All connections to this virtual machine are 
performed from the the directory you installed it in; you must cd to it (e.g. `cd
~/Vagrants/stoqsvm`) before logging in with the `vagrant ssh -- -X` command.  After 
installation finishes log into your new virtual machine and test it:

    vagrant ssh -- -X
    cd ~/dev/stoqsgit && source venv-stoqs/bin/activate
    export DATABASE_URL=postgis://stoqsadm:CHANGEME@127.0.0.1:5432/stoqs
    ./test.sh CHANGEME

In another terminal window start the development server (after a `cd ~/Vagrants/stoqsvm`):

    vagrant ssh -- -X
    cd ~/dev/stoqsgit && source venv-stoqs/bin/activate
    export DATABASE_URL=postgis://stoqsadm:CHANGEME@127.0.0.1:5432/stoqs
    stoqs/manage.py runserver 0.0.0.0:8000 --settings=config.settings.local

Visit your server's STOQS User Interface using your host computer's browser:

    http://localhost:8000

More instructions are in the doc/instructions directory &mdash; see [LOADING](doc/instructions/LOADING.md) 
for how to load your own data and [CONTRIBUTING](doc/instructions/CONTRIBUTING.md) for how to share your work.
See example [Jupyter Notebooks](stoqs/contrib/notebooks) that demonstrate specific analyses and 
visualizations that cannot be accomplished in the STOQS User Interface.
Visit the [STOQS Wiki pages](https://github.com/stoqs/stoqs/wiki) for updates and links to presentations.
The [stoqs-discuss](https://groups.google.com/forum/#!forum/stoqs-discuss) list in Google Groups is also 
a good place to ask questions and engage in discussion with the STOQS user and developer communities.

Supported by the David and Lucile Packard Foundation, STOQS undergoes continual development
to help support the mission of the Monterey Bay Aquarium Research Institue.  If you have your
own server you will occaisionally want to get new features with:

    git pull
    ./setup.sh

If you use STOQS for your research please cite this publication:

> McCann, M.; Schramm, R.; Cline, D.; Michisaki, R.; Harvey, J.; Ryan, J., "Using STOQS (The spatial 
> temporal oceanographic query system) to manage, visualize, and understand AUV, glider, and mooring data," 
> in *Autonomous Underwater Vehicles (AUV), 2014 IEEE/OES*, pp.1-10, 6-9 Oct. 2014
> doi: 10.1109/AUV.2014.7054414