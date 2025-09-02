#  Calculadora de CDT

Aplicación web sencilla para calcular el rendimiento de un **Certificado de Depósito a Término (CDT)** con **interés simple o compuesto**.  

El usuario ingresa el capital inicial, la tasa de interés anual, el tiempo en años y el tipo de interés, y la aplicación muestra el monto final y el interés ganado.

---

## Tecnologías

- **HTML5** → estructura de la aplicación  
- **CSS3** → estilos básicos  
- **JavaScript (Vanilla)** → lógica de cálculo  
- **Nginx** (para despliegue en AWS EC2)  

---

## Estructura del proyecto

## Estructura del proyecto

```bash
calculadora-cdt/
├── index.html   # Página principal
├── style.css    # Estilos de la interfaz
└── app.js       # Lógica de cálculo
```

---

### Uso

## Despliegue en AWS EC2 con Nginx

Sigue estos pasos para desplegar la aplicación en una instancia de **Ubuntu EC2** usando **Nginx**:

## 1. Conectar a la instancia
En la consola de AWS → EC2 → **Connect** → **EC2 Instance Connect** (o con SSH si tienes llaves).

---
## 2. Instalar dependencias
Actualiza e instala Git y Nginx:
```bash
sudo apt update
sudo apt install -y git nginx
```

## 3. Clona este repositorio:

   ```bash
   git clone https://github.com/tu-usuario/calculadora-cdt.git
   cd calculadora-cdt
```

## 4. Copiar archivos al directorio web

Crea el directorio de publicación de Nginx y copia los archivos del proyecto:

  ```bash
sudo mkdir -p /var/www/cdt
sudo cp -r ~/calculadora-cdt/* /var/www/cdt/
sudo chown -R www-data:www-data /var/www/cdt
```
## 5. Configurar Nginx

Crea un archivo de configuración para tu sitio:
```bash
sudo nano /etc/nginx/sites-available/cdt
```

Agrega este contenido:

```
server {
    listen 80;
    listen [::]:80;
    server_name _;

    root /var/www/cdt;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```
Activa la nueva configuración y elimina la predeterminada:

```bash
sudo ln -s /etc/nginx/sites-available/cdt /etc/nginx/sites-enabled/
sudo rm /etc/nginx/sites-enabled/default
```


# 🛠️ Registro de Errores y Soluciones - Despliegue en AWS

Este documento recopila los errores más comunes que surgieron durante el despliegue de la aplicación en **AWS EC2**, incluyendo configuración de servidor, instalación de dependencias y problemas de compilación.

---

## 📌 1. Error: `Command 'aws' not found`
**Contexto:**  
Al intentar usar `aws ec2 describe-instance`.

**Causa:**  
La CLI de AWS no estaba instalada.

**Solución:**  
```bash
sudo apt update
sudo apt install awscli -y





