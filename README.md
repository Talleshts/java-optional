# java-optional
Estudo dos métodos inclusos no Optional do Java Util

# Projeto: Uso da Classe Optional em Java

## Descrição

Este projeto explora a utilização da classe `Optional` em Java, introduzida na versão 8 da linguagem. A `Optional` é uma abstração que serve como contêiner para valores que podem ou não estar presentes, com o objetivo de reduzir a ocorrência de erros como `NullPointerException`, promovendo um código mais seguro e legível.

## Objetivo

O principal objetivo deste projeto é demonstrar como a classe `Optional` pode ser utilizada para tratar a ausência de valores de forma segura, evitando o uso direto de `null` e as possíveis falhas associadas. Além disso, o projeto mostra como utilizar métodos comuns da classe `Optional` para manipular esses valores de forma segura e expressiva.

## Estrutura do Projeto

### 1. Classe `Ativo`
A classe `Ativo` modela um ativo financeiro, com atributos como código, nome, valor atual e data da última atualização. Essa classe serve de exemplo para demonstrar como informações de ativos podem ser armazenadas e manipuladas.

### 2. Classe `AtivoRepository`
A classe `AtivoRepository` simula um repositório que armazena e gerencia uma lista de objetos `Ativo`. Ela demonstra o uso de `Optional` ao buscar ativos por código.

```java
import java.math.BigDecimal;
import java.time.LocalDate;
import java.util.ArrayList;
import java.util.List;
import java.util.Optional;

class AtivoRepository {
    private List<Ativo> ativos = new ArrayList<>();

    public AtivoRepository() {
        ativos.add(new Ativo("PETR4", "Petrobras PN", new BigDecimal("28.50"), LocalDate.now()));
        // Demais ativos...
    }

    public Optional<Ativo> findByCodigo(String codigo) {
        for (Ativo ativo : ativos) {
            if (ativo.getCodigo().equals(codigo)) {
                return Optional.of(ativo);
            }
        }
        return Optional.empty();
    }
}
```

### 3. Classe `Main`
A classe `Main` contém exemplos práticos de como usar métodos da classe `Optional`, como `isPresent()`, `get()`, `orElse()`, `orElseGet()`, `orElseThrow()`, e `ifPresent()`.

```java
public class Main {
    public static void main(String[] args) {
        AtivoRepository repository = new AtivoRepository();

        // Exemplo de uso do método isPresent()
        Optional<Ativo> ativoOpt1 = repository.findByCodigo("PETR4");
        if (ativoOpt1.isPresent()) {
            System.out.println("Ativo encontrado: " + ativoOpt1.get().getNome());
        } else {
            System.out.println("Ativo não encontrado.");
        }

        // Exemplo de uso do método get()
        Ativo ativo = repository.findByCodigo("VALE3").get();
        System.out.println("Ativo encontrado: " + ativo.getNome());

        // Outros exemplos de uso...
    }
}
```

## Métodos Principais da Classe Optional

- **`isPresent()`**: Verifica se há um valor presente no `Optional`.
- **`get()`**: Retorna o valor encapsulado, se presente; caso contrário, lança `NoSuchElementException`.
- **`orElse(T other)`**: Retorna o valor encapsulado, se presente; caso contrário, retorna um valor alternativo.
- **`orElseGet(Supplier<? extends T> other)`**: Retorna o valor encapsulado, se presente; caso contrário, chama o `Supplier` fornecido.
- **`orElseThrow(Supplier<? extends X> exceptionSupplier)`**: Retorna o valor encapsulado, se presente; caso contrário, lança uma exceção fornecida.
- **`ifPresent(Consumer<? super T> action)`**: Executa uma ação se o valor estiver presente.

## Conclusão

Este projeto ilustra como a classe `Optional` pode ser usada para tornar o código Java mais robusto e seguro, evitando erros comuns como `NullPointerException` e promovendo uma programação mais clara e explícita quanto ao tratamento de valores opcionais.
