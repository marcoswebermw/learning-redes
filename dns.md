## DNS(Domain Name System)
  
O DNS é um protocolo e uma base dados hierárquica, distribuída mundialmente, que faz o mapeamento entre o hostnames e os seus endereços ips.
  
O DNS procura por hostnames em servidores de cache de forma hierárquica. Ou seja, se não encontra no primeiro servidor, passa para o próximo, e assim por diante até encontrar o host requerido.
  
Abaixo uma ferramenta que busca um endereço à partir do host passado usando servidores dns.
  
```sh
nslookup google.com.br

#RESULTADO:
Server:		127.0.1.1
Address:	127.0.1.1#53

Non-authoritative answer:
Name:	google.com.br
Address: 216.58.202.67
```
  
