# 🩸 Bloodell — Histórias de Usuário

> **Entrega 01**

## Sobre este documento

Este documento apresenta as histórias de usuário do projeto **Bloodell**, elaboradas a partir das personas identificadas para o sistema.

# Personas relacionadas

As histórias foram construídas com base nas seguintes personas:

| Persona                                                     | Perfil                                 |
| ----------------------------------------------------------- | -------------------------------------- |
| 🔬 Técnico de Hemoterapia                                   | Operacional e gerenciamento de estoque |
| 🏥 Profissional Responsável pelas Solicitações Hospitalares | Solicitação de hemocomponentes         |
| 🚚 Coordenador Logístico                                    | Distribuição e roteirização            |
| 📊 Gestor da Rede de Sangue                                 | Gestão estratégica e indicadores       |


# Priorização das histórias

As histórias foram classificadas utilizando o método **MoSCoW**.

| Prioridade     | Significado                                 |
| -------------- | ------------------------------------------- |
| 🔴 Must Have   | Essencial para a primeira versão do sistema |
| 🟠 Should Have | Muito importante para o produto             |
| 🟡 Could Have  | Diferencial que agrega valor                |
| ⚪ Won't Have  | Planejado para versões futuras              |


# US01 — Cadastro de bolsa por código de barras

**Persona:** 🔬 Técnico de Hemoterapia
**Prioridade:** 🟡 Could Have

## História de usuário

**Como Técnico de Hemoterapia, quero escanear o código de barras de uma nova bolsa para preencher automaticamente suas informações e registrar sua entrada no estoque de forma rápida e organizada.**

## Contexto de negócio

O Técnico de Hemoterapia trabalha diretamente com a entrada e organização das bolsas disponíveis.

O cadastro manual pode tornar o processo mais lento e aumentar a possibilidade de erros na digitação.

O Bloodell deverá permitir a simulação da leitura de um código de barras para preencher automaticamente as informações associadas à bolsa.

O usuário deverá revisar as informações antes de confirmar o cadastro.

## Regras de negócio

* Cada bolsa deve possuir um identificador único;
* O sistema deve tentar localizar os dados associados ao código informado;
* As informações encontradas devem ser preenchidas automaticamente;
* O usuário poderá revisar os dados antes da confirmação;
* Após a confirmação, a bolsa deverá ser registrada no estoque;
* O código de barras será utilizado apenas em uma simulação acadêmica.

## Valor entregue

* Redução de erros manuais;
* Maior velocidade no cadastro;
* Melhor organização do estoque;
* Maior rastreabilidade das bolsas.



## 🧪 Critérios de aceitação — BDD

### Cenário 1: Leitura válida do código

```gherkin
Dado que o Técnico de Hemoterapia está na tela de cadastro de bolsas
E possui um código de barras válido
Quando o código for escaneado
Então o sistema deve preencher automaticamente as informações disponíveis da bolsa
E permitir que o Técnico revise os dados.
```

### Cenário 2: Código não encontrado

```gherkin
Dado que o Técnico de Hemoterapia está cadastrando uma nova bolsa
Quando um código de barras não reconhecido for informado
Então o sistema deve informar que o código não foi encontrado
E permitir o preenchimento manual das informações.
```

### Cenário 3: Confirmação do cadastro

```gherkin
Dado que os dados da bolsa foram preenchidos corretamente
Quando o Técnico confirmar o cadastro
Então a bolsa deve ser registrada no sistema
E ficar disponível no estoque conforme seu status.
```

# US02 — Previsão de demanda e risco de desperdício

**Persona:** 📊 Gestor da Rede de Sangue
**Prioridade:** 🟠 Should Have

## História de usuário

**Como Gestor da Rede de Sangue, quero visualizar previsões de demanda para os próximos sete dias para identificar riscos de desperdício ou falta de hemocomponentes e tomar decisões antecipadamente.**

## Contexto de negócio

O Gestor precisa acompanhar não apenas a situação atual do estoque, mas também possíveis cenários futuros.

Bolsas possuem prazo de validade limitado e podem ser desperdiçadas caso não sejam utilizadas antes do vencimento.

O sistema deverá analisar dados históricos sintéticos e informações do estoque para gerar previsões para os próximos sete dias.

## Regras de negócio

* A previsão deve utilizar dados históricos sintéticos;
* O período analisado será de sete dias;
* O sistema deverá comparar a demanda prevista com o estoque disponível;
* Bolsas próximas do vencimento devem ser consideradas na análise;
* O sistema poderá identificar risco de desperdício;
* O sistema poderá identificar possível falta de estoque;
* As previsões possuem finalidade exclusivamente acadêmica.

## 🎯 Valor entregue

* Antecipação de possíveis problemas;
* Redução do desperdício;
* Melhor planejamento do estoque;
* Apoio à tomada de decisões estratégicas.

## Critérios de aceitação — BDD

### Cenário 1: Visualização da previsão

```gherkin
Dado que existem dados históricos sintéticos disponíveis
Quando o Gestor acessar a área de previsões
Então o sistema deve apresentar estimativas para os próximos sete dias.
```

### Cenário 2: Risco de desperdício

```gherkin
Dado que existem bolsas próximas da data de validade
E a previsão indica baixa demanda para determinado hemocomponente
Quando o sistema analisar os dados
Então deve identificar um possível risco de desperdício.
```

### Cenário 3: Possível falta de estoque

```gherkin
Dado que existe uma previsão de aumento da demanda
Quando o estoque disponível for menor que a demanda prevista
Então o sistema deve apresentar um alerta de possível falta de hemocomponentes.
```

# US03 — Análise de rotas e possíveis congestionamentos

**Persona:** 🚚 Coordenador Logístico
**Prioridade:** 🟡 Could Have


## História de usuário

**Como Coordenador Logístico, quero receber análises sobre as condições das rotas de distribuição para identificar possíveis congestionamentos ou atrasos e escolher uma rota alternativa para reduzir o risco de atraso nas entregas.**

## Contexto de negócio

O Coordenador Logístico é responsável por organizar a distribuição de hemocomponentes entre os pontos da rede.

Atrasos podem comprometer o planejamento da entrega e dificultar o cumprimento das janelas de distribuição.

O Bloodell deverá representar os locais da rede através de um grafo e utilizar informações simuladas sobre as condições das rotas.

---

## 📌 Regras de negócio

* Os locais da rede devem ser representados como nós de um grafo;
* As conexões devem representar caminhos possíveis;
* Cada caminho poderá possuir informações como distância e tempo estimado;
* O sistema poderá simular congestionamentos;
* O sistema deverá comparar rotas alternativas quando disponíveis;
* As informações de trânsito terão finalidade exclusivamente acadêmica.

---

## 🎯 Valor entregue

* Melhor planejamento das entregas;
* Identificação antecipada de atrasos;
* Comparação entre rotas;
* Maior eficiência logística.

---

## 🧪 Critérios de aceitação — BDD

### Cenário 1: Identificação de congestionamento

```gherkin
Dado que existe uma rota planejada para uma entrega
Quando o sistema identificar um congestionamento simulado na rota
Então deve informar o Coordenador Logístico sobre o possível atraso.
```

### Cenário 2: Rota alternativa

```gherkin
Dado que a rota principal possui congestionamento
E existe uma rota alternativa disponível
Quando o sistema analisar as condições das rotas
Então deve apresentar uma alternativa ao Coordenador Logístico.
```

### Cenário 3: Comparação de rotas

```gherkin
Dado que existem múltiplas rotas entre dois locais da rede
Quando o Coordenador solicitar uma análise
Então o sistema deve apresentar a distância e o tempo estimado de cada rota disponível.
```

---

# ⏳ US04 — Seleção automática utilizando FEFO

**Persona:** 🔬 Técnico de Hemoterapia

**Épico:** Gestão de Estoque e Distribuição

**Prioridade:** 🔴 Must Have

---

## 👤 História de usuário

**Como Técnico de Hemoterapia, quero que o sistema priorize automaticamente as bolsas com data de validade mais próxima para reduzir o desperdício causado pelo vencimento de hemocomponentes.**

---

## 💼 Contexto de negócio

Durante o atendimento de uma solicitação, é necessário selecionar bolsas disponíveis para separação e distribuição.

O sistema deverá utilizar a estratégia:

> **FEFO — First Expire, First Out**

Após identificar bolsas elegíveis dentro das regras da simulação, o sistema deverá priorizar aquelas que vencem primeiro.

Para fins acadêmicos, a implementação poderá utilizar uma **fila de prioridade**, aplicando conceitos de estruturas de dados.

---

## 📌 Regras de negócio

* Bolsas vencidas não podem ser selecionadas;
* Apenas bolsas disponíveis podem participar da seleção;
* A seleção deve considerar as regras de compatibilidade didática do sistema;
* Bolsas com vencimento mais próximo possuem maior prioridade;
* O sistema deve informar quando o estoque for insuficiente.

---

## 🎯 Valor entregue

* Redução do desperdício;
* Melhor aproveitamento do estoque;
* Aplicação automática da estratégia FEFO;
* Maior eficiência na separação das bolsas.

---

## 🧪 Critérios de aceitação — BDD

### Cenário 1: Priorização por validade

```gherkin
Dado que existem várias bolsas elegíveis disponíveis
E cada bolsa possui uma data de validade diferente
Quando o sistema selecionar bolsas para atender uma requisição
Então as bolsas com vencimento mais próximo devem ser selecionadas primeiro.
```

### Cenário 2: Bolsa vencida

```gherkin
Dado que existe uma bolsa com validade expirada
Quando o sistema realizar a seleção das bolsas
Então a bolsa vencida não deve ser selecionada.
```

### Cenário 3: Estoque insuficiente

```gherkin
Dado que uma requisição necessita de uma quantidade maior que o estoque disponível
Quando o sistema tentar selecionar as bolsas
Então deve informar que o estoque é insuficiente para atender completamente a solicitação.
```

---

# 🩸 US05 — Visualização e controle do estoque

**Persona:** 🔬 Técnico de Hemoterapia

**Épico:** Gestão de Estoque

**Prioridade:** 🔴 Must Have

---

## 👤 História de usuário

**Como Técnico de Hemoterapia, quero visualizar as bolsas disponíveis organizadas por tipo sanguíneo e hemocomponente para acompanhar a situação do estoque e identificar necessidades de reposição ou riscos de vencimento.**

---

## 💼 Contexto de negócio

O Técnico precisa acompanhar constantemente a disponibilidade dos hemocomponentes.

Uma visualização organizada permite identificar rapidamente:

* Estoque disponível;
* Bolsas próximas do vencimento;
* Bolsas vencidas;
* Tipos sanguíneos com pouca disponibilidade;
* Situação dos hemocomponentes.

---

## 📌 Regras de negócio

Cada bolsa deve possuir informações como:

* Código ou identificador;
* Tipo sanguíneo;
* Fator Rh;
* Hemocomponente;
* Quantidade;
* Data de validade;
* Local de armazenamento;
* Status.

O sistema deverá permitir a organização e consulta dessas informações.

---

## 🎯 Valor entregue

* Maior controle operacional;
* Visualização rápida da disponibilidade;
* Identificação de riscos;
* Apoio ao gerenciamento do estoque.

---

## 🧪 Critérios de aceitação — BDD

### Cenário 1: Visualização do estoque

```gherkin
Dado que existem bolsas cadastradas no sistema
Quando o Técnico acessar a área de estoque
Então o sistema deve apresentar as bolsas disponíveis.
```

### Cenário 2: Agrupamento do estoque

```gherkin
Dado que existem bolsas de diferentes tipos sanguíneos e hemocomponentes
Quando o Técnico visualizar o resumo do estoque
Então o sistema deve apresentar as quantidades agrupadas por tipo sanguíneo e hemocomponente.
```

### Cenário 3: Bolsas próximas do vencimento

```gherkin
Dado que existem bolsas próximas da data de validade
Quando o Técnico acessar o estoque
Então o sistema deve destacar essas bolsas.
```

---

# 🏥 US06 — Criação e acompanhamento de requisições

**Persona:** 🏥 Profissional Responsável pelas Solicitações Hospitalares

**Épico:** Gestão de Requisições

**Prioridade:** 🔴 Must Have

---

## 👤 História de usuário

**Como profissional responsável pelas solicitações hospitalares, quero registrar uma requisição de hemocomponentes informando quantidade, prioridade e prazo para que o hemocentro possa organizar o atendimento da necessidade do hospital.**

---

## 💼 Contexto de negócio

Os hospitais precisam comunicar suas necessidades ao hemocentro responsável pela distribuição.

A requisição centraliza as informações necessárias para organizar o atendimento e permite acompanhar seu progresso.

---

## 📌 Regras de negócio

Cada requisição deverá possuir:

* Hospital solicitante;
* Tipo sanguíneo necessário;
* Hemocomponente solicitado;
* Quantidade;
* Prioridade;
* Prazo ou janela de entrega;
* Status da requisição.

---

## 🎯 Valor entregue

* Organização das solicitações;
* Melhor comunicação entre hospital e hemocentro;
* Priorização dos atendimentos;
* Maior rastreabilidade.

---

## 🧪 Critérios de aceitação — BDD

### Cenário 1: Criação da requisição

```gherkin
Dado que o Profissional está autorizado a criar uma requisição
Quando informar todos os dados obrigatórios
Então o sistema deve registrar a solicitação com status pendente.
```

### Cenário 2: Organização por prioridade

```gherkin
Dado que existem múltiplas requisições pendentes
Quando o sistema organizar as solicitações
Então deve considerar o nível de prioridade informado em cada requisição.
```

### Cenário 3: Acompanhamento da requisição

```gherkin
Dado que uma requisição foi registrada
Quando o Profissional consultar sua solicitação
Então o sistema deve apresentar o status atual do atendimento.
```

---

# ❄️ US07 — Monitoramento da cadeia fria durante o transporte

**Persona:** 🚚 Coordenador Logístico

**Épico:** Monitoramento Logístico

**Prioridade:** 🔴 Must Have

---

## 👤 História de usuário

**Como Coordenador Logístico, quero acompanhar a temperatura e o status das entregas durante o transporte para identificar problemas na cadeia fria e agir rapidamente diante de possíveis riscos logísticos.**

---

## 💼 Contexto de negócio

Durante a distribuição de hemocomponentes, o Coordenador Logístico precisa acompanhar as condições das entregas.

O Bloodell deverá simular informações de telemetria relacionadas ao transporte, permitindo identificar situações anormais.

As informações poderão incluir:

* Temperatura;
* Localização GPS simulada;
* Status da conexão;
* Situação da entrega.

---

## 📌 Regras de negócio

* A telemetria será simulada;
* A temperatura deverá ser monitorada durante a entrega;
* A faixa aceitável será configurável para fins de simulação;
* Temperaturas fora da faixa devem gerar alertas;
* Falhas de comunicação devem gerar alertas;
* Os alertas devem possuir informações sobre o problema identificado.

---

## 🎯 Valor entregue

* Maior visibilidade das entregas;
* Identificação rápida de problemas;
* Melhor acompanhamento da cadeia logística;
* Registro de alertas operacionais.

---

## 🧪 Critérios de aceitação — BDD

### Cenário 1: Temperatura dentro da faixa

```gherkin
Dado que uma entrega está em andamento
Quando o sistema receber uma temperatura dentro da faixa configurada
Então o status da cadeia fria deve permanecer normal.
```

### Cenário 2: Temperatura fora da faixa

```gherkin
Dado que uma entrega está em andamento
Quando o sistema identificar uma temperatura fora da faixa configurada
Então deve gerar um alerta de temperatura.
```

### Cenário 3: Falha de comunicação

```gherkin
Dado que existe uma entrega sendo monitorada
Quando a conexão de telemetria for perdida
Então o sistema deve gerar um alerta de falha de comunicação.
```

### Cenário 4: Visualização dos alertas

```gherkin
Dado que existem alertas ativos
Quando o Coordenador Logístico acessar o painel de monitoramento
Então o sistema deve apresentar os alertas ativos relacionados às entregas.
```

---

# 📊 Matriz de rastreabilidade

A tabela abaixo demonstra a relação entre as personas e as histórias de usuário.

| ID   | História                      | Persona Principal           | Prioridade     |
| ---- | ----------------------------- | --------------------------- | -------------- |
| US01 | Cadastro por código de barras | 🔬 Técnico de Hemoterapia   | 🟡 Could Have  |
| US02 | Previsão de demanda           | 📊 Gestor da Rede de Sangue | 🟠 Should Have |
| US03 | Análise de rotas              | 🚚 Coordenador Logístico    | 🟡 Could Have  |
| US04 | Seleção utilizando FEFO       | 🔬 Técnico de Hemoterapia   | 🔴 Must Have   |
| US05 | Controle do estoque           | 🔬 Técnico de Hemoterapia   | 🔴 Must Have   |
| US06 | Requisições hospitalares      | 🏥 Profissional Hospitalar  | 🔴 Must Have   |
| US07 | Monitoramento da cadeia fria  | 🚚 Coordenador Logístico    | 🔴 Must Have   |

---

# 🔄 Relação entre Personas e Histórias

```text
🔬 TÉCNICO DE HEMOTERAPIA
│
├── US01 → Cadastro por código de barras
├── US04 → Seleção utilizando FEFO
└── US05 → Controle do estoque


🏥 PROFISSIONAL HOSPITALAR
│
└── US06 → Criação e acompanhamento de requisições


🚚 COORDENADOR LOGÍSTICO
│
├── US03 → Análise de rotas
└── US07 → Monitoramento da cadeia fria


📊 GESTOR DA REDE DE SANGUE
│
└── US02 → Previsão de demanda
```

---

# 🎯 Cobertura dos módulos do Bloodell

As histórias cobrem os quatro principais módulos do projeto.

| Módulo           | Histórias         |
| ---------------- | ----------------- |
| 🩸 Estoque       | US01, US04 e US05 |
| 🏥 Requisições   | US06              |
| 🚚 Distribuição  | US03 e US04       |
| 📊 Monitoramento | US02 e US07       |

---

# ⚠️ Limitações do escopo

O Bloodell é um projeto acadêmico baseado em simulações.

Portanto:

* Todos os dados utilizados serão sintéticos;
* Não serão utilizados dados reais de pacientes ou doadores;
* A compatibilidade sanguínea terá finalidade exclusivamente didática;
* A telemetria será simulada;
* As informações sobre trânsito poderão ser simuladas;
* As previsões possuem finalidade acadêmica;
* O sistema não substitui protocolos clínicos ou sistemas oficiais da Hemorrede/SUS.

---

# 🚀 Conclusão

As histórias de usuário apresentadas foram construídas a partir das necessidades das principais personas do Bloodell.

Essa relação permite garantir que cada funcionalidade desenvolvida possua um propósito claro e entregue valor para pelo menos um perfil de usuário do sistema.

A estrutura definida estabelece a seguinte relação:

```text
👥 PERSONAS
     ↓
🎯 NECESSIDADES
     ↓
📖 HISTÓRIAS DE USUÁRIO
     ↓
📌 REGRAS DE NEGÓCIO
     ↓
🧪 CENÁRIOS BDD
     ↓
💻 DESENVOLVIMENTO
```

> 🩸 **Bloodell — Gestão, distribuição e monitoramento inteligente da rede de sangue.**
