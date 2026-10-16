# Rossi Formaturas — Sistema de Planejamento Operacional

> *"Você conquista, nós tornamos inesquecível."*

Sistema web completo, funcional, responsivo e seguro para planejamento, organização e controle operacional de eventos de formatura da **Rossi Formaturas**. O sistema centraliza o cadastro de formaturas, alocação de fotógrafos e equipe de campo, cálculo automático de custos, geolocalização e proximidade com base oficial do IBGE, relatórios operacionais/administrativos com exportação em A4 e integração oficial com o WhatsApp.

---

## 1. Identidade Visual da Rossi Formaturas

O sistema foi concebido respeitando com rigor a identidade visual da Rossi Formaturas e as diretrizes de design de alto padrão (anti-AI slop, zero-pill discipline, tipografia geométrica):

* **Roxo Profundo:** `#4A148C` (Barra superior institucional, botões de ação primária, destaques)
* **Roxo Vibrante:** `#8E24AA` (Gradientes dinâmicos de destaque)
* **Ouro Nobre:** `#C5A869` (Detalhes nobres, destaques de valor e coroamento)
* **Grafite:** `#2D2D2D` (Títulos e textos estruturais)
* **Branco e Neutros:** `#FFFFFF` e `#FAF9F6` (Fundo limpo e áreas de leitura com contraste ideal)
* **Gradiente Oficial:** `#4A148C` → `#8E24AA`
* **Tipografia:** `Plus Jakarta Sans` para textos, cabeçalhos e navegação, e `JetBrains Mono` com `tabular-nums` para valores monetários e tabelas.

---

## 2. Funcionalidades Implementadas

### A. Painel de Controle Operacional (Dashboard)
* **Indicadores em Tempo Real:** Total de eventos, próximos eventos, eventos aguardando equipe ou com equipe incompleta, fotógrafos ativos e custos previstos/realizados.
* **Filtros Dinâmicos:** Filtros instantâneos por período (próximos 30 dias, futuros), status do evento, estado (UF) e segmento.
* **Alertas Operacionais:** Identificação imediata de vagas não preenchidas e carência de profissionais na equipe.

### B. Gestão Completa de Eventos
* **Segmentos Atendidos:** Pré-escola, 5º ano, 9º ano, Terceirão, Cursos Técnicos, Ensino Superior, Pós-Graduação e Outros.
* **Campos Detalhados:** Instituição, turma, horários de início e término, local/espaço, endereço completo, quantidade de formandos e metas de fotógrafos e assistentes.
* **Status do Evento:** Em Planejamento, Aguardando Equipe, Equipe Parcial, Equipe Confirmada, Realizado, Cancelado e Arquivado.
* **Preservação Histórica:** Arquivamento seguro de eventos com histórico financeiro preservado.

### C. Base Oficial de Estados e Municípios Brasileiros (IBGE)
* **Todos os 26 Estados + DF:** Seleção intuitiva de UF.
* **Municípios Oficiais:** Integração em tempo real com a API oficial de Localidades do IBGE (`servicodados.ibge.gov.br/api/v1/localidades/estados/{UF}/municipios`), com cache inteligente em memória e catálogo offline de contingência.
* **Tratamento de Homônimos:** Identificação inequívoca pelo código IBGE oficial do município.

### D. Seleção de Profissionais por Proximidade e Conflito de Agenda
* **Cálculo de Distância:** Cálculo de distância em linha reta pela fórmula de Haversine (`calculateStraightLineDistance`) com identificação explícita de *"distância estimada em linha reta"*.
* **Ordenação Inteligente:** Prioriza profissionais do mesmo município (0 km) e lista municípios vizinhos por proximidade crescente.
* **Prevenção de Duplicidade:** O sistema impede que o mesmo profissional seja adicionado em duplicidade no mesmo evento.
* **Detecção de Conflito de Agenda:** Alerta automático caso o profissional já esteja alocado em outro evento concomitante na mesma data e com choque de horários.

### E. Escala de Equipe e Níveis de Alocação
* **Categorias:** Fotógrafo, Assistente de Iluminação, Cerimonialista, Decorador e Coordenador de Campo.
* **Status da Alocação:** Convidado, Aguardando Confirmação, Confirmado, Recusado, Substituído e Cancelado.
* **Contato Rápido:** Acesso direto ao WhatsApp e discador telefônico de cada membro com formatação brasileira `(XX) XXXXX-XXXX`.

### F. Controle Financeiro e Orçamentos Auditáveis
* **Cálculos Automáticos:** Custo Individual = Cachê Freelancer + Alimentação + Deslocamento + Hospedagem + Outras despesas.
* **Totais Consolidados:** Total de cachês, despesas com alimentação, deslocamento, hotelaria e despesas gerais do evento (rádios comunicadores, credenciais, etc.).
* **Padrão Monetário:** Exibição oficial em Reais (`R$ 1.500,00`).
* **Privacidade de Custos:** Visibilidade financeira restrita ao perfil de Administrador.

### G. Relatórios de Evento & Compartilhamento WhatsApp
* **Relatório Operacional de Campo:** Dados da instituição, turma, horários, local e lista completa da equipe com funções e contatos telefônicos — **sem valores financeiros por padrão**.
* **Relatório Administrativo:** Detalhamento financeiro completo com subtotais por categoria profissional e balanço previsto vs. realizado.
* **Impressão Otimizada A4 & PDF:** Folha de estilo `@media print` que remove menus, rodapés e botões, garantindo diagramação limpa em papel A4 ou exportação para arquivo PDF.
* **Compartilhamento WhatsApp:** Geração do link oficial (`api.whatsapp.com/send`) com texto diagramado com clareza, pronto para envio aos líderes de equipe e grupos operacionais.

### H. Níveis de Acesso e Permissões (RBAC)
* **Administrador:** Acesso integral a todas as telas, cadastros, relatórios financeiros e aprovação de colaboradores.
* **Coordenadora:** Acesso a eventos, escalas e relatórios operacionais de campo, sem exposição de dados financeiros confidenciais da empresa.
* **Fotógrafo (Portal Exclusivo):** Acesso restrito ao seu próprio perfil. Pode atualizar dados de contato, áreas atendidas e calendário de disponibilidade. Bloqueado de consultar a agenda geral, custos e dados de terceiros.
* **Página Pública de Cadastro:** Formulário externo para novos fotógrafos enviarem sua candidatura, com status inicial "Pendente" para avaliação do administrador.

---

## 3. Estrutura do Projeto

```
├── .env.example                  # Variáveis de ambiente
├── index.html                    # Ponto de entrada com fontes oficiais e meta tags
├── metadata.json                 # Metadados e capacidades
├── package.json                  # Dependências e scripts
├── tsconfig.json                 # Configurações TypeScript
├── vite.config.ts                # Configuração do Vite e Tailwind CSS
├── supabase/
│   └── schema.sql                # DDL PostgreSQL completo com Row Level Security (RLS)
├── src/
│   ├── main.tsx                  # Ponto de entrada React
│   ├── App.tsx                   # Controlador principal e roteamento por papéis
│   ├── index.css                 # Import do Tailwind, scrollbar e regras @media print
│   ├── types/
│   │   └── index.ts              # Tipagens TypeScript para usuários, eventos e finanças
│   ├── utils/
│   │   └── formatters.ts         # Formatação de BRL, datas brasileiras, telefones e status
│   ├── data/
│   │   ├── brazilLocations.ts    # Estados, integração IBGE e cálculo Haversine
│   │   └── mockDatabase.ts       # Repositório com persistência em LocalStorage e seeds
│   └── components/
│       ├── RossiLogo.tsx         # Logo vetorizada oficial com gradientes da marca
│       ├── Header.tsx            # Barra superior (Top Bar Contract) e seletor de perfil
│       ├── DashboardView.tsx     # Painel com KPIs operacionais e agenda
│       ├── EventsView.tsx        # Lista completa de formaturas com busca e filtros
│       ├── EventDetailView.tsx   # Escala da equipe, relatórios A4 e WhatsApp
│       ├── EventEditorModal.tsx  # Modal de cadastro e edição de formaturas
│       ├── ProfessionalsView.tsx # Gestão de fotógrafos e aprovação de candidatos
│       ├── FinancialView.tsx     # Módulo de custos e auditoria para administradores
│       ├── PhotographerPortalView.tsx # Portal restrito do fotógrafo
│       ├── CitySelector.tsx      # Seletor de Estado e Município com busca IBGE
│       ├── ProfessionalPickerModal.tsx # Seletor de equipe por proximidade geográfica
│       └── PublicPhotographerRegistration.tsx # Formulário público de candidatura
```

---

## 4. Instruções de Instalação e Execução Local

### Pré-requisitos
* Node.js v18+ ou superior.
* Gerenciador de pacotes npm, yarn ou pnpm.

### Passo a passo
1. Clone o repositório ou navegue até o diretório do projeto:
   ```bash
   cd rossi-formaturas
   ```

2. Instale as dependências:
   ```bash
   npm install
   ```

3. Inicie o servidor de desenvolvimento:
   ```bash
   npm run dev
   ```

4. Abra o navegador no endereço indicado:
   ```
   http://localhost:3000
   ```

---

## 5. Configuração do Backend com Supabase

Para conectar a aplicação ao banco de dados PostgreSQL com Supabase:

1. Acesse o [Supabase](https://supabase.com) e crie um novo projeto.
2. No menu lateral, acesse **SQL Editor** e crie uma nova query.
3. Copie todo o conteúdo do arquivo `supabase/schema.sql` e execute o script.
   * O script criará as tabelas `profiles`, `professionals`, `events`, `team_members` e `general_expenses`.
   * Habilitará os tipos enums, índices de performance e todas as políticas de segurança RLS (Row Level Security).
4. No menu lateral do Supabase, acesse **Project Settings** > **API**.
5. Copie a **Project URL** e a chave pública **anon / public**.
6. Preencha no seu arquivo `.env`:
   ```env
   VITE_SUPABASE_URL=https://seu-projeto.supabase.co
   VITE_SUPABASE_ANON_KEY=sua-chave-anonima-publica
   ```
   > ⚠️ **Segurança:** Nunca exponha a chave `service_role` no código público ou no frontend.

---

## 6. Criação Segura do Primeiro Administrador

Para criar o primeiro usuário administrador com segurança:

1. Acesse o painel do Supabase em **Authentication** > **Users**.
2. Clique em **Add User** > **Create User**.
3. Informe o e-mail oficial (ex: `admin@rossiformaturas.com.br`) e defina uma senha forte com caracteres especiais e números.
4. Após criar o usuário, anote o `UUID` gerado.
5. No **SQL Editor** do Supabase, execute o comando para promover o usuário a Administrador:
   ```sql
   INSERT INTO public.profiles (id, name, email, role, phone)
   VALUES (
     'UUID-DO-USUARIO-CRIADO',
     'Edilson Lima',
     'admin@rossiformaturas.com.br',
     'admin',
     '(11) 98765-4321'
   )
   ON CONFLICT (id) DO UPDATE SET role = 'admin';
   ```
6. O usuário agora possui acesso administrativo irrestrito garantido pelas políticas RLS.

---

## 7. Instruções para Publicação na Vercel via GitHub

1. Faça o commit e envie o código para seu repositório no GitHub:
   ```bash
   git add .
   git commit -m "feat: Sistema de Planejamento Operacional Rossi Formaturas"
   git push origin main
   ```
2. Acesse a [Vercel](https://vercel.com) e conecte sua conta do GitHub.
3. Clique em **Add New Project** e selecione o repositório `rossi-formaturas`.
4. Em **Environment Variables**, adicione as variáveis de ambiente necessárias:
   * `VITE_SUPABASE_URL`
   * `VITE_SUPABASE_ANON_KEY`
5. Clique em **Deploy**. A Vercel executará o build e disponibilizará o link HTTPS seguro da aplicação.

---

## 8. Verificação e Testes Executados

* [x] **Autenticação e Perfis (RBAC):** Alternância e isolamento completo entre Administrador, Coordenadora e Fotógrafo.
* [x] **Isolamento de Dados do Fotógrafo:** Fotógrafos não conseguem consultar relatórios administrativos, custos da empresa ou dados de outros fotógrafos.
* [x] **Seleção de Estados e Cidades:** Integração oficial com a API do IBGE cobrindo todos os municípios e estados brasileiros.
* [x] **Cálculo de Proximidade:** Cálculo de distância por coordenadas geográficas com ordenação crescente e tratamento para ausência de profissionais na cidade sede.
* [x] **Prevenção de Duplicidade:** Bloqueio de alocação duplicada do mesmo profissional no mesmo evento.
* [x] **Detecção de Conflitos de Agenda:** Alerta para profissionais alocados em horários concorrentes no mesmo dia.
* [x] **Cálculo de Custos e Totais:** Soma de cachês, alimentação, deslocamento, hotelaria e despesas gerais sem contagem duplicada.
* [x] **Impressão e PDF:** Estilos `@media print` formatados para papel A4 sem corte de elementos ou interferência de barras de navegação.
* [x] **Compartilhamento WhatsApp:** Link oficial com texto estruturado operacional pronto para envio sem valores financeiros sensíveis.
* [x] **Responsividade Mobile-First:** Navegação fluida testada em celulares, tablets e computadores.
