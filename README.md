# Fundamentos-de-Redes
Tarea investigativa con el profe Guido para introducirnos a los conceptos básicos de una red

# 🌐 Router, Switch y Hub para Developers

---

## 🧩 1. ¿Qué es cada dispositivo?

| Concepto | Definición simple | Nivel técnico (breve) | Ejemplo real |
|----------|------------------|----------------------|--------------|
| Router | Conecta redes distintas (como tu casa con internet) | Trabaja con direcciones IP y enruta paquetes entre redes | Tu router WiFi enviando tu request a una API |
| Switch | Conecta dispositivos dentro de la misma red | Usa direcciones MAC para enviar datos al destino correcto | Red interna de un data center |
| Hub | Repite la información a todos los dispositivos | No filtra ni decide, hace broadcast total | Red antigua donde todos reciben todo |

---

## ⚙️ 2. ¿Cómo funciona realmente?

### 📡 ¿Qué hace el router con los paquetes?

- Recibe paquetes con IP destino  
- Consulta su tabla de rutas  
- Decide por dónde enviarlos  
- Los reenvía hacia otra red (internet, otra subred)  

👉 Ejemplo:  
fetch("https://api.miapp.com")

Tu router decide a qué camino de internet enviar esa petición.

---

### 🔀 ¿Cómo decide un switch?

- Aprende direcciones MAC  
- Mantiene una tabla (MAC → puerto)  
- Envía datos solo al dispositivo correcto  

👉 Resultado:

- Más rápido  
- Menos tráfico innecesario  

---

### 📢 ¿Por qué el hub es obsoleto?

- Envía datos a todos (broadcast)  
- Genera:  
  - tráfico innecesario  
  - colisiones  
  - baja seguridad  

👉 En simple:  
Es como gritar en una sala llena en vez de hablarle a alguien específico.

---

## 💻 3. Conexión directa con desarrollo (CLAVE)

### 🌐 Router en una petición API

Cuando haces:  
fetch("https://api.miapp.com") //- fetch → función de JavaScript para hacer peticiones HTTP desde el frontend hacia una API

El router:

1. Envía tu request fuera de tu red local  
2. La dirige hacia internet  
3. Pasa por múltiples routers hasta el servidor  

👉 Sin router:  
❌ No hay conexión con APIs externas  

---

### 🏢 Switch en backend / data center

- Conecta:  
  - servidores  
  - bases de datos  
  - contenedores  

- Permite comunicación rápida interna  

👉 Ejemplo real:  
Backend Node.js → DB PostgreSQL  

Todo pasa por switches internos.

---

### ⚠️ Problemas de red que rompen tu app

Aunque tu código esté perfecto:

- Latencia alta → app lenta  
- Pérdida de paquetes → requests fallan  
- DNS mal configurado → API “no existe”  
- Congestión → timeouts  

👉 Clásico error:  
Error: ETIMEDOUT  

No es tu código… es la red 😅

---

## 🌍 4. Caso práctico real

### 🚨 “Mi app no funciona en producción”

---

### 🔎 ¿Puede ser el router?

✅ Sí:

- mala configuración  
- firewall bloqueando tráfico  
- rutas incorrectas  

👉 Resultado:  
La API nunca recibe la request  

---

### 🔎 ¿Puede ser el switch?

✅ Sí:

- fallo en red interna  
- servidor no accesible  
- puerto incorrecto  

👉 Resultado:  
Backend no puede hablar con la DataBase (Base de datos) 

---

### 🧠 ¿Cómo distinguir red vs código?

#### Checklist:

| Prueba | Qué indica |
|--------|----------|
| ping | Conectividad básica | //- ping → comando que verifica conectividad básica con un servidor y mide latencia
| traceroute | Dónde se corta la red | //- traceroute → comando que muestra la ruta que siguen los paquetes y permite identificar en qué punto se corta la red
| curl | Si la API responde | // curl → herramienta de terminal para hacer peticiones HTTP y verificar si una API responde
| logs backend | Si llega la request | //- logs backend → registros del servidor que permiten ver si una petición llegó y qué ocurrió internamente

👉 Regla de oro:

- Si no llega al servidor → problema de red  
- Si llega pero falla → problema de código  

---

## 🧪 5. Analogía (clave para explicar)

- Router = Oficina de correos entre ciudades 🌍  
- Switch = Conserje que sabe a quién entregar un paquete 📬  
- Hub = Persona que grita el mensaje a todos 📢  

---

## 🧠 BONUS

### ⚖️ Load Balancer

Un balanceador de carga (load balancer) es un dispositivo o software 
que distribuye eficientemente el tráfico de red o aplicaciones 
entrante entre múltiples servidores.

👉 Es como un router inteligente para servidores

- Distribuye tráfico entre varios servidores  
- Evita sobrecarga  

Ejemplo:  
Usuario → Load Balancer → Server 1 / Server 2 / Server 3  

---

### ☁️ Relación con Cloud (AWS, Azure, etc.)

El Cloud Computing (AWS, Azure, GCP) es el alquiler de infraestructura
 tecnológica (servidores, bases de datos, almacenamiento) 
a través de internet, bajo un modelo de pago por uso. Permite a empresas 
escalar recursos instantáneamente sin gestionar hardware físico, 
ofreciendo alta seguridad, flexibilidad y almacenamiento global. 

Todo esto existe pero “virtualizado”:

- Router → VPC / Internet Gateway  // VPC (Virtual Private Cloud) Es una red privada virtual dentro de AWS. Funciona como tu “red local” en la nube  
- Switch → Redes internas (subnets)  
- Load balancer → servicios gestionados  

👉 Ejemplo en AWS: //Amazon Web Services (AWS) es la plataforma de nube más completa y utilizada del mundo, ofreciendo más de 200 servicios integrales desde centros de datos globales.

- EC2 (servidores)  //Amazon EC2 (Elastic Compute Cloud) es un servicio de la nube de Amazon Web Services (AWS) que proporciona capacidad de computación escalable y segura mediante máquinas virtuales (instancias).
- VPC (red)  // Una VPC (Virtual Private Cloud o Nube Privada Virtual) es una red virtual aislada lógicamente dentro de una nube pública (como AWS, Google Cloud o Azure).
- ELB (load balancer)  

---

## 🧠 Cierre

> “Un developer que entiende redes no solo programa…  
> entiende por qué las cosas fallan, escala mejor sus soluciones  
> y deja de culpar al código cuando el problema es internet.” 🚀
