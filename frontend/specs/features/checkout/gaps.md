# Checkout - gaps & Planning

## 1. Informações Faltantes para Desenvolvimento

### 1.1 Contratos de API Necessários
Liste os endpoints que o frontend provavelmente precisará consumir:
- GET /events/:id/checkout-config - obter configuração do checkout
- POST /checkout/participants - enviar dados dos participantes (Bloco 1)
- POST /checkout/responsible - informar responsável pelos ingresso (Bloco 2)
- POST /checkout/validate-coupon - validar cupom de desconto
- POST /checkout/reserve - reservar ingresso (iniciar checkout)
- POST /checkout/process-payment - processar pagamento (Bloco 3)
- POST /checkout/create-account - criar conta automática
- GET /checkout/:id/status - verificar status do pagamento
- POST /checkout/confirm - confirmar compra
- POST /auth/check - verificar se usuário está logado
- (outros endpoints que o dev precisar definir baseado nos fluxos)

### 1.2 Estados de Loading/Error Não Detalhados
- Loading ao carregar configuração do evento: Qual skeleton/spinner usar?
- Loading ao validar cupom: Como exibir feedback?
- Loading ao processar pagamento: Qual estado de espera?
- Loading ao criar conta: Mensagem para o usuário?
- Tratamento de erros de rede: Como exibir para o usuário?
- Tratamento de timeouts: Quanto tempo esperar?

### 1.3 Componentes UI Não Especificados
- Componentes de formulários necessários:
  - Input com DDI + máscara de celular
  - Dropdown com busca (responsável)
  - Checkbox com link (termos)
  - Campo de cupom com botão
  - Seletor de método de pagamento (radio/toggle)
- Componentes de display de erros:
  - Erro por campo
  - Erro geral do checkout
  - Erro de pagamento
- Componentes de loading:
  - Loading de submit
  - Loading de pagamento
  - Skeleton de configuração
- Componentes de resumo do pedido:
  - Card com detalhes do evento
  - Lista de inúmerosingressos
  - Cálculo de desconto
  - Total
- Outros componentes:
  - Contador regressivo (15 min)
  - QR Code (Pix)
  - Boleto embed/link

### 1.4 edge Cases de UX Não Detalhados
- O que acontece se o usuário fecha a aba durante checkout: Salvar no localStorage?
- O que acontece se o usuário atualiza a página: Restaurar dados do formulário?
- Persistência de dados do formulário entre sessões: Por quanto tempo?
- Validação em tempo real vs validação no submit: Quando validar cada campo?
- Ordenação de validações de campos: Validar todos de uma vez ou um a um?

## 2. Cenários de Teste Suggestivos

### 2.1 Cenários Happy Path
- Fluxo completo de checkout nominal pago
- Fluxo completo de checkout nominal gratuito
- Fluxo completo de checkout não nominal pago
- Fluxo completo de checkout não nominal gratuito (logado)
- Aplicação de cupom válido com sucesso
- Remoção de cupom aplicado
- Criação automática de conta com novo e-mail
- Criação automática de conta com e-mail existente (sem login)
- Pagamento com cartão aprovado
- Pagamento com Pix (exibição do QR Code)
- Pagamento com Boleto (exibição do boleto)

### 2.2 Cenários de Interrupção
- Usuário fecha navegador durante checkout
- Usuário clica em "voltar" do navegador
- Sessão expira durante checkout (15 min)
- Tempo expirado - redirecionamento para página do evento
- Usuário perde conectividade durante pagamento
- Retorno ao checkout após login (checkout não nominal gratuito)

### 2.3 Cenários de Erro
- Campos obrigatórios não preenchidos
- CPF/CNPJ inválido (se campo customizado)
- E-mail em formato inválido
- Celular em formato inválido
- Cupom inválido/expirado/não encontrado
- Pagamento recusado (manter dados preenchidos)
- Timeout de comunicação com servidor
- Erro genérico de checkout

### 2.4 Cenários de Usuário Logado
- Usuário com dados salvos vs sem dados salvos
- Usuário altera dados salvos durante checkout
- Usuário desmarca "salvar dados"
- Usuário com cartão salvo (preencher apenas CVV)
- Pré-preenchimento de dados do comprador via dropdown

## 3. Fluxos de Navegação Não Especificados

- Rota para tela de checkout: /event/:id/checkout?
- Rota para tela de sucesso: /checkout/:id/success?
- Rota para tela de "Aguardando pagamento" (boleto): /checkout/:id/pending?
- Comportamento do botão "voltar" entre blocos: Voltar ao bloco anterior?
- Redirecionamento após expiração de tempo: /event/:id?
- Retorno ao checkout após login: Retornar ao ponto exato?

## 4. Casos de edge Case Visuais

- Como exibir muitos participantes (scroll): Scroll dentro do bloco?
- Como exibir muitos tipos de ingresso: Lista expansível?
- Como exibir campos customizados longos: Input multilinha?
- Responsividade em mobile: Stack vertical?
- Orientação landscape em mobile: Ajustar layout?
- Tamanho do QR Code em diferentes telas: Tamanho fixo ou responsivo?

## 5. Perguntas para o Product Owner

- [ ] Qual a biblioteca de formulários (React Hook Form, Formik, etc.)?
- [ ] Qual biblioteca de máscaras (React Input Mask, etc.)?
- [ ] Qual biblioteca de gestão de estado (Zustand, Redux, Context)?
- [ ] Quais os endpoints exatos para integração?
- [ ] Qual o tempo de timeout para chamadas de API?
- [ ] O que exibir no skeleton de loading?
- [ ] Como restaurar dados do formulário após refresh?
- [ ] Qual biblioteca de QR Code usar?
- [ ] Como integrar com o Pay (frontend)?
- [ ] Quais são as rotas exatas?
- [ ] O que acontece ao clicar "voltar" no navegador?
- [ ] Como tratar expiração de sessão durante checkout?

## 6. Sugestões de Implementação

Liste pontos que o desenvolvedor deve considerar no planejamento:
- Componentização sugerida:
  - CheckoutContainer (gerencia estado global)
  - BlockParticipants (Bloco 1)
  - BlockDelivery (Bloco 2)
  - BlockPayment (Bloco 3)
  - OrderSummary (painel lateral)
  - CouponInput
  - ParticipantCard
  - PaymentMethodSelector
  - CountdownTimer
- Gerenciamento de estado:
  - Estado do formulário por bloco
  - Session ID do checkout
  - Timer de 15 minutos (sync com backend)
  - Estado de pagamento (pending, processing, success, error)
- Integração com provider de pagamento:
  - SDK do Pay para cartão
  - Geração de QR Code Pix
  - Exibição de boleto
- Tratamento de concorrência de estoque:
  - Poll de status de checkout
  - Exibir erro se ingressos esgotados
- Accessibility considerations:
  - Labels ARIA para todos os campos
  - Navegação por teclado
  - Mensagens de erro descritivas
- Internacionalização:
  - Textos de botões
  - Mensagens de erro
  - Labels de campos
