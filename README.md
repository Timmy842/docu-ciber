# 🛡️ HackNotes — Documentación de Ciberseguridad

Apuntes personales de mi formación en ciberseguridad y hacking ético: cursos, preparación de certificaciones, plataformas de práctica y writeups de máquinas resueltas.

Las notas están escritas en Markdown y organizadas como un vault de [Obsidian](https://obsidian.md/), aunque se pueden leer directamente desde GitHub.

> ⚠️ **Aviso legal:** todo el contenido tiene fines exclusivamente educativos. Las técnicas descritas se han practicado en entornos controlados y autorizados (laboratorios, CTFs y máquinas vulnerables). No las utilices contra sistemas sin permiso explícito.

---

## 📚 Contenido

### 🐧 [Linux](Linux)
Fundamentos de Linux orientados a pentesting.
- Comandos básicos, control de flujo y procesos en segundo plano
- Permisos y estructura de directorios del sistema
- Oh My Tmux, búsquedas a nivel de sistema y Bash avanzado

### 🎓 [Certificaciones](Certificaciones)
#### eJPTv2 (eLearnSecurity Junior Penetration Tester)
- **Curso ElPinguinoDeMario**
  - Conceptos básicos de redes (IP, máscaras, clases, CIDR)
  - Conceptos básicos de hacking (Netcat, transferencia de archivos, ARP-scan, Nmap)
  - Explotación y fuerza bruta (Metasploit, Msfvenom, Hydra, John The Ripper)
  - Explotación web (fuzzing, enumeración de subdominios con Wfuzz)
- **Curso INE**
  - Information Gathering (Sublist3r, DNS y transferencia de zona)
- **Curso Udemy Álvaro Chirou** *(en progreso)*

### 🟢 [Hack The Box](Hack%20The%20Box)
- **Labs — Starting Point (Tier 0):** Meow, Fawn, Dancing, Redeemer, Explosion, Preignition, Mongod, Synced

### 🔴 [TryHackMe](Try%20Hack%20Me)
- **Academia**
  - *Pre Security:* Network Fundamentals y How The Web Works
  - *Cyber Security 101:* Linux y Windows Fundamentals, línea de comandos, networking, criptografía, explotación básica, web hacking, herramientas ofensivas y defensivas, SOC/DFIR, soluciones de seguridad, carrera profesional y OWASP Top 10
- **Challenges:** writeup de la room *Vulnversity* (Easy)

### 🐳 [DockerLabs](DokcerLabs)
- Writeup de la máquina *Backend* (Easy)

---

## 🗂️ Estructura del repositorio

```
.
├── Certificaciones/
│   └── eJPTv2/
├── DokcerLabs/
├── Hack The Box/
│   └── Labs/
├── Linux/
├── Try Hack Me/
│   ├── Academia/
│   └── Challenges/
└── .obsidian/          # Configuración del vault de Obsidian
```

Las capturas usadas en los writeups se guardan en las carpetas `Imagenes WriteUps/` de cada sección.

## 🚀 Cómo usarlo

1. Clona el repositorio:
   ```bash
   git clone https://github.com/Timmy842/docu-ciber.git
   ```
2. Abre la carpeta como vault en Obsidian (*Open folder as vault*) para tener enlaces internos, imágenes y vista de grafo.
3. O simplemente navega por las carpetas desde GitHub.

---

📌 *Repositorio en constante actualización a medida que avanzo en mi aprendizaje.*
