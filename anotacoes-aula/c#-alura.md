# Alterando o GET com lambda

## Exemplo da Aula 2:6

<!-- Em C# chamamos a arrow function de Lambda -->

> public string Nome { get; set; }
public string Artista { get; set; }
public int Duracao { get; set; }
public bool Disponivel { get; set; }
public string DescricaoResumida => $"A música {Nome} pertence à banda {Artista}";

O corpo de uma instrução lambda pode consistir em qualquer número de instruções. No entanto, na prática, normalmente não há mais do que dois ou três.

    ```
    Action<string> greet = name =>
    {
    string greeting = $"Hello {name}!";
    Console.WriteLine(greeting);
    };
    greet("World");
    // Output:
    // Hello World!
    ```
Em C#, você usa o operador => (expression-bodied member) para simplificar ou customizar o acessor get de uma propriedade de forma enxuta

> public class Produto
{
    public decimal Preco { get; set; }
    // Propriedade somente leitura com lambda
    public decimal PrecoComDesconto => Preco * 0.9m;
    // Alterando apenas o 'get' de uma propriedade completa
    private string _nome;
    public string Nome
    {
        get => _nome?.ToUpper() ?? "SEM NOME";
        set => _nome = value;
    }
}

### Estrutura de codigo lambda

> (parametros) => expressao

**Parâmetros:** É uma lista opcional de parâmetros, separados por vírgulas, que especifica as entradas da função lambda. Cada parâmetro pode ser tipado explicitamente ou pode ser inferido pelo compilador.

**Operador =>:** É o operador de seta (=>), que separa a lista de parâmetros da expressão lambda. Ele indica que os parâmetros estão sendo mapeados para a expressão ou bloco de código seguinte.

#### Exemplo de codigo sem lambda

> List<int> numeros = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
List<int> numerosPares = numeros.FindAll(BuscarNumerosQueSaoPares);
bool BuscarNumerosQueSaoPares(int numero)
{
    return numero % 2 == 0;
}
foreach (int numero in numerosPares)
{
    Console.WriteLine(numero);
}

#### Agora o mesmo comdigo com lambda

>List<int> numeros = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
List<int> numerosPares = numeros.FindAll(numero => numero % 2 == 0);
numerosPares.ForEach(numero => Console.WriteLine(numero));

### Quando nao é recomenddo uso de lambda :joy:

Complexidade excessiva: Se a lógica da expressão lambda se tornar muito complexa ou difícil de entender, é preferível usar métodos e blocos de código separados para manter a clareza e legibilidade do código.

Reutilização de código: Se você precisa reutilizar a lógica em várias partes do seu código, é mais adequado criar um método separado em vez de usar uma função lambda repetidamente. Isso promove a reutilização do código e torna mais fácil a manutenção.

Aumento da complexidade do código: ==Em alguns casos, o uso excessivo de funções lambda pode tornar o código mais difícil de entender e dar manutenção==, especialmente quando as expressões lambdas são aninhadas. Nesses casos, pode ser melhor dividir o código em partes menores e mais legíveis.
