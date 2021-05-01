# cpf
DECLARE 
    @Objeto VARCHAR(128) = 'sys.objects',
    @Nome_Objeto VARCHAR(128) = 'syscerts',
    @Query VARCHAR(MAX)

-- Monta a nossa query dinâmica    
SET @Query = 'SELECT * FROM ' + @Objeto + ' WHERE [name] = ''' + @Nome_Objeto + ''''

-- Mostra na tela a query final depois de montada
SELECT @Query

-- Executa o comando no banco
EXEC(@Query)
DECLARE 
    @Schema_ID INT = 4,
    @Nome_Objeto VARCHAR(128) = 'syscerts',
    @Type VARCHAR(10),
    @object_id INT

SELECT *
FROM sys.objects
WHERE (@Schema_ID IS NULL OR [schema_id] = @Schema_ID)
AND (@Nome_Objeto IS NULL OR [name] = @Nome_Objeto)
AND (@Type IS NULL OR [type] = @Type)
AND (@object_id IS NULL OR [object_id] = @object_id)
DECLARE 
    @Schema_ID INT = 4,
    @Nome_Objeto VARCHAR(128) = 'syscerts',
    @Type VARCHAR(10),
    @object_id INT,
    @Query VARCHAR(MAX)


-- Monta a base da nossa query dinâmica 
SET @Query = 'SELECT * FROM sys.objects WHERE 1=1'


-- Aplica os filtros dinâmicamente
IF (@Nome_Objeto IS NOT NULL)
    SET @Query += ' AND [name] = ''' + @Nome_Objeto + ''''

IF (@Type IS NOT NULL)
    SET @Query += ' AND [type] = ''' + @Type + ''''

IF (@Schema_ID IS NOT NULL)
    SET @Query += ' AND [schema_id] = ' + CAST(@Schema_ID AS VARCHAR(10))

IF (@object_id IS NOT NULL)
    SET @Query += ' AND [object_id] = ' + CAST(@object_id AS VARCHAR(10))


-- Mostra na tela a query final depois de montada
SELECT @Query

-- Executa o comando no banco
EXEC(@Query)
CREATE TABLE dbo.Usuarios (
    Id_Usuario INT IDENTITY(1,1) NOT NULL PRIMARY KEY CLUSTERED,
    Ds_Email VARCHAR(200) NOT NULL,
    Ds_Senha VARCHAR(100) NOT NULL
)

INSERT INTO dbo.Usuarios
VALUES('analistadeperon@hotmail.com', 'matheus')
SELECT * FROM dbo.Usuarios WHERE Ds_Email = '' OR 'x'='x'--' AND Ds_Senha = ''SELECT cpfcnpj, FirstName, [Uid], ID 
FROM dbo.Tabela 
WHERE cpfcnpj = ''; SELECT name, name, name, name FROM sys.tables; --'
DECLARE @Objetos_Query_Dinamica TABLE ( [Ds_Database] nvarchar(256), [Ds_Objeto] nvarchar(256), [Ds_Tipo] nvarchar(128), [definition] VARCHAR(MAX) )


IF (OBJECT_ID('tempdb.dbo.#Palavras_Exec') IS NOT NULL) DROP TABLE #Palavras_Exec
CREATE TABLE #Palavras_Exec (
    Palavra VARCHAR(100) COLLATE SQL_Latin1_General_CP1_CI_AI
)

INSERT INTO #Palavras_Exec
VALUES('%EXEC (%'), ('%EXEC(%'), ('%EXECUTE (%'), ('%EXECUTE(%'), ('%sp_executesql%')


INSERT INTO @Objetos_Query_Dinamica
EXEC sys.sp_MSforeachdb '
IF (''?'' <> ''tempdb'')
BEGIN

    SELECT DISTINCT TOP(100)
        ''?'' AS Ds_Database,
        B.[name],
        B.[type_desc],
        A.[definition]
    FROM
        [?].sys.sql_modules A WITH(NOLOCK)
        JOIN [?].sys.objects B WITH(NOLOCK) ON B.[object_id] = A.[object_id]
        JOIN #Palavras_Exec C WITH(NOLOCK) ON A.[definition] COLLATE SQL_Latin1_General_CP1_CI_AI LIKE C.Palavra
    WHERE
        B.is_ms_shipped = 0
        AND ''?'' <> ''ReportServer''
        AND B.[name] NOT IN (''sp_WhoIsActive'', ''sp_showindex'', ''sp_AllNightLog'', ''sp_AllNightLog_Setup'', ''sp_Blitz'', ''sp_BlitzBackups'', ''sp_BlitzCache'', ''sp_BlitzFirst'', ''sp_BlitzIndex'', ''sp_BlitzLock'', ''sp_BlitzQueryStore'', ''sp_BlitzWho'', ''sp_DatabaseRestore'')
        AND NOT (B.[name] LIKE ''stp_DTA_%'' AND ''?'' = ''msdb'')
        AND NOT (B.[name] = ''sp_readrequest'' AND ''?'' = ''master'')
        AND EXISTS (
            SELECT NULL
            FROM [?].sys.parameters X1 WITH(NOLOCK)
            JOIN [?].sys.types X2 WITH(NOLOCK) ON X1.system_type_id = X2.user_type_id
            WHERE A.[object_id] = X1.[object_id]
            AND X2.[name] IN (''text'', ''ntext'', ''varchar'', ''nvarchar'')
            AND (X1.max_length > 10 OR X1.max_length < 0)
        )
            
END'

SELECT * FROM @Objetos_Query_Dinamica
ALTER PROCEDURE dbo.stpConsulta_CPF ( 
    @CPF VARCHAR(14) 
)
AS
BEGIN
    
    DECLARE @Query VARCHAR(MAX) = 'SELECT * FROM dbo._Teste WHERE CPF = ''' + @CPF + ''''
    EXEC(@Query)

END
ALTER PROCEDURE dbo.stpConsulta_CPF ( 
    @CPF VARCHAR(14) 
)
AS
BEGIN
    
    SELECT * 
    FROM dbo._Teste 
    WHERE CPF = @CPF

END
DECLARE 
    @Schema_ID INT = 4,
    @Nome_Objeto VARCHAR(128) = 'syscerts',
    @Type VARCHAR(10),
    @object_id INT,
    @Query VARCHAR(MAX)


-- Monta a base da nossa query dinâmica 
SET @Query = 'SELECT * FROM sys.objects WHERE 1=1'


-- Aplica os filtros dinâmicamente
IF (@Nome_Objeto IS NOT NULL)
    SET @Query += ' AND [name] = ''' + @Nome_Objeto + ''''

IF (@Type IS NOT NULL)
    SET @Query += ' AND [type] = ''' + @Type + ''''

IF (@Schema_ID IS NOT NULL)
    SET @Query += ' AND [schema_id] = ' + CAST(@Schema_ID AS VARCHAR(10))

IF (@object_id IS NOT NULL)
    SET @Query += ' AND [object_id] = ' + CAST(@object_id AS VARCHAR(10))


-- Mostra na tela a query final depois de montada
SELECT @Query

-- Executa o comando no banco
EXEC(@Query)
DECLARE 
    @Schema_ID INT = 4,
    @Nome_Objeto VARCHAR(128) = 'syscerts',
    @Type VARCHAR(10),
    @object_id INT,
    @Query NVARCHAR(MAX)


-- Monta a base da nossa query dinâmica 
SET @Query = 'SELECT * FROM sys.objects WHERE 1=1'


-- Aplica os filtros dinâmicamente
IF (@Nome_Objeto IS NOT NULL)
    SET @Query += ' AND [name] = @Nome_Objeto'

IF (@Type IS NOT NULL)
    SET @Query += ' AND [type] = @Type'

IF (@Schema_ID IS NOT NULL)
    SET @Query += ' AND [schema_id] = @Schema_ID'

IF (@object_id IS NOT NULL)
    SET @Query += ' AND [object_id] = @object_id'


-- Mostra na tela a query final depois de montada
SELECT @Query

-- Executa o comando no banco
EXEC sys.sp_executesql 
    @stmt = @Query,
    @params = N'@Nome_Objeto VARCHAR(128), @Type VARCHAR(10), @Schema_ID INT, @object_id INT',
    @Nome_Objeto = @Nome_Objeto, @Type = @Type, @Schema_ID = @Schema_ID, @object_id = @object_id
   




    
Resumo do que a linguagem colocada em pratica nesse trabalho.

    O que é Query Dinâmica?
Recurso muito utilizado em sistema e rotinas de bancos de dados, Query Dinâmica consiste em montar uma string com comandos T-SQL a serem executados.

Essa string é montada baseada em concatenação de strings e possíveis validações com IFs de acordo com determinados cenários.

Após a string final ter sido construída, ela é processada pelo comando EXECUTE (ou EXEC, para os mais íntimos) e o que estiver nessa string será executada no banco de dados.

É muito importante observar que query dinâmica não é específica apenas para consultas montadas a partir do SQL Server.

Um sistema pode fazer a mesma coisa, criando uma variável string no código-fonte C#. Por exemplo, montar a string e depois enviar essa string para o banco de dados.
