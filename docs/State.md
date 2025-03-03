# O que é 

O state é um padrão de projeto compotamental que visa estruturar objetos que mudam de comportamento quando o estado interno é modificado. Como analogia, um celular pode ser comportar de maneiras diferentes quando está ligado ou desligado e os mesmos botões também podem mudar de comportamento. 

## Problema

Supondo que criemos um programa que um objeto pode ser comportar de diferentes maneiras quando seu estado muda com o if-else ou switch. A medida que a aplicação continue evoluindo, a quantidade de estados também vai continuar crescendo. Como resultado, a quantidade de estados torna-se absurdamente grande, tornando a aplicação complexa demais para melhora-la e torna-la eficiente. 

## Solução 

Para descomplica-la e resolver este problema, é pertinente o uso deste padrão, construindo objetos concretos que tenha os comportamentos inclusos, herdados da interface *state*. Dessa forma, é possivel administrar a quantidade de estados, sem ter a necessidade de analisar um por um os estados if-else ou switch, sendo apenas preciso modificar estes estados, adaptando-as conforme as dores. 

```java

// Interface para os estados
interface CelularState {
    void exibirStatus();
}


// Estado: Celular disponível em estoque
class EmEstoque implements CelularState {
    @Override
    public void exibirStatus() {
        System.out.println("📱 O celular está disponível para compra!");
    }
}

// Estado: Celular fora de estoque
class ForaDeEstoque implements CelularState {
    @Override
    public void exibirStatus() {
        System.out.println("❌ O celular está fora de estoque.");
    }
}

// Estado: Celular em promoção
class EmPromocao implements CelularState {
    @Override
    public void exibirStatus() {
        System.out.println("🔥 O celular está em promoção! Aproveite!");
    }
}

// Classe Contexto que mantém o estado atual
class Celular {
    private CelularState estadoAtual;

    public Celular(CelularState estadoInicial) {
        this.estadoAtual = estadoInicial;
    }

    public void setEstado(CelularState novoEstado) {
        this.estadoAtual = novoEstado;
    }

    public void exibirStatus() {
        estadoAtual.exibirStatus();
    }
}



public class LojaDeCelulares {
    public static void main(String[] args) {
        // Criando um celular que começa em estoque
        Celular celular = new Celular(new EmEstoque());

        // Exibir status atual
        celular.exibirStatus();

        // Mudar estado para "Fora de Estoque"
        celular.setEstado(new ForaDeEstoque());
        celular.exibirStatus();

        // Mudar estado para "Em Promoção"
        celular.setEstado(new EmPromocao());
        celular.exibirStatus();
    }
}

```
