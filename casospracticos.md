# CASOS PRÁCTICOS
## a) Versión de Nginx instalado.
![version](https://github.com/samarameit/NGINX/blob/main/imagenes/nginx3.PNG?raw=true)
## b) Ficheros de configuración.

El fichero de configuración inicial es el siguiente: /etc/nginx/nginx.conf
![confi1](https://github.com/samarameit/NGINX/blob/main/imagenes/nginx5.PNG?raw=true)

Página html por defecto en nginx: /var/www/html/index.nginx-debian.html
![confi2](https://github.com/samarameit/NGINX/blob/main/imagenes/nginx6confi.PNG?raw=true)

## c) Página web por defecto:
1. Cambiamos el html por defecto
![paginahtml](https://github.com/samarameit/NGINX/blob/main/imagenes/paginanginx1.PNG?raw=true)

2. Actualizamos la página

![actualizar](https://github.com/samarameit/NGINX/blob/main/imagenes/pagina2.PNG?raw=true)

3. Comprobamos en el navegador si se han realizado los cambios
![comprobar](https://github.com/samarameit/NGINX/blob/main/imagenes/pagina3.PNG?raw=true)

## d) Virtual Hosting:
Queremos que nuestro servidor web ofrezca balanceo de carga desde https  a dos sitios web que tengan también https.

El balanceo de carga es una técnica o un mecanismo que distribuye las solicitudes entrantes al grupo de servidores del backend. Se utiliza para aumentar la disponibilidad, confiabilidad y escalabilidad de las aplicaciones. Permite agregar muchos servidores cuando aumenta el tráfico.

Para ello deberemos crear 3 máquinas virtuales que hagan de servidores. Configuramos la red para que las tres estén en la misma.
En este caso voy a usar las siguientes IPs:

-Balanceador de carga: 192.168.2.214

-Servidor1: 192.168.2.215

-Servidor2: 192.168.2.216

1. Debemos instalar nginx en todos los servidores. Para ver como instalarlo: [INSTALACIÓN](https://github.com/samarameit/NGINX/blob/main/instalacion.md)

2. Una vez instalado hay qeu habilitar el servicio nginx para que inicie al arrancar el sistema con 'systemctl enable nginx'.

3. Cambiamos las páginas html por defecto del servidor1 y servidor2:

![servidor1](https://github.com/samarameit/NGINX/blob/main/imagenes/htmlserv1.PNG?raw=true)
![](https://github.com/samarameit/NGINX/blob/main/imagenes/serv1.PNG?raw=true)
![servidor2](https://github.com/samarameit/NGINX/blob/main/imagenes/htmlserv2.PNG?raw=true)
![](https://github.com/samarameit/NGINX/blob/main/imagenes/serv2.PNG?raw=true)

4. Comprobamos que desde el servidor2 podemos ver la pagina nginx del servidor 1:

![ejemplo](https://github.com/samarameit/NGINX/blob/main/imagenes/2ve1.PNG?raw=true)
5. Ahora comenzamos a preparar la máquina de balanceo. Una vez hemos configurado la red como hemos mencionado anteriormente y hemos instalado Nginx procedemos a borrar el archivo de configuracion predeterminado de Nginx y crear uno nuevo:

![balanceo1](https://github.com/samarameit/NGINX/blob/main/imagenes/balanceo1.PNG?raw=true)

Una vez creado el fichero le añadimos las siguientes líneas indicando la IP de nuestros servidores y el nombre del servidor que queramos:
![balanceo2](https://github.com/samarameit/NGINX/blob/main/imagenes/balanceo2.PNG?raw=true)

6. Comprobamos la sintaxis de los ficheros con 'nginx -t'.

![balanceo2](https://github.com/samarameit/NGINX/blob/main/imagenes/balanceo3.PNG?raw=true)

7. Cambiamos el fichero /etc/hosts y añadimos la ip del servidor de balanceo con el nombre que hemos indicado anteriormente.

![balanceo4](https://github.com/samarameit/NGINX/blob/main/imagenes/balanceo4.PNG?raw=true)

8. Reiniciamos el servicio.

9. Verificamos el Balanceo de carga. Abrimos desde el navegador y accedemos al servidor de equilibrio de carga utilizando la URL http://www.samarameit.com y se redirigirá al servidor 1. 

![balanceo2](https://github.com/samarameit/NGINX/blob/main/imagenes/comprobarbalanceo1.PNG?raw=true)

Despues actualizamos la página continuamente después de un tiempo,y debería cargarse desde el segundo servidor de aplicaciones como se muestra a continuación:

![balanceo2](https://github.com/samarameit/NGINX/blob/main/imagenes/comprobarbalanceo2.PNG?raw=true)
