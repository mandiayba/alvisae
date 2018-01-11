# AlvisAE

AlvisAE is an editor that facilitates the annotation of text documents with the goal of extracting knowledge.

This project containsAlvisAE two main components: an Annotation Editor (alvisae-ui)  and an Web Service (alvisae-ws). 

## Try it...

> Note that, you must have [docker](https://www.docker.com/) installed on your computer

1. Run the following command
```
sudo docker run -d --rm --name alvisae.ws -p 8080:8080 -p 5432:5432  bibliome/alvisae:1.0.0
``` 

2. Test Using Web Interface
* Go to [http://localhost:8080/alvisae/alvisae-ws/AlvisAE/](http://192.168.56.101:8080/alvisae/alvisae-ws/AlvisAE)
* Sing-In with login *annotator1* and password *annotator1*


3. Test Using REST calls

The web service implement the [aero protocol](https://github.com/openminted/omtd-aero). Here are the calls avalaible to the users. 

#### Projects
##### List Projects
```sh
curl -u aae_root:Tadmin -w "%{http_code}" http://localhost:8080/alvisae-ws/api/projects
```
##### Create a project named with the creator named Ba
```sh
curl -u aae_root:Tadmin -w "%{http_code}" -X POST -d 'name=new project&creator=Ba' http://localhost:8080/alvisae-ws/api/projects
```
##### Delete the project 1
```sh
curl -u aae_root:Tadmin -w "%{http_code}" -X DELETE http://localhost:8080/alvisae-ws/api/projects/1
```

##### JSON export
```sh
curl -u aae_root:Tadmin -w "\n%{http_code}\n" http://localhost:8080/alvisae-ws/api/projects/5/export.zip
```

##### JSON import
```sh
```

#### Documents
##### List documents of project 4
```sh
curl -u aae_root:Tadmin -w "%{http_code}" http://localhost:8080/alvisae-ws/api/projects/4/documents
```
##### Create a document into the project 1
```sh
curl -u aae_root:Tadmin -w "%{http_code}" -X POST -d 'name=new document&format=text&content=some content&creator' http://localhost:8080/alvisae/api/projects/1/documents
```
##### Delete Document
```
curl -u aae_root:Tadmin -w "%{http_code}" -X DELETE http://localhost:8080/alvisae-ws/api/projects/1/documents/3
```

#### Annotations
##### List Annotations
```
curl -u aae_root:Tadmin -w "%{http_code}" http://localhost:8080/alvisae-ws/api/projects/4/documents/4/annotations
```
##### Create Annotation
```shh
curl -u aae_root:Tadmin -w "%{http_code}" -X POST \
-d 'format=json&content=[{"id":"946b5154-6b47-4e72-86cb-9f9096e7475f","propes":{},"text":[[0,28]],"type":"","kind":0}]&state=NEW' \
http://localhost:8080/alvisae-ws/api/projects/4/documents/4/annotations/1
```
##### Delete Annotation
```shh
curl -u aae_root:Tadmin -w "%{http_code}" -X DELETE http://localhost:8080/alvisae-ws/api/projects/4/documents/4/annotations/1
```

