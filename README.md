# Programas-UFC
Programas para resolução das atividades do curso de Engenharia de Computação da UFC


* Aluna: Clarisse Maria Cabral Montenegro
* Matrícula: 580585
* Cálculo 2 - 2025.2 - Prof. Renan da Silva Santos


Calculadora de Integrais Numéricas
* Linguagem: Java



# Visão Geral:

Uma aplicação Java robusta para cálculo numérico de integrais definidas utilizando o método dos retângulos (soma de Riemann) com refinamento adaptativo de precisão.



# Funcionalidades:

* Cálculo preciso de integrais definidas usando método dos retângulos com ponto médio

* Suporte extensivo a funções matemáticas elementares e compostas

* Refinamento adaptativo automático baseado em tolerância definida pelo usuário

* Interface interativa amigável via linha de comando

* Sistema de testes integrado com funções de validação



# Funções Suportadas

* Operações Básicas	+, -, *, /, ^	x^2 + 3*x - 5

* Trigonométricas	sin, cos, tan	sin(x)*cos(x)

* Exponenciais/Log	exp, log	exp(-x^2)

* Outras	sqrt, abs	sqrt(x^2 + 1)



# Como Executar:

* Pré-requisitos - Java JDK 8 ou superior

* Passo a Passo:

1) Salve o código em um arquivo chamado Main.java


2) Compile o programa:

bash

javac Main.java


3) Execute o programa:

bash

java Main


4) Siga as instruções no terminal para inserir:

* Função matemática

* Limites de integração

* Tolerância desejada



# Exemplos de Uso

* Exemplo 1: Polinômio

text
Função: x^2 + 2*x + 1

Limite inferior: 0

Limite superior: 2

Tolerância: 0.0001

Saída esperada: ∫[0.00, 2.00] x^2 + 2*x + 1 dx ≈ 6.666667


* Exemplo 2: Função Trigonométrica

text

Função: sin(x) + cos(x)

Limite inferior: 0

Limite superior: 3.1416

Tolerância: 0.00001

Saída esperada: ∫[0.00, 3.14] sin(x) + cos(x) dx ≈ 2.000000


* Exemplo 3: Função Exponencial

text
Função: exp(x)

Limite inferior: 0

Limite superior: 1

Tolerância: 0.000001

Saída esperada: ∫[0.00, 1.00] exp(x) dx ≈ 1.718282



# Arquitetura do Código

* Estrutura de Classes

java

Main

├── ExpressionEvaluator (Classe interna estática)

│   ├── avaliar()          // Avalia expressões com substituição de x

│   ├── avaliarExpressao() // Processa a expressão completa

│   ├── avaliarOperacoes() // Executa operações matemáticas

│   └── encontrarFimFuncao() // Auxiliar para parsing

├── calcularIntegral()     // Método principal de integração

├── calcularRiemann()      // Implementação do método dos retângulos

├── main()                 // Ponto de entrada do programa

└── testarIntegral()       // Função de teste e validação



# Método de Integração


* O programa implementa o método dos retângulos com as seguintes características:

Ponto médio: Cada retângulo é calculado no centro do intervalo


* Refinamento adaptativo:

Inicia com 1000 retângulos

Dobra a quantidade a cada iteração

Para quando a diferença entre iterações for menor que a tolerância


* Controle de erro: Monitora a convergência do resultado



# Algoritmo Principal

java

public static double calcularIntegral(String funcao, double a, double b, double tolerancia) {
    if (a == b) return 0;
    if (a > b) return -calcularIntegral(funcao, b, a, tolerancia);
    
    int n = 1000; // Retângulos iniciais
    double resultadoAnterior = 0;
    double resultadoAtual = calcularRiemann(funcao, a, b, n);
    
    // Refinamento iterativo
    while (Math.abs(resultadoAtual - resultadoAnterior) > tolerancia) {
        n *= 2;
        resultadoAnterior = resultadoAtual;
        resultadoAtual = calcularRiemann(funcao, a, b, n);
    }
    
    return resultadoAtual;
}



# Sistema de Avaliação de Expressões

Parser Matemático

O ExpressionEvaluator processa expressões em múltiplas etapas:

* Substituição de variável: x → valor numérico

* Processamento de parênteses: Resolve expressões aninhadas

* Avaliação de funções: Aplica funções matemáticas

* Execução de operações: Realiza cálculos seguindo precedência


# Ordem de Operações

1) Parênteses ( )

2) Funções (sin, cos, exp, etc.)

3) Exponenciação ^

4) Multiplicação * e Divisão /

5) Adição + e Subtração -



# Testes e Validação
Testes Automáticos

O programa inclui testes integrados para validar a precisão:

java

testarIntegral("x", 0, 1, 0.0001, 0.5);          // ∫x dx = 0.5

testarIntegral("x^2", 0, 1, 0.0001, 1.0/3);      // ∫x² dx = 1/3

testarIntegral("sin(x)", 0, Math.PI, 0.0001, 2.0); // ∫sin(x) dx = 2



# Métricas de Precisão

Tolerância típica: 0.0001 a 0.000001

Retângulos iniciais: 1000

Crescimento exponencial: Dobra a cada iteração



# Casos de Uso

* Educacional:

Ensino de cálculo integral

Demonstração de métodos numéricos

Experimentação com diferentes funções


* Científico:

Cálculo de áreas sob curvas

Solução de problemas de física

Análise de dados experimentais


* Engenharia:

Cálculos de engenharia

Simulações numéricas

Análise de sistemas
