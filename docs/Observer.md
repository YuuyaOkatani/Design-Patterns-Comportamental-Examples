# O que é 

é um padrão de projeto comportamental que visa construir um sistema de notificação, muito utilizada por redes sociais. Este sistema é composto por objetos Publisher (publicadora) e os Subscribers (inscritos), sendo a publicadora esponsável por notificar os inscritos sobre os novos produtos ou novo conteúdo a ser consumido, através dos métodos. 

## Problema 

Supondo que uma pessoa está interessada em um novo celular, e ela vá a uma loja perto. Entretanto, esta descobre que o novo produto que ela deseja ainda não está disponível e, portanto, volta para casa frustrado. 
E volta para loja um tempo depois, mas não a encontra, e fica neste vai e volta. 

Outro problema é de que, se uma loja utiliza um sistema de notificação que notifica até usuários não interessados (spam), poderá ter a chance de perder mais clientes do que conquista-las, irritando-as. 
![Observer](https://github.com/user-attachments/assets/31a3d59a-9a6e-49a4-ad55-ab6df81a870a)

## Solução

Para evitar despedício de tempo dos clientes e a loja aumentar os mesmos, seria uma solução a implementação deste padrão, cadastrando seus clientes (Subscribers) na publicadora (Publisher). Dessa forma, a loja poderá notificar somente os clientes que estão interessados. 

![Observer2](https://github.com/user-attachments/assets/19cd9a98-bdc2-400f-8cf9-d2dd199f8711)

Ademais, este padrão pode ser altamente customizável, permitindo os desenvolvedores até adiconar métodos que notificam os inscritos com um interesse específico. 


## Código 

```java
import java.util.ArrayList;
import java.util.List;

// Publisher Interface (Sujeito)
interface Publisher {
    void subscribe(Subscriber subscriber);
    void unsubscribe(Subscriber subscriber);
    void notifySubscribers();
}

// ConcretePublisher (Sujeito - Loja de Celulares)
class CellPhoneStore implements Publisher {
    private List<Subscriber> subscribers = new ArrayList<>();
    private String newProduct;  // A loja vai notificar sobre um novo produto ou promoção

    @Override
    public void subscribe(Subscriber subscriber) {
        subscribers.add(subscriber);
    }

    @Override
    public void unsubscribe(Subscriber subscriber) {
        subscribers.remove(subscriber);
    }

    @Override
    public void notifySubscribers() {
        for (Subscriber subscriber : subscribers) {
            subscriber.update(newProduct);
        }
    }

    // Método para a loja anunciar um novo produto ou promoção
    public void setNewProduct(String product) {
        this.newProduct = product;
        notifySubscribers();  // Notificar todos os clientes inscritos
    }
}

// Subscriber Interface (Observador - Cliente)
interface Subscriber {
    void update(String product);  // Método chamado quando há novidades na loja
}

// ConcreteSubscriber (Observador Concreto - Cliente)
class Customer implements Subscriber {
    private String name;

    public Customer(String name) {
        this.name = name;
    }

    @Override
    public void update(String product) {
        System.out.println(name + " recebeu uma notificação sobre: " + product);
    }
}

// Client (Classe Principal)
public class Main {
    public static void main(String[] args) {
        // Criando a loja de celulares (Publisher)
        CellPhoneStore store = new CellPhoneStore();

        // Criando os clientes (Subscribers)
        Customer customer1 = new Customer("João");
        Customer customer2 = new Customer("Maria");

        // Inscrevendo os clientes na loja
        store.subscribe(customer1);
        store.subscribe(customer2);

        // A loja anuncia um novo produto
        store.setNewProduct("iPhone 15 - Lançamento!");

        // Removendo um cliente e anunciando outro produto
        store.unsubscribe(customer1);
        store.setNewProduct("Samsung Galaxy S25 - Promoção!");
    }
}
![Observer drawio (1)](https://github.com/user-attachments/assets/77838ce6-b831-4047-957e-ec392cecc85a)

