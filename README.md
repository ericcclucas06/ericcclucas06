## Instalación

pfSense es un software de codigo abierto utilizado para gestionar y proteger redes. Funciona como un firewall  y router, permitiendo controlar el trafico de internet,proteger la red de ataques y intrusos,y crear VPN 

pf Sense Se basa en el sistema operatibo  FreeBSD, conocido por su seguridad y estabilidad.

#### Entre sus principales características están:

>
>Firewall avanzado: Reglas potentes para filtrar y controlar el tráfico de red.
>
>Enrutamiento: Funciones avanzadas para conectar redes.
>
>VPN: Soporta OpenVPN, IPSec, PPTP, entre otros.
>
>Proxy y filtrado web: Control y supervisión de acceso a Internet 
>
>Balanceo de carga y redundancia: Distribuye el tráfico y asegura redundancia en conexiones.
>
>Seguridad: IPS, filtrado de contenido, protección contra ataques DoS.
>
>Interfaz gráfica: Web intuitiva para gestión y configuración.
>
>
#### PfSense es una solucion para proteger y gestionar lasredes, facil de instalar en maquinas virtuales y altamente configurable para adaptarse a distintas necesidades de seguridad y conectividad.
## Configuración de un servidor VPN en pfSense

### Instalar el pluguin OpenVPN Client
Ir a System - Package Manager - Available Packages
Buscar openvpn-client-export y hacer clic en Install
![image](https://github.com/user-attachments/assets/5bf56a2e-9477-4872-9827-3c4a368dc0c2)



### Crear los certificados digitales
Ir a System - Certificate Manager y agregar una nueva CA
Asignarle un nombre como OpenVPN_CA
Generar un certificado para el servidor VPN desde System - Certificates
Creamos el certificado manteniendo casi todas las opciones por defecto y asignando un nombre.

| Opción  | Descripción |
| ------------- | ------------- |
| Descriptive name  | OpenVPN_CA  |
| Common name  | OpenVPN_CA  |

Una vez realizado los cambios y guardando nos aparece nuestro certificado:
![image](https://github.com/user-attachments/assets/e7b3372c-cc16-446c-adf0-674b7d818663)


Crear el certificado del servidor OpenVPN
En el apartado siguiente, System – Certificates clicamos en agregar un certificado:

### Configurar el servidor OpenVPN
Ir a VPN - OpenVPN - Servers y agregar un nuevo servidor
Configurar los siguientes parámetros:
Modo: Remote Access (SSL/TLS + User Auth)
Protocolo: UDP en IPv4
Puerto: 5194 (puede cambiarse)
Certificado: Seleccionar el certificado generado previamente
Red VPN: Definir una red privada, por ejemplo, 10.4.44.0/24
Opciones adicionales:
Habilitar Redirect IPv4 Gateway para forzar el tráfico a través del túnel VPN
Permitir la comunicación entre clientes si es necesario
Definir servidores DNS (por ejemplo, 1.1.1.1 y 8.8.8.8)

### Configurar reglas en el firewall
Crear una regla en Firewall - Rules - WAN para permitir el tráfico a través del puerto VPN
Agregar una regla en OpenVPN que permita todo el tráfico dentro de la red VPN

### Exportar archivos de configuración para los clientes
Crear un usuario en System - User Manager
Generar un certificado de usuario
Ir a VPN - OpenVPN - Client Export y descargar la configuración para cada cliente

### Verificar la conexión
Comprobar el estado del servicio en Status - Service.
Probar la conexión en un cliente, por ejemplo, con la aplicación OpenVPN en Android o iOS.
Confirmar que la conexión es exitosa accediendo a la IP del pfSense desde el navegador.


## Pfsense portForwar

## Open VPN

