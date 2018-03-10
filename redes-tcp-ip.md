## Redes em Python
  
### Endereços IP
  
O IP serve para endereçar todo dispositivo conectado a uma rede como também ajudar no roteamento de pacotes dentro de uma rede.
  
Dentro de uma rede só pode haver um dispositivo com determinado IP atribuito. Todos os outros dispositivos tem IP diferente.
  
O endereço IP é um número de 32 bits representado na forma de 4 octetos separados por pontos. Cada octeto só pode formar valores de 0 à 255.
  
Para verificar os endereços IPs atribuidos às interfaces de rede(placas de rede, placa wireless, etc) na máquina use o comando:
  
```sh
ip addr
```
  
Cada dispositivo normalmente tem um endereço ip para se auto-referenciar chamado de endereço de `loopback`. Este endereço gerealmente é o `127.0.0.1` ou `localhost`.
  
### Atribuição de IPs
  
Endereços IPs podem ser atribuidos para um dispositivo de duas formas. 

- `Estaticamente` - Um endereço é definido estaticamente no sistema operacional.  
  
- `Dinamicamente` - No momento em que o dispositivo se conecta à rede, um servidor `DHCP`(Dynamic Host Configuration Protocol) lhe fornece um endereço IP aleatório. O DHCP é muito usado em redes em que muitos dispositivos diferentes se conectam a ela.
  
### IPs na Internet
  
A `Internet` é uma grande rede IP tendo todos os dispositivos conectados à ela um endereço IP associado.  
  
A `IANA`(Internet Assigned Numbers Authority) é a organização mundial que gerencia a alocação das faixas de endereços IPs. Ela repassa blocos de faixas IPs para determinadas regiões através das `RIRs`(Regional Internet Registries) que tem a responsabilidade que alocar blocos de IPs para países e organizações.
  
A IANA definiu que determinadas faixas só poderiam ser usadas dentro de redes locais. Essas faixas de IPs são chamados de `endereços privados`.
  
Como várias máquinas em diferentes redes usam o mesmo endereço IP privado localmente, quando essas tentam acessar redes externas através da Internet, elas usam a técnica do `NAT`(Network Address Translation) que converte qualquer endereço privado em um endereço público válido, evitando que mais de uma máquina tenha o mesmo endereço IP dentro da Internet.
  
Abaixo as faixas de endereços privados definidos pela IANA:
  
* 10.0.0.0 até 10.255.255.255  
* 172.16.0.0 até 172.31.255.255  
* 192.168.0.0 até 192.168.255.255
  
### Pacotes
  
Para os dados serem transmitidos pela rede, primeiro tem que sofrer uma transformação chamada de `empacotamento`. Essa transformação consiste em quebrar o dado em partes menores de bytes.
  
Cada pequena parte do dado é separadamente prefixada com uma informação sobre o protocolo que irá manipulá-la. Esse prefixo é chamado de `header` ou `cabeçalho`.
  
Cada pequena parte do `dado` junto com o seu `cabeçalho` formam um `pacote`. O dado dentro de um pacote também é chamado de `payload` que é a carga útil do pacote.
  
Em outros protocolos ou camadas um pacote pode ser referenciado com outros nomes como por exemplo o `frame`.
  
O `header` contém todas as informações que o protocolo que receberá o pacote necessitará saber para trabalhar com o pacote. O cabeçalho de um pacote IP contém as seguintes informações:
  
* Endereço IP de origem e destino do pacate;  
* Tamanho total do pacote;  
* E o checksum dos dados(Verificar a integridade do pacote).
  
Depois de criados, os pacotes são enviados para a rede onde serão roteados separadamente até o destino.
  
### Vantagens em usar pacotes(unidades de dados)
  
Como os pacotes são pequenos, as redes podem se beneficiar de algumas formas quando os usam, como:
  
* Multiplexação - Vários dispositivos podem enviar pacotes ao mesmo tempo;  
* Erros na transmissão de pacotes podem ser percebidos e notificados rapidamente;  
* Controle de congestionamento;  
* Rotear pacotes novamente de forma dinâmica.
  
### Encapsulamento de pacotes
  
Quando um pacote é enviado para outro protocolo de uma camada acima do seu protocolo, ele pode ser `encapsulado` em outro pacote. Se tornando o payload desse segundo e novo pacote.
  
### Gateway
  
`Gateway` geralmente é o ponto de conexão entre os dispositivos de uma rede. O gateway geralmente existe em forma de `roteador`.
  
O roteador direciona o tráfego de dados entre redes. Ele fica entre duas ou mais redes. Tem duas ou mais interfaces; uma para cada rede conectada a ele.
  
Dentro do roteador existe a `tabela de roteamento` que indica, através do ip, o destino de pacotes que passam por ele.
  
O roteador ou gateway encaminha os pacotes para outro roteador que geralmente está em um nível acima do dele, e geralmente localizado no `ISP`(Internet Service Provider).
  
Os roteadores dos ISP trafegam em uma rede externa, uma rede de gateways. São organizados em camadas e, os de nível acima fazem o roteamento entre países e continentes formando o `backbone`(espinha dorsal) da Internet.
  
### Roteando com IP
  
Um endereço ip pode ser interpretado como feito de duas partes lógicas:
  
* `Um prefixo de rede` - São os "n" primeiros números(em binário) de um endereço de rede.  
* `Um identificador de host` - São os "n" números(em binário) restantes de um endereço de rede.  
  
O número de bits alocados para o prefixo de rede pode ser determinado de duas formas: `CIDR notation` ou com `máscara de subrede`.
  
* CIDR notation - É mostrado o número ip e, logo após, uma barra seguida do número de bits destinados à rede. Ex.: 192.168.0.2/24.
  
* Máscara de subrede - É um número de 32 bits escrito em notação de pontos. Onde, em binário, os números mais a esquerda com valor 1 somados indicarão o número de bits reservados para o endereço de rede.
  
```
255.255.255.0
11111111.11111111.11111111.00000000 = /24
```
  
