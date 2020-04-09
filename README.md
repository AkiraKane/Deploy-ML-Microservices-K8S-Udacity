[![CircleCI](https://circleci.com/gh/AkiraKane/Deploy-ML-Microservices-K8S-Udacity.svg?style=svg)](https://circleci.com/gh/AkiraKane/Deploy-ML-Microservices-K8S-Udacity)

## Project Overview

In this project, you will apply the skills you have acquired in this course to operationalize a Machine Learning Microservice API. 

You are given a pre-trained, `sklearn` model that has been trained to predict housing prices in Boston according to several features, such as average rooms in a home and data about highway access, teacher-to-pupil ratios, and so on. You can read more about the data, which was initially taken from Kaggle, on [the data source site](https://www.kaggle.com/c/boston-housing). This project tests your ability to operationalize a Python flask app—in a provided file, `app.py`—that serves out predictions (inference) about housing prices through API calls. This project could be extended to any pre-trained machine learning model, such as those for image recognition and data labeling.

### Project Tasks

Your project goal is to operationalize this working, machine learning microservice using [kubernetes](https://kubernetes.io/), which is an open-source system for automating the management of containerized applications. In this project you will:
* Test your project code using linting
* Complete a Dockerfile to containerize this application
* Deploy your containerized application using Docker and make a prediction
* Improve the log statements in the source code for this application
* Configure Kubernetes and create a Kubernetes cluster
* Deploy a container using Kubernetes and make a prediction
* Upload a complete Github repo with CircleCI to indicate that your code has been tested

You can find a detailed [project rubric, here](https://review.udacity.com/#!/rubrics/2576/view).

**The final implementation of the project will showcase your abilities to operationalize production microservices.**

---

## Setup the Environment

* Create a virtualenv and activate it
* Run `make install` to install the necessary dependencies

### Running `app.py`

1. Standalone:  `python app.py`
2. Run in Docker:  `./run_docker.sh`
3. Run in Kubernetes:  `./run_kubernetes.sh`

### Kubernetes Steps

* Setup and Configure Docker locally
* Setup and Configure Kubernetes locally
* Create Flask app in Container
* Run via kubectl

## Application Overview
The Python application is a pre-trained `sklearn` model that can be used to predict housing prices in Boston. A sample script to use the application is [included as `make_prediction.sh`](./make_prediction.sh).

```shell
$ ./make_prediction.sh
```

## Run the application locally
A `Makefile` is included that will set up a virtual environment with all the dependencies necessary for the project.
To setup the `venv`:
```shell
$ make setup
```
This will create a virtual environment in `~/.devops` and source it to activate it. You can deactivate by running the command:
```shell
$ deactivate
```
All that is left is to install the dependencies and start the application:
```shell
$ make install
$ python app.py
```

## Run the application in a Docker container
The [included `run_docker.sh` script](./run_docker.sh) is all that is needed to get a Docker container running with the application. It will create an image (if one does not exist already) and start a container.
```shell
$ ./run_docker.sh
```
It will start the container and attach the current terminal to it to be able to see the log output. In a separate terminal, run the `make_prediction` script to see a prediction and the log output.
```shell
$ ./make_prediction.sh
```

### Running the application in a Kubernetes cluster
To start a Kubernetes cluster of the application, run the following command and use the [included `run_kubernetes.sh` script](./run_kubernetes.sh):
```shell
$ minikube start
$ ./run_kubernetes.sh
```
The script will attempt to start port-forwarding automatically; however, the pod takes time to load. After the pod has loaded, you can run the script again to start port-forwarding and interact with the application as above (in another terminal, run `make_prediction.sh`).

After you are finished testing the cluster, use `CTRL+C` to send a `SIGINT` to the port forwarding, stop the `minikube` and (optionally) delete the resources.
```shell
$ minikube stop
$ minikube delete
```
