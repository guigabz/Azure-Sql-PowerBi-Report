# Azure Company Database & Power BI Dashboard

Este repositório contém o projeto **Azure Company**, que inclui:

- Um banco de dados SQL no Azure representando informações de funcionários, departamentos, projetos e dependentes.
- Um **dashboard interativo no Power BI** para análise e visualização de dados corporativos.

---

## 1️⃣ Descrição do Projeto

O objetivo deste projeto é simular um ambiente corporativo completo, contendo:

- Informações de **funcionários** (`employee`), incluindo salário, cargo, gerente e departamento.
- **Departamentos** (`departament`) e suas localizações (`dept_locations`).
- **Projetos** (`project`) e participação de funcionários (`works_on`).
- **Dependentes** (`dependent`) dos funcionários.

O dashboard do Power BI permite analisar os dados de forma intuitiva, exibindo KPIs, hierarquia de gerentes, distribuição salarial e alocação em projetos.

---

## 2️⃣ Criação do Servidor SQL no Azure

Para executar este projeto em nuvem, você pode criar um servidor SQL no Azure:

1. Acesse o [Portal do Azure](https://portal.azure.com/).  
2. Clique em **Criar um recurso → Banco de dados → SQL Database**.  
3. Preencha os campos:
   - **Assinatura**: escolha sua assinatura do Azure.
   - **Grupo de recursos**: crie um novo ou use um existente.
   - **Nome do banco de dados**: `azure_company`.
   - **Servidor**: crie um novo servidor:
     - **Nome do servidor**: ex.: `azurecompanyserver`.
     - **Login de administrador**: ex.: `adminuser`.
     - **Senha**: escolha uma senha segura.
     - **Localização**: escolha a região mais próxima.
4. Clique em **Revisar + criar** e depois em **Criar**.  
5. Após criar, configure a **regra de firewall** para permitir seu IP acessar o servidor:
   - No menu do servidor → **Conexão de firewall → Adicionar seu IP atual**.

---

## 3️⃣ Conectando ao Servidor SQL do Azure

- No **MySQL Workbench** ou **Azure Data Studio**, conecte usando:
  - **Servidor**: `azurecompanyserver.database.windows.net`
  - **Login**: `adminuser`
  - **Senha**: sua senha
  - **Banco de dados**: `azure_company`

- Execute os scripts:
  1. `create_tables.sql` → Criação das tabelas.
  2. `insert_data.sql` → Inserção de dados de exemplo.

---

## 4️⃣ Estrutura do Banco de Dados

### Tabelas principais:

1. **employee** – Funcionários da empresa
   - Fname, Minit, Lname, Ssn, Bdate, Address, Sex, Salary, Super_ssn, Dno
   - Chave primária: `Ssn`
   - Chave estrangeira: `Super_ssn` → `Ssn` (auto-relacionamento para gerente)

2. **departament** – Departamentos
   - Dname, Dnumber, Mgr_ssn, Mgr_start_date, Dept_create_date
   - Chave primária: `Dnumber`
   - Chave estrangeira: `Mgr_ssn` → `employee.Ssn`

3. **dept_locations** – Localizações dos departamentos
   - Dnumber, Dlocation
   - Chave primária: `(Dnumber, Dlocation)`
   - Chave estrangeira: `Dnumber` → `departament.Dnumber`

4. **project** – Projetos
   - Pname, Pnumber, Plocation, Dnum
   - Chave primária: `Pnumber`
   - Chave estrangeira: `Dnum` → `departament.Dnumber`

5. **works_on** – Alocação de funcionários em projetos
   - Essn, Pno, Hours
   - Chaves primária e estrangeira: `Essn` → `employee.Ssn`, `Pno` → `project.Pnumber`

6. **dependent** – Dependentes dos funcionários
   - Essn, Dependent_name, Sex, Bdate, Relationship
   - Chave primária: `(Essn, Dependent_name)`
   - Chave estrangeira: `Essn` → `employee.Ssn`

---

## 5️⃣ Dashboard Power BI

O dashboard permite:

- Visualizar **KPIs**: total de funcionários, gerentes, departamentos, projetos e dependentes.
- Tabela de **funcionários e seus gerentes**.
- Gráfico de **distribuição salarial por departamento e sexo**.
- Gráfico de **participação em projetos por horas trabalhadas**.
- Tabela de **dependentes por funcionário**.
- Mapa ou gráfico de **localizações dos departamentos**.
- Filtros interativos por departamento, gerente, sexo ou projeto.

---

## 6️⃣ Como Usar

### Banco de Dados:

1. Crie o servidor SQL no Azure (conforme seção 2).  
2. Conecte via MySQL Workbench ou Azure Data Studio.  
3. Execute os scripts `create_tables.sql` e `insert_data.sql`.

### Power BI:

1. Abra o Power BI Desktop.  
2. Conecte ao banco de dados SQL do Azure (`azure_company`).  
3. Importe todas as tabelas: `employee`, `departament`, `dept_locations`, `project`, `works_on`, `dependent`.  
4. Configure os relacionamentos entre tabelas (baseados nas chaves estrangeiras).  
5. Crie visualizações e KPIs conforme a seção **Dashboard Power BI**.

---

## 7️⃣ Estrutura do Repositório

/azure_company_project
│
├─ create_tables.sql # Script de criação do schema e tabelas
├─ insert_data.sql # Script de inserção de dados
├─ azure_company.pbix # Arquivo do Power BI
└─ README.md


---

## 8️⃣ Tecnologias

- Azure SQL Database
- MySQL 8.0
- Power BI Desktop
- DAX (para cálculos no Power BI)

---

## 9️⃣ Contato

Para dúvidas ou sugestões, entre em contato:

- Nome: [Guilherme Gabriel]  
- Email: [guigabfz@gmail.com]  
- GitHub: [https://github.com/guigabz]
