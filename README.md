# MyDrive

Technologies in my project:
1. Java
2. Spring Framework
3. ConfigServer
4. MongoDB
5. PostgreSQL
6. Vsftpd (FTP Server)
7. Docker
8. Kafka
9. Monitoring:
	1. Prometheus 
	2. Grafana

Links to code:
1. LoginAndRegister - [https://github.com/Daniel200555/LoginAndRegister](https://github.com/Daniel200555/LoginAndRegister)
2. FileFtpMicroservice - [https://github.com/Daniel200555/FileFtpMicroservice](https://github.com/Daniel200555/FileFtpMicroservice)
3. FileMongoMicroservice - [https://github.com/Daniel200555/FileMongoMicroservice](https://github.com/Daniel200555/FileMongoMicroservice)
4. Docker-Compose - [https://github.com/Daniel200555/runner](https://github.com/Daniel200555/runner)

Structure of microservices in my project:
1. LoginAndRegister - this is microservice which create new user account and save new unique nickname, save email of new user and new **ENCODING** password in PostgreSQL database. After that register request send to FileFtpMicroservice message to create folder with unique nickname of user and also register function send to FileMongoMicroservice message to create body of user with unique name for to save body of files.
2. FileFtpMicroservice - this is microservice which enabled to ftp server and save in user folder, folders and files which user want to save in MyDrive site, delete this files and stream this files, all this function works by getting kafka messages from LoginAndRegister and FileMongoMicroservice.
3. FileMongoMicroservice - this is microservice which enabled to MongoDB which save body of files which save files in FTP server, delete and rename files.
4. ConfigServer - this is a microservice which send for all microservices configuration files from GitHub configuration repository (https://github.com/Daniel200555/newconfig)
5. Server - this is a (Eureka Server) central microservice which by link can to show status about all microservices which enaable to this microservice like (EurekaClient) and via this microservice Config Server can to send for all microservices configaration files (.xml).

The next version of my project:
1. I will finish my Front-End side
2. Add Elastic Search + Kibana
3. Create new microservice which will enabled to Redis (Cash Database)
4. Add share function of files or folders
5. Run microservices via Kubernetes (I want to try create replications for microservice) + LoadBalancer

Diagram of structure my projects:

```mermaid
flowchart TB
	id1(Angular CLI)
	id2(LoginAndRegister)
	id3(FileFtpMicroservice)
	id4(FileMongoMicroservice)
	id5(Kafka)
	id6(MongoDB)
	id7(FTP server)
	id8(Prometheus)
	id9(Grafana)
	id10(PostgerSQL)
	id1 == Register ==> id2
	id3 == Save/Delete File ==> id7
	id2 == Save User Details ==> id10
	id4 == Save Body Of Files ==> id6
	id2 == Create Folder ==> id5 == Send Message ==> id3 == Save Body ==> id5 == Send Message ==> id4
	id1 == Request ==> id4
	id4 == Create/Delete ==> id5 == Send Message ==> id3
	id10 -.-> id8 -.-> id9
	
```

**I RUNNED ALL DATABASES AND KAFKA WITH GRAFANA IN VIRTUAL MASHINE**
