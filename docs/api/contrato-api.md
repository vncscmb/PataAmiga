# Contrato da API e Plano de Integração Externa - Pata Amiga

## 1. Introdução
Este documento define o contrato inicial da API REST própria da plataforma **Pata Amiga** (exposta para consulta por terceiros) e detalha o plano técnico de consumo da API externa (*The Dog/Cat API*), contemplando os *endpoints*, métodos HTTP, códigos de estado, exemplos de respostas JSON e estratégias de tratamento de falhas, em conformidade com os requisitos da disciplina.

---

## 2. API REST Própria (`/api/v1/`)
A aplicação disponibiliza *endpoints* estruturados em JSON para que sistemas externos possam consultar os animais disponíveis e submeter pedidos de adoção.

### 2.1. Listar Animais Disponíveis
Permite consultar a lista de animais registados na plataforma, suportando filtros opcionais por espécie e porte.

*   **URL-base e Endpoint:** `GET /api/v1/animais/`
*   **Parâmetros de Query (Opcionais):** 
    *   `especie` (ex: `cao`, `gato`)
    *   `porte` (ex: `pequeno`, `medio`, `grande`)
    *   `page` (para paginação de resultados)
*   **Códigos de Estado HTTP:** 
    *   `200 OK`: Sucesso na obtenção da listagem.
    *   `500 Internal Server Error`: Erro interno no servidor.
*   **Exemplo de Resposta (JSON):**

    {
      "count": 15,
      "next": null,
      "previous": null,
      "results": [
        {
          "id": 1,
          "nome": "Max",
          "especie": "Cão",
          "raca": "Labrador Retriever",
          "porte": "Grande",
          "temperamento": "Brincalhão, dócil, energético",
          "status_disponivel": true,
          "abrigo_id": 3
        }
      ]
    }

### 2.2. Submeter Pedido de Adoção
Permite a submissão de um interesse de adoção por parte de um utilizador externo direcionado a um animal específico.

*   **Endpoint:** `POST /api/v1/pedidos-adocao/`
*   **Formato do Corpo (JSON):**

    {
      "animal_id": 1,
      "nome_adotante": "Ana Ferreira",
      "contacto_adotante": "ana.ferreira@email.com",
      "mensagem": "Gostaria de agendar uma visita para conhecer o Max."
    }

*   **Códigos de Estado HTTP:** 
    *   `201 Created`: Pedido registado com sucesso.
    *   `400 Bad Request`: Erro de validação (campos em falta ou formato inválido).
*   **Exemplo de Resposta de Sucesso (JSON):**

    {
      "id": 12,
      "mensagem_sucesso": "Pedido submetido com sucesso! O abrigo entrará em contacto.",
      "data_pedido": "2026-10-06T18:00:00Z"
    }

---

## 3. Plano de Integração Externa (The Dog/Cat API)
A aplicação integra-se de forma ativa com a **The Dog/Cat API** para enriquecer automaticamente os perfis dos animais registados pelos abrigos.

*   **Finalidade:** Obter dinamicamente características comportamentais, níveis de energia e temperamento com base na raça escolhida pelo abrigo durante o cadastro do animal.
*   **Endpoints Consumidos:** Consultas parametrizadas por raça na API pública de cães e gatos.
*   **Autenticação e Segurança:** Utilização de chave de acesso (*API Key*) injetada de forma segura através de variáveis de ambiente no servidor, garantindo que nenhum segredo é exposto no repositório GitHub.
*   **Tratamento de Indisponibilidade e Exceções:**
    *   *Timeout / Falha de Ligação:* Caso a API externa demore demasiado tempo a responder ou esteja offline, o sistema apanha a exceção, grava o registo do animal com os dados manuais preenchidos pelo abrigo e emite um aviso informativo.
    *   *Regra para Animais "Sem Raça Definida" (SRD):* Se o abrigo selecionar a opção SRD/Vira-lata, o sistema evita o pedido HTTP externo para poupar recursos, atribuindo automaticamente a etiqueta comportamental personalizada.