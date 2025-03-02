## O que é
--- 

É um padrão de porjeto que faz parte do gurpo dos comportamentais, que permite que reduza a quantidade de dependencias caóticas entre os objetos. Por exemplo: se um objeto estiver ligado com outro, e mais outro, e assim por diante, a codifcação se tornaria complexo demais da realizar manutenção. Uma modifcação de uma classe poderia geral inúmeros problemas, dificultando a sua melhoria. 

Portanto, este padrão visa simplifcar a comunicação entre os objetos, adicionando um mediator entre elas, sendo responsável por administrar a comunicação entre elas. É como se fosse um curso online onde os alunos não poderão contactar pessoalmente, mas poderá se comunicar atráves da plataforma do curso. Outro exemplo seria a aba de comentários de redes sociais. 

Resumindo, este modelo tem como objetivo usar um objeto para administrar a comunicação entre objetos, tornando a aplicação mais dinamica e eficiente e diminuindo a comunicação direta entre objetos. 

---

**Problema** 

Existem ocorrencia de erros por causa da complexificação excessiva de forma frequente conforme a aplicação vai evoluindo, principalemte quando não é implementado um padrão de projeto. Por exemplo, é comum que as aplicações que não tenham esses padrões terem erros em virtude da quantidade absurda de objetos ligados entre si, tornando suas modificações complexas. Se um objeto sofre uma modifcação, há uma grande chance de isso afetar outros objetos, tendo como consequencia o aumento do tempo requerido para analisar e modificar os objetos afetados, sendo esta superior ao tempo requerido para modificação.  


Desse modo, é de suma importancia solucionar esta problemática com o uso do padrão Mediator

**Solução** 

Como solução, ao invés de criar objetos e conecta-los de forma desordenada, é válido criar um objeto Mediator, que torna os objetos independentes um ao outro. Em outras palavras, quando um objeto é acionado para se comunicar com os outros, ele envia uma mensagem através do objeto Mediator, e este Mediator direciona esta para o destinatário. 

**Código** 

Este código serve como exemplo para mostrar este conceito de forma prática. No código, o ChatRoom herda os métodos do ChatMediator, enquanto a classe abstrata User agrega o ChatRoom, instanciada pela ChatUser. 
Dessa forma, para um usuário enviar uma mensagem, ele passa por ChatRoom, que usa os métodos do ChatMediator modifcados, e todos usuarios receberão a mensagem.

