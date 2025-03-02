# O que é


É um padrão de porjeto que faz parte do gurpo dos comportamentais, que permite que reduza a quantidade de dependencias caóticas entre os objetos. Por exemplo: se um objeto estiver ligado com outro, e mais outro, e assim por diante, a codifcação se tornaria complexo demais da realizar manutenção. Uma modifcação de uma classe poderia geral inúmeros problemas, dificultando a sua melhoria. 

Portanto, este padrão visa simplifcar a comunicação entre os objetos, adicionando um mediator entre elas, sendo responsável por administrar a comunicação entre elas. É como se fosse um curso online onde os alunos não poderão contactar pessoalmente, mas poderá se comunicar atráves da plataforma do curso. Outro exemplo seria a aba de comentários de redes sociais. 

Resumindo, este modelo tem como objetivo usar um objeto para administrar a comunicação entre objetos, tornando a aplicação mais dinamica e eficiente e diminuindo a comunicação direta entre objetos. 



## Problema 

Existem ocorrencia de erros por causa da complexificação excessiva de forma frequente conforme a aplicação vai evoluindo, principalemte quando não é implementado um padrão de projeto. Por exemplo, é comum que as aplicações que não tenham esses padrões terem erros em virtude da quantidade absurda de objetos ligados entre si, tornando suas modificações complexas. Se um objeto sofre uma modifcação, há uma grande chance de isso afetar outros objetos, tendo como consequencia o aumento do tempo requerido para analisar e modificar os objetos afetados, sendo esta superior ao tempo requerido para modificação.  

![](https://github.com/YuuyaOkatani/Design-Patterns-Comportamental-Examples/blob/main/docs/images/Mediator.png)

Desse modo, é de suma importancia solucionar esta problemática com o uso do padrão Mediator



## Solução

Como solução, ao invés de criar objetos e conecta-los de forma desordenada, é válido criar um objeto Mediator, que torna os objetos independentes um ao outro. Em outras palavras, quando um objeto é acionado para se comunicar com os outros, ele envia uma mensagem através do objeto Mediator, e este Mediator direciona esta para o destinatário. 

![Mediator2](https://github.com/user-attachments/assets/290e7793-0bc5-4995-b059-c16180da2cc9)

## Código

Este código serve como exemplo para mostrar este conceito de forma prática. No código, o ChatRoom herda os métodos do ChatMediator, enquanto a classe abstrata User agrega o ChatRoom, instanciada pela ChatUser. 
Dessa forma, para um usuário enviar uma mensagem, ele passa por ChatRoom, que usa os métodos do ChatMediator modifcados, e todos usuarios receberão a mensagem.


```

import java.util.ArrayList;
import java.util.List;

// Interface Mediator
interface ChatMediator {
    void sendMessage(String message, User sender);
    void addUser(User user);
}

// Implementação concreta do Mediator
class ChatRoom implements ChatMediator {
    private List<User> users = new ArrayList<>();

    @Override
    public void addUser(User user) {
        users.add(user);
    }

    @Override
    public void sendMessage(String message, User sender) {
        for (User user : users) {
            if (user != sender) {
                user.receiveMessage(message);
            }
        }
    }
}

// Classe base para os participantes do chat
abstract class User {
    protected ChatMediator mediator;
    protected String name;

    public User(String name, ChatMediator mediator) {
        this.name = name;
        this.mediator = mediator;
    }

    public abstract void sendMessage(String message);
    public abstract void receiveMessage(String message);
}

// Implementação concreta de um usuário
class ChatUser extends User {
    public ChatUser(String name, ChatMediator mediator) {
        super(name, mediator);
    }

    @Override
    public void sendMessage(String message) {
        System.out.println(name + " enviando: " + message);
        mediator.sendMessage(message, this);
    }

    @Override
    public void receiveMessage(String message) {
        System.out.println(name + " recebeu: " + message);
    }
}

// Testando a implementação
public class MediatorPatternExample {
    public static void main(String[] args) {
        ChatMediator chatRoom = new ChatRoom();

        User alice = new ChatUser("Alice", chatRoom);
        User bob = new ChatUser("Bob", chatRoom);
        User charlie = new ChatUser("Charlie", chatRoom);

        chatRoom.addUser(alice);
        chatRoom.addUser(bob);
        chatRoom.addUser(charlie);

        alice.sendMessage("Oi, pessoal!");
        bob.sendMessage("Olá, Alice!");
    }
}

```

