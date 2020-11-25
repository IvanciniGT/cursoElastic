docker run -d --name mielastic -p 8080:9200 -e "discovery.type=single-node" elasticsearch:7.9.3

RAM <<<<< Tomar un trozo de HDD para usarlo como RAM


ElasticSearch
---->>>> Lucenes
        ----> Shard o Fragmento de un Indice 
                Shard ---> Fichero(s) en el HDD
                     Lucene va a subir un shard a la RAM cuando se use mucho

# Procedimiento instalación de ElasticSearch
## Requisitos a nivel de SO
### Desactivar el swap

Deshabilitar el Swap temporalmente (Solo en la sesión actual)
sudo swapoff -a

Hacer el cambio permanentemente (para la próxima vez)
sudo vim /etc/fstab

sudo su -  # Nos convierte en adminitrador de la maquina

### Ampliar número máximo de ficheros simultaneamente abiertos
ulimit -n 65535

### Ampliar la memoria virtual del SO
sysctl -w vm.max_map_count=262144   ### TEMPORALMENTE

exit ### Dejar de ser adminitrador

Para hacerlo definitivo, tenemos que modificar el fichero /etc/sysctl.conf
sudo su -
echo "vm.max_map_count=262144" >> /etc/sysctl.conf
exit

# Instalar ElasticSearch como contenedor

## Paso 1: Descargar la imagen del contenedor

docker pull elasticsearch:7.9.3

## Paso 2: Generar el contenedor desde la imagen descargada

docker container create --name mielastic -p 8080:9200 -e "discovery.type=single-node" elasticsearch:7.9.3

## Paso 3: Arrancar el contenedor

docker start mielastic

### Parar elasticSearch

### Borrar el contenedor que hemos creado

docker rm mielastic

### Borrar la imagen del contenedor
docker images <<<< De aqui saco el ID
docker rmi <ID: 1ab13f928dc8>

### Descargar una imagen de elastic, generar un contenedor y arrancarlo
docker run -d --name mielastic -p 8080:9200 -e "discovery.type=single-node" elasticsearch:7.9.3