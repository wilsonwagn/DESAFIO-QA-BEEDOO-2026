# Relatório de Bugs — Módulo de Cursos

**Aplicação:** https://creative-sherbet-a51eac.netlify.app/  
**Data da execução:** 07/03/2026  
**Testador:** Wilson

---

## BUG-001: Formulário permite cadastro com todos os campos vazios

| Campo | Detalhe |
|-------|---------|
| **Severidade** | 🔴 **Crítica** |
| **Módulo** | Cadastro de Curso |
| **Ambiente** | Produção (Netlify) |

### Descrição
O formulário de cadastro de curso não possui nenhuma validação de campos obrigatórios, permitindo que o usuário submeta o formulário completamente vazio.

### Passos para reproduzir
1. Acessar a aplicação em https://creative-sherbet-a51eac.netlify.app/
2. Clicar no botão **"CADASTRAR CURSO"** no header
3. Sem preencher nenhum campo, clicar no botão **"CADASTRAR CURSO"** no final do formulário

### Resultado atual
- O sistema aceita o envio do formulário vazio
- Exibe a mensagem de sucesso "Curso cadastrado com sucesso!"
- Redireciona para a listagem de cursos
- Um card "fantasma" (vazio, sem informações) é criado na listagem

### Resultado esperado
- O sistema deveria exibir mensagens de validação em todos os campos obrigatórios
- O formulário não deveria ser submetido enquanto os campos obrigatórios não estivessem preenchidos
- Nenhum registro deveria ser criado no banco de dados

### Impacto
- Poluição da base de dados com registros vazios/inválidos
- Cards vazios na listagem prejudicam a experiência do usuário
- Pode causar erros em outras funcionalidades que dependam dos dados do curso

### Evidência
📎 `evidencias/03_cadastro_campos_vazios.webp`

---

## BUG-002: Botão "Excluir Curso" não funciona (Erro 405)

| Campo | Detalhe |
|-------|---------|
| **Severidade** | 🔴 **Crítica** |
| **Módulo** | Listagem de Cursos |
| **Ambiente** | Produção (Netlify) |

### Descrição
O botão "Excluir Curso" presente em cada card da listagem não realiza a exclusão. Ao clicar, a API retorna erro HTTP 405 (Method Not Allowed).

### Passos para reproduzir
1. Acessar a aplicação em https://creative-sherbet-a51eac.netlify.app/
2. Na listagem de cursos, verificar que existe pelo menos um curso cadastrado
3. Clicar no botão **"Excluir Curso"** em qualquer card
4. Observar o console do navegador (F12 → Console)

### Resultado atual
- Nada acontece visualmente na interface
- No console do navegador, aparece o erro: `DELETE https://creative-sherbet-a51eac.netlify.app/test-api/courses/{id} 405 (Method Not Allowed)`
- O curso permanece na listagem

### Resultado esperado
- O curso deveria ser removido da listagem
- Uma mensagem de confirmação deveria ser exibida antes da exclusão (ou pelo menos após a mesma)
- Opcionalmente, uma mensagem de sucesso deveria confirmar a exclusão

### Impacto
- O usuário não consegue remover cursos cadastrados incorretamente
- Cursos-fantasma (criados sem dados — ver BUG-001) acumulam-se na listagem sem possibilidade de remoção
- A funcionalidade de exclusão está completamente inoperante

### Evidência
📎 `evidencias/04_exclusao_curso.webp`

---

## BUG-003: Typo no título do header da aplicação

| Campo | Detalhe |
|-------|---------|
| **Severidade** | 🟡 **Baixa** |
| **Módulo** | Header / Interface |
| **Ambiente** | Produção (Netlify) |

### Descrição
O título da aplicação no header está escrito como **"Beedoo QA Chalenge"** ao invés de **"Beedoo QA Challenge"** (falta a letra "l" em "Challenge").

### Passos para reproduzir
1. Acessar a aplicação em https://creative-sherbet-a51eac.netlify.app/
2. Observar o título no header da página

### Resultado atual
- O título exibe: **"Beedoo QA Chalenge"**

### Resultado esperado
- O título deveria exibir: **"Beedoo QA Challenge"**

### Impacto
- Erro de ortografia visível na interface principal da aplicação
- Prejudica a imagem profissional do produto
- Pode confundir usuários que procurem pelo nome correto

### Evidência
📎 `evidencias/07_listagem_cursos.webp`

---

## BUG-004: Campo "Número de vagas" aceita valores negativos

| Campo | Detalhe |
|-------|---------|
| **Severidade** | 🟠 **Alta** |
| **Módulo** | Cadastro de Curso |
| **Ambiente** | Produção (Netlify) |

### Descrição
O campo "Número de vagas" aceita valores negativos sem nenhuma validação, permitindo cadastrar cursos com número de vagas como -1, -100, etc.

### Passos para reproduzir
1. Acessar a aplicação em https://creative-sherbet-a51eac.netlify.app/
2. Clicar em **"CADASTRAR CURSO"**
3. Preencher os demais campos com dados válidos
4. No campo **"Número de vagas"**, digitar **"-5"**
5. Clicar no botão **"CADASTRAR CURSO"**

### Resultado atual
- O sistema aceita o valor negativo
- O curso é cadastrado com "-5" vagas
- Na listagem, o card exibe o número negativo de vagas

### Resultado esperado
- O sistema deveria validar que o número de vagas é um inteiro positivo (≥ 1)
- Uma mensagem de erro deveria ser exibida caso o valor seja negativo ou zero

### Impacto
- Dados inconsistentes no sistema
- Número de vagas negativo não faz sentido do ponto de vista de negócio
- Pode causar problemas em funcionalidades futuras que utilizem esse dado (ex: controle de inscrições)

### Evidência
📎 `evidencias/06_vagas_negativas.webp`

---

## BUG-005: Campo "URL da imagem de capa" aceita textos que não são URLs

| Campo | Detalhe |
|-------|---------|
| **Severidade** | 🟠 **Média** |
| **Módulo** | Cadastro de Curso |
| **Ambiente** | Produção (Netlify) |

### Descrição
O campo "URL da imagem de capa" aceita qualquer texto, incluindo strings que não são URLs válidas, resultando em cards sem imagem na listagem.

### Passos para reproduzir
1. Acessar a aplicação em https://creative-sherbet-a51eac.netlify.app/
2. Clicar em **"CADASTRAR CURSO"**
3. No campo **"URL da imagem de capa"**, digitar **"texto-invalido"**
4. Preencher os demais campos com dados válidos
5. Clicar no botão **"CADASTRAR CURSO"**

### Resultado atual
- O sistema aceita o texto inválido como URL
- O curso é cadastrado normalmente
- Na listagem, o card não exibe imagem (área de imagem fica vazia/quebrada)

### Resultado esperado
- O sistema deveria validar que o valor informado é uma URL válida (iniciando com http:// ou https://)
- Uma mensagem de erro deveria ser exibida caso o formato seja inválido

### Impacto
- Cards com imagens quebradas prejudicam a experiência visual
- Dados inconsistentes no banco de dados

### Evidência
📎 `evidencias/01_cadastro_valido_presencial.webp`

---

## BUG-006: Data de fim pode ser anterior à data de início

| Campo | Detalhe |
|-------|---------|
| **Severidade** | 🟠 **Alta** |
| **Módulo** | Cadastro de Curso |
| **Ambiente** | Produção (Netlify) |

### Descrição
O sistema não valida a coerência entre as datas de início e fim do curso, permitindo que a data de fim seja anterior à data de início.

### Passos para reproduzir
1. Acessar a aplicação em https://creative-sherbet-a51eac.netlify.app/
2. Clicar em **"CADASTRAR CURSO"**
3. Preencher os demais campos com dados válidos
4. Selecionar **"Data de início"** como **"2026/06/30"**
5. Selecionar **"Data de fim"** como **"2026/04/01"**
6. Clicar no botão **"CADASTRAR CURSO"**

### Resultado atual
- O sistema aceita as datas inconsistentes
- O curso é cadastrado com data de fim anterior à data de início
- Na listagem, as datas aparecem invertidas

### Resultado esperado
- O sistema deveria validar que a data de fim é igual ou posterior à data de início
- Uma mensagem de erro deveria ser exibida caso as datas sejam inconsistentes

### Impacto
- Dados logicamente inconsistentes no sistema
- Cursos com período impossível podem confundir usuários e causar problemas em funcionalidades de agenda/calendário

### Evidência
📎 `evidencias/01_cadastro_valido_presencial.webp`

---

## BUG-007: Warning de formato de data no console do navegador

| Campo | Detalhe |
|-------|---------|
| **Severidade** | 🟡 **Baixa** |
| **Módulo** | Cadastro de Curso |
| **Ambiente** | Produção (Netlify) |

### Descrição
Ao acessar a página de cadastro, o console do navegador exibe warnings sobre formato de data inválido.

### Passos para reproduzir
1. Acessar a aplicação em https://creative-sherbet-a51eac.netlify.app/
2. Clicar em **"CADASTRAR CURSO"**
3. Abrir o console do navegador (F12 → Console)

### Resultado atual
- O console exibe: `The specified value "YYYY/MM/DD" does not conform to the required format, "yyyy-MM-dd"`

### Resultado esperado
- O componente de data deveria ser configurado corretamente, sem warnings no console

### Impacto
- Apesar de não afetar diretamente a funcionalidade visível ao usuário, indica um problema na implementação do componente de data
- Pode causar comportamentos inesperados em diferentes navegadores

---

## BUG-008: Mensagem de sucesso exibida mesmo com dados inválidos

| Campo | Detalhe |
|-------|---------|
| **Severidade** | 🟠 **Alta** |
| **Módulo** | Cadastro de Curso |
| **Ambiente** | Produção (Netlify) |

### Descrição
A mensagem "Curso cadastrado com sucesso!" é exibida mesmo quando o formulário é enviado com dados vazios ou inválidos, dando ao usuário uma falsa sensação de que tudo está correto.

### Passos para reproduzir
1. Acessar a aplicação em https://creative-sherbet-a51eac.netlify.app/
2. Clicar em **"CADASTRAR CURSO"**
3. Sem preencher nenhum campo, clicar no botão **"CADASTRAR CURSO"**

### Resultado atual
- A mensagem de sucesso "Curso cadastrado com sucesso!" é exibida
- O sistema redireciona para a listagem

### Resultado esperado
- Mensagem de sucesso só deveria ser exibida após validação bem-sucedida de todos os campos obrigatórios
- Em caso de erro, mensagens de validação específicas deveriam ser mostradas

### Impacto
- Confunde o usuário que pode pensar que o cadastro foi feito corretamente
- Não fornece feedback adequado sobre problemas nos dados enviados

### Evidência
📎 `evidencias/03_cadastro_campos_vazios.webp`

---

---

## BUG-009: Mensagem de sucesso exibida ao falhar a exclusão de curso

| Campo | Detalhe |
|-------|---------|
| **Severidade** | 🟠 **Alta** |
| **Módulo** | Listagem de Cursos |
| **Ambiente** | Produção (Netlify) |

### Descrição
Ao clicar no botão "Excluir Curso", o sistema exibe a mensagem de sucesso "Curso excluído com sucesso!" mesmo quando a operação falha no backend (erro 405). O curso permanece na listagem após a suposta exclusão.

### Passos para reproduzir
1. Acessar a aplicação em https://creative-sherbet-a51eac.netlify.app/
2. Na listagem, clicar no botão **"Excluir Curso"** de qualquer card
3. Observar a notificação exibida no topo da tela

### Resultado atual
- A mensagem verde "Curso excluído com sucesso!" é exibida
- O curso NÃO é removido da listagem
- No console, existe erro 405 (Method Not Allowed)

### Resultado esperado
- O sistema deveria capturar o erro da API e exibir uma mensagem de erro informando que a exclusão falhou
- A mensagem de sucesso só deveria ser exibida após confirmação do backend

### Impacto
- O usuário é induzido a acreditar que a exclusão foi realizada com sucesso
- O curso permanece na listagem, gerando confusão
- Falha no tratamento de erros da API

### Evidência
📎 `evidencias/04_exclusao_curso.webp`

---

## Resumo dos Bugs

| ID | Título | Severidade | Módulo |
|----|--------|:----------:|--------|
| BUG-001 | Formulário permite cadastro com campos vazios | 🔴 Crítica | Cadastro |
| BUG-002 | Botão "Excluir Curso" não funciona (Erro 405) | 🔴 Crítica | Listagem |
| BUG-003 | Typo no título do header ("Chalenge") | 🟡 Baixa | Interface |
| BUG-004 | Número de vagas aceita valores negativos | 🟠 Alta | Cadastro |
| BUG-005 | URL da imagem aceita textos inválidos | 🟠 Média | Cadastro |
| BUG-006 | Data de fim pode ser anterior à data de início | 🟠 Alta | Cadastro |
| BUG-007 | Warning de formato de data no console | 🟡 Baixa | Cadastro |
| BUG-008 | Mensagem de sucesso com dados inválidos | 🟠 Alta | Cadastro |
| BUG-009 | Mensagem de sucesso ao falhar exclusão | 🟠 Alta | Listagem |
