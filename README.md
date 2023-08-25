# Sistema de monitoramento com nomeadotuple

## Introduction

Olá, pessoal! 👋

Hoje, quero compartilhar com vocês uma ferramenta incrível do Python que pode tornar seu código mais limpo, organizado e fácil de entender: collections.namedtuple.

Vamos supor que estamos trabalhando em um projeto de gerenciamento de uma loja de eletrônicos, e precisamos lidar com informações sobre produtos. Ao invés de usar dicionários ou tuplas tradicionais para armazenar esses dados, podemos aproveitar ao máximo a funcionalidade do collections.namedtuple.

```python
from collections import namedtuple

# Definindo uma estrutura de dados usando namedtuple.
field_names = 'name description services'
System = namedtuple('System', field_names)
# Os campos também podemos definir assim:
Services = namedtuple('Services', ('url_api', 'healthcheck'))
HealthCheck = namedtuple('HealthCheck', 'status datetime latency')

# Criando instância da namedtuple para representar um sistema de monitoramento
system_eagle = System(name='Eagle', description='Monitoring from the sky', services=[])
services_api_healthcheck = Services(url_api='www.system_eagle.com/healthcheck', healthcheck=[])
services_api_database = Services(url_api='www.system_eagle.com/database', healthcheck=[])
system_eagle.services.extend([services_api_healthcheck, services_api_database])

# Registrando os dados de chamadas de API de HealthCheck no sistema de monitoramento.
# 2ª Chamada API HealthCheck
healthcheck_api = HealthCheck(status=True, datetime='2023-07-29 14:25:01.065', latency=292)
services_api_healthcheck.healthcheck.append(healthcheck_api)
healthcheck_database = HealthCheck(status=True, datetime='2023-07-29 14:26:01.065', latency=632)
services_api_database.healthcheck.append(healthcheck_database)

# 2ª Chamada API -> Também podemos informar os valores seguindo a posição
services_api_healthcheck.healthcheck.append(HealthCheck(False, '2023-07-29 14:30:02.052', 125))
services_api_database.healthcheck.append(HealthCheck(False, '2023-07-29 14:35:01.027', 195))


# Agora podemos acessar e imprimir os detalhes das chamadas de API registradas
print(f"Sistema: {system_eagle.name} - {system_eagle.description}:\n")
for service in system_eagle.services:
    for healthcheck in service.healthcheck:
        status = "Online" if healthcheck.status else "Offline"
        print(f"API: {service.url_api} | Status: {status} | Data e Hora: {healthcheck.datetime} | Latência: {healthcheck.latency} ms")
    print()  # Adding a blank line between services

'''
    Sistema: Eagle - Monitoring from the sky

    API: www.system_eagle.com/healthcheck | Status: Online | Data e Hora: 2023-07-29 14:25:01.065 | Latência: 292 ms
    API: www.system_eagle.com/healthcheck | Status: Offline | Data e Hora: 2023-07-29 14:30:02.052 | Latência: 125 ms

    API: www.system_eagle.com/database | Status: Online | Data e Hora: 2023-07-29 14:26:01.065 | Latência: 632 ms
    API: www.system_eagle.com/database | Status: Offline | Data e Hora: 2023-07-29 14:35:01.027 | Latência: 195 ms
'''
```
Neste exemplo, estamos usando a collections.namedtuple para criar uma estrutura de dados para sistemas de monitoramento e seus serviços associados. Registramos dados de chamadas de API no sistema e, em seguida, imprimimos esses detalhes de forma organizada.
