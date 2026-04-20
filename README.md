# OpenVAS Stack (Portainer)

Este repositório está pronto para deploy via **Portainer > Stacks > Repository**.

## Campos no Portainer

- **Repository URL**: `https://github.com/andersondrt84/openvas.git`
- **Repository reference**: `refs/heads/main`
- **Compose path**: `docker-compose.yml`

## Acesso

Após subir a stack e aguardar a inicialização dos feeds:

- URL: `https://SEU_HOST:8080`
- Usuário padrão: `admin`
- Senha padrão: `admin`

> Na primeira inicialização, o OpenVAS pode levar alguns minutos para ficar 100% operacional.

## Segurança (recomendado)

Altere imediatamente as credenciais em `docker-compose.yml`:

- `USERNAME`
- `PASSWORD`
