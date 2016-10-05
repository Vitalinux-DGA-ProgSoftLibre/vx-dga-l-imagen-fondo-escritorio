# Paquete DEB vx-dga-l-imagen-fondo-escritorio

Paquete encargado de modificar el fondo de Escritorio o Wallpaper en los equipos Vitalinux.  Este paquete afectará a todos aquellos equipos que no hayan modificado el Wallpaper que viene por defecto (equipos congelados, etc.).  Además, este cambio permitirá al usuario final saber que su equipo se encuentra correctamente actualizado a través de Migasfree.

# Usuarios/Equipos Destinatarios

Principalmente serán aquellos equipos que tienen marcada la etiqueta migasfree de congelación de escritorio.

# Aspectos Interesantes:

Existen dos resolciones de fondo de pantalla pensados para monitores 4x3 y 16x9.  El resto de equipos/resoluciones se ajustará al más cercano a los anteriores.

```
RESOLUCION=$(/usr/bin/obtener-resolucion-pantalla)
_FILE1=/usr/share/lubuntu/wallpapers/vitalinux-edu-wallpaper.png
_FILE2=/usr/share/lubuntu/wallpapers/vitalinux-login.png

case $RESOLUCION in
	"4:3" )
	ln -sf /usr/share/divert/usr/share/lubuntu/wallpapers/vitalinux-edu-wallpaper-4x3-1600x1200.png \
		/usr/share/divert$_FILE1
	ln -sf /usr/share/divert/usr/share/lubuntu/wallpapers/vitalinux-login-4x3-1600x1200.png \
		/usr/share/divert$_FILE2
	;;
	* )
	ln -sf /usr/share/divert/usr/share/lubuntu/wallpapers/vitalinux-edu-wallpaper-16x9-1920x1080.png \
		/usr/share/divert$_FILE1
	ln -sf /usr/share/divert/usr/share/lubuntu/wallpapers/vitalinux-login-16x9-1920x1080.png \
		/usr/share/divert$_FILE2
	;;
esac

_FILE=/usr/share/lubuntu/wallpapers/vitalinux-edu-wallpaper.png
dpkg-divert --add --package vx-dga-l-imagen-fondo-escritorio --rename \
  --divert $_FILE.orig $_FILE
[ ! -e $_FILE -o -L $_FILE ] && \
  ln -sf /usr/share/divert$_FILE $_FILE

_FILE=/usr/share/lubuntu/wallpapers/vitalinux-login.png
dpkg-divert --add --package vx-dga-l-imagen-fondo-escritorio --rename \
  --divert $_FILE.orig $_FILE
[ ! -e $_FILE -o -L $_FILE ] && \
  ln -sf /usr/share/divert$_FILE $_FILE
```
# Como Crear el paquete DEB a partir del codigo de GitHub
Para crear el paquete DEB será necesario encontrarse dentro del directorio donde localizan los directorios que componen el paquete.  Una vez allí, se ejecutará el siguiente comando (es necesario tener instalados los paquetes apt-get install debhelper devscripts):

```
apt-get install debhelper devscripts
/usr/bin/debuild --no-tgz-check -us -uc
```

# Como Instalar el paquete generado vx-dga-l-lupa*.deb:
Para la instalación de paquetes que estan en el equipo local puede hacerse uso de ***dpkg*** o de ***gdebi***, siendo este último el más aconsejado para que se instalen también las dependencias correspondientes.
```
gdebi vx-dga-l-*.deb
```
