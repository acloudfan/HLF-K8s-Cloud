By: Raj   raj@acloudfan.com
Content: Part of a course "Hyperledger Fabric Network Setup & Design"
More information: http://acloudfan.com    http://bcmentors.com

PS: 
- You cannot build images from the provided Dockerfile(s) as the dependencies are missing
- Please take a look at my course on getting more information on how to create images

Notes:
======
Kubernetes require the applications to be provided in Docker images

The Docker images are pulled by the K8s runtime from the Registry
- Registry can be local or remote 
- Registry can be public or private

For testing, developers commonly use the public DockerHub.com registry

When developing the images it is easier to use local Registry as it would
save you the "push" step. 

Minikube = a Kubernetes development environment is commonly used for quick
development and testing of the images locally. 
