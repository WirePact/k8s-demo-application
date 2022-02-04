# Kubernetes Demo Application for Distributed Authentication Mesh

This repository represents a demo application that can be used to showcase the Distributed Authentication Mesh.
The application consists of an API that uses Basic Authentication and a "frontend" application that uses OIDC with "Keycloak".

To install the application, follow these steps:

- Get a Kubernetes cluster somehow (Docker Desktop, minikube or a "real" cluster)
- If you are using a local cluster you'll need some host entries (wirepact-api.localhost, wirepact-app.localhost, and keycloak.localhost)
- If you are using a real cluster, adjust the ingress.yaml files for the app/keycloak and api
- Install the prerequisities (WirePact Operator and NGINX Ingress Controller)
- Install the application

All installations shall be done with ["Kustomize"](https://kustomize.io/).

It takes quite a while for Keycloak to start up, but the applications will correctly start up, as soon as Keycloak is up and running.

After everything runs, you may connect to the app and use the test user to login. When you press the "Call API" button, you should receive data from the API. As a test, you may delete the mesh-participant entity for the API. The API will be accessible, but only with Basic Auth credentials.

The credentials are as follows:

- Test User: username `test` password `test`
- Keycloak Admin: username `admin` password `admin`
- Basic Auth Credentials: username `user` password `pass`
