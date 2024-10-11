
# Instructions

    git clone https://github.com/techmaniack/docker-local-cache.git
    cd docker-local-cache
    docker-compose up -d
    
Once the registry container is up and listening in port 5000 you must set the `registry-mirrors` key to `localhost:5000` and restart docker service.

This is taken from the [docker documentation] (https://docs.docker.com/docker-hub/mirror/ 'link for local docker mirror')
>Configure the Docker daemon
>Either pass the --registry-mirror option when starting dockerd manually, or edit /etc/docker/daemon.json and add the registry-mirrors key and value, to make the change persistent.
>
>>{
>>  "registry-mirrors": "http://localhost:5000"
>>}
>Save the file and reload Docker for the change to take effect.

# Example
First pull for mongo image takes 71 seconds while next pull is complete in 19 seconds.

    $ time docker pull mongo
    Using default tag: latest
    latest: Pulling from library/mongo
    ...
    Status: Downloaded newer image for mongo:latest
    docker pull mongo  0.17s user 0.07s system 0% cpu 1:11.08 total

     $ docker rmi mongo
    Untagged: mongo:latest
    Untagged: mongo@sha256:c4bc4644b967a4b58022a79cf5c9afcd25ed08180c958a74df57b7753cfc8649
    ...
    Deleted: sha256:5d924e3b1efdcda770bc33e6d7563f5ca2411dcc6b7368c8a30356bed474ae5a

     $ time docker pull mongo
    Using default tag: latest
    latest: Pulling from library/mongo
    ...
    Status: Downloaded newer image for mongo:latest
    docker pull mongo  0.13s user 0.05s system 0% cpu 19.296 total
