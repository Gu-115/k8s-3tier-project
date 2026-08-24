# Kubernetes 3-Tier Application

A containerized 3-tier web application deployed on Kubernetes using Minikube.

## Architecture

```text
                    User / Browser
                          |
                          v
                 Frontend Service
                    NodePort :31130
                          |
                          v
                  Frontend Pod
                          |
                          v
                 Backend Service
                  ClusterIP :5000
                          |
                          v
                  Backend Pod
                    Flask App
