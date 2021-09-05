// FAIL FIRST

//ANTES
//-----------------------------------------------------------------------------------//
```
public boolean baixar(int qtd){
    if (this.quantidade - qtd < qtdMin){
        System.out.println("Operação não realizada.");
        System.out.println("O produto estará abaixo da quantidade mínima.");
        return false;
    } else {
        this.quantidade =  this.quantidade - qtd; 
        return true;
    }
}
```
//DEPOIS
//-----------------------------------------------------------------------------------//
```
public boolean baixar(int qtd){
    if (this.quantidade - qtd < qtdMin){
        System.out.println("Operação não realizada.");
        System.out.println("O produto estará abaixo da quantidade mínima.");
        return false;
    } 
    this.quantidade =  this.quantidade - qtd; 
    return true;
}
```

// FAIL FIRST
//-----------------------------------------------------------------------------------//
```
public void inserir(Conta c){
    if (indice >= contas.length) {
        throw new AplicacaoException("Número máximo de contas atingido (50).");
    }
    contas[indice] = c;
    indice+=1;
}
```
//-----------------------------------------------------------------------------------//

// FAIL FIRST 
//-----------------------------------------------------------------------------------//
```
public Conta consultar(String numero) {
    Conta c = null;

    for(int i=0 ; i<indice ; i++) {
        if(contas[i].getNumero().equals(numero)){
            c = contas[i];
            break;
        }
    }
    
    if (c == null) {
        throw new AplicacaoException("Conta inexistente!");
    }
    return c;
}
```
//-----------------------------------------------------------------------------------//


//TELL DONT ASK
//ANTES 
//-----------------------------------------------------------------------------------//
```
let j1 = new Jogo();
    
function rodada(): void {
    let size = j1.getArray().length;
    for (let i = 1; i < size+1; i ++) {
        for(let j = 1; j < size+1; j ++) {
            j1.atacar(i,j)
        }
    }
}


for (let i = 0 ; i < 3; i++) {
    rodada()
    j1.avaliarbatalha()
}
```
//DEPOIS
//-----------------------------------------------------------------------------------//
```
rodada(jg: Jogo): void {
    let size = jg.getArray().length;
    for (let i = 1; i < size+1; i ++) {
        for(let j = 1; j < size+1; j ++) {
            jg.atacar(i,j)
        }
    }
}

// BATALHA 
batalha(jg: Jogo, j: number) {
    for (let i = 0 ; i < j; i++) {
        rodada(jg)
        jg.avaliarbatalha()
    }
}

let j1 = new Jogo();
batalha(j1,3);
```
//-----------------------------------------------------------------------------------//


//TELL DONT ASK
//-----------------------------------------------------------------------------------//
```
export class CovidCasos {
    private media_quartoze: number;
    private media_hoje: number;

    constructor(media_quartoze: number, media_hoje: number) {
        this.media_quartoze = media_quartoze;
        this.media_hoje = media_hoje;
    }

    CalculaVariacao() {
        let media_quartoze: number = this.media_quartoze;
        let media_hoje: number = this.media_hoje;
        let variacao: number = 0;

        variacao = ((media_hoje/media_quartoze -1)* 100);

        return variacao;
    }

    Resultado() {
        let variacao: number = this.CalculaVariacao();
        let percentual: number = 15;
        let resultado: string = "";

        if (variacao > percentual) {
            resultado = "Em alta.";
        } else if (variacao < percentual*(-1)) {
            resultado = "Em queda.";
        } else {
            resultado = "Em estabilidade.";
        }
        return variacao.toFixed(2) + "%" + ", " + resultado;
    }
}
```
// TESTE
//-----------------------------------------------------------------------------------//
```
import {CovidCasos} from './01_questao';

let cov1 = new CovidCasos(400,500);
let cov2 = new CovidCasos(400,350);
let cov3 = new CovidCasos(400,340);

console.log(cov1.Resultado());
console.log(cov2.Resultado());
console.log(cov3.Resultado());
```
//-----------------------------------------------------------------------------------//
