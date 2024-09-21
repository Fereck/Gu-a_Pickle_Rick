# Guia_Pickle_Rick
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

























