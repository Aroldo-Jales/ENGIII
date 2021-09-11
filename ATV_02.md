

### Acoplamento

```java
public class Conta {
    private String numero;
    private double saldo;

    public Conta(String numero, double saldo) {
        this.numero = numero;
        this.saldo = saldo;
    }

    public void sacar(double valor) {
        validarValor(valor);
        this.saldo -= valor;
    }
```

```java
public class ContaImposto extends Conta {
    private double taxa = 0.38/100;

    public ContaImposto(String numero, double saldo) {
        super(numero, saldo);
    }
    
    @Override
    public void sacar(double valor){
        super.sacar(valor);
        super.sacar(valor*getTaxa()); 
    }
```

```java
public class Poupanca extends Conta {
    private double taxaDeJuros;

    public Poupanca(double taxaDeJuros, String numero, double saldo) {
        super(numero, saldo);
        this.taxaDeJuros = taxaDeJuros;
    }
    
    public void renderJuros() {
        double juros = this.getSaldo() * this.taxaDeJuros/100;
        depositar(juros);
    }

```

### Coesão

```java

public class Retangulo implements FiguraGeometrica, Comparavel {
    
    private double altura;
    private double base;

    public Retangulo(double altura, double base) {
        this.altura = altura;
        this.base = base;
    }

```


```java
public class Quadrado implements FiguraGeometrica, Comparavel{
    
    private double lado;

    public Quadrado(double lado) {
        this.lado = lado;
    }
    
```

```java

public class Triangulo implements FiguraGeometrica, Comparavel{
    
    private double base;
    private double altura;
    private double lado1;
    private double lado2;

    public Triangulo(float base, float altura, float lado1, float lado2) {
        this.base = base;
        this.altura = altura;
        this.lado1 = lado1;
        this.lado2 = lado2;
    }

```

### Encapsulamento

#### Antes
```java

public class Conta {
    private String numero;
    private double saldo;

    public Conta(String numero, double saldo) {
        this.numero = numero;
        this.saldo = saldo;
    }
    
    public void depositar(double valor) {
        this.saldo += valor;
    }

}


```
#### Depois

```java

public void depositar(double valor) {
    if(valor <= 0){
        throw new RuntimeException("Valor inválido!");
    } 
    this.saldo += valor;
}

```

## Encapsulamento

#### Antes

```java
public class Gerente extends Funcionario implements IAutenticavel{
    
    private double salario;
    private String login;
    private String senha;
    
    public Gerente(double salario, String login, String senha) {
        this.salario = salario;
        this.login = login;
        this.senha = senha;
    }
    
    @Override
    public double getBonificacao() {
        return (this.salario*0.7)+1000;
    }

    @Override
    public boolean autentica(String login, String senha) {
        if(login.equals(this.login) && senha.equals(this.senha)){
            return true;
        } else {
            return false;
        }
    }

    public double getSalario() {
        return salario;
    }

    public void setSalario(double salario) {
        this.salario = salario;
    }

    public String getLogin() {
        return login;
    }

    public void setLogin(String login) {
        this.login = login;
    }

    public String getSenha() {
        return senha;
    }

    public void setSenha(String senha) {
        this.senha = senha;
    }
}
```

#### Depois

```java
public class Gerente extends Funcionario implements IAutenticavel{
    
    private double salario;
    private String login;
    private String senha;
    
    public Gerente(double salario, String login, String senha) {
        this.salario = salario;
        this.login = login;
        this.senha = senha;
    }
    
    @Override
    public double getBonificacao() {
        return (this.salario*0.7)+1000;
    }

    @Override
    public boolean autentica(String login, String senha) {
        Boolean valido = (login.equals(this.login) && senha.equals(this.senha)) ? true: false;
        return valido;
    }

    public double getSalario() {
        return salario;
    }

    public void setSalario(double salario) {
        if (salario > 1000000 || salario < 0) {
            throw new RuntimeException("Valor para Salário inválido!");
        }
        this.salario = salario;
    }

    public String getLogin() {
        return login;
    }

    public void setLogin(String login) {
        this.login = login;
    }

    public String getSenha() {
        return senha;
    }

    public void setSenha(String senha) {
        if (validarSenha(senha)){
            this.senha = senha;
        }
    }

    private boolean validarSenha(String senha) {
        if (senha.length() < 11) {
            throw new RuntimeException("Senha com menos de 11 caraceteres, Inválida!");
        }
    }
}
```
