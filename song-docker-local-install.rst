.. _docker_for_song_ref:

=============================
Docker for SONG   -   Adjustments for local install
=============================
..
    .. image:: ../../song-docker/song-logo.gif
       :align:  center
       :scale: 60%

Introduction
========================

.. warning::
This page is aimed to describe the small adjustments a new user has to apply in a local Vm to install SONG.
We Recommend to apply the instructions on `SONG for Docker https://github.com/overture-stack/SONG/tree/develop/song-docker`


Adjustments
--------------------------
* For new started VMs we should make sure that docker Daemon is started.

.. code-block:: bash

    systemctl enable docker.service
    systemctl start docker.service
    
  
*  Minio service ``(distributed object storage server)``:
   A warning message on minio service may appears asking for version update.
   on ``docker-compose.yml`` file change the build image name.
   
.. code-block:: bash

    object-storage:
     image: minio/minio:RELEASE.2019-01-10T00-21-20Z
     
*  Auth service ``(SimpleAuth)``: 
In this docker config the ``(SimpleAuth)`` is applying as a lightweight oAuth server provider. 
and to correct the ``(auth_data)`` issue you may see on ``docker-compose up``:
  1. On auth folder, create an empty ``auth_data`` sub folder.
  
  .. code-block:: bash
    
    mkdir auth_data    
    
    
  2. On auth service Dockerfile file:

  .. code-block:: bash

    ADD auth_data $AUTH_DATA
     
* Run the build, and start all services.
You may have probably need to do a `!!! CLEAN UP` of your docker images and containers created at first try.

``DONT USE If you want to clean cache and intermediates images, containers individually``

.. code-block:: bash

  docker rm $(docker ps -a -q) -f			
  docker rmi $(docker images -q) -f			
  sudo service docker stop			
  sudo rm -rf /var/lib/docker			
  sudo service docker start
  
  docker-compose up




Issues
=============
If you encounter any issues, please report them `here <https://github.com/overture-stack/SONG/issues>`_

License
=============
Copyright (c) 2018. Ontario Institute for Cancer Research

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as
published by the Free Software Foundation, either version 3 of the
License, or (at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.
