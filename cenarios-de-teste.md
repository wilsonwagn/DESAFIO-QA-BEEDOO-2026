# Cenários e Casos de Teste — Módulo de Cursos

## CT-001: Cadastro de curso presencial com dados válidos

```gherkin
Funcionalidade: Cadastro de curso
  Cenário: Cadastrar curso presencial com todos os campos preenchidos
    Dado que o usuário está na página de cadastro de curso "/new-course"
    Quando preencher o campo "Nome do curso" com "Curso de Java Avançado"
    E preencher o campo "Descrição do curso" com "Curso completo de Java para desenvolvedores"
    E preencher o campo "Instrutor" com "Prof. João Silva"
    E preencher o campo "URL da imagem de capa" com "https://picsum.photos/400/200"
    E selecionar a "Data de início" como "2026-04-01"
    E selecionar a "Data de fim" como "2026-06-30"
    E preencher o campo "Número de vagas" com "30"
    E selecionar "Tipo de curso" como "Presencial"
    E preencher o campo "Endereço" com "Rua das Flores, 123 - São Paulo/SP"
    E clicar no botão "CADASTRAR CURSO"
    Então o sistema deve exibir a mensagem "Curso cadastrado com sucesso!"
    E o curso deve aparecer na listagem de cursos
    E o card deve exibir as informações cadastradas corretamente
```

---

## CT-002: Cadastro de curso online com dados válidos

```gherkin
  Cenário: Cadastrar curso online com todos os campos preenchidos
    Dado que o usuário está na página de cadastro de curso "/new-course"
    Quando preencher o campo "Nome do curso" com "Curso de Python para Iniciantes"
    E preencher o campo "Descrição do curso" com "Introdução à programação com Python"
    E preencher o campo "Instrutor" com "Profa. Maria Souza"
    E preencher o campo "URL da imagem de capa" com "https://picsum.photos/400/201"
    E selecionar a "Data de início" como "2026-05-01"
    E selecionar a "Data de fim" como "2026-07-31"
    E preencher o campo "Número de vagas" com "100"
    E selecionar "Tipo de curso" como "Online"
    E preencher o campo "Link de inscrição" com "https://exemplo.com/inscricao"
    E clicar no botão "CADASTRAR CURSO"
    Então o sistema deve exibir a mensagem "Curso cadastrado com sucesso!"
    E o curso deve aparecer na listagem de cursos
```

---

## CT-003: Cadastro com todos os campos vazios

```gherkin
  Cenário: Tentar cadastrar curso sem preencher nenhum campo
    Dado que o usuário está na página de cadastro de curso "/new-course"
    Quando não preencher nenhum campo do formulário
    E clicar no botão "CADASTRAR CURSO"
    Então o sistema deve exibir mensagens de validação nos campos obrigatórios
    E o curso NÃO deve ser cadastrado
```

---

## CT-004: Cadastro sem nome do curso

```gherkin
  Cenário: Tentar cadastrar curso sem o nome
    Dado que o usuário está na página de cadastro de curso "/new-course"
    Quando preencher todos os campos obrigatórios EXCETO "Nome do curso"
    E clicar no botão "CADASTRAR CURSO"
    Então o sistema deve exibir mensagem de erro no campo "Nome do curso"
    E o curso NÃO deve ser cadastrado
```

---

## CT-005: Cadastro sem descrição do curso

```gherkin
  Cenário: Tentar cadastrar curso sem a descrição
    Dado que o usuário está na página de cadastro de curso "/new-course"
    Quando preencher todos os campos obrigatórios EXCETO "Descrição do curso"
    E clicar no botão "CADASTRAR CURSO"
    Então o sistema deve exibir mensagem de erro no campo "Descrição do curso"
    E o curso NÃO deve ser cadastrado
```

---

## CT-006: Cadastro sem instrutor

```gherkin
  Cenário: Tentar cadastrar curso sem o instrutor
    Dado que o usuário está na página de cadastro de curso "/new-course"
    Quando preencher todos os campos obrigatórios EXCETO "Instrutor"
    E clicar no botão "CADASTRAR CURSO"
    Então o sistema deve exibir mensagem de erro no campo "Instrutor"
    E o curso NÃO deve ser cadastrado
```

---

## CT-007: Cadastro com data de fim anterior à data de início

```gherkin
  Cenário: Cadastrar curso com data de fim anterior à data de início
    Dado que o usuário está na página de cadastro de curso "/new-course"
    Quando preencher todos os campos com dados válidos
    E selecionar a "Data de início" como "2026-06-30"
    E selecionar a "Data de fim" como "2026-04-01"
    E clicar no botão "CADASTRAR CURSO"
    Então o sistema deve exibir mensagem de erro informando que a data de fim deve ser posterior à data de início
    E o curso NÃO deve ser cadastrado
```

---

## CT-008: Cadastro com número de vagas negativo

```gherkin
  Cenário: Cadastrar curso com número de vagas negativo
    Dado que o usuário está na página de cadastro de curso "/new-course"
    Quando preencher todos os campos com dados válidos
    E preencher o campo "Número de vagas" com "-5"
    E clicar no botão "CADASTRAR CURSO"
    Então o sistema deve exibir mensagem de erro no campo "Número de vagas"
    E o curso NÃO deve ser cadastrado
```

---

## CT-009: Cadastro com número de vagas igual a zero

```gherkin
  Cenário: Cadastrar curso com zero vagas
    Dado que o usuário está na página de cadastro de curso "/new-course"
    Quando preencher todos os campos com dados válidos
    E preencher o campo "Número de vagas" com "0"
    E clicar no botão "CADASTRAR CURSO"
    Então o sistema deve exibir mensagem de erro no campo "Número de vagas"
    E o curso NÃO deve ser cadastrado
```

---

## CT-010: Cadastro com URL de imagem inválida

```gherkin
  Cenário: Cadastrar curso com URL de imagem inválida
    Dado que o usuário está na página de cadastro de curso "/new-course"
    Quando preencher todos os campos com dados válidos
    E preencher o campo "URL da imagem de capa" com "texto-invalido"
    E clicar no botão "CADASTRAR CURSO"
    Então o sistema deve exibir mensagem de erro no campo "URL da imagem de capa"
    E o curso NÃO deve ser cadastrado
```

---

## CT-011: Campo condicional — Tipo Presencial exibe campo Endereço

```gherkin
  Cenário: Verificar que campo "Endereço" aparece ao selecionar tipo "Presencial"
    Dado que o usuário está na página de cadastro de curso "/new-course"
    Quando selecionar "Tipo de curso" como "Presencial"
    Então o campo "Endereço" deve ser exibido
    E o campo "Link de inscrição" NÃO deve ser exibido
```

---

## CT-012: Campo condicional — Tipo Online exibe campo Link de inscrição

```gherkin
  Cenário: Verificar que campo "Link de inscrição" aparece ao selecionar tipo "Online"
    Dado que o usuário está na página de cadastro de curso "/new-course"
    Quando selecionar "Tipo de curso" como "Online"
    Então o campo "Link de inscrição" deve ser exibido
    E o campo "Endereço" NÃO deve ser exibido
```

---

## CT-013: Cadastro presencial sem endereço

```gherkin
  Cenário: Cadastrar curso presencial sem informar endereço
    Dado que o usuário está na página de cadastro de curso "/new-course"
    Quando preencher todos os campos com dados válidos
    E selecionar "Tipo de curso" como "Presencial"
    E deixar o campo "Endereço" vazio
    E clicar no botão "CADASTRAR CURSO"
    Então o sistema deve exibir mensagem de erro no campo "Endereço"
    E o curso NÃO deve ser cadastrado
```

---

## CT-014: Cadastro online sem link de inscrição

```gherkin
  Cenário: Cadastrar curso online sem informar link de inscrição
    Dado que o usuário está na página de cadastro de curso "/new-course"
    Quando preencher todos os campos com dados válidos
    E selecionar "Tipo de curso" como "Online"
    E deixar o campo "Link de inscrição" vazio
    E clicar no botão "CADASTRAR CURSO"
    Então o sistema deve exibir mensagem de erro no campo "Link de inscrição"
    E o curso NÃO deve ser cadastrado
```

---

## CT-015: Listagem de cursos

```gherkin
Funcionalidade: Listagem de cursos
  Cenário: Verificar que cursos cadastrados aparecem na listagem
    Dado que existem cursos cadastrados no sistema
    Quando o usuário acessar a página de listagem "/"
    Então os cursos cadastrados devem ser exibidos em formato de cards
    E cada card deve conter: nome, descrição, instrutor, datas, tipo de curso e imagem
```

---

## CT-016: Exclusão de curso

```gherkin
  Cenário: Excluir um curso da listagem
    Dado que existe pelo menos um curso cadastrado na listagem
    Quando o usuário clicar no botão "Excluir Curso" de um card
    Então o curso deve ser removido da listagem
    E uma mensagem de confirmação ou sucesso deve ser exibida
```

---

## CT-017: Cadastro com caracteres especiais no nome

```gherkin
  Cenário: Cadastrar curso com caracteres especiais no nome
    Dado que o usuário está na página de cadastro de curso "/new-course"
    Quando preencher o campo "Nome do curso" com "<script>alert('XSS')</script>"
    E preencher os demais campos com dados válidos
    E clicar no botão "CADASTRAR CURSO"
    Então o sistema deve sanitizar a entrada ou rejeitar caracteres perigosos
    E o nome não deve ser interpretado como código HTML/JavaScript
```

---

## CT-018: Cadastro com nome muito longo

```gherkin
  Cenário: Cadastrar curso com nome excessivamente longo
    Dado que o usuário está na página de cadastro de curso "/new-course"
    Quando preencher o campo "Nome do curso" com um texto de 1000 caracteres
    E preencher os demais campos com dados válidos
    E clicar no botão "CADASTRAR CURSO"
    Então o sistema deve limitar o tamanho do campo ou exibir erro de validação
```

---

## CT-019: Navegação entre páginas

```gherkin
Funcionalidade: Navegação
  Cenário: Navegar entre listagem e cadastro
    Dado que o usuário está na página de listagem "/"
    Quando clicar no botão "CADASTRAR CURSO" no header
    Então o usuário deve ser redirecionado para "/new-course"
    Quando clicar no botão "LISTAR CURSOS" no header
    Então o usuário deve ser redirecionado para "/"
```

---

## CT-020: Cadastro com datas de início e fim iguais

```gherkin
  Cenário: Cadastrar curso com data de início igual à data de fim
    Dado que o usuário está na página de cadastro de curso "/new-course"
    Quando preencher todos os campos com dados válidos
    E selecionar "Data de início" como "2026-05-01"
    E selecionar "Data de fim" como "2026-05-01"
    E clicar no botão "CADASTRAR CURSO"
    Então o sistema deve permitir ou rejeitar o cadastro conforme a regra de negócio
```

---

## Resumo dos Cenários

| ID | Cenário | Tipo | Prioridade |
|----|---------|------|:----------:|
| CT-001 | Cadastro presencial com dados válidos | Positivo | Alta |
| CT-002 | Cadastro online com dados válidos | Positivo | Alta |
| CT-003 | Cadastro com todos os campos vazios | Negativo | Alta |
| CT-004 | Cadastro sem nome do curso | Negativo | Alta |
| CT-005 | Cadastro sem descrição | Negativo | Média |
| CT-006 | Cadastro sem instrutor | Negativo | Média |
| CT-007 | Data de fim anterior à data de início | Negativo | Alta |
| CT-008 | Número de vagas negativo | Negativo | Alta |
| CT-009 | Número de vagas igual a zero | Negativo | Média |
| CT-010 | URL de imagem inválida | Negativo | Média |
| CT-011 | Campo condicional — Presencial → Endereço | Funcional | Alta |
| CT-012 | Campo condicional — Online → Link de inscrição | Funcional | Alta |
| CT-013 | Presencial sem endereço | Negativo | Média |
| CT-014 | Online sem link de inscrição | Negativo | Média |
| CT-015 | Listagem de cursos | Positivo | Alta |
| CT-016 | Exclusão de curso | Positivo | Alta |
| CT-017 | Caracteres especiais (XSS) | Segurança | Alta |
| CT-018 | Nome excessivamente longo | Borda | Baixa |
| CT-019 | Navegação entre páginas | Funcional | Média |
| CT-020 | Datas de início e fim iguais | Borda | Baixa |
