# O que é 

O state é um padrão de projeto compotamental que visa estruturar objetos que mudam de comportamento quando o estado interno é modificado. Como analogia, um celular pode ser comportar de maneiras diferentes quando está ligado ou desligado e os mesmos botões também podem mudar de comportamento. 

![State](https://github.com/user-attachments/assets/33a9fdc6-8e50-4fd1-8dfa-3f5aabbe20af)

## Problema

Supondo que criemos um programa que um objeto pode ser comportar de diferentes maneiras quando seu estado muda com o if-else ou switch. A medida que a aplicação continue evoluindo, a quantidade de estados também vai continuar crescendo. Como resultado, a quantidade de estados torna-se absurdamente grande, tornando a aplicação complexa demais para melhora-la e torna-la eficiente. 

**Exemplo**: 
```java
public class ObjetoColorido {
    private String estadoAtual;

    // Construtor inicializando a cor
    public ObjetoColorido(String estadoInicial) {
        this.estadoAtual = estadoInicial;
    }

    // Método para alterar o estado (mudar a cor)
    public void setEstado(String novoEstado) {
        this.estadoAtual = novoEstado;
    }

    // Método para exibir a cor atual
    public void mostrarCor() {
        if (estadoAtual.equalsIgnoreCase("vermelho")) {
            System.out.println("🔴 O objeto está na cor VERMELHO.");
        } else if (estadoAtual.equalsIgnoreCase("verde")) {
            System.out.println("🟢 O objeto está na cor VERDE.");
        } else if (estadoAtual.equalsIgnoreCase("azul")) {
            System.out.println("🔵 O objeto está na cor AZUL.");
        } else if (estadoAtual.equalsIgnoreCase("amarelo")) {
            System.out.println("🟡 O objeto está na cor AMARELO.");
        } else {
            System.out.println("⚫ Cor desconhecida.");
        }
    }

    public static void main(String[] args) {
        // Criando um objeto que começa na cor Vermelho
        ObjetoColorido objeto = new ObjetoColorido("vermelho");

        // Exibir estado atual
        objeto.mostrarCor();

        // Mudar para Verde
        objeto.setEstado("verde");
        objeto.mostrarCor();

        // Mudar para Azul
        objeto.setEstado("azul");
        objeto.mostrarCor();

        // Mudar para Amarelo
        objeto.setEstado("amarelo");
        objeto.mostrarCor();
    }
}
```

## Solução 

Para descomplica-la e resolver este problema, é pertinente o uso deste padrão, construindo objetos concretos que tenha os comportamentos inclusos, herdados da interface *state*. Dessa forma, é possivel administrar a quantidade de estados, sem ter a necessidade de analisar um por um os estados if-else ou switch, sendo apenas preciso modificar estes estados, adaptando-as conforme as dores. 

## Código 

No código, o objeto pode mudar de comportamento conforme a mudança de cor, utilizando os métodos do próprio objeto Cor
```java

// Interface para os estados de cor
interface CorState {
    void mostrarCor();
}

// Estado: Vermelho
class CorVermelho implements CorState {
    @Override
    public void mostrarCor() {
        System.out.println("🔴 O objeto está na cor VERMELHO.");
    }
}

// Estado: Verde
class CorVerde implements CorState {
    @Override
    public void mostrarCor() {
        System.out.println("🟢 O objeto está na cor VERDE.");
    }
}

// Estado: Azul
class CorAzul implements CorState {
    @Override
    public void mostrarCor() {
        System.out.println("🔵 O objeto está na cor AZUL.");
    }
}

// Estado: Amarelo
class CorAmarelo implements CorState {
    @Override
    public void mostrarCor() {
        System.out.println("🟡 O objeto está na cor AMARELO.");
    }
}

// Classe Contexto que mantém a referência para o estado atual
class ObjetoColorido {
    private CorState estadoAtual;

    // Construtor inicializando com uma cor
    public ObjetoColorido(CorState estadoInicial) {
        this.estadoAtual = estadoInicial;
    }

    // Método para alterar o estado (mudar a cor)
    public void setEstado(CorState novoEstado) {
        this.estadoAtual = novoEstado;
    }

    // Método para exibir a cor atual
    public void mostrarCor() {
        estadoAtual.mostrarCor();
    }
}

public class TesteState {
    public static void main(String[] args) {
        // Criando um objeto que começa na cor Vermelho
        ObjetoColorido objeto = new ObjetoColorido(new CorVermelho());

        // Exibir estado atual
        objeto.mostrarCor();

        // Mudar para Verde
        objeto.setEstado(new CorVerde());
        objeto.mostrarCor();

        // Mudar para Azul
        objeto.setEstado(new CorAzul());
        objeto.mostrarCor();

        // Mudar para Amarelo
        objeto.setEstado(new CorAmarelo());
        objeto.mostrarCor();
    }
}

```
## Diagrama para melhor entendimento
![State drawio](https://github.com/user-attachments/assets/fc0ca8de-6d85-49bb-adb0-015084bff85c)
