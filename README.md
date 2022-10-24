# Tarea2-Taller de redes y servicios

## Información general
En el siguiente documento, de deja registro de los pasos utilizados para establecer la conexion cliente-servidor en el protocolo MDNS.
Primero se debe tener instalado docker en la consola de ubuntu

## Primeros pasos

Para el Servidor se usa el siguiente repositorio: (https://github.com/mafintosh/multicast-dns) y el siguiente dockerfile (https://github.com/mygeone2/softwares-dockerfiles-TDR-2022-2/blob/main/MDNS/multicast-dns.Dockerfile) 

Para el Cliente se usa el siguiente repositorio: (https://github.com/rosetta-home/mdns) y el siguiente dockerfile (https://github.com/mygeone2/softwares-dockerfiles-TDR-2022-2/blob/main/MDNS/rosetta.Dockerfile) 

Se deben copiar los dockerfile en carpeta Cliente y Servidor, segun corresponda.
Luego, para crear las imagenes e iniciar los contenedores, utilizando las siguientes lineas de codigo, para el servidor: 

```
docker build -t server}
Mdns.Server.start
```
Para el cliente:
```
docker build -t client
Mdns.Client.start
```
## Envio de paquetes
Para corroborar la conexión cliente-servidor, se ocupan los siguientes, se recomienda iniciar una captura de wireshark para visualizar los paquetes enviados a continuación:

```
Mdns.Server.add_service(%Mdns.Server.Service{
    domain: "nerves.local",
    data: "_rosetta._tcp.local",
    ttl: 120,
    type: :ptr
})

Mdns.Server.add_service(%Mdns.Server.Service{
    domain: "prueba1.local",
    data: :ip,
    ttl: 120,
    type: :a
})

Mdns.Server.set_ip ([192,168,1,4])

Mdns.Server.add_service(%Mdns.Server.Service{
    domain: "pruebatexto._tcp.local",
    data: ["Hola, como estas?"],
    ttl: 790,
    type: :txt
})
```
Para el cliente:
```
Mdns.Client.query ("nerves.local")

Mdns.Client.query("prueba1")

Mdns.Client.query("pruebatexto._tcp.local")
```
