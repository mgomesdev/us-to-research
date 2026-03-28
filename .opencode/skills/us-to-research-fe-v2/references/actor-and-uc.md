## 1. Atores

Os atores representam papeis desempenhados pelos diversos usuarios que interagem com os serviços e funções do sistema.
- um ator pode representar algum hardware ou outro software que interaja com o sistema. 
- Na maioria das vezes, um ator representará uma pessoa que utilizará o sistema. 
- Cada ator deve ter um nome e um estereótipo ex `<<system>>` que torna explicito que não é um ator humano, e sim sistemas de software ou hardware.
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

### 2.1 Classificação

Os casos de uso podem ser classificados em dois tipos: **primários** ou **secundários**

- **Primários**:
    - Se refere a um processo importante, relacionado com um dos requisitos funcionais do software, ex: **Realizar um saque** ou **Emitir um extrato** em um sistema de controle bancário.
- **Secundários**:
    - Se refere a processos menos importantes, como manutençôes simples. 

**Obs.** É importante retornar o maximo de casos de uso, primários e secundários, detalhando-os o máximo possível para evitar inconsistências e frustrações com a entrega final do software.

### 2.2 Documentação dos Casos de Uso

- TODO