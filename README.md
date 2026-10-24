# logitrack-config

Repositorio de configuraciones externas de LogiTrack, servido por `config-server` (Spring Cloud Config).

## Convención de nombres

| Archivo                        | Se aplica a                     |
|--------------------------------|---------------------------------|
| `<servicio>.yaml`              | todos los perfiles              |
| `<servicio>-dev.yaml`          | perfil `dev` (IDE / local)      |
| `<servicio>-prod.yaml`         | perfil `prod` (Docker Compose)  |

`<servicio>` = valor de `spring.application.name` del cliente: `shipment-service`, `courier-service`, `security-service`.
El perfil sobrescribe al archivo base.

## Regla de oro: NO SECRETOS

Acá solo va configuración no sensible. Las claves se escriben como placeholders (`${DB_PASSWORD}`) y
cada contenedor las recibe por variable de entorno (ver `.env.example` del Compose).

## Verificación rápida

```
curl http://localhost:8888/courier-service/dev
curl http://localhost:8888/courier-service/prod
```

Los placeholders aparecen sin resolver (`${DB_PASSWORD}`): es lo esperado, los resuelve cada cliente con su entorno.

## Cambios

Los clientes leen la configuración al arrancar. Tras un commit a `main`, reiniciá el servicio que quieras actualizar.
