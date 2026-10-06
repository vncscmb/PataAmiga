# Modelo de Dados - Pata Amiga

## 1. Introdução
Este documento descreve o modelo relacional da base de dados da plataforma **Pata Amiga**, especificando as tabelas, atributos, tipos de dados, chaves primárias (PK), chaves estrangeiras (FK) e cardinalidades necessárias para suportar os casos de uso do sistema[cite: 4].

---

## 2. Dicionário de Dados e Tabelas

### Tabela: `abrigo`
Armazena as informações das instituições de proteção animal ou protetores independentes registados no sistema.

| Atributo | Tipo de Dado | Chave / Restrição | Descrição |
| :--- | :--- | :--- | :--- |
| `id` | Inteiro (Auto-incremento) | Chave Primária (PK) | Identificador único do abrigo[cite: 4]. |
| `nome` | Varchar(150) | Not Null | Designação oficial da instituição ou responsável[cite: 4]. |
| `email` | Varchar(100) | Not Null, Unique | Endereço de correio eletrónico de contacto[cite: 4]. |
| `telefone` | Varchar(20) | Not Null | Número de contacto telefónico. |
| `senha` | Varchar(128) | Not Null | Hash encriptado da senha de acesso ao sistema[cite: 4]. |

### Tabela: `animal`
Armazena os registos dos animais disponíveis ou adotados, contemplando os dados inseridos manualmente e os recolhidos através da integração com a *The Dog/Cat API*[cite: 3, 4].

| Atributo | Tipo de Dado | Chave / Restrição | Descrição |
| :--- | :--- | :--- | :--- |
| `id` | Inteiro (Auto-incremento) | Chave Primária (PK) | Identificador único do animal[cite: 4]. |
| `nome` | Varchar(100) | Not Null | Nome do animal[cite: 4]. |
| `especie` | Varchar(50) | Not Null | Espécie do animal (ex: Cão, Gato)[cite: 4]. |
| `raca` | Varchar(100) | Not Null | Raça específica obtida via API ou a indicação "SRD"[cite: 4]. |
| `porte` | Varchar(30) | Not Null | Classificação do porte (Pequeno, Médio, Grande)[cite: 4]. |
| `temperamento` | Texto (Text) | Nullable | Características comportamentais obtidas da API ou inseridas manualmente[cite: 3, 4]. |
| `status_disponivel`| Booleano (Boolean)| Not Null (Default: True) | Indica se o animal continua disponível para adoção[cite: 4]. |
| `abrigo_id` | Inteiro | Chave Estrangeira (FK) | Identificador do abrigo responsável pelo animal[cite: 4]. |

### Tabela: `pedido_adocao`
Regista o interesse manifestado pelos adotantes em relação a um animal específico da plataforma[cite: 4].

| Atributo | Tipo de Dado | Chave / Restrição | Descrição |
| :--- | :--- | :--- | :--- |
| `id` | Inteiro (Auto-incremento) | Chave Primária (PK) | Identificador único do pedido de adoção[cite: 4]. |
| `nome_adotante` | Varchar(150) | Not Null | Nome completo da pessoa interessada[cite: 4]. |
| `contacto_adotante`| Varchar(100) | Not Null | Email ou telefone de contacto do adotante[cite: 4]. |
| `mensagem` | Texto (Text) | Nullable | Mensagem opcional ou justificação enviada ao abrigo[cite: 4]. |
| `data_pedido` | Data/Hora (DateTime)| Not Null (Auto) | Momento temporal em que o pedido foi submetido[cite: 4]. |
| `animal_id` | Inteiro | Chave Estrangeira (FK) | Identificador do animal alvo do pedido de adoção[cite: 4]. |

---

## 3. Relacionamentos e Cardinalidades

*   **Abrigo para Animal (1 para N):** 
    Uma instituição (Abrigo) pode registar e gerir múltiplos animais na plataforma, mas cada perfil de animal está associado a exatamente um único abrigo[cite: 4].
*   **Animal para Pedido de Adoção (1 para N):** 
    Um animal publicado pode receber vários pedidos de adoção submetidos por diferentes interessados ao longo do tempo, contudo, cada registo individual de pedido de adoção refere-se a apenas um animal específico[cite: 4].

---

## 4. Ferramentas e Observações de Implementação
*   **Ferramenta de Modelação:** O diagrama conceptual/relacional foi desenhado numa ferramenta externa (como *dbdiagram.io* ou *MySQL Workbench*)[cite: 4].
*   **Ficheiros Entregues:** O ficheiro-fonte editável e a respetiva exportação visual em formato PDF/PNG encontram-se arquivados nesta mesma pasta (`/docs/banco-de-dados/`), cumprindo os critérios de qualidade e rastreabilidade da disciplina[cite: 4, 5].