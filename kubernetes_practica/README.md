# Despliegue de Aplicación en Kubernetes con Base de Datos Utilizando Helm

Este proyecto tiene como objetivo desplegar una aplicación junto a una base de datos MySQL en un clúster de Kubernetes, utilizando Helm como herramienta de gestión. Se asegura la accesibilidad, escalabilidad y persistencia de datos en todo momento. Además, se manejan las configuraciones sensibles de forma segura y se garantiza la alta disponibilidad (HA) de la aplicación.

## Requisitos Previos
Herramientas necesarias:
Docker Desktop: Para ejecutar contenedores localmente.
Minikube: Para crear un clúster local de Kubernetes.
Kubectl: Para interactuar con Kubernetes.
Helm: Para gestionar y desplegar los charts en Kubernetes.
Visual Studio Code (o cualquier editor de texto): Para editar los archivos YAML y trabajar en el código.
MySQL Workbench (opcional): Para conectarse y gestionar la base de datos MySQL.

## Instalación de las herramientas:
Instalar Docker Desktop: Puedes descargarlo desde Docker Desktop.
Instalar Minikube:
brew install minikube
O consulta la guía oficial para otros sistemas operativos.

Instalar Kubectl:
brew install kubectl

Instalar Helm:
brew install helm

Configuración del clúster
Una vez que hayas instalado las herramientas, inicia Minikube y configura el clúster:
minikube start

Verifica que el clúster esté en funcionamiento:
kubectl get nodes

## Estructura del Proyecto
A continuación se presenta la estructura del proyecto. Asegúrate de crear estos archivos en la ruta correcta.



kubernetes_practica/
│
├── Chart.yaml
├── values.yaml
├── templates/
│   ├── deployment.yaml
│   ├── statefulset.yaml
│   ├── service-app.yaml
    ├──service-db.yaml
│   ├── secret.yaml
│   └── ingress.yaml
    └──configmap.yaml
    └──hpa.yaml
└── README.md

## Pasos Detallados para Desplegar la Aplicación
1. Crear el Chart de Helm
Crea un nuevo chart de Helm para la aplicación:
helm create my-helm-chart
cd my-helm-chart
2. Configurar Namespaces
En Kubernetes, los namespaces te permiten organizar tus recursos. En esta práctica, crearemos dos namespaces: uno para la base de datos y otro para la aplicación.
Crear los namespaces:
kubectl create namespace db-namespace
kubectl create namespace app-namespace
3. Configurar Secret. Crea el secret.yaml, copia el código en tu documento
Para aplicar este secret en los namespace ejecuta:
kubectl apply -f secret.yaml -n db-namespace
kubectl apply -f secret.yaml -n app-namespace
4. Configurar StatefulSet para la Base de Datos, copia el código en tu documento
Aplica este StatefulSet en el namespace db-namespace:
kubectl apply -f statefulset.yaml -n db-namespace
5. Configurar Deployment para la Aplicación
Despliega la aplicación con un Deployment, asegurando que sea escalable y manejable, copia el código en tu documento
Aplica este deployment en el namespace app-namespace:
kubectl apply -f deployment.yaml -n app-namespace
6. Configurar Servicios (ClusterIP)
Los servicios en Kubernetes permiten la comunicación entre los pods y la exposición de la aplicación al exterior, copia el código en tu documento
Aplica estos servicios:
kubectl apply -f service-db.yaml -n db-namespace
kubectl apply -f service-app.yaml -n app-namespace
7. Configurar Ingress (Opcional)
Si quieres exponer tu aplicación fuera del clúster, puedes usar un Ingress, copia el código en tu documento
Aplica el Ingress:
kubectl apply -f ingress.yaml -n app-namespace
8. Verificar el Despliegue
Verifica que todos los recursos se hayan desplegado correctamente:
kubectl get all -n db-namespace
kubectl get all -n app-namespace


