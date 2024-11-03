# Descomplicando as Networks no Docker

<br>

Docker **Network** refere-se à capacidade dos containers se conectarem e se comunicarem entre si ou com cargas de trabalho não Docker.

<br>

## Drivers

Os seguintes drivers de rede estão disponíveis por padrão e fornecem funcionalidades básicas de rede:

- `bridge`: O driver de rede padrão.
- `host`: Remova o isolamento de rede entre o container e o host Docker.
- `none`: Isole completamente um contêiner do host e de outros contêineres.
- `overlay`: Conecta vários daemons Docker (hosts) entre si.
- `ipvlan`: As redes IPvlan fornecem controle total sobre o endereçamento IPv4 e IPv6.
- `macvlan`: Atribua um endereço MAC a um container.

Para mais informações consulte: [Network drivers](https://docs.docker.com/engine/network/drivers/).

<br>

