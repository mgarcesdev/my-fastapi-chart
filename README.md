# Instala Kubernetes

Instalar PI OS 64bit Lite

Si has reinstalado el SO de la raspberry pi limpia la keygen

```
ssh-keygen -R 192.168.0.37
```

Conectate por ssh

```
ssh pi@192.168.0.37
```

Actualiza la raspberri pi

```
sudo apt update && sudo apt upgrade -y
```

Prepara la rasberry pi. Indica que el cluster es único

```
sudo nano /boot/firmware/cmdline.txt
cgroup_memory=1 cgroup_enable=memory
```

Reinicia

```
sudo reboot
```

Instala ks3

```
curl -sfL https://get.k3s.io | sh -
```

Para poder usar kubectl sin sudo añade `--write-kubeconfig-mode 644`

```
sudo nano /etc/systemd/system/k3s.service

ExecStart=/usr/local/bin/k3s server --write-kubeconfig-mode 644
```

Con la nueva confiuración reinicia ks3

```
sudo systemctl daemon-reload
sudo systemctl restart k3s
```

Prueba la conexión

```
kubectl get nodes
```

# kubectl o k9s desde MAC

En el servidor copia:

```
cat /etc/rancher/k3s/k3s.yaml
```

En tu portatil pegalo en `~/.kube/config`

```
open ~/.kube/
```

Y ejecuta `k9s`

## Desplegar helm

Crea namespace

```
kubectl create namespace myapp
```

```
helm install myapp . --namespace myapp
```

```
helm upgrade myapp . -n myapp
```
