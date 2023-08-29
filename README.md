# Distributed Streaming with Python and Kafka
Sistema Distribuido de streaming de video usando kafka:
Pasos para su utilización:
1. Verificar si tenemos instalado java:
   java -version
2. Instalar zookeperd:
   sudo apt-get install zookeeperd
3. verificar si zookeper se instalo correctamente:
   ZooKeeper se iniciará automáticamente como un demonio configurado en el puerto 2181. Asegurémonos de que se esté ejecutando con:
   netstat -ant | grep :2181
4. La salida del comando anteior nos dara algo como esto:
   tcp6       0      0 :::2181           :::*         LISTEN
5. Descargamos Kafka:
   wget https://archive.apache.org/dist/kafka/3.0.0/kafka_2.13-3.0.0.tgz
6. Creamos un directorio donde se va a istalar Kafka:
   sudo mkdir /opt/Kafka
7. Descomprimimos el archivo de kafka descrgado en nuestro directorio:
   sudo tar -xvf kafka_2.13-3.0.0.tgz -C /opt/Kafka/
8. Ingresamos a nuestro directorio y a la carpeta que se creo de kafka:
   cd /opt/Kafka/kafka_2.13-3.0.0
9. Corremos kafka para poderlo utilizar con nuestra app de Streaming
    sudo  bin/kafka-server-start.sh config/server.properties
Con esto tenemos nuestro servicio de Kafka levantado.

Ahora vamos con nuestra app de Streaming
1. Lo primero que vamos a hcer es clonar el repositorio en nuestra pc con el comando:
   git clone https://github.com/kmhoran/DistributedStreamingWithPythonAndKafka.git  
2. Activamos nuestro entorno virtual:
   virtualenv env                                
. env/bin/activate
No olvidar que debemos instalar pyhton:
sudo apt install python3 python3-venv         
sudo apt install virtualenv python3-virtualenv
4. Dentro de nuestro entorno virtual instalamos lo siguiente:
   pip install kafka-python opencv-contrib-python Flask
5. Listo con kafka levntado procedemos a correr nuestro cliente y nuestro servicio de streaming:
   entramos en la carpeta de consumer y ejecutamos el archivo consumer.py:
   pyhton consumer.py
   Esto va a levantar un servicio en el puerto 5000:
   si todo esta correcto observaremos lo siguiente en nuestra consola:
   >python consumer.py
 * Serving Flask app 'consumer'
 * Debug mode: on
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:5000
 * Running on http://192.168.182.128:5000
Press CTRL+C to quit
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 139-595-409
6. Luego de esto procedemos a levatar el servicio de streaming:
entramos en la carpeta de producer y corremos el archivo producer.py:
python producer.py ../../../../Descargas/videoperro.mp4
se puede observar que yo envio un video desde mi carpeta de descragas esto se puede variar dependiendo de donde tengamos el video, si no se pone la ruta lo que hace al app es utilizar directamete la camara del equipo, esto haria que se capture las imagenes de la cmara y se haga el stream, por el mometo utilizamos solo un video.
Si todo esta correcto vereos lo siguiente:
❯ python producer.py ../../../../Descargas/videoperro.mp4
publishing video...

Y listo en nuestro navegador en la ruta:
http://127.0.0.1:5000 se puede observar el streaming

Derechos de autor:
Source code for a project detailed [here](https://medium.com/@kevin.michael.horan/distributed-video-streaming-with-python-and-kafka-551de69fe1dd) in my blog.
