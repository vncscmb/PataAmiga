# Especificação dos Casos de Uso - PataAmiga

Documentação textual detalhada dos casos de uso do sistema **PataAmiga**, modelada em conformidade com o Diagrama UML de Casos de Uso.

---

## Atores do Sistema
* **Gestor do Abrigo:** Utilizador responsável por gerir a instituição, os animais alojados e os processos de adoção.
* **Cliente:** Utilizador interessado em procurar e adotar animais.
* **Veterinário:** Profissional de saúde animal responsável pelo acompanhamento médico e vacinação dos animais do abrigo.
* **TheDog/CatAPI:** Sistema/API externa integrada para obtenção de características técnicas e informações sobre raças de cães e gatos.

---

## Detalhamento dos Casos de Uso

### UC01 - Registar Abrigo
* **Ator Principal:** Gestor do abrigo
* **Objetivo:** Cadastrar uma nova instituição/abrigo de animais no sistema.
* **Pré-condições:** O gestor deve aceder à plataforma e não possuir um abrigo cadastrado sob o seu registo.
* **Pós-condições:** O abrigo fica registado e ativo no sistema para gestão de animais e adoções.

#### Fluxos de Eventos:
1. **Fluxo Principal:**
   1. O gestor acede à opção "Registar Abrigo".
   2. O sistema exibe o formulário de registo do abrigo (Nome, Endereço, Contacto, NIF/CNPJ e Capacidade).
   3. O gestor preenche os dados e submete.
   4. O sistema valida os campos obrigatórios e guarda as informações.
   5. O sistema exibe mensagem de confirmação do registo.

2. **Exceções:**
   * **4a. Dados inválidos ou incompletos:** O sistema alerta o utilizador sobre os campos incorretos e solicita a correção antes de guardar.

---

### UC02 - Registar Animal
* **Ator Principal:** Gestor do abrigo
* **Atores Secundários:** TheDog/CatAPI
* **Objetivo:** Inserir um novo animal no catálogo do abrigo para disponibilização para adoção.
* **Pré-condições:** O abrigo deve estar devidamente cadastrado no sistema.
* **Pós-condições:** O animal é adicionado ao sistema e associado ao abrigo do gestor.

#### Relações do Caso de Uso:
* **Include:** `Validar Formulário` (obrigatoriamente executado para garantir a consistência dos dados).
* **Extend:** `Atribuir Perfil SRD` (executado quando o animal não possui raça definida).
* **Extend:** `Obter Características da Raça` (executado para consultar dados via API externa).

#### Fluxos de Eventos:
1. **Fluxo Principal:**
   1. O gestor seleciona a opção "Registar Animal".
   2. O sistema exibe o formulário de cadastro do animal.
   3. O gestor preenche os dados do animal (Nome, Espécie, Idade, Raça, Fotos, Estado de Saúde).
   4. O sistema executa obrigatoriamente o caso de uso **Validar Formulário**.
   5. O sistema guarda o registo do animal e exibe confirmação.

2. **Fluxos Alternativos:**
   * **3a. Animal Sem Raça Definida (SRD / Vira-lata):**
     1. O gestor marca a opção "Sem Raça Definida / Vira-lata".
     2. O sistema executa o caso de uso **Atribuir Perfil SRD**, definindo as características visuais e comportamentais padrão para SRD.
     3. O fluxo retorna ao passo 4 do fluxo principal.
   * **3b. Consulta de Raça via API Externa:**
     1. O gestor seleciona uma raça de cão ou gato listada na integração.
     2. O sistema executa o caso de uso **Obter Características da Raça**, consumindo a *TheDog/CatAPI* para importar automaticamente o porte, expectativa de vida e temperamento da raça.
     3. O fluxo retorna ao passo 4 do fluxo principal.

3. **Exceções:**
   * **4a. Falha na validação do formulário:** O sistema destaca os erros e impede o envio até correção.

---

### UC03 - Validar Formulário (Include)
* **Ator Principal:** Sistema (Interno)
* **Objetivo:** Verificar a consistência, integridade e preenchimento correto dos campos obrigatórios do formulário de registo.
* **Pré-condições:** Invocado diretamente pelo caso de uso `Registar Animal` ou `Analisar Pedidos de Adoção`.
* **Pós-condições:** Confirmação de que os dados cumprem todas as regras de negócio do sistema.

#### Fluxos de Eventos:
1. **Fluxo Principal:**
   1. O sistema recebe os dados enviados do formulário.
   2. O sistema valida se os campos obrigatórios estão preenchidos.
   3. O sistema valida os formatos de ficheiros (imagens) e limites de texto.
   4. O sistema retorna status de validação com sucesso.

2. **Exceções:**
   * **2a. Campo obrigatório omitido ou inválido:** O sistema rejeita o formulário e devolve uma lista de erros.

---

### UC04 - Atribuir Perfil SRD (Extend)
* **Ator Principal:** Sistema (Interno)
* **Objetivo:** Preencher e classificar automaticamente o perfil de um animal sem raça definida.
* **Pré-condições:** Selecionado como opção durante o caso de uso `Registar Animal`.
* **Pós-condições:** O animal é marcado como SRD e recebe atributos genéricos ajustáveis.

#### Fluxos de Eventos:
1. **Fluxo Principal:**
   1. O sistema identifica a seleção de SRD.
   2. O sistema preenche a raça como "Sem Raça Definida (SRD)".
   3. O sistema habilita campos descritivos adicionais para porte e pelagem.

---

### UC05 - Obter Características da Raça (Extend)
* **Ator Principal:** TheDog/CatAPI
* **Objetivo:** Consumir dados de raças a partir de uma API REST externa para enriquecer a ficha do animal.
* **Pré-condições:** Seleção de uma raça existente durante o `Registar Animal` e conexão à internet ativa.
* **Pós-condições:** Dados oficiais da raça são incorporados à ficha do animal no PataAmiga.

#### Fluxos de Eventos:
1. **Fluxo Principal:**
   1. O sistema dispara uma requisição HTTP para a *TheDog/CatAPI* com o identificador da raça.
   2. A API retorna os dados em formato JSON (ex.: temperamento, exp. de vida, tamanho).
   3. O sistema mapeia e preenche automaticamente esses campos no formulário.

2. **Exceções:**
   * **1a. Indisponibilidade da API externa:** O sistema exibe um aviso e permite que o gestor preencha os dados da raça manualmente.

---

### UC06 - Analisar Pedidos de Adoção
* **Ator Principal:** Gestor do abrigo
* **Objetivo:** Avaliar e aprovar ou rejeitar candidaturas de adoção submetidas por clientes.
* **Pré-condições:** Existir pelo menos uma candidatura pendente para um animal do abrigo.
* **Pós-condições:** O estado do pedido de adoção é atualizado (Aprovado / Rejeitado).

#### Relações do Caso de Uso:
* **Include:** `Validar Formulário` (para validar os critérios da avaliação).

#### Fluxos de Eventos:
1. **Fluxo Principal:**
   1. O gestor acede à lista de pedidos de adoção pendentes.
   2. O gestor seleciona uma candidatura para analisar os detalhes do cliente e as suas respostas.
   3. O gestor toma a decisão (Aprovar ou Rejeitar) e insere uma justificativa/parecer.
   4. O sistema executa o caso de uso **Validar Formulário**.
   5. O sistema atualiza o estado do pedido e notifica o candidato.

---

### UC07 - Pesquisar Animais
* **Ator Principal:** Cliente
* **Objetivo:** Buscar e filtrar animais disponíveis para adoção no catálogo geral do PataAmiga.
* **Pré-condições:** Nenhuma (pode ser executado publicamente ou por cliente autenticado).
* **Pós-condições:** Exibição da lista de animais correspondentes aos filtros aplicados.

#### Fluxos de Eventos:
1. **Fluxo Principal:**
   1. O cliente acede à página de pesquisa de animais.
   2. O cliente aplica filtros (ex.: espécie, idade, porte, localização do abrigo, raça).
   3. O sistema processa os filtros e apresenta a lista de animais encontrados.
   4. O cliente seleciona um animal para ver os seus detalhes completos.

2. **Fluxo Alternativo:**
   * **3a. Nenhum animal atende aos critérios:** O sistema exibe mensagem informando que nenhum resultado foi encontrado e sugere a limpeza dos filtros.

---

### UC08 - Submeter Candidatura a Adoção
* **Ator Principal:** Cliente
* **Objetivo:** Enviar um formulário de interesse e prontidão para adotar um animal específico.
* **Pré-condições:** O cliente deve estar autenticado no sistema e ter selecionado um animal disponível.
* **Pós-condições:** O pedido de adoção é registado no sistema com status "Pendente" para análise do abrigo.

#### Fluxos de Eventos:
1. **Fluxo Principal:**
   1. O cliente visualiza o perfil de um animal e clica em "Quero Adotar".
   2. O sistema apresenta o formulário de candidatura (perguntas sobre habitação, rotina e experiência prévia).
   3. O cliente preenche o formulário e confirma a submissão.
   4. O sistema regista o pedido e gera uma notificação para o gestor do abrigo responsável.

2. **Exceções:**
   * **3a. O cliente já possui uma candidatura em andamento para o mesmo animal:** O sistema informa que o pedido já foi submetido anteriormente.

---

### UC09 - Registar Ficha Médica e Vacinas
* **Ator Principal:** Veterinário
* **Objetivo:** Registar o histórico veterinário, vacinações aplicadas, desparasitações e procedimentos efetuados num animal.
* **Pré-condições:** O veterinário deve estar autenticado e associado ao animal ou abrigo.
* **Pós-condições:** A ficha de saúde do animal é atualizada com o histórico médico.

#### Fluxos de Eventos:
1. **Fluxo Principal:**
   1. O veterinário pesquisa e seleciona o animal.
   2. Seleciona a opção "Registar Ficha Médica / Vacinas".
   3. Preenche as informações do procedimento (data, nome da vacina/medicamento, lote, lote de desparasitante, observações).
   4. O sistema valida e regista o histórico na base de dados do animal.

---

### UC10 - Emitir Parecer de Saúde
* **Ator Principal:** Veterinário
* **Objetivo:** Emitir um laudo ou parecer atestando a aptidão de saúde do animal para adoção final.
* **Pré-condições:** O animal deve ter a ficha médica atualizada no sistema.
* **Pós-condições:** O parecer é anexado ao perfil do animal, ficando visível para o gestor do abrigo durante a análise de adoção.

#### Fluxos de Eventos:
1. **Fluxo Principal:**
   1. O veterinário acede à ficha do animal.
   2. Seleciona a opção "Emitir Parecer de Saúde".
   3. Preenche o laudo (Status: Apto / Em Tratamento / Inapto Temporariamente) e adiciona os detalhes clínicos.
   4. O sistema guarda o parecer e atualiza o status sanitário do animal no sistema.
