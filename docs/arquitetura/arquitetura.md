# Arquitetura da Aplicação - Pata Amiga

## 1. Introdução
Este documento descreve a arquitetura de software da plataforma **Pata Amiga**, especificando as camadas de organização do código, a divisão de responsabilidades, as tecnologias adotadas e o fluxo de dados entre os componentes do sistema.

---

## 2. Padrão Arquitetural (Django MVT)
A aplicação segue rigorosamente o padrão arquitetural **Model-View-Template (MVT)** nativo do framework Django, complementado com uma camada de API REST construída através do Django REST Framework (DRF).

[Cliente / Browser] ⇄ [URLs / Roteamento] ⇄ [Views (Lógica de Negócio)] ⇄ [Models (ORM)] ⇄ [Base de Dados Relacional]
                                                    ↕
                                         [The Dog/Cat API Externa]

---

## 3. Descrição das Camadas e Componentes

### 3.1. Camada de Apresentação (Templates & Frontend)
*   **Responsabilidade:** Responsável pela interface do utilizador, renderização das páginas HTML e recolha de interações através de formulários.
*   **Tecnologias:** HTML5, CSS3, JavaScript e frameworks de estilização responsiva (Bootstrap/Tailwind), garantindo compatibilidade com computadores e dispositivos móveis.

### 3.2. Camada de Roteamento (URLs)
*   **Responsabilidade:** Direciona os pedidos HTTP recebidos do cliente para a função ou classe de controlo correspondente (*View*), organizando as rotas da aplicação de modo modular.

### 3.3. Camada de Aplicação e Controlo (Views)
*   **Responsabilidade:** Processa os pedidos recebidos, aplica as regras de negócio, interage com a base de dados através dos modelos e orquestra o consumo da API externa quando necessário. É nesta camada que se efetua a validação dos dados enviados pelos utilizadores.

### 3.4. Camada de Domínio e Persistência (Models & ORM)
*   **Responsabilidade:** Define a estrutura dos dados da aplicação em classes Python, mapeando-os diretamente para as tabelas da base de dados relacional através do ORM (Object-Relational Mapping) do Django. Garante a integridade das restrições e cardinalidades.

---

## 4. Fluxo de Dados Funcional (Exemplo: Registo de Animal com API Externa)
1. O utilizador (Gestor do Abrigo) preenche o formulário de novo animal na interface de apresentação.
2. A camada de *Views* recebe os dados submetidos e valida os campos essenciais no servidor.
3. Se o animal for de raça pura, a aplicação executa um pedido HTTP seguro para a **The Dog/Cat API** para recolher as características comportamentais associadas.
4. Caso seja selecionada a opção "Sem Raça Definida (SRD)", o sistema ignora o pedido externo, otimizando o desempenho e poupando recursos.
5. Os dados consolidados são gravados na base de dados relacional através do ORM do Django.
6. O sistema retorna uma resposta de sucesso e atualiza a interface visível para o utilizador.

---

## 5. Justificativas Tecnológicas
*   **Python e Django:** Escolhidos pela robustez, segurança nativa contra vulnerabilidades comuns (como injeções SQL e CSRF) e rapidez na implementação de estruturas CRUD completas.
*   **Django REST Framework (DRF):** Utilizado para implementar a API REST própria devido à sua modularidade, suporte a serialização em JSON e facilidade na documentação de endpoints.