# Time synchronization on Raspberry Pi: Timedatectl

El **problema** era que el Rasperry Pi con el OS DietPi no estaba sincronizando la hora

* **Paso 1:** Editar el archivo con el siguiente comando `sudo nano /etc/systemd/timesyncd.conf`

```bash
NTP=aqui-va-server-ntp.com
FallbackNTP=aqui-va-server-ntp-alternativo.com
RootDistanceMaxSec=30
#PollIntervalMinSec=32
#PollIntervalMaxSec=2048
```

* **Paso 2:** Desactivar y activar la sincronizacion del ntpserver.
```bash
$ timedatectl set-ntp false
$ timedatectl set-ntp true
```
Cuando se activa el valor queda asi `NTP service: active`.

Ejm.
```bash
$ timedatectl
               Local time: Sat 2019-06-22 13:49:53 AEST
           Universal time: Sat 2019-06-22 03:49:53 UTC
                 RTC time: Sat 2019-06-22 03:49:54
                Time zone: Australia/Sydney (AEST, +1000)
System clock synchronized: no
              NTP service: active
          RTC in local TZ: no
```
Esperamos un rato hasta que el valor quede asi `System clock synchronized: yes`. Si no queda asi hay que revisar que esta pasando.

**Trouble shooting**

Para ver el log del problema ejecutamos el siguiente comando.
```bash
$ journalctl --unit=systemd-timesyncd.service
```

Cambiar zona horaria a la de Panamá. Yo en lo personal eligo Bogota.
```bash
sudo timedatectl set-timezone America/Bogota
```


**Referencias**
* https://serverfault.com/questions/948974/force-systemd-timesyncd-to-sync-time-with-ntp-server-immediately
* https://raspberrytips.com/time-sync-raspberry-pi/
