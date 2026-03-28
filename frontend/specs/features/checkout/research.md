# Checkout - Frontend

## 1. Visão Geral

O checkout do Linka Eventos é o momento mais crítico de toda a jornada do participante. É nele que a intenção de participar de um evento se converte em uma inscrição ou compra, e qualquer fricção nesse processo representa diretamente perda de conversão, abandono de carrinho e experiência negativa para o participante.

O objetivo é que o checkout do Linka se torne referência em plataformas de eventos: rápido, seguro e com a menor quantidade possível de etapas obrigatórias para o participante.

## 2. Estrutura Geral do Checkout

### 2.1 Layout

O checkout deve ser exibido em uma tela única, com rolagem vertical contínua, organizada em três blocos sequenciais:
- **Bloco 1** — Dados dos participantes
- **Bloco 2** — Recebimento do ingresso
- **Bloco 3** — Pagamento e dados do comprador

### 2.2 Painel Lateral

O sistema deve exibir um painel lateral direito com o resumo do pedido, contendo:
- Nome do evento
- Datas
- Discriminação dos ingressos selecionados com seus respectivos valores
- Desconto aplicado via cupom quando houver
- Valor total da compra

### 2.3 Botão Principal

O botão de ação principal deve estar posicionado ao final do terceiro bloco, com o texto **"Avançar para pagamento"**. Esse botão só deve ser habilitado quando todos os campos obrigatórios dos três blocos estiverem corretamente preenchidos e validados.

### 2.4 Contador de Tempo

O contador de tempo deve ser exibido no painel de resumo do pedido, indicando o tempo restante para conclusão da compra. O comportamento do sistema ao expirar esse tempo está descrito no Tópico 8.

## 3. Bloco 1: Dados dos Participantes

### 3.1 Checkout Nominal (pago ou gratuito)

No checkout nominal, o sistema deve exibir um card de preenchimento para cada ingresso selecionado, identificado pelo tipo do ingresso e seu valor.

Cada card deve conter os campos obrigatórios:
- Nome do participante
- E-mail
- Celular (com seletor de DDI com bandeira do país, Brasil pré-selecionado como padrão)

O organizador pode configurar campos adicionais por ingresso (CPF, empresa, cargo ou campo customizado). Quando configurados, esses campos devem aparecer nos cards de participante do respectivo ingresso, abaixo dos campos padrão, seguindo as regras de obrigatoriedade definidas pelo organizador.

Todos os campos obrigatórios devem ser validados antes que o participante consiga avançar para o próximo bloco. Caso algum campo não esteja preenchido ou contenha dado inválido, o sistema deve destacar o campo com indicação visual de obrigatoriedade e exibir uma mensagem explicativa abaixo do campo correspondente.

### 3.2 Checkout Não Nominal (pago ou gratuito)

No checkout não nominal, o Bloco 1 não deve ser exibido. O sistema não solicita nenhum dado por ingresso, pois o ingresso não é vinculado a um participante no momento da compra. O checkout deve iniciar diretamente no Bloco 2 — Recebimento do ingresso.

## 4. Bloco 2: Recebimento do Ingresso

O Bloco 2 deve exibir um campo do tipo dropdown com o label **"Responsável pelos ingressos"**.

O dropdown deve listar como opções os nomes de todos os participantes informados no Bloco 1, seguidos da opção **"Outro"**. No caso do checkout não nominal, onde o Bloco 1 não é exibido, o dropdown não deve ser exibido.

Quando o participante seleciona uma das opções da lista de participantes, o sistema deve usar automaticamente o e-mail daquele participante como destinatário dos ingressos. Nenhum campo adicional precisa ser exibido.

Quando o participante seleciona a opção **"Outro"**, o sistema deve exibir os campos: nome completo, e-mail e celular, todos obrigatórios. Esses dados serão usados para identificar o responsável pelos ingresses e para criação automática de conta.

O bloco deve exibir também os seguintes elementos obrigatórios antes do avanço:
- Checkbox com o texto **"Eu li e concordo com os termos e condições"** com link para a página correspondente
- Checkbox com o texto **"Aceito receber contato e informações sobre o evento"**. Esse checkbox não deve ser obrigatório para avanço

O sistema deve exibir uma nota informativa abaixo dos checkboxes indicando que uma conta será criada automaticamente no Linka com o e-mail informado, sendo esse e-mail o responsável pela gestão dos ingresses adquiridos.

## 5. Bloco 3: Pagamento e Dados do Comprador

### 5.1 Seleção do Método de Pagamento

O sistema deve exibir as opções de método de pagamento disponíveis para o evento: **Pix**, **Cartão de crédito** e **Boleto**. Apenas os métodos habilitados pelo organizador devem ser exibidos.

O participante deve selecionar um método antes de prosseguir.

### 5.2 Dados do Comprador

O bloco deve exibir um campo dropdown com o label **"Responsável pelo pagamento"**.

O dropdown deve listar os nomes de todos os participantes informados no Bloco 1 e a opção **"Outro"**. No checkout não nominal, onde o Bloco 1 não foi exibido, o dropdown não deve ser exibido.

Esse campo é independente do campo "Responsável pelos ingresses" do Bloco 2. O participante pode escolher pessoas diferentes para cada responsabilidade.

Quando o participante seleciona um dos participantes listados, o sistema deve pré-preencher os campos de dados do comprador com as informações já fornecidas no Bloco 1 para aquele participante.

Quando o participante seleciona **"Outro"**, o sistema deve exibir campos para preenchimento manual dos dados do comprador.

### 5.3 Salvar Dados para Compras Futuras

Caso o participante esteja logado e tenha optedo por salvar os dados em uma compra anterior, o sistema deve pré-preencher automaticamente os campos do comprador com os dados salvos e exibir o cartão salvo como opção de pagamento, exigindo apenas o preenchimento do CVV para confirmar.

Os dados de compra devem ficar vinculados ao usuário logado, e não ao método de pagamento, ou seja, caso a primeira compra de um usuário seja realizada via Pix e ele opte por salvar os dados, o sistema deve armazenar as informações pessoais. Em uma compra posterior, caso o pagamento seja realizado com cartão, o sistema deverá preencher automaticamente os dados pessoais já salvos, enquanto os dados do cartão devem permanecer em branco.

Caso o usuário possua dados salvos, preenchidos automaticamente pelo sistema, mas realize alguma alteração antes de prosseguir com a compra, essas informações atualizadas devem passar a ser consideradas como os novos dados salvos.

Caso o usuário possua dados salvos, mas em uma nova compra desmarque a opção de manter os dados salvos e atualizados, o sistema não deverá manter essas informações armazenadas.

Embora o sistema preencha automaticamente os dados quando disponíveis, o usuário deve ter total autonomia para editar ou alterar qualquer um dos campos antes de concluir o processo.

Para **"dados de pagamento armazenados no sistema"** entende-se:

**Dados que devem ser salvos e reutilizados:**
- Nome completo do comprador
- E-mail
- CPF/CNPJ/Passaporte
- Telefone

**Dados que NÃO devem ser salvos no banco de dados:**
- Para pagamentos com cartão, o sistema deve armazenar apenas o card_id retornado pelo gateway de pagamento, que permitirá recuperar o cartão previamente utilizado, sem armazenar dados sensíveis.

O sistema deve exibir uma opção de checkbox com o texto **"Salvar dados para futuras compras"**. Quando marcada, o sistema deve armazenar os dados do comprador e os dados do cartão para uso em compras futuras do mesmo usuário logado.

### 5.4 Checkout Gratuito

Quando o evento ou ingresso for gratuito, o Bloco 3 não deve exibir os campos de método de pagamento nem os dados do comprador. O sistema deve exibir apenas o botão de confirmação da inscrição.

## 6. Criação Automática de Conta

### 6.1 Checkout Nominal Pago e Nominal Gratuito

Ao concluir o checkout com sucesso, o sistema deve criar automaticamente uma conta na plataforma usando os dados do responsável pelos ingresses definido no Bloco 2. Se o participante selecionou um dos participantes informados no Bloco 1, a conta deve ser criada com o nome e e-mail daquele participante. Se o participante selecionou "Outro", a conta deve ser criada com os dados informados manualmente.

### 6.2 Checkout Não Nominal Pago

O comportamento de criação de conta deve seguir a mesma lógica do checkout nominal: a conta é criada com os dados do responsável pelos ingresses informado no Bloco 2, seja um participante selecionado ou a opção "Outro" preenchida manualmente.

### 6.3 Checkout Não Nominal Gratuito

No checkout não nominal gratuito, o participante deve obrigatoriamente estar autenticado para acessar o checkout. Caso o participante tente avançar sem estar logado, o sistema deve redirecioná-lo para a tela de login ou cadastro. Após autenticação, o sistema deve retornar o participante ao checkout no ponto em que estava.

### 6.4 E-mail Informado Já Possui Conta Existente

Quando o e-mail informado no campo "Responsável pelos ingresses" já estiver cadastrado na base da plataforma, o sistema deve usar a conta existente automaticamente, sem criar uma nova conta duplicada. O participante não precisa fazer login para concluir a compra nos tipos de checkout que permitem compra sem autenticação.

### 6.5 Comunicações Enviadas Após Criação Automática de Conta

Após a criação automática de conta, o sistema deve enviar dois e-mails distintos para o responsável pelos ingresses:
- Primeiro: e-mail de boas-vindas à plataforma solicitando que o participante defina sua senha de acesso
- Segundo: e-mail com os ingresses adquiridos, enviado após a confirmação do pagamento

## 7. Cupom de Desconto

O campo de cupom deve estar disponível no painel de resumo do pedido, com um campo de texto e um botão com o texto **"Adicionar"**.

A validação do cupom deve ocorrer no momento em que o participante clica no botão "Adicionar".

Quando o cupom for válido, o sistema deve exibir o desconto aplicado no resumo do pedido, com o nome do cupom e o valor descontado em destaque, além de disponibilizar uma opção para remover o cupom aplicado.

Quando o cupom for inválido, expirado ou não encontrado, o sistema deve exibir uma mensagem de erro imediatamente abaixo do campo, informando o motivo da rejeição de forma clara ao usuário.

Apenas um cupom pode estar ativo por pedido. O sistema não deve aplicar regras de restrição por CPF ou e-mail do participante.

## 8. Expiração do Tempo de Checkout

O sistema deve reservar os ingresses selecionados pelo participante durante o preenchimento do checkout por um período de **15 minutos**, exibido como contador regressivo no painel de resumo do pedido.

O comportamento do sistema ao atingir zero no contador é redirecionar o participante para a página do evento com os ingresses liberados, permitindo que o participante reinicie o checkout caso os ingresses ainda estejam disponíveis.

## 9. Confirmação de Pagamento e Tela de Sucesso

### 9.1 Pagamento via Cartão de Crédito

Após o envio dos dados do cartão, o sistema deve processar o pagamento e aguardar a resposta da operadora. Caso o pagamento seja aprovado, o sistema deve exibir a tela de confirmação de compra.

Quando o cartão for recusado, o sistema deve retornar ao bloco de pagamento mantendo todos os dados preenchidos, exibir a mensagem de erro retornada de forma clara e com instruções para o participante. O participante pode tentar novamente com o mesmo cartão ou alterar o método de pagamento.

### 9.2 Pagamento via Pix

Após a seleção do Pix como método de pagamento e a confirmação do comprador, o sistema deve gerar e exibir o QR Code e o código Pix copia e cola, juntamente com o tempo restante para pagamento. A tela de confirmação completa deve ser exibida somente após a confirmação do pagamento pelo sistema financeiro, mediante recebimento do webhook de pagamento confirmado.

### 9.3 Pagamento via Boleto

O comportamento pós-seleção de boleto deve considerar o tempo de compensação desse meio de pagamento. Após a escolha, o usuário deve ser direcionado para uma tela de **"Aguardando pagamento"**, onde poderá visualizar as instruções, baixar o boleto e/ou copiar o código para pagamento.

### 9.4 Tela de Confirmação

A tela de confirmação deve ser a mesma já existente hoje no sistema.

### 9.5 E-mails Transacionais Pós-Checkout

Após a confirmação do pagamento, o sistema deve enviar ao responsável pelos ingresses o e-mail com os ingresses adquiridos em PDF. O sistema já envia hoje o e-mail de confirmação de compra e o comprovante de compra quando aplicável, e esses comportamentos devem ser mantidos. Para contas criadas automaticamente, o e-mail de boas-vindas com link de criação de senha deve ser enviado conforme descrito no Tópico 6.5.

## 10. Proteção e Segurança do Checkout

A definir com o time dev.

## 11. Comportamento por Tipo de Ingresso

O sistema deve se comportar de forma diferente em cada combinação de tipo de ingresso e contexto de autenticação:

### Checkout Nominal Pago
- Exibe Bloco 1 com campos por participante
- Exibe Bloco 2 com dropdown de responsável
- Exibe Bloco 3 com métodos de pagamento
- Cria conta automaticamente com os dados do responsável pelos ingresses ao concluir

### Checkout Nominal Gratuito
- Exibe Bloco 1 com campos por participante
- Exibe Bloco 2 com dropdown de responsável
- Não exibe Bloco 3 apenas com os campos de pagamento
- Cria conta automaticamente com os dados do responsável pelos ingresses ao concluir

### Checkout Não Nominal Pago
- Não exibe Bloco 1
- Exibe Bloco 2 sem o dropdown
- Exibe Bloco 3 com métodos de pagamento
- Cria conta automaticamente com os dados do responsável pelos ingresses ao concluir

### Checkout Não Nominal Gratuito
- Exige autenticação do participante antes de acessar o checkout
- Caso não esteja logado, redireciona para login ou cadastro ao tentar avançar
- Após autenticação, retorna ao checkout
- Não exibe Bloco 1
- Exibe Bloco 2
- Não exibe o Bloco 3

## 12. Requisitos Funcionais

- RF-01: Checkout nominal deve exibir Bloco 1 com cards para cada ingresso contendo nome, e-mail e celular (DDI)
- RF-02: Campos customizados configurados pelo organizador devem aparecer nos cards de participante
- RF-03: Checkout não nominal não deve exibir Bloco 1
- RF-04: Bloco 2 deve ter dropdown "Responsável pelos ingresses" com participantes + "Outro"
- RF-05: Selecionar "Outro" no Bloco 2 deve exibir campos de nome, e-mail e celular
- RF-06: Bloco 2 deve exibir checkbox de termos (obrigatório) e recebimento de contato (opcional)
- RF-07: Bloco 2 deve ter nota informativa sobre criação automática de conta
- RF-08: Bloco 3 deve exibir métodos de pagamento apenas os habilitados pelo organizador
- RF-09: Bloco 3 deve ter dropdown "Responsável pelo pagamento" com participantes + "Outro"
- RF-10: Selecionar participante no Bloco 3 deve pré-preencher dados do comprador
- RF-11: Checkout gratuito não deve exibir métodos de pagamento no Bloco 3
- RF-12: Conta deve ser criada automaticamente exceto em checkout não nominal gratuito
- RF-13: Se e-mail já existe, usar conta existente sem duplicar
- RF-14: Dados salvos devem ser vinculados ao usuário (não ao método de pagamento)
- RF-15: Alterações nos dados devem atualizar os dados salvos
- RF-16: Desmarcar "Salvar dados" deve limpar dados salvos
- RF-17: Usuário pode editar dados pré-preenchidos
- RF-18: Campos obrigatórios devem ser validados antes de permitir avanço
- RF-19: Cupom deve ser validado ao clicar "Adicionar"
- RF-20: Cupom válido deve exibir nome e valor descontado com opção remover
- RF-21: Cupom inválido deve exibir mensagem de erro abaixo do campo
- RF-22: Apenas um cupom por pedido
- RF-23: Countdown de 15 minutos deve ser exibido no resumo
- RF-24: Ao expirar countdown, redirect para página do evento
- RF-25: Cartão recusado deve manter campos e exibir mensagem de erro
- RF-26: Pix deve exibir QR Code e código copia e cola
- RF-27: Tela de sucesso Pix após confirmação via webhook
- RF-28: Boleto deve exibir tela "Aguardando pagamento" com download e código

## 13. Requisitos Não-Funcionais

- RNF-01: Componentes responsivos (mobile-first)
- RNF-02: Skeleton/spinner em todos estados de loading
- RNF-03: Erros de validação inline
- RNF-04: Acessibilidade: labels, aria-labels, focus states

## 14. Métricas de Sucesso

A definir com o Product Owner:
- Taxa de conclusão de checkout
- Tempo médio no checkout
- Taxa de abandono por step (Bloco 1, 2, 3)
- Taxa de erro de validação por campo
- Conversão por método de pagamento (Pix vs Cartão vs Boleto)
- Taxa de cupons aplicados vs tentativos

## 15. Fora do Escopo

- Proteção e segurança do checkout (Tópico 10 — a definir com time dev)
- Integração com gateway de pagamento (backend)
- E-mails transacionais (backend)
- Gestão de eventos/criar ingresso (backoffice)
- Autenticação/login (já existe)

## 16. Questões em Aberto

- [ ] Tópico 10 (Proteção e Segurança) — a definir com time dev
- [ ] Definição de métricas de sucesso com Product Owner
