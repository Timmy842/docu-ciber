## 1. ¿Qué es DNS?

**DNS (Domain Name System)** es un sistema que traduce nombres de dominio legibles para humanos  (p. ej. `hackwithcarlos.com`) en direcciones IP que entiende una máquina  (p. ej. `54.37.224.62`).

Es, básicamente, la _agenda telefónica de Internet_.

### ✔️ Funciones principales

- Resolver nombres de dominio → direcciones IP.
- Gestionar registros como:
	- **A** (IPv4)
	- **AAAA** (IPv6)
	- **MX** (correo)
	- **TXT** (verificaciones, SPF, DKIM…)
	- **NS** (nameservers)
	- **CNAME** (alias)
- Delegar zonas entre servidores.

### ✔️ Cómo funciona a alto nivel

1. El usuario escribe `hackwithcarlos.com`.
2. El navegador pregunta al **resolver DNS local**.
3. El resolver consulta uno o varios **DNS autoritativos**.
4. Se obtiene una respuesta con los registros de la zona.
5. Se devuelve la IP al navegador.

## 2. ¿Qué es una DNS Zone?

Una **zona DNS** es la “base de datos” que contiene todos los registros DNS de un dominio.

Ejemplo sencillo de zona:

`hackwithcarlos.com.  IN  A      54.37.224.62`
`www                  IN  CNAME  hackwithcarlos.com.`
`mx                   IN  MX     10 mx.zoho.com.`

La zona está gestionada por los **DNS autoritativos** del dominio (ej. Cloudflare, DonDominio, OVH…).

# 3. DNS Zone Transfer (AXFR / IXFR)

Un **DNS Zone Transfer** es un mecanismo usado para copiar el contenido completo de la zona DNS desde un servidor autoritativo a otro.

Se usa para **replicar información entre varios DNS** y mantenerlos sincronizados.

### ✔️ Tipos

|Tipo|Nombre|Descripción|
|---|---|---|
|**AXFR**|_Full Zone Transfer_|Copia completa de la zona.|
|**IXFR**|_Incremental Zone Transfer_|Copia solo cambios desde la última versión.|

---

## 4. Riesgos de Seguridad: Zone Transfer abierto

Un **Zone Transfer mal configurado** permite que cualquier persona solicite una copia de la zona DNS completa.

Esto puede filtrar:

- Subdominios internos (`dev.`, `staging.`, `vpn.`, etc.)
- Infraestructura
- Correos, configuraciones MX
- Servicios ocultos

Es una vulnerabilidad muy común en auditorías de pentesting.

---

# 5. Cómo comprobar un Zone Transfer

### Usando **dig**

`dig AXFR hackwithcarlos.com @ns1.servidor.com`

### Usando **host**

`host -l hackwithcarlos.com ns1.servidor.com`

### Si está mal configurado…

Verás _toda la zona DNS_ listada.

### Si está protegido…

Recibirás:

`Transfer failed.`

o

`Refused.`

---

# 6. Cómo se protege un Zone Transfer

Buenas prácticas:

- Permitir AXFR solo entre **nameservers autorizados**.
- Bloquearlo a cualquier otra IP.
- Usar **TSIG** (Transaction SIGnature) para autenticación.
- Dejar la gestión en proveedores seguros como Cloudflare (que no permite AXFR público).

Ejemplo de configuración en BIND:

`allow-transfer { 192.168.1.2; };`

---

# 📝 7. Resumen rápido

- DNS → sistema que traduce dominios a IP.
- Zona DNS → registros de un dominio.
- Zone Transfer (AXFR/IXFR) → mecanismo para replicar una zona completa.
- Un Zone Transfer abierto es una vulnerabilidad grave.
- Se comprueba con `dig AXFR dominio @servidor`.