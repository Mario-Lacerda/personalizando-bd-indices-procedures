# Desafio Dio - Personalizando o Banco de Dados com Índices e Procedures



Neste projeto, vamos criar um banco de dados simples e personalizá-lo usando índices e procedures para melhorar o desempenho e a funcionalidade.



### **Pré-requisitos**

- MySQL ou outro sistema de gerenciamento de banco de dados
- Conhecimento básico de SQL



**Criando o Banco de Dados**



1. ### Crie um novo banco de dados chamado "tarefas".

2. Crie uma tabela chamada "tarefas" com as seguintes colunas:

   - id (INT, chave primária)
   - nome (VARCHAR(255))
   - descrição (TEXT)
   - concluído (BOOLEAN)



### **Criando Índices**

Os índices são estruturas de dados que ajudam o banco de dados a encontrar dados rapidamente. Vamos criar um índice na coluna "nome" da tabela "tarefas":

sql



```sql
CREATE INDEX idx_nome ON tarefas (nome);
```



### **Criando Procedures**

As procedures são funções armazenadas no banco de dados que podem ser chamadas para executar tarefas específicas. Vamos criar uma procedure para marcar uma tarefa como concluída:

sql



```sql
CREATE PROCEDURE marcar_tarefa_como_concluida(IN tarefa_id INT)
BEGIN
    UPDATE tarefas SET concluído = TRUE WHERE id = tarefa_id;
END;
```



### **Executando a Procedure**

Para executar a procedure, use a seguinte consulta:

sql



```sql
CALL marcar_tarefa_como_concluida(1);
```

### **Criando Funções**

Além das procedures, também podemos criar funções no banco de dados. As funções retornam um valor e podem ser usadas em consultas SQL. Vamos criar uma função para obter o número de tarefas concluídas:

sql



```sql
CREATE FUNCTION contar_tarefas_concluidas() RETURNS INT
BEGIN
    RETURN (SELECT COUNT(*) FROM tarefas WHERE concluído = TRUE);
END;
```



### **Criando Triggers**

Os triggers são procedimentos que são executados automaticamente quando certos eventos ocorrem no banco de dados. Vamos criar um trigger para registrar quando uma tarefa for concluída:

sql



```sql
CREATE TRIGGER tarefa_concluida AFTER UPDATE ON tarefas
FOR EACH ROW
BEGIN
    INSERT INTO log (tarefa_id, data_hora) VALUES (OLD.id, NOW());
END;
```



### **Exemplo de Uso**

Aqui está um exemplo de como usar as funções e triggers que criamos:

sql



```sql
-- Obter o número de tarefas concluídas
SELECT contar_tarefas_concluidas();

-- Marcar uma tarefa como concluída
CALL marcar_tarefa_como_concluida(1);

-- Verificar o log de tarefas concluídas
SELECT * FROM log;
```



### **Conclusão**

Neste projeto, criamos um banco de dados simples e o personalizamos usando índices, procedures, funções e triggers. Isso melhorou ainda mais o desempenho e a funcionalidade do banco de dados. Você pode personalizar ainda mais o banco de dados para atender às suas necessidades específicas.
