# Helm

- Añadir repositorio

> helm repo add [repo_name] [repo_url]

- Instalar un deployment

> helm install [nombre_local] [repo_name]/[chart] --version [version] --namespace [namespace_to_install]

Para indicar un archivos de valores "-f [archivo].yml"

- Ver valores para instalar en el deployment

> helm show values [repo_name]/[chart]


