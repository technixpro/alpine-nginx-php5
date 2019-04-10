Building the Image:
I am primarily using docker swarm, so I am building the image, and pushing to a private registry:

$ docker build -t registry.gitlab.com/<user>/<repo>/alpine:php5 .
$ docker push registry.gitlab.com/<user>/<repo>/alpine:php5

$ docker service create \
--name php-app \
--network appnet \
--replicas 3 \
--with-registry-auth registry.gitlab.com/<user>/<repo>/alpine:php5

For a Container from the Image on the Host:

docker run -itd --name php-app -p 80:80 registry.gitlab.com/<user>/<repo>/alpine:php5

Test the Web App:

$ curl -XGET http://127.0.0.1:80/
The word is: foo
