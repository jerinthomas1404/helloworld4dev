# helloworld4dev
---
> A basic Todo App to explore the language of Go

What did I learn?

> - [Chi](https://go-chi.io/) 
This is a light weight router for building Go HTTP services. It is build on context package to handle signaling,cancelation and other.

> - [renderer](https://github.com/thedevsaddam/renderer) 
This is light weight rendering package for Go. This has been used to render the .tpl files (Template files).

> - [mgo](https://pkg.go.dev/gopkg.in/mgo.v2) 
This is a MongoDB driver for Go. It deals with connecting with MongoDB Session, executing various commands on the database.

---
#### Code dissection
1. Creation of DB model. 
In order to interact with DB created a Todo Model, as MongoDB stores data in BSON.
2. Creation of JSON model
The frontend(tpl files) receives data in JSON format, there the BSON data needs to encoded to JSON vice-versa.
3. Init function
Here we're creating a new session with MongoDB cluster, this session will enable communication and connects with the particular collection. 
In this section we also initialze a renderer as well.
4. main function
Creates a new router using chi package and adds a logger middleware to it. The root "/" *GET* request is handled by the home handler, also we mount "/todo" router to main router.
5. Creating a http Server, serving it using a go routine. Inorder to gracefully stop the server we're using a unbuffered channel (size 1) **stopChan** of type os.Signal, as we're waiting for one signal.
6. With help of signal package, the signal is relayed to channel. The main go routine waits for this signal(^C) to execute from line 215 to 220.
7. With the help of context package, we send a cancellation context to the server to shut it down.
8. All the other functions is to fetch/delete/update data from MongoDB database.





