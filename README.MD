Trabalho 1 de Inteligência Artificial   Tema: autocomplete
Professora: Aline Paes Disciplina/Semestre: Inteligência Artificial/2019.1
Alunos: Alan Gomes, Eduardo Peniche e Marcelo José

1. Introdução
Este trabalho foi desenvolvido na linguagem python e em conjunto pelos alunos citados acima. Usamos as bibliotecas NLTK e anytree. O NLTK foi de uma biblioteca de excelente ajuda, já que a mesma foi desenvolvida para auxiliar no processamento de linguagem natural. Já o anytree foi uma excelente ferramenta na ajuda no processo de construir e trabalhar com as árvores de busca. A ideia estrutural do trabalho foi criar uma árvore de possibilidades para a sugestão inicial de palavras e posteriormente fazer consultas a essa árvore de modo a gerar uma certa precisão de acordo com as palavras fornecidas pelo próprio usuário. Sendo assim o autocomplete se torna algo mais “personalizado”, já que quem fornece a sua base de dados é o próprio usuário.

2. Base de dados
    Usamos inicialmente um texto que se encontra na pasta do projeto para a base de dados inicial.

3. Ferramentas
3.1 Usamos a biblioteca NLTK e dela fizemos o uso das seguintes funções:
3.1.1 word_tokenize
    Retorna todas as palavras separadas em uma string.

3.2 Também usamos a biblioteca anytree
  O anytree é uma biblioteca que auxilia muito na criação de árvores. Ela foi usada para a criação das árvores de busca que são estruturas essenciais para não só para implementar as estratégias de busca. Usamos algumas funçoes do anytree:
3.2.1. node: é uma estrutura de dado que simula um nó, possui como informação obrigatória um id e um pai(parent), que pode ser None caso seja uma raiz e pode ter inúmeros outros atributos de qualquer tipo. No caso os id’s foram equivalentes a palavra parcial. Ex: palavra completa “qual”. Id’s dos nós: “q”,”qu”,”qua”,”qual". E como atributo colocamos em cada nó um dicionário que possui todos os possíveis resultados a qual aquele nó leva e como chave o número de vezes que aquele resultado foi digitado. No mesmo exemplo da palavra "qual" todos os nós teriam em seu dicionário a chave “qual” com valor 1.

3.2.1.1 Outras funções do node: find
Retorna um nó a partir de uma raiz dada ou false se não encontrar.
3.2.1.2 Outras funções do node: findpath
Retorna uma lista com todo o caminho, nó por nó, da raiz até um dado nó.

4. Estratégias/algoritmos de busca

4.1 Busca A*
Na busca A* usamos como parâmetro para a função g(n) o custo da raiz até o nó desejado com soma de 1. Ou seja, a cada nível que descemos na árvore a função g(n) soma +1. A função heurística ficou como a média entre quantas vezes aquele nó levou a um resultado, durante o percursso da árvore, sobre todas as opções a qual o nó n leva a um resultado. Toda essa fração é multiplicada por -0,75. O teste de objetivo foi feito simplesmente somado o valor da função g(n) + f(n). E buscando o menor valor possível.

4.2 Busca Local
Na busca local fizemos uso do dicionário que colocamos em todos os nós. O dicionário possui todas as opções a qual aquele nó pode nos levar e quantas vezes essa opção foi um resultado (a ocorrência da palavra no treinamento), então ele simplesmente retorna essa opção.

5. Testando
O código é inicializado criando-se uma lista de árvores com somente as raízes. E cada índice da lista são nós com cada letra do alfabeto. Após isso temos um pequeno texto inicial que é normalizado com a retirada de números, símbolos e caixas altas esse texto consequentemente vira o primeiro aprendizado da árvore. Suas palavras então são decompostas e cada pedaço vira um nó para sua respectiva raiz do alfabeto. Exemplo: a palavra ”qual”, vira: “q”,”qu”,”qua”,”qual”. A palavra completa (“qual”) é adicionada ao dicionário de cada nó como resultado e com valor 1 indicando que foi utilizada uma vez.
 Após a inicialização é pedido que o usuário digite a palavra a ser completada. O programa pega a entrada dada e a executa tanto na busca local, quanto na busca A* e retorna para o usuário como recomendação p resultado de cada uma. Se o usuário digitar “0” (zero) o programa encerra a execução. Caso o usuário digite uma palavra nova, que ainda não está em nenhuma das árvores do programa, o programa irá fazer o processo de adicionar essa palavra a sua árvore de conhecimento.