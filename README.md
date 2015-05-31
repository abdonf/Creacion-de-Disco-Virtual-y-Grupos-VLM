##RECUPERATORIO DE LAS PRÁCTICAS
* 1.- Crear un disco dura virtual de 8 GB
* 2.- Crear el grupo LVM 'sistemas-kvm01'
* 3.- Crear el grupo LVM 'sistemas-kvm02'
* 4.- Crear 3 volúmenes lógicos dentro de 'sistemas-kvm'

##1.- Crear un disco dura virtual de 8 GB
En local host (QEMU)

* Clic derecho vamos a detalles, elegimos almacenamiento y seleccionamos ‘Directorio del Sistema de Archivos’ o unidad de disco.

* Elegimos nuevo volumen colocamos el nombre en este caso como ejemplo ‘hdd-virt8gb’ dar el tamaño  y finalizar. Para más detalles consultar las imágenes siguientes:

* Posteriormente vamos a la máquina virtual creada, clic derecho, le decimos abrir y elegimos el foco, donde podremos elegir ‘Adicionar HardWare’ (nuevo), particionamiento (storage) y en almacenamiento, en explorar elegimos el disco virtual creado de 8GB, le damos tipo de Bus ‘VirtD’ y en opciones avanzadas formato de almacenaje ‘raw’ y finalizar, como indica en las siguientes imágenes.

* Una vez creada un disco duro virtual de 8GB, iniciamos la maquina virtual.

* Posteriormente creamos las particiones correspondientes de acuerdo al tamaño que se requiera (en este caso utilizamos el disco virtual que fue creado de 8GB), para ello usamos el siguiente comando en nuestra terminal:

        cfdisk /dev/vda

Le damos nueva partición – damos el tamaño, y le damos escribir para confirmar presionamos ‘yes’ para finalizar salimos.
Una vez realizado estas particiones creamos las particiones físicas con el siguiente comando utilizando nuestra terminal.

        pvcreate /dev/vda1
        pvcreate /dev/vda1
        pvcreate /dev/vda1

Verificamos las particiones las particiones con el comando # fdisk -l

##2.- Crear el grupo LVM 'sistemas-kvm01'
##3.- Crear el grupo LVM 'sistemas-kvm02' y el grupo ‘sistemas-kvm’

* Posteriormente creamos volúmenes de GRUPO:

        vgcreate sistemas-kvm     /dev/vda1
        vgcreate sistemas-kvm01     /dev/vda2
        vgcreate sistemas-kvm02     /dev/vda3

* Verificamos con el comando # lvs    //nos dará volúmenes de grupos creados.

        4.- Crear 3 volúmenes lógicos dentro de 'sistemas-kvm'

* Por ultimo nos indica crear 3 volúmenes lógicos dentro de ‘sistemas-kvm’, para ello creamos en este caso cada volumen de 2GB como sigue a continuación:

        lvcreate   -L  2048m    -n   volumen1    sistemas-kvm   
        lvcreate   -L  2048m    -n   volumen2    sistemas-kvm
        lvcreate   -L  2048m    -n   volumen3    sistemas-kvm
