---

## 🔍 Análise Inicial da Aplicação

### Objetivo da Aplicação

A aplicação é um **sistema de gerenciamento de cursos** que permite ao usuário cadastrar novos cursos e visualizá-los em formato de cards. Foi construída utilizando o framework **Quasar (Vue.js)** e se comunica com uma API para persistência dos dados.

### Principais Fluxos Disponíveis

A aplicação possui **duas páginas principais**:

| Página | Rota | Descrição |
|--------|------|-----------|
| **Listagem de Cursos** | `/` | Exibe os cursos cadastrados em formato de cards com imagem, título, descrição, instrutor, datas e tipo. Cada card possui um botão "Excluir Curso". |
| **Cadastro de Curso** | `/new-course` | Formulário com 10 campos para registrar um novo curso. Dois campos são condicionais: "Endereço" aparece quando o tipo é "Presencial", e "Link de inscrição" aparece quando o tipo é "Online". |

**Navegação:** O header contém o título da aplicação e dois botões de navegação: **"LISTAR CURSOS"** e **"CADASTRAR CURSO"**.

### Campos do Formulário de Cadastro

| Campo | Tipo | Obrigatório | Observação |
|-------|------|:-----------:|------------|
| Nome do curso | Text input | ❓ | Sem validação visível |
| Descrição do curso | Textarea | ❓ | Sem validação visível |
| Instrutor | Text input | ❓ | Sem validação visível |
| URL da imagem de capa | Text input | ❓ | Sem validação de formato URL |
| Data de início | Date picker | ❓ | Componente Quasar de data |
| Data de fim | Date picker | ❓ | Componente Quasar de data |
| Número de vagas | Number input | ❓ | Aceita valores negativos |
| Tipo de curso | Select/Dropdown | ❓ | Opções: "Presencial" ou "Online" |
| Endereço | Text input | ❓ | Condicional — só aparece se tipo = "Presencial" |
| Link de inscrição | Text input | ❓ | Condicional — só aparece se tipo = "Online" |

> **Nota:** O símbolo ❓ indica que não há indicação clara na interface se o campo é obrigatório ou opcional, pois **não existe validação implementada**.

### Pontos Críticos para Teste

1. **Validação do formulário de cadastro** — Ponto mais crítico. O formulário não possui nenhuma validação, permitindo envio de dados vazios ou inválidos.
2. **Funcionalidade de exclusão** — O botão "Excluir Curso" não funciona (erro 405 na API).
3. **Integridade dos dados** — Campos como datas, URLs e número de vagas aceitam qualquer valor sem validação.
4. **Campos condicionais** — Garantir que "Endereço" e "Link de inscrição" apareçam/desapareçam corretamente conforme o tipo de curso.
5. **Persistência dos dados** — Verificar se cursos cadastrados são de fato salvos e exibidos na listagem.

---

## 🧠 Decisões Tomadas e Raciocínio

### Abordagem de Teste

Adotei uma abordagem de testes **exploratórios** seguida de **testes estruturados**:

1. **Exploração inicial:** Naveguei pela aplicação sem script, observando a interface, os componentes, o fluxo de navegação e o comportamento geral do sistema.

2. **Identificação de riscos:** Após a exploração, identifiquei que a **ausência total de validações** no formulário era o maior risco, pois permite a criação de registros inconsistentes que podem impactar toda a listagem.

3. **Priorização:** Priorizei os cenários de teste por impacto:
   - **Alta prioridade:** Validações de campos obrigatórios, cadastro com dados válidos, exclusão de cursos
   - **Média prioridade:** Campos condicionais, limites de campos, formatos de dados
   - **Baixa prioridade:** Responsividade, usabilidade, aspectos visuais

4. **Formato dos cenários:** Optei pelo formato **Gherkin (Dado/Quando/Então)** por ser amplamente utilizado em BDD e facilitar a comunicação entre equipes técnicas e de negócio.

5. **Cenários negativos:** Dei ênfase especial aos cenários negativos e de borda, pois a ausência de validação frontend indica que provavelmente também não há validação adequada no backend.

### Uso de Inteligência Artificial

Utilizei IA como ferramenta de apoio para:
- Automatizar a exploração sistemática da aplicação via browser
- Estruturar a documentação de forma padronizada
- Garantir cobertura abrangente dos cenários de teste

Todas as análises, priorizações e conclusões foram revisadas e validadas com base no comportamento real observado na aplicação.

---

## 📁 Estrutura do Repositório

```
├── README.md                  # Este arquivo — análise e documentação geral
├── cenarios-de-teste.md       # Cenários e casos de teste em formato Gherkin
├── relatorio-de-bugs.md       # Relatório detalhado de bugs encontrados
└── evidencias/                # Evidências de execução dos testes
    ├── 01_cadastro_valido_presencial.webp
    ├── 02_cadastro_valido_online.webp
    ├── 03_cadastro_campos_vazios.webp
    ├── 04_exclusao_curso.webp
    ├── 05_campo_condicional.webp
    ├── 06_vagas_negativas.webp
    └── 07_listagem_cursos.webp
```

---

## 🔗 Links

| Recurso | Link |
|---------|------|
| Aplicação testada | [https://creative-sherbet-a51eac.netlify.app/](https://creative-sherbet-a51eac.netlify.app/) |
| Planilha de cenários (Google Sheets) | *https://docs.google.com/spreadsheets/d/1943woAhpSMzRH10XdFBbV_Nn7lLkYohOY-HwRd1ls68/edit?usp=sharing* |
| Evidências (Google Drive) | *Dentro da pasta "evidencias" nesse mesmo repositório* |

---

## 👤 Candidato

- **Nome:** *Wilson Wagner*
- **E-mail:** contatowwsn@gmail.com
