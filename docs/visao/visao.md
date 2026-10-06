# Documento de Visão - Pata Amiga

## 1. Contexto, Problema e Justificativa
Muitos abrigos e associações de proteção animal enfrentam dificuldades em divulgar os animais disponíveis de forma organizada, dependendo de redes sociais que dispersam a informação. A plataforma justifica-se ao centralizar estes dados, facilitando a pesquisa por parte de potenciais adotantes e agilizando a gestão para as instituições.

## 2. Objetivos
Criar uma plataforma web centralizada ("Pata Amiga") que ligue abrigos a famílias adotantes, simplificando a pesquisa, a triagem e a gestão dos perfis dos animais.

## 3. Público-Alvo e Stakeholders
* **Gestores de Abrigos:** Entidades que inserem, atualizam e gerem os registos dos animais no sistema.
* **Adotantes:** Público em geral que pesquisa os perfis de animais e submete pedidos de adoção.

## 4. Escopo e Funcionalidades
* Manutenção (CRUD) de perfis de animais e de contas de abrigos.
* Pesquisa de animais filtrada por critérios como espécie, porte e localização.
* Geração de relatórios de dados consolidados e exportáveis.
* Consumo da *The Dog/Cat API* para o preenchimento automático de características comportamentais das raças.
* Disponibilização de uma API REST própria para a consulta pública dos animais.

## 5. Itens Fora do Escopo
* Processamento de pagamentos de taxas de adoção ou donativos na plataforma.
* Sistema de mensagens ou chat em tempo real entre adotantes e abrigos.
* Logística e agendamento automático de transporte dos animais.

## 6. Restrições
* O backend tem de ser desenvolvido exclusivamente com Python e o framework Django.
* A aplicação final deve estar publicada numa URL pública com ligação HTTPS.
* A base de dados utilizada deve ser relacional e compatível com o ambiente de hospedagem.

## 7. Premissas
* Os gestores de abrigos possuem dispositivos com acesso à internet para operar a plataforma.
* O serviço da *The Dog/Cat API* manter-se-á ativo, documentado e com a estrutura de resposta JSON inalterada.

## 8. Riscos Iniciais
* Indisponibilidade temporária ou *timeout* da API externa no momento do registo de um animal.
* Dificuldades técnicas ou atrasos na configuração do alojamento da aplicação no ambiente de produção.
* Identificação de vulnerabilidades complexas durante as análises de segurança (SAST e DAST) exigidas para a entrega.

## 9. Critérios de Sucesso
* O sistema permitir as funções completas de cadastro, busca e relatório.
* A API externa estar a ser consumida ativamente num fluxo funcional (registo de raças), com tratamento eficaz para animais Sem Raça Definida (SRD).
* A aplicação estar hospedada com configurações seguras e aprovada pelos relatórios de análise de código e testes de vulnerabilidade.