# Deploy Server - Rally Logistique

Serveur web avec nginx-proxy, acme-companion (Let's Encrypt) et accès HTTPS sur rally-logistique.cloud.

## Prérequis

- Docker et Docker Compose
- Le domaine `rally-logistique.cloud` doit pointer vers l’IP du serveur (DNS A ou AAAA)
- Ports 80 et 443 ouverts sur le pare-feu

## Configuration

1. Copier `.env.example` en `.env` :
   ```bash
   cp .env.example .env
   ```

2. Renseigner l’email Let's Encrypt dans `.env` :
   ```
   LETSENCRYPT_EMAIL=admin@rally-logistique.cloud
   ```

## Lancement

```bash
docker compose up -d
```

## Accès

- **HTTP :** http://rally-logistique.cloud (redirection vers HTTPS si certif OK)
- **HTTPS :** https://rally-logistique.cloud

## Structure

```
.
├── docker-compose.yaml   # nginx-proxy + acme-companion + web
├── nginx/
│   ├── conf.d/           # config globale nginx
│   │   └── custom.conf
│   └── vhost.d/          # config par vhost
│       └── rally-logistique.cloud
├── www/
│   └── index.html        # contenu du site
└── .env                  # LETSENCRYPT_EMAIL
```

## Fichiers nginx

- `nginx/conf.d/custom.conf` : paramètres globaux (timeouts, buffers)
- `nginx/vhost.d/rally-logistique.cloud` : paramètres spécifiques au domaine (headers de sécurité, client_max_body_size)
