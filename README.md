# Configuración de hosts con Ansible

Práctica de Ansible que define dos grupos de hosts (DB y ML) y ejecuta tareas específicas en cada uno.

---

## Estructura del proyecto

```
host-config-ansible/
├── playbook.yml        # Playbook principal
├── inventory.yml       # Inventario de hosts
└── README.md
```

---

## Grupos y tareas

**DB:**
- Instala Nginx
- Crea el usuario nginx
- Deja un fichero /etc/provisioned con la fecha de aprovisionamiento

**ML:**
- Instala Python, pip y venv
- Crea un entorno virtual en /opt/venv
- Instala Pandas en el entorno virtual
- Deja un fichero /etc/provisioned con la fecha de aprovisionamiento

---

## Requisitos

- Debian 12/13
- Ansible 2.9+
- Acceso sudo en el host destino

---

## Uso

### 1. Clona el repositorio

```bash
git clone git@github.com:Pedro-Sarmiento/host-config-ansible.git
cd host-config-ansible
```

### 2. Ejecuta el playbook

```bash
ansible-playbook -i inventory.yml playbook.yml --ask-become-pass
```

### 3. Verifica el aprovisionamiento

```bash
cat /etc/provisioned
```

---

## Idempotencia

El playbook puede ejecutarse varias veces sin efectos secundarios ni errores.

---

## Licencia

MIT
