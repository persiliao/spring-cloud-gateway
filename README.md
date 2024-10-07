# Spring cloud gateway

The latest spring cloud gateway integrates with nacos and supports dynamically updating routes from nacos configurations.

## Environment

```ini
; Application
GATEWAY_CFG_PORT=80
GATEWAY_CFG_APPLICATION_NAME="gateway"
GATEWAY_CFG_PROFILES_ACTIVE="dev"

; Nacos Config
GATEWAY_CFG_CONFIG_SERVER="127.0.0.1:8848"
GATEWAY_CFG_CONFIG_NAMESPACE="plublic"
GATEWAY_CFG_CONFIG_FILE_EXTENSION="yml"

; Nacos Discovery
GATEWAY_CFG_DISCOVERY_SERVER="127.0.0.1:8848"
GATEWAY_CFG_DISCOVERY_NAMESPACE="public"

# Java
JAVA_OPTS="-Xms256m -Xmx1024m -XX:+UseG1GC"
```

## Nacos Config

```yml
# Nacos Config DataId: gateway-dev.yml
spring:
  cloud:
    gateway:
      routes:
        # Auth Service
        - id: auth-service
          uri: lb://auth-service
          predicates:
            - Path=/auth/**
          filters:
            - StripPrefix=1
```

## Usage

```shell
docker run -t -d --name spring-cloud-gateway persiliao/spring-cloud-gateway
```