## Enfoque de la práctica
Esta práctica debe ser implementada, no solo diseñada.
El objetivo es aplicar DevSecOps de manera práctica, integrando:
        - - Front-end
        - - Back-end
        - - Inicio de sesión seguro
        - - Arquitectura de microservicios
        - - Automatización CI/CD con seguridad embebida
     

# 1. Adición del Front-end

[ Front-end ]
     |
     | Login / JWT
     v
[ users-service ]
     |
     | JWT
     v
[ api-gateway ]
     |
     v
[ academic-service ]


## Integración DevSecOps (obligatoria)
El Front-end y el inicio de sesión deben estar cubiertos por el pipeline DevSecOps existente:

- SAST: análisis del código de autenticación y manejo de inputs.
- SCA: análisis de dependencias relacionadas con seguridad.
- DAST: pruebas de acceso no autorizado a endpoints protegidos.

**El login no se asume seguro, se valida automáticamente

## Propósito de esta extensión
Consolidar una visión end-to-end DevSecOps, donde:
 - El diseño,
 - La seguridad,
 - La automatización,
  Y la experiencia de usuario,
se integran desde las primeras etapas del desarrollo.

## Pipeline 
Commit / Pull Request
   ↓
Tests automatizados
   ↓
SAST (Semgrep)
   ↓
Build (Docker)
   ↓
SCA (dependencias)
   ↓
Deploy automático
   ↓
DAST (aplicación en ejecución)

## Docker Compose
docker-compose down
docker-compose up --build

## Estructura del Pipeline
Push / Pull Request
   ↓
Install dependencies
   ↓
Tests (backend + frontend)
   ↓
SAST (Semgrep)
   ↓
Build Docker images
   ↓
SCA (Trivy)
   ↓
docker-compose up
   ↓
Smoke tests

## Kubernetes
kubectl apply -f k8s/users-service/
kubectl apply -f k8s/academic-service/
kubectl apply -f k8s/api-gateway/

kubectl get pods
kubectl get services

# Correr api-gateway
minikube service api-gateway
minikube start
# Trabajar con Docker
eval $(minikube docker-env -u)
# Trabajar Docker dentro Kubernetes
1. minikube start --driver=docker
   eval $(minikube docker-env)
2. minikube status
3. kubectl config current-context
4. kubectl get nodes
## Construir las imágenes
docker build -t frontend:latest ../frontend
kubectl get pods -n backend
docker build -t users-service:latest ../backend/users-service

## Desplegar en Kubernetes
kubectl apply -f k8s/namespace.yaml
kubectl apply -f k8s/users-service/
kubectl apply -f k8s/academic-service/
kubectl apply -f k8s/api-gateway/
kubectl apply -f k8s/frontend/

# eliminar cluster
minikube delete


minikube start
eval $(minikube docker-env)

docker build -t users-service backend/users-service
docker build -t academic-service backend/academic-service
docker build -t api-gateway backend/api-gateway
docker build -t frontend frontend

kubectl apply -f k8s/


## Estructura
```
└── 📁practica2
    └── 📁.github
        └── 📁workflows
            ├── devsecops.yml
    └── 📁backend
        └── 📁academic-service
            └── 📁__tests__
                ├── health.test.js
            └── 📁src
                └── 📁controllers
                    ├── courses.controller.js
                └── 📁facades
                    ├── academic.facade.js
                └── 📁middleware
                    ├── auth.middleware.js
                └── 📁routes
                    ├── courses.routes.js
                └── 📁services
                    ├── courses.service.js
                ├── app.js
                ├── server.js
            ├── .dockerignore
            ├── .env
            ├── .env.example
            ├── Dockerfile
            ├── package-lock.json
            ├── package.json
        └── 📁api-gateway
            └── 📁__tests__
                ├── health.test.js
            └── 📁src
                ├── server.js
            ├── .dockerignore
            ├── .env
            ├── .env.example
            ├── Dockerfile
            ├── package-lock.json
            ├── package.json
        └── 📁semgrep-rules
            ├── hardcoded-secret.yaml
            ├── no-eval.yaml
            ├── unvalidated-input.yaml
        └── 📁users-service
            └── 📁__tests___
                ├── health.test.js
            └── 📁src
                └── 📁controllers
                    ├── auth.controllers.js
                └── 📁facades
                    ├── auth.facades.js
                └── 📁routes
                    ├── auth.routes.js
                └── 📁services
                    ├── auth.services.js
                ├── app.js
                ├── server.js
            ├── .dockerignore
            ├── .env
            ├── .env.example
            ├── Dockerfile
            ├── package-lock.json
            ├── package.json
        ├── docker-compose.yml
        ├── Readme.md
    └── 📁frontend
        └── 📁__tests__
            ├── health.test.js
        └── 📁public
            ├── vite.svg
        └── 📁src
            └── 📁assets
                ├── react.svg
            └── 📁pages
                ├── Courses.jsx
                ├── Login.jsx
            └── 📁services
                ├── api.jsx
            └── 📁styles
                ├── login.css
            ├── App.css
            ├── App.jsx
            ├── index.css
            ├── main.jsx
        ├── .dockerignore
        ├── .env
        ├── .env.example
        ├── cypress.config.js
        ├── Dockerfile
        ├── eslint.config.js
        ├── index.html
        ├── package-lock.json
        ├── package.json
        ├── README.md
        ├── vite.config.js
    └── 📁k8s
        └── 📁academic-service
            ├── deployment.yaml
            ├── service.yaml
        └── 📁api-gateway
            ├── deployment.yaml
            ├── service.yaml
        └── 📁frontend
            ├── deployment.yaml
            ├── service.yaml
        └── 📁users-service
            ├── deployment.yaml
            ├── service.yaml
        ├── namespace.yaml
    ├── .gitignore
    ├── devesecops-python.yml
    └── Readme.md
```