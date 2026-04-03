## Portainer Nginx y Nginx Proxy manager

- ``NGINX`` base of web traffic
- ``Portainer`` visual container management
- ``NGINX Proxy Manager`` simplifies proxies + HTTPS

**OVERVIEW (BEFORE STARTING)**

Think of this as real architecture:
```
Internet → NGINX / Proxy Manager → your apps (Docker)
                              ↘ Portainer (Manager)
```
- **NGINX** = web server + reverse proxy
- **Portainer** = panel for operating Docker
- **NGINX Proxy Manager** = Easy UI for proxies + SSL

## LEVEL 0 - FUNDAMENTALS (WITHOUT IT, EVERYTHING FAILS)

### What is a web server?

A web server:
- Receives requests (e.g. open a website)
- Respond with content (HTML, API, etc.)

Example:
```
You http://your-server NGINX response
```

### What is a reverse proxy?

A **reverse proxy** receives traffic and redirects it internally:
```
User → NGINX → App (Port 3000)
```
Advantages:

* Hide your backend
* Allows multiple apps with a single domain
* Handles HTTPS

### What is Docker? (key for Portainer)

``Docker = apps in containers.``

Example:

* App Node on port 3000
* DB in another container

---

## Steps to create a ``local domain`` (e.g., project.local):

### Windows:
1. Open the ``Notepad`` as an Administrator (or ``powershell``).
2. Open the etc hosts file ``C:\Windows\System32\drivers\etc\hosts``
3. Add at the end: ``127.0.0.1 project.local``
4. Save changes.

### macOS/Linux:
1. Open the terminal.
2. Executes: ``sudo nano /etc/hosts``
3. Add: ``127.0.0.1 project.local``
4. Save (Ctrl+O, Enter) and exit (Ctrl+X).