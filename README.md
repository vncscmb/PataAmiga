# [Pata Amiga]

> Substitua os trechos entre colchetes `[ ]` pelas informações reais do trabalho. Remova esta nota e as demais orientações em *itálico* antes da entrega.

[![Status](https://img.shields.io/badge/status-[em_desenvolvimento]-yellow)]()
[![Versão](https://img.shields.io/badge/versão-[0.1.0]-blue)]()
[![Licença](https://img.shields.io/badge/licença-[acadêmica]-lightgrey)]()

**Instituição:** Centro de Ensino Universitário de Brasília

**Curso:** Ciência da Computação  

**Disciplina:** Desenvolvimento Web  

**Turma / Semestre:** 2026.2

**Professor(a):** Felippe Pires Ferreira

**Status do projeto:** Em desenvolvimento]

---

## Sumário

- [1. Descrição do projeto](#1-descrição-do-projeto)
- [2. Funcionalidades](#2-funcionalidades)
- [3. Demonstração](#3-demonstração)
- [4. Tecnologias utilizadas](#4-tecnologias-utilizadas)
- [5. Arquitetura](#5-arquitetura)
- [6. Organização dos diretórios](#6-organização-dos-diretórios)
- [7. Participantes](#7-participantes)
- [8. Como executar](#8-como-executar)
- [9. Configuração](#9-configuração)
- [10. Testes](#10-testes)
- [11. Uso de inteligência artificial](#11-uso-de-inteligência-artificial)
- [12. Contribuição e fluxo de trabalho](#12-contribuição-e-fluxo-de-trabalho)
- [13. Histórico de versões](#13-histórico-de-versões)
- [14. Limitações e próximos passos](#14-limitações-e-próximos-passos)
- [15. Licença, referências e contato](#15-licença-referências-e-contato)

---

## 1. Descrição do projeto
*Apresente o contexto, o problema e a solução proposta. Use linguagem objetiva (dois a quatro parágrafos).*

Muitos abrigos e associações de proteção animal enfrentam dificuldades em divulgar de forma organizada os animais disponíveis, dependendo muitas vezes de redes sociais que dispersam a informação. Isto dificulta a pesquisa por parte de potenciais adotantes e atrasa o processo de adoção. 

O **Pata Amiga** é uma plataforma web centralizada que conecta abrigos a famílias adotantes, simplificando a pesquisa, a triagem e a gestão dos perfis dos animais. O sistema conta com uma interface de gestão para as instituições e uma página pública de pesquisa rica em dados comportamentais.

[Descreva o que o sistema faz, para quem ele se destina e qual problema ele resolve.]

### Objetivos

*Liste os objetivos gerais e específicos do projeto.*

### Objetivos

- **Objetivo geral:** Desenvolver uma aplicação web em Python e Django para centralizar a gestão e divulgação de animais disponíveis para adoção.
- **Objetivos específicos:**
  - Permitir o cadastro seguro de abrigos e o gerenciamento (CRUD) de perfis de animais.
  - Disponibilizar uma busca pública de animais com múltiplos filtros (espécie, porte, localização).
  - Integrar automaticamente os perfis das raças puras com características comportamentais via The Dog/Cat API.
  - Gerar relatórios de ocupação e histórico de adoções para os abrigos.
  - Disponibilizar os dados públicos através de uma API REST própria.

### Público-alvo

- **Gestores de Abrigos / Protetores Independentes:** Responsáveis por registar, gerir e atualizar o estado dos animais.
- **Adotantes (Público em Geral):** Pessoas à procura de um animal de estimação que utilizam a plataforma para pesquisar perfis e submeter pedidos de adoção.

---

## 2. Funcionalidades

| Funcionalidade | Descrição | Status |
| --- | --- | --- |
| Autenticação e Perfis | Login seguro e gestão do perfil do Abrigo | Planejada (Fase 2) |
| Cadastro de Animais (CRUD) | Criação e gestão de perfis de animais disponíveis | Planejada (Fase 2) |
| Busca Pública de Animais | Filtros por espécie, porte, idade e localização | Planejada (Fase 2) |
| Relatórios de Gestão | Exportação em PDF do histórico e animais aguardando adoção | Planejada (Fase 2) |
| Integração The Dog/Cat API | Autopreenchimento de características de raça e tratamento para SRD | Planejada (Fase 2) |
| API REST Pata Amiga | Disponibilização de dados públicos via endpoints em JSON | Planejada (Fase 2) |

### Requisitos não funcionais

- **Segurança:** Senhas protegidas, variáveis sensíveis em `.env` e acesso por HTTPS em produção. Avaliação via testes SAST/DAST.
- **Integração:** Tratamento de indisponibilidade e timeouts na comunicação com a API externa.
- **Usabilidade:** Interface responsiva para acesso via dispositivos móveis (Mobile First).

---

## 3. Demonstração

*Inclua capturas de tela, GIF ou link para vídeo. Coloque as imagens em `images/`.*

![Tela principal](images/[screenshot-principal].png)

| Tela | Descrição |
| --- | --- |
| [Login] | [Acesso ao sistema com e-mail e senha] |
| [Painel] | [Visão geral das reservas do dia] |

**Vídeo / protótipo:** [URL do YouTube, Loom ou Figma]

---

## 4. Tecnologias utilizadas

*Informe as tecnologias de fato usadas no projeto. Remova as linhas que não se aplicarem.*

| Camada | Tecnologia | Versão |
| --- | --- | --- |
| Linguagem | Python | 3.12+ |
| Backend e Frontend | Django (Arquitetura MVT) | 5.x |
| API Própria | Django REST Framework (DRF) | 3.x |
| Banco de dados | PostgreSQL / SQLite (Local) | - |
| Estilização | HTML5, CSS3, Bootstrap/Tailwind | - |
| Análise de Segurança | Bandit (SAST) / OWASP ZAP (DAST) | - |
| Outras ferramentas | Git, GitHub, Draw.io (Diagramas), Figma (Protótipos) | - |

---


## 5. Arquitetura

*Explique como o sistema está organizado: camadas, principais componentes e o fluxo entre eles. Inclua um diagrama no PDF de arquitetura ou de classes em `docs/` e descreva-o em texto.*

[Ex.: a solução segue uma arquitetura em camadas (apresentação, aplicação, domínio e persistência). O frontend consome uma API REST. O backend aplica as regras de negócio e persiste os dados no banco.]

```text
[Usuário] → [Interface / Frontend] → [API / Backend] → [Banco de dados]
```

**Decisões relevantes:**

- Uso do Django pela robustez e segurança no CRUD de informações.
- Integração da "The Dog/Cat API" no momento do cadastro do animal, utilizando lógica condicional para animais "Sem Raça Definida" (SRD), o que poupa requisições desnecessárias.
- Implementação de API REST própria para expor a lista pública de animais disponíveis para adoção, favorecendo parcerias externas futuras.

### Endpoints principais (quando houver API)

| Método | Rota | Descrição |
| --- | --- | --- |
| `POST` | `/api/[recurso]` | [Ex.: criar um registro] |
| `GET` | `/api/[recurso]` | [Ex.: listar registros] |
| `GET` | `/api/[recurso]/{id}` | [Ex.: obter um registro] |
| `PUT` | `/api/[recurso]/{id}` | [Ex.: atualizar um registro] |
| `DELETE` | `/api/[recurso]/{id}` | [Ex.: remover um registro] |

Documentação completa da API: [link para Swagger, Postman ou `docs/api.md`]

---

## 6. Organização dos diretórios

### 6.1. Casos de Uso
O diagrama de casos de uso com os fluxos principais da aplicação (cadastro de abrigos, consulta de animais e submissão de candidaturas) encontra-se disponível na pasta [`docs/casos-de-uso/`](docs/casos-de-uso/).

### 6.2. Planejamento e Backlog
A relação de tarefas técnicas e o planejamento para a Fase 2 (desenvolvimento em Django, ORM e APIs) estão detalhados em [`docs/planejamento/backlog.md`](docs/planejamento/backlog.md).

### 6.3. Protótipos e Identidade Visual
A especificação da paleta de cores (Azul Oceano e Verde Saúde), tipografia e a estrutura dos ecrãs principais mapeados no Figma estão documentadas em [`docs/prototipos/README.md`](docs/prototipos/README.md).

```text
.
├── README.md                 # Documentação principal do projeto
├── .env.example              # Modelo de variáveis de ambiente
├── docs/               # Artefatos técnicos e documentação da Fase 1
│   ├── casos-de-uso/         # Diagrama e especificações de casos de uso
│   ├── planejamento/         # Backlog e planejamento da Fase 2
│   └── prototipos/          # Identidade visual e especificações do Figma
├── images/                   # Imagens e ativos gráficos da documentação
└── src/                      # Código-fonte da aplicação (Django / Back-end e Front-end)

```
| Diretório / arquivo | Função |
| --- | --- |
| `README.md` | Apresentação do projeto, objetivos, tecnologias e instruções de uso |
| `.env.example` | Modelo de variáveis de ambiente sem credenciais reais |
| `docs/` | Artefatos técnicos, casos de uso, planejamento e protótipos da Fase 1 |
| `images/` | Imagens e ativos gráficos da documentação |
| `src/` | Código-fonte da aplicação (Django / Back-end e Front-end) |

## 7. Participantes

| Nome | Matrícula | Função no projeto |
| --- | --- | --- |
| Vinicius Coelho de Matos Batista | 22508555 |  coordenação / backend / frontend / testes / documentação |
| Victor Hugo Cândido Feitoza Albuquerque Santos  | 22507444 | Ex.: backend |
| João Paulo Costa Sales | 22503901 | frontend, documentação, backend,  |
| Matheus Lopes Cundari | 000000 | Ex.: testes e documentação |

**Professor(a) responsável:** Felippe Pires Ferreira

---

## 8. Como executar

### Pré-requisitos

- Git
- Python 3.12+
- PostgreSQL

### Instalação e execução

```bash
# 1. Clonar o repositório
git clone [https://github.com/vncscmb/PataAmiga.git](https://github.com/vncscmb/PataAmiga.git)
cd PataAmiga

# 2. Criar e ativar o ambiente virtual
python -m venv venv
# No Windows (Git Bash):
source venv/Scripts/activate

# 3. Instalar dependências
pip install -r requirements.txt

# 4. Configurar variáveis de ambiente
cp .env.example .env

# 5. Executar as migrações da base de dados
python manage.py migrate

# 6. Executar a aplicação
python manage.py runserver
```
### Implantação (quando houver)

- **Ambiente:** [Ex.: Render, Railway, Vercel, servidor da instituição]
- **URL de produção:** [https://...]
- **Observações:** [Ex.: é necessário configurar as variáveis de ambiente no painel do provedor]

---

## 9. Configuração

| Variável | Obrigatória | Descrição | Exemplo |
| --- | --- | --- | --- |
| `DEBUG` | Sim | Modo de depuração do Django | `True` |
| `SECRET_KEY` | Sim | Chave de segurança do Django | `sua-chave-secreta-local` |
| `DATABASE_URL` | Sim | String de conexão com o banco de dados | `postgresql://user:senha@localhost:5432/pataamiga_db` |

Credenciais reais devem ficar apenas no arquivo `.env` (não versionado).

---

## 10. Testes

Para executar a suíte de testes automatizados do Django, utilize o comando abaixo na raiz do projeto:

```bash
python manage.py test
```

| Tipo | Ferramenta | O que verifica |
| --- | --- | --- |
| Unitários | unittest / Django Test Framework | Regras de negócio isoladas, validações de modelos e formulários|
| Integração |Django REST Framework APIClient | Endpoints da API, rotas de visualização e persistência no banco de dados |
| Manuais | Checklist interno em docs/ | Fluxos principais da interface e navegação do usuário |

**Cobertura atual:** [Ex.: 70% / não medida]

---

## 11. Uso de inteligência artificial

Este repositório segue a política de uso de IA da disciplina (semáforo pedagógico):

![Política de uso de IA — semáforo](images/semaforo.png)

| Situação | Significado |
| --- | --- |
| **Vermelho — uso proibido** | Atividades de autonomia intelectual (ex.: provas presenciais sem consulta). |
| **Amarelo — uso limitado** | IA pode ser ferramenta auxiliar, desde que haja declaração de uso. |
| **Verde — uso permitido** | Uso livre ao longo da atividade acadêmica. |

- ### Declaração de uso

- **Houve uso de IA neste projeto?** Sim
- **Ferramentas utilizadas:** Google Gemini e ChatGPT
- **Finalidade:** Esclarecimento de dúvidas sobre comandos Git, estruturação do README e auxílio na organização de ficheiros no terminal
- **O que NÃO foi delegado à IA:** A definição do tema do projeto, o desenho do diagrama de casos de uso e a tomada de decisões de arquitetura

---

## 12. Contribuição e fluxo de trabalho

### Branches do projeto

- `main` — versão estável e pronta para entrega/avaliação
- `feat/cadastro-abrigos` — implementação do módulo de abrigos
- `feat/cadastro-animais` — implementação do catálogo e cadastro de animais
- `feat/pedidos-adocao` — implementação do fluxo de pedidos de adoção
- `fix/autenticacao` — correções em rotas e autenticação do sistema
- `docs/atualizacao-readme` — alterações na documentação do repositório

### Padrão de Commits

Mensagens curtas, diretas e no imperativo:

- `feat: adiciona modelo de dados para animais`
- `fix: corrige validacao do formulario de adocao`
- `docs: atualiza instrucoes de execucao no readme`

### Passo a passo para contribuição

1. Criar uma nova branch a partir da `main`.
2. Implementar as alterações e testar localmente.
3. Subir a branch para o GitHub.
4. Abrir um *Pull Request* para revisão e aprovação da equipe antes de integrar à `main`.

**Issues e quadro de tarefas:** [link do GitHub Projects, Trello ou similar]

---

## 13. Histórico de versões

| Versão | Data | Descrição |
| --- | --- | --- |
| `0.1.0` | 2026-10-07 | Conclusão da Fase 1: Especificação de casos de uso, planeamento do backlog e protótipos de ecrãs |
| `0.0.1` | 2026-10-01 | Estrutura inicial do repositório e organização de pastas |
---

## 14. Limitações e próximos passos

### Problemas conhecidos

- Integração completa com o banco de dados PostgreSQL ainda pendente para a Fase 2
- Telas e rotas da interface do usuário ainda não implementadas no front-end

### Roadmap

- [ ] Setup inicial do ambiente Django e conexão com PostgreSQL
- [ ] Criação e migração dos modelos (`Abrigo`, `Animal`, `PedidoAdocao`)
- [ ] Implementação das rotas REST (Django REST Framework)
- [ ] Integração com a *The Dog / Cat API* para catálogo de raças
---

## 15. Licença, referências e contato

**Licença:** Uso exclusivamente acadêmico.

Este material destina-se a fins educacionais no âmbito da disciplina.

### Documentação complementar

- Casos de uso: [`docs/casos-de-uso/`](docs/casos-de-uso/)
- Planejamento e backlog: [`docs/planejamento/backlog.md`](docs/planejamento/backlog.md)
- Protótipos e identidade visual: [`docs/prototipos/README.md`](docs/prototipos/README.md)

### Referências

- Documentação Oficial do Django: https://docs.djangoproject.com/
- Documentação Oficial do PostgreSQL: https://www.postgresql.org/docs/
- Documentação da The Dog API: https://thedogapi.com/

### Contato

Dúvidas sobre o projeto: [jotape152006@gmail.com] ou abra uma *issue* no repositório.
