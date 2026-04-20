# OpenVAS Stack (Portainer)

Este repositório está pronto para deploy via **Portainer > Stacks > Repository**.

## Campos no Portainer

- **Repository URL**: use a URL de clone Git (exemplo: `https://github.com/SEU_USUARIO/SEU_REPO.git`)
- **Repository reference**: `refs/heads/main`
- **Compose path**: `docker-compose.yml`

> **Importante:** não use link de página (como `/tree/main` ou URL copiada do navegador).

## stack.env (modo Repository)

No modo **Repository**, o Portainer espera que o arquivo `stack.env` já exista no repositório.

Este repo já inclui `stack.env` com variáveis usadas no `docker-compose.yml`:

- `OPENVAS_USERNAME`
- `OPENVAS_PASSWORD`
- `OPENVAS_HTTPS_PORT`

Antes de subir em produção, altere usuário e senha no `stack.env`.

## Acesso

Após subir a stack e aguardar a inicialização dos feeds:

- URL: `https://SEU_HOST:${OPENVAS_HTTPS_PORT}` (padrão `8080`)
- Usuário: valor de `OPENVAS_USERNAME`
- Senha: valor de `OPENVAS_PASSWORD`

> Na primeira inicialização, o OpenVAS pode levar alguns minutos para ficar 100% operacional.

## Troubleshooting do erro "repository not found: <!DOCTYPE html>"

Esse erro normalmente indica que o Portainer recebeu HTML do GitHub em vez de uma resposta Git.

Verifique:

1. URL termina com `.git`.
2. URL aponta para o repositório (não para página web `/tree/...`, `/blob/...`, etc).
3. Se o repo for privado, habilite **Authentication** no Portainer e use usuário + PAT/token.
4. Teste no host do Portainer:

```bash
git ls-remote https://github.com/SEU_USUARIO/SEU_REPO.git
```

Se esse comando falhar no host, o Portainer também vai falhar.


## Se o feed sync ficar preso mesmo com porta 873 liberada

Se `nc -vz` no host funcionar, mas o container continuar preso no download dos feeds, o problema pode ser resolução/rota IPv6.

Este `docker-compose.yml` já inclui `extra_hosts` para forçar IPv4 nos endpoints de feed:

- `rsync.immauss.com -> 57.129.41.31`
- `feed.community.greenbone.net -> 45.135.106.143`

Após atualizar a stack, force recriação do container para aplicar os hosts:

```bash
docker compose down
docker compose up -d
```

> Observação: `nc` não existe dentro da imagem por padrão. Isso é esperado e não indica erro do OpenVAS.
