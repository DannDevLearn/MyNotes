# Multiples opciones al iniciar el Grub en Fedora 

Para eliminar los kernels que son actualiados y quedan en Fedora podemos eliminarlos y limitarlos

### 1- Eliminarlos

debemos checar primero los kernels que tenemos disponibles con

Fedora en mi caso 

```
    rpm -q kernel    
```

Esto nos mostrara los kernels que tenemos disponibles.

> [!TIP]
> Recuerda que es bueno tener al menos 2 Kernels el actual y el anterior
> pero tu decides cuantos tener.

Para poder eliminar el kernel que no queremos que aparesca en el grub

```
    sudo dnf remove <Kernel version>
```

la version del kernel es la que elegimios anteriormente.

Ahora tambien debemos de checar que si existen restos del kernel que borramos
para ello usaremos 

```
    ls /boot/
```
para listar y poder ver si hay restos de kernels borrados o del que recien borramos

```
    sudo rm /boot/vmlinuz-<versión_antigua>
    sudo rm /boot/initramfs-<versión_antigua>.img
    sudo rm /boot/config<version antigua>
    sudo rm /boot/symvers<version antigua>.xz
    sudo rm /boot/ System.map-<version antigua>
```

Estos en mi caso fueron todos los archivos relacionados el kernel que borre.
Ahora solo queda limpiar cache y regenerar el archivo grub

```
    Regenerar el grub
    sudo grub2-mkconfig -o /boot/grub2/grub.cfg

    limpiar cache
    sudo dnf clean all
    sudo dnf autoremove
```

solo reinicia y listo!


### 2- Modificar las instancias

Tambien si ya hicimos lo anterior podemos hacer este paso ya que es buena idea para indicar cuantas
versiones del kernel queremos mantener, en mi caso solo la actual  y la anterior para ello vamos a

```
    sudo nano /etc/dnf/dnf.conf
```

agregamos la siguiente linea

```
    installonly_limit=2
```

y como en los pasos anterior solo queda generar el archivo grub y limpiar cache y listo!
