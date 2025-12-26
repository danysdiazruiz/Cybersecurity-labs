# Nmap Scan Lab – Descubrimiento y Enumeración

## Descripción
Este laboratorio documenta el uso de **Nmap** para realizar descubrimiento de hosts, escaneo de puertos y enumeración básica de servicios en un entorno controlado.

El ejercicio se alinea con tácticas del framework **MITRE ATT&CK**, específicamente en la fase de reconocimiento.

---

## Objetivo
- Identificar hosts activos en una red.
- Detectar puertos abiertos.
- Enumerar servicios y versiones.
- Comprender la importancia del reconocimiento en un análisis de seguridad.

---

## Relación con MITRE ATT&CK

| Táctica | Técnica | ID | Descripción |
|--------|----------|----|-------------|
Reconnaissance | Network Service Discovery | T1046 | Descubrimiento de servicios de red mediante escaneo. |
Reconnaissance | Active Scanning | T1595 | Escaneo activo para recopilar información del objetivo. |

---

## Entorno de laboratorio
- **Atacante:** Kali Linux  
- **Objetivo:** Metasploitable 2  
- **Red:** Laboratorio local en VirtualBox (Host-Only / NAT)  

> Todas las pruebas se realizan en entornos controlados con fines educativos.

---

## Herramienta utilizada
- Nmap

---

## Procedimiento

### 1. Descubrimiento de host
Comando utilizado: ```bash nmap -sn 192.168.1.0/24  ```

---

## Evidencia ![Descubrimiento de hosts](images/host-discovery.png)

Se detectaron múltiples hosts activos en la red local. Para efectos del laboratorio, se analiza únicamente el host objetivo (Metasploitable) con IP 192.168.1.79.

### Validación del host objetivo

Se valida conectividad con el host identificado como objetivo (Metasploitable 2) en la IP **192.168.1.79** mediante ICMP.

```bash
ping -c 3 192.168.1.79
```

## Evidencia
![Validación de IP objetivo](images/target-validation-ping.png)

### Confirmación de IP en el host objetivo (Metasploitable 2)

Se verifica desde el sistema objetivo que la interfaz de red tiene asignada la IP **192.168.1.79**.

## Evidencia
![IP en Metasploitable 2](images/metasploitable-ifconfig.png)


### 2. Escaneo de puertos TCP

Comando utilizado:
```bash
nmap 192.168.1.79
```

## Evidencia
![Escaneo de puertos TCP](images/port-scan-basic.png)

**Resultado:**  
El escaneo revela múltiples puertos TCP abiertos en el host objetivo, incluyendo servicios como FTP (21), SSH (22), Telnet (23), SMTP (25), HTTP (80) y MySQL (3306), lo que indica una amplia superficie de ataque y justifica la necesidad de realizar una enumeración más detallada de servicios.


### 3. Enumeración de servicios y versiones

Se realiza la enumeración de servicios para identificar las aplicaciones y versiones que se ejecutan en los puertos abiertos del host objetivo **192.168.1.179**.

Comando utilizado:
```bash
nmap -sV 192.168.1.179
```

## Evidencia
![Enumeración de servicios](images/service-enumeration.png)
**Resultado:**  
La enumeración identifica múltiples servicios desactualizados y potencialmente vulnerables, como **vsftpd 2.3.4**, **Apache 2.2.8**, **Samba 3.x**, **MySQL 5.0.51a** y la presencia de un **bind shell en el puerto 1524**, lo que evidencia una superficie de ataque crítica en el host objetivo y justifica la continuación con análisis de vulnerabilidades.
