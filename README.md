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
Services = namedtuple('Services', ['status', 'datetime', 'latency'])

# Criando instância da namedtuple para representar um sistema de monitoramento
system_eagle = System(name='Eagle', description='Monitoring from the sky', services=[])

# Registrando os dados de chamadas de API de HealthCheck no sistema de monitoramento.
# 2ª Chamada API HealthCheck
services_api_health_check = Services(status=True, datetime='2023-07-29 14:25:01.065', latency=292)
system_eagle.services.append(services_api_health_check)

# 2ª Chamada API -> Também podemos informar os valores seguindo a posição
system_eagle.services.append(Services(False, '2023-07-29 14:30:02.052', 125))
system_eagle.services.append(Services(False, '2023-07-29 14:35:01.027', 195))

# Agora podemos acessar e imprimir os detalhes das chamadas de API registradas
print(f"Sistema: {system_eagle.name} - {system_eagle.description}")
# Sistema: Eagle - Monitoring from the sky
for idx, service in enumerate(system_eagle.services, start=1):
    status = "Online" if service.status else "Offline"
    print(f"Consulta {idx}: Status: {status} | Data e Hora: {service.datetime} | Latência: {service.latency} ms")

#	Consulta 1: Status: Online | Data e Hora: 2023-07-29 14:25:01.065 | Latência: 292 ms
#	Consulta 2: Status: Offline | Data e Hora: 2023-07-29 14:30:02.052 | Latência: 125 ms
#	Consulta 3: Status: Offline | Data e Hora: 2023-07-29 14:35:01.027 | Latência: 195 ms
```
Neste exemplo, estamos usando a collections.namedtuple para criar uma estrutura de dados para sistemas de monitoramento e seus serviços associados. Registramos dados de chamadas de API no sistema e, em seguida, imprimimos esses detalhes de forma organizada.
