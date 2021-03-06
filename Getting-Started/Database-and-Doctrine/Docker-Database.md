
### Pull the MySQL and Phpmyadmin Docker Image
Start by pulling the appropriate Docker image for MySQL and Phpmyadmin. You can download a specific version or opt for the latest release as seen in the following command:
```bash
> docker pull mysql/mysql-server:latest
> docker pull phpmyadmin/phpmyadmin:latest
```
If you want a particular version of MySQL, replace `latest` with the version number.

![](uploads/fc34c85345f7201539cc59be3c0deab2/download-mysql-docker-image.png)
Verify the image is now stored locally by listing the downloaded Docker images:
```bash
> docker images
```

The output should include mysql/mysql-server among the listed images.
![](uploads/cb2b4be945f4dde37de12a5675e78393/Screenshot_26.png)

### Deploy the MySQL Container
Once you have the image, move on to deploying a new MySQL container with:
```bash
> docker run -p [Port]:3306/tcp --name=[image_name] -e MYSQL_ROOT_HOST='%' -e MYSQL_ROOT_PASSWORD=[password] -d mysql/mysqlserver:latest
```

- Replace [container_name] with the name of your choice. If you do not provide a name, Docker generates a random one.
- The -d option instructs Docker to run the container as a service in the background.
- Replace [image_name] with the name of the image downloaded. You might have to use the Image ID in case wsl wont find an any images. Also replace [Port] with a free port and [password] with your mysql password

Then, check to see if the MySQL container is running:
```bash
> docker ps
```
If everything went well you could see the running container:

![](uploads/5d1ca3fa255925136e03ad5e5f4aed63/Screenshot_27.png)

### Running phpMyAdmin docker container
After downloading the image, we need to run the container making sure that the container connects with the other container running mysql. In order to do so we type the following command:
```bash
> docker run --name [phpmyadmin_name] -d --link [image_name]:db -p [port]:80 phpmyadmin/phpmyadmin
```
Let’s explain the options for the command docker run.
-The options name and d has been explained in the previous section.
-The option --link provides access to another container running in the host. In our case the container is the one created in the previous section, called my-own-mysql and the resource accessed is the MySQL db.
-The mapping between the host ports and the container ports is done using the option -p followed by the port number of the host (8081) that will be redirected to the port number of the container (80, where the ngix server with the phpMyAdmin web app is installed).
-Finally, the docker run command needs the image used to create the container, so we will use the phpmyadmin image just pulled from docker hub.

If everything went well you could see the running container using the previus command:
```bash
> docker ps -a
```

![](uploads/5d1ca3fa255925136e03ad5e5f4aed63/Screenshot_27.png)

## Access PhpMyAdmin
Yes, that's all…everything is done! Easy right? You only need to open your favourite browser and type the following url: http://localhost:[yourPhpMyadminPort]/ so your instance of phpMyAdmin will show up. To access, type root as username and the password you established in the step one when running the mysql container (if you followed the tutorial the password is mypass123).

A few helpfull sites this is based on:- https://migueldoctor.medium.com/run-mysql-phpmyadmin-locally-in-3-steps-using-docker-74eb735fa1fc
- https://docs.docker.com/engine/reference/commandline/run/#publish-or-expose-port--p---expose
- https://phoenixnap.com/kb/mysql-docker-container