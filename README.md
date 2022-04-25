# Perfil Profissional

Projeto Perfil Profíssional, implementado no módulo 2 do curso fábrica de programador em High Tech Cursos.

Este projeto implemente uma **API** em **NodeJS**, utilizando *Express* como gerenciador de **HTTP**, banco de dados não relacional **MongoDB** e o framework ODM **Mongoose** para intermediar a comunicação entre a aplicação e o banco de dados.

O projeto trata-se de uma aplicação de gerenciamento de perfis profissionais e conexões entre eles. Portanto é possível cadastrar perfis, conectar perfis e a comunicação entre perfis por meio de notificações.

Este documento tem por objetivo detalhar os elementos presentes no projeto do Perfil Profissional, incluindo dependências, scripts de execução, definição de entidades e endpoints. 


# Entidades

- Perfil
- Notificação

## Perfil

Atributo | Tipo
------- | -------
nome | String*
dataNascimento | Date*
disponibilidadeMudança | Boolean*
disponibilidadeHorario | Enum [ "Meio Periodo", "Integral" ]*
skills | Array< String >*
educacao | Array< Educacao >*
certificacoes | Array< Cerficacao >
experiencias | Array< Experiencia >
usuario | Usuario*
conexoes | Array< Perfil >

 ## Notificacao

 Atributo | Tipo
 -------- | --------
 tipo | Enum ["Contato", "Solicitação de Amizade"]*
 titulo | String*
 descricao | String
 lida | Boolean*
 remetente | Perfil*
 destinatario | Perfil*

 > Entidades marcadas com asterisco são entidades obrigatórias.

 ## Entidades Internas

 ### Educacao

 Atributo | Tipo
 -------- | --------
 instituicao | String
 ingresso | Date
 conclusao | Date
 nivelEscolaridade | Enum [ "Ensino Fundamental", "Ensino Médio", "Ensino Superior", "Pós-Graduação", "Mestrado", "Doutorado" ]
 completo | Boolean

 ### Certificação

Atributo | Tipo
 -------- | --------
 instituicao | String
 titulo | String
 cargaHoraria | Number
 
 ### Experiencias

 Atributo | Tipo
 -------- | --------
 instituicao | String
 ingresso | Date
 conclusao | Date

 ### Usuario

  Atributo | Tipo
 -------- | --------
 email | String
 senha | String

 # Endpoints

 ## Perfil

 Recurso | Método | Autenticado? | Objetivo | Retorno
 ------- | ------ | ------------ | ------- | -------
 /perfil | GET | Não | Últimos 5 perfis cadastrados | Lista de Perfis JSON
 /perfil/:id | GET | Não | Busca um perfil por ID | Perfil JSON
 /perfil | POST | Não | Cadastrar um perfil | Perfil JSON
 /perfil | PUT | Sim | Editar um perfil | Perfil JSON
 /perfil/conexao | POST | Sim | Conecta dois perfis (Conexão/Amizade) | Mensagem JSON

 ## Login

 Recurso | Método | Autenticado? | Objetivo | Retorno
 ------- | ------ | ------------ | ------- | -------
 /login | POST | Não | Efetuar autenticação do usuario | Token, Email e Perfil

 ## Notificação 

 Recurso | Método | Autenticado? | Objetivo | Retorno
 ------- | ------ | ------------ | ------- | -------
 /notificacao/:id | GET | Sim | Buscar uma notificação por ID | Notificação em JSON
 /notificacao/perfil/:id | GET | Sim | Buscar todas as notificações do perfil por ID | Lista de notificações JSON
/notificacao | POST | Sim | Cadastrar uma notificação | Notificação em JSON
/notificacao/lida/:id | PUT | Sim | Muda o <status> da notificação para "lida" | Notificação em JSON
