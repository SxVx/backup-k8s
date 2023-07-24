# Anotaciones de uso con minukube

## Crear imagen de docker y resolver problemas de minikube

En resumidas cuentas es hacer una imagen del proyecto que elaboraste, se necesita hacer una imagen para que k8s pueda hacer el cluster.

Por lo tanto **minikube no tiene** el contexto de tu entorno local, si tu creas una imagen del proyecto minikube no la va encontrar aun que en el manifiesto de k8s tenga la opción de buscar en tu local:

```yaml
spec:
  containers:
  - name: backend
    image: image-mio
    imagePullPolicy: IfNotPresent
```

Para hacer que minikube reconozca la imagen debemos darle el contexto, y lo hacemos de la siguiente manera:

```bash
  # Comandos de la terminal
  eval $(minikube docker-env)
  minikube image load image-mio
```

## Consultar en el navegador
Recuerda que para ver el pod que este corriendo tienes que poner en el navegador la ip del cluster, en este caso la de minikube

```bash
  minikube ip
```

Si el servicio lo dejaste con un port fijo, es decir, tu se lo asignaste recuerda consultar el port del servicio

```bash
  kubectl get svc
```

**Nota:** Recuerda el servicio que quieras consultar debe de ser NodePort y la url del navegador debe ser http o no existir la definición del protocolo

**Pegar el puerto del pod a nuestro equipo**
Esto sirve para poder consultarlo desde nuestra maquina, esto en caso de no tener una ip publica el servicio o el pod

```bash
  kubectl port-forward nombre-pod 8080:80
  # el primer puerto es de nuestra pc y el otro es el del pod
```