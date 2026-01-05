Hangperson: tarefa inicial de um curso de engenharia de software como serviço
=============================================================

(v1.1, setembro de 2015)

Nesta tarefa você entra em contato com uma parte do ciclo de criação de SaaS de forma disciplinada.

O ciclo completo que seguimos no curso inclui conversar com o cliente, escrever cenários em BDD, transformar esses cenários em testes de aceitação executáveis, usar esses cenários somados a TDD para guiar a escrita do código, e publicar o resultado de cada iteração na nuvem.

Nesta primeira parte, os testes unitários já vêm prontos, para que você use TDD na lógica do jogo da forca. Num ciclo completo, esses testes seriam escritos por você conforme o código nasce.

Depois disso você usa um framework minimalista para expor o jogo como serviço. Adaptar a lógica para a web obriga a pensar em rotas e em arquitetura orientada a serviços. Conforme a versão web toma forma, você usa a ferramenta de BDD para descrever o comportamento do ponto de vista de quem joga, e esses cenários viram testes de integração que guiam o desenvolvimento.

A publicação é feita num serviço de hospedagem, o que dá contato com automação de deploy.

**Por que o framework minimalista?** Ele evita a complexidade de um framework completo, deixando o foco nas ferramentas, na mecânica e nos conceitos de serviço — tudo isso transfere direto para frameworks maiores depois. Como o app não tem banco de dados e tem pouquíssimas funções, é o caminho mais curto.

Pré-requisitos
-------------

Você precisa estar confortável com:

* Uso básico de controle de versão e envio de código para um repositório remoto.

* Linha de comando em nível de sobrevivência, e um editor para mexer nos arquivos.

* Noções de arquitetura de aplicações como serviço.

Parte 0: desmistificando a criação de um app
==============================

**Objetivo:** entender os passos para criar, versionar e publicar um app, incluindo o rastreamento das bibliotecas de que ele depende, para que produção e desenvolvimento fiquem o mais parecidos possível.

**O que fazer:** criar um "olá mundo" com o framework minimalista, versionar direito e publicar.

Criando e versionando um app simples
-----------------------------------------

Aplicações como serviço são desenvolvidas na sua máquina mas rodam em produção num servidor acessível por outras pessoas. A ideia é reduzir ao mínimo a diferença entre os dois ambientes, evitando aquele problema clássico em que algo funciona localmente e falha (ou se comporta diferente) no servidor.

São dois mecanismos para manter os ambientes consistentes. O primeiro é o controle de versão do código. Mas como quase todo app depende de bibliotecas escritas por terceiros, precisamos também registrar quais versões dessas bibliotecas foram testadas, para que as mesmas sejam usadas nos dois lados.

Felizmente a linguagem tem um gerenciador de dependências dedicado: ele procura um arquivo de manifesto na raiz do projeto, contendo a lista de bibliotecas e versões. O gerenciador confere se tudo está instalado e acessível, incluindo as dependências dessas dependências.

### Observação

Caso o comando nao responda, confira se a porta ja esta em uso.