# Sistema Ajax

## Configuration

>**IMPORTANTE**
>
>Para ter um feedback em tempo real, é ABSOLUTAMENTE necessário que seu Jeedom esteja acessível de fora (URL de acesso externo usado)

A configuração do plugin é muito simples e ocorre em 2 passos : 

- Configurando o link entre seu jeedom e seu alarme
- adição de um compartilhamento de e-mail para relatar eventos 

>**IMPORTANTE**
>
>Um ponto importante Ajax não emite um alerta global quando um alarme é acionado, mas levanta o status no detector que acionou o alarme (comando de eventos)

### Configuração de link 

Para configurar o link entre seu Jeedom e seu alarme Ajax, vá para "Plugin" -> "Gerenciamento de Plugin" -> "Sistema Ajax" e clique em "Conectar", insira seus identificadores Ajax e clique em "Validar".

>**NOTA**
>
> Jeedom absolutamente não salva suas credenciais Ajax, é apenas uma usada para a primeira solicitação ao Ajax e para ter o token de acesso e o token de atualização. O token de atualização torna possível recuperar um novo token de acesso que tem uma vida útil de apenas algumas horas

>**NOTA**
>
> Uma vez feito o link, todas as solicitações passam por nossa nuvem, mas em nenhum momento a nuvem armazena seu token de acesso, portanto não é possível apenas com a nuvem jeedom atuar no seu alarme. Para qualquer ação sobre isso, você absolutamente precisa da combinação de seu token de acesso Jeedom e uma chave conhecida apenas por nossa nuvem 

### Configuração de relatórios de eventos

No aplicativo Ajax, vá para o hub e, em seguida, nas configurações (pequena engrenagem no canto superior direito), vá para o usuário e adicione o usuário : ajax@jeedom.com 

## Equipamento 

Uma vez que a configuração está em "Plugin" -> "Gerenciamento de Plugin" -> "Sistema Ajax" você apenas tem que sincronizar, Jeeodm irá criar automaticamente todo o equipamento Ajax vinculado à sua conta Ajax. 

### Detector de movimento

Pequena especificidade para o detector de movimento, não vai até a detecção de movimento de forma permanente. Na verdade, só sobe quando o alarme está ativo e pelo comando do evento

### Detector de abertura

Para ele não se preocupe você tem todo o tempo e em tempo real as informações da janela aberta ou não.