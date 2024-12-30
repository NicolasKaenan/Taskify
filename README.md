# TASKIFY: Gerenciador de tarefas pessoais.
> Este é um projeto pessoal. Ele combina Spring boot e Angular pra criar um gerenciador de tarefas, tal projeto tem como objetivo demonstrar minha competência com estes frameworks.

## Banco de dados:
> Este projeto utiliza banco de dados, gerenciado pela API Resful criado com Spring Boot. Possui duas tabelas: Tasks, Users e Categories.

### Tabela tasks
> Tabela responsável por armazenar as informações das tarefas criadas pelos usuários. 
```
CREATE TABLE tasks (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    description TEXT,
    status VARCHAR(50) DEFAULT 'PENDING',
    priority VARCHAR(50) DEFAULT 'LOW',
    due_date DATE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP
);
```

### Tabela users
    Tabela responsável por manter as informações dos usuários.
```
CREATE TABLE users (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(100) NOT NULL UNIQUE,
    email VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Tabela categorias
> Tabela responsável por definir as categorias também criadas pelos usuários.
```
CREATE TABLE categories (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Relacionamento das tabelas do banco de dados.
> Para relacionar as tasks, categorias e usuários, precisamos definir relacionamentos entre as tabelas. Para a tabela tasks, adicionaremos um user_id, que se relaciona ao usuario dono da task e um category_id, que se relaciona com categories.
```
ALTER TABLE tasks ADD COLUMN user_id BIGINT;
ALTER TABLE tasks ADD CONSTRAINT fk_user FOREIGN KEY (user_id) REFERENCES users(id);

ALTER TABLE tasks ADD COLUMN category_id BIGINT;
ALTER TABLE tasks ADD CONSTRAINT fk_category FOREIGN KEY (category_id) REFERENCES categories(id);
```

## API Restful
> Abaixo listarei os caminhos da API, responsável por gravar, atualizar, deletar e buscar, as tasks e categorias de determinado usuário.

> GET de tasks e categorias.
```
GET /tasks - Listar todas as tarefas.
GET /categories - Listar todas as categorias.
```

> POST de tasks e categorias. 
```
POST /tasks - Criar nova tarefa.
POST /categories - Criar nova categoria.
```

> PUT de tasks e categorias.
```
PUT /tasks/{id} - Atualizar tarefa.
PUT /categories/{id} - Atualizar categorias.
```

> DELETE de tasks e categorias.
```
DELETE /tasks/{id} - Excluir tarefa.
DELETE /categories/{id} - Excluir categoria.
```

### Login e Registro:
    A API também apresenta caminhos para requisição de login e registro, vale ressaltar que "/login" é POST por boas práticas.
```
POST /register
POST /login
```
