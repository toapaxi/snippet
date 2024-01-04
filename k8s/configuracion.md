# Configuracion para acceder
Se debe agregar los archivos de configuracion para poder acceder a los cluster.

Para mi efecto cd ~/.kube/clusters/

En el terminal se de configurar lo siguiente:
### BASH
Abre el archivo ~/.bashrc en un editor de texto:
```bash
nano ~/.bashrc
```
Agrega la línea al final del archivo:
```bash
export KUBECONFIG=$(echo /home/muerte/.kube/clusters/* | tr ' ' ':')
```
### Zsh
Abre el archivo ~/.zshrc en un editor de texto:
```bash
nano ~/.zshrc
```
Agrega la línea al final del archivo:
```bash
export KUBECONFIG=$(echo /home/muerte/.kube/clusters/* | tr ' ' ':')
```

### Fish:
Abre el archivo ~/.config/fish/config.fish en un editor de texto:
```bash
nano ~/.config/fish/config.fish
```
Agrega la línea al final del archivo:
```bash
set -x KUBECONFIG (echo /home/muerte/.kube/clusters/* | tr ' ' ':')
```
