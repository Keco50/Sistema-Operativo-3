# Sistema-Operativo-3**Práctica 1: Instalación del Sistema Operativo (Red Hat)**

1. **Crear una máquina virtual** con los siguientes recursos:
   - **CPU**: 2 núcleos
   - **RAM**: 4 GB
   - **Disco**: 20 GB
   - **Tarjeta de red**: Modo **Bridge**

2. **Configurar la tarjeta de red en modo Bridge:**
   - En **VirtualBox**:
     - Configuración > Red > Adaptador 1 > Modo Bridge
   - En **VMware**:
     - Settings > Network Adapter > Bridged

3. **Instalar Red Hat:**
   - Descargar la imagen desde el sitio oficial.
   - Iniciar la instalación en la máquina virtual.
   - Configurar usuario root y una contraseña segura.
   - Finalizar la instalación y reiniciar.

---

**Práctica 2: Configuración de Parámetros de Red**

### **Configuración con DHCP**
```bash
nmcli device show
nmcli con mod eth0 ipv4.method auto
nmcli con up eth0
ip addr show
```

### **Configuración con IP Estática**
```bash
nmcli con mod eth0 ipv4.addresses 192.168.1.100/24
nmcli con mod eth0 ipv4.gateway 192.168.1.1
nmcli con mod eth0 ipv4.dns "8.8.8.8 8.8.4.4"
nmcli con mod eth0 ipv4.method manual
nmcli con up eth0
```

**Alternativa manual en /etc/sysconfig/network-scripts/ifcfg-eth0:**
```bash
sudo nano /etc/sysconfig/network-scripts/ifcfg-eth0
```
Agregar:
```
DEVICE=eth0
BOOTPROTO=none
ONBOOT=yes
IPADDR=192.168.1.100
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
DNS1=8.8.8.8
DNS2=8.8.4.4
```

Reiniciar la red:
```bash
sudo systemctl restart NetworkManager
```

---

**Práctica 3: Gestión de Usuarios y Grupos**

**Crear usuario y agregarlo a sudoers:**
```bash
sudo useradd LuisDavidHilario
sudo passwd LuisDavidHilario
sudo usermod -aG wheel LuisDavidHilario
```

**Crear grupo y usuario asociado:**
```bash
sudo groupadd guest
sudo useradd -G guest usuario_guest
sudo passwd usuario_guest
```

**Eliminar usuario y grupo:**
```bash
sudo userdel -r usuario_guest
sudo groupdel guest
```

---

**Práctica 4: Gestión de Permisos de Archivos**

**Crear carpeta y archivo:**
```bash
mkdir materia
cd materia
touch estudiante.txt
vi estudiante.txt
```
(Escribir dentro de `vi`, guardar con `ESC + :wq`)
```
Nombre - Luis David Hilario Meran
Matrícula - 20230771
```

**Modificar permisos:**
```bash
chmod 700 estudiante.txt
chown :tu_grupo estudiante.txt
chmod 770 estudiante.txt
```

**Crear una nueva carpeta y copiar archivo:**
```bash
mkdir materia2
cp estudiante.txt materia2/
```

**Eliminar la carpeta original:**
```bash
rm -rf materia
```

---

**Entregables**

1. **Subir archivo de comandos a GitHub:**
```bash
git init
git add log.txt
git commit -m "Prácticas de Red Hat"
git remote add origin https://github.com/ejemplo/mi_repositorio.git
git push -u origin main
```


