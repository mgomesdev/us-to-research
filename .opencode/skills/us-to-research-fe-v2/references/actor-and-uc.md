## 1. Atores

Os atores representam papeis desempenhados pelos diversos usuarios que interagem com os serviços e funções do sistema.
- um ator pode representar algum hardware ou outro software que interaja com o sistema. 
- Na maioria das vezes, um ator representará uma pessoa que utilizará o sistema. 
- Cada ator deve ter um nome e um estereótipo ex **system** que torna explicito que não é um ator humano, e sim sistemas de software ou hardware.
- Em resumo um ator é um usuário que pode representar mais de um papel no sistema

**Obs.** A utilização de estereótipo de sistemas de software ou hardware não é obrigatório, é apenas recomendado para destacar a caracteristica especial que o diferencia dos atores mais comuns.

### 1.1 Como identificar atores

- Deve-se procurar e identificar as entidades externas que interagirão com o sistema, tanto usuários humanos, como também, eventualmente, softwares e/ou hardwares especiais.

- **Candidatos a atores:**
    - Que tipos de usuários poderão usar o sistema?
    - Quais usuários estão interessados ou usarão quais funcionalidades e serviços do software?
    - Quem fornecerá informações ao sistema?
    - Quem usará as informações do sistema?
    - Existe algum outro software que interagirá com o sistema?
    - Existe algum hardware especial (com oum robô, por exemplo) que interagirá com o software?

- **Exemplo de atores válidos**
    - Gerente
    - Funcionario
    - Cliente
    - Sistema Integrado
    - Medidor de Radiação

**Obs.** Os candidatos a atores devem ser listados e deve-se tantar atribuir responsabilidades e objetivos a cada um deles, ou seja, metas que cada ator poderia desejar atingir ao usar o software. Atores para os quais não é possível atribuir um objetivo dificilmente serão atores verdadeiros e deverão ser eliminados.

---

## 2. Casos de Uso

Os casos de uso são usados para capturar os requisitos funcionais do sistema (serviços, tarefas, funcionalidades) identificadas como necessários ao software e que podem ser usados de alguma maneira pelos **atores**. Descrevem e documentam os comportamentos pretendidos para as funções do software.

- Descreve de forma resumida a funcionalidade ao qual o caso de uso se refere.
- O caso de uso costuma ser descrito com um verbo que descreve a ação que será realizada quando for executado. ex: **Abrir Conta**.

### 2.2. Localização

- Cada caso de uso e tudo relacionado é salvo em sua pasta propria dentro da pasta da feature. ex: `/specs/features/[name]/[uc-01]/uc-01.md` kebab-case.

### 2.3. Classificação

Os casos de uso podem ser classificados em dois tipos: **primários** ou **secundários**

- **Primários**:
    - Se refere a um processo importante, relacionado com um dos requisitos funcionais do software, ex: **Realizar um saque** ou **Emitir um extrato** em um sistema de controle bancário.
- **Secundários**:
    - Se refere a processos menos importantes, como manutençôes simples. 

**Obs.** É importante retornar o maximo de casos de uso, primários e secundários, detalhando-os o máximo possível para evitar inconsistências e frustrações com a entrega final do software.

### 2.4. Como identificar Casos de Uso

**Para identificar os casos de uso, é necessário determinar as funcionalidades necessárias ao software, ou seja:**
- Funçôes
- Serviços que correspondem aos requisitos funcionais declarados como necessários ao sistema

Uma maneira de auxiliar na identificação das funcionalidades é verificar a lista dos atores que comporão o sistema e quais os objetivos de cada ator. Esses objetivos muitas vezes corresponderão a uma ou mais funcionalidades. Tambem pode ser útil identificar os eventos externos que afetarão o software.Tais eventos muitas vezes acarretam a execução de uma funcionalidade ou influenciam de alguma forma seu processamento.

Outra maneira de identificar casos de uso é verificar a lista de requisitos funcionais estabelecidos e se cada um deles possui um (ou até mais) caso de uso especificando seu comportamento e, obviamente, qual ator ou atores podem utilizá-lo.

**Observações**
- Um caso de uso costuma ter uma série de passos ou etapas. Uma maneira de determinar se uma funcionalidade é real, ou seja, se realmente corresponde a um caso de uso, é verificar quais ações seriam realizadas quando o caso de uso fosse executado. Se não for possível identificar essas etapas, provavelmente não será um caso de uso real.
- Se o número de passos atribuidos a um caso de uso for muito pequeno, deve-se verificar se esse caso de uso não deveria ser englobado por outro, acrescentando seus passos ás etapas dele ou mesmo se tornando um cenário alternativo de outro caso de uso.

### 2.5. Documentação dos Casos de Uso

A documentação de caso de uso representa o comportamento de um caso de uso da maneira o mais completa possível, mas sem detalhes técnicos de implementação. 

**Obs.**: O detalhamento maior a nível de implementação, será feito em outra etapa posterior (**research-to-plan**). 

Consulte `../assets/uc-spec-example.md` para um exemplo de **Estrutura de Documentação de um Caso de Uso**.

---

## 3. Associações

Representam interações ou relacionamentos entre os atores e os casos de uso e os relacionamentos entre os casos de uso e outros casos de uso. Recebem nomes especiais, como **include**, **extends**, **generalization**.

- Uma associação entre um ator e um caso de uso demonstra que o ator utiliza de alguma maneira a funcionalidade do sistema representada pelo caso de uso em questão, seja requisitando a execução dessa função, seja recebendo o resultado produzido por ela a pedido de outro ator.

**A associação entre um ator e um caso de uso é representada por uma linha ligando o ator ao caso de uso, podendo ocorrer que as extremidades da linha contenham setas, indicando o sentido em que as informações trafegam:**

- Se estas setas são fornecidas pelo ator ao caso de uso, se são transmitidas pelo caso de uso ao ator ou ambos (nesse ultimo caso, a linha não tem setas, significando que as informações são transmitidas nas duas direções)
- As setas tambem servem para indicar quem inicia a comunicação.
- Uma associação pode ter uma descrição propria quando é necessário esclarecer a natureza da informação que está sendo transmitida ou dar um nome a esta, se isso for necessário.

**Exemplo:** Se o ator Cliente utiliza, de alguma forma, a funcionalidade de Abrir Conta, percebemos que o ator Cliente utiliza de alguma forma, a funcionalidade Abrir Conta, e que a informação referente a esse processo trafega nas duas direções.

---