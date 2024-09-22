# E-commerce

Gestão de vendas este projeto conta com varisas funcionaliades sendo elas a da lista abaixo 

<img width=50% src="https://github.com/Lucasbarbosa332/E-commerce/blob/main/Captura%20de%20tela%202024-09-22%20172048.png?raw=true"></img>

# Instalação 
Voce precisa ter a versão java 11 ou superior para esse projeto voce precisa ter um IDE para executalo sendo eles VS CODE Ou NETBEANS 
As tabelas e bancos de Dados estão dentro do arquivi zip 

# Cadastro de Usuário
 
  <img width=50% src="https://github.com/Lucasbarbosa332/E-commerce/blob/main/Captura%20de%20tela%202024-09-22%20171942.png"></img>

* Registro: Permite que novos usuários se cadastrem com informações como nome, e-mail e senha.
* Login/Senha: Autenticação de usuários com validação de senhas.
* Recuperação de Senha: Opção para recuperação de senha via e-mail.

 <img width=50% src="https://github.com/Lucasbarbosa332/E-commerce/blob/main/Captura%20de%20tela%202024-09-22%20172206.png?raw=true"></img>

# Seção de Produtos

 <img width=50% src="https://github.com/Lucasbarbosa332/E-commerce/blob/main/Captura%20de%20tela%202024-09-22%20172228.png?raw=true"></img>

* Listagem de Produtos: Exibição de todos os produtos disponíveis com imagens, descrições e preços.
* Filtragem e Pesquisa: Permite aos usuários buscar produtos por categoria, preço ou palavras-chave.
* Detalhes do Produto: Página com informações detalhadas sobre cada produto, incluindo avaliações.

# Seção de Clientes

 <img width=50% src="https://github.com/Lucasbarbosa332/E-commerce/blob/main/Captura%20de%20tela%202024-09-22%20172318.png?raw=true"></img>
 
* Perfil do Cliente: Visualização e edição das informações do perfil do cliente.
* Histórico de Compras: Exibição das compras anteriores, permitindo reordenação de produtos.

<img width=50% src="https://github.com/Lucasbarbosa332/E-commerce/blob/main/Captura%20de%20tela%202024-09-22%20172331.png?raw=true"></img>
 
* Avaliações de Produtos: Permitir que os clientes deixem avaliações e comentários sobre os produtos comprados.

# Seção de Vendas

* Carrinho de Compras: Funcionalidade para adicionar produtos ao carrinho e calcular o total da compra.
* Checkout: Processo de finalização da compra, onde o usuário insere informações de pagamento e envio.
* Gestão de Pedidos: Visualização do status dos pedidos e possibilidade de cancelamento.

# Seção de Usuários (Admin)

<img width=50% src="https://github.com/Lucasbarbosa332/E-commerce/blob/main/Captura%20de%20tela%202024-09-22%20172342.png?raw=true"></img>

* Gerenciamento de Usuários: Visualização, edição e exclusão de contas de usuários.
* Controle de Produtos: Adição, edição e remoção de produtos no sistema.
* Relatórios de Vendas: Geração de relatórios sobre vendas e desempenho do e-commerce


# Estrutura do Banco de Dados

Exemplo de Banco de Dados SQL
Este repositório contém um exemplo de criação de tabelas para um sistema de ordens de serviço com usuários, clientes e ordens de serviço (OS).

``` java 
-- Criação da tabela tbusuarios para armazenar informações de usuários
create table tbusuarios(
  iduser int primary key,                  -- Identificador único para o usuário
  usuario varchar(15) not null,            -- Nome do usuário, campo obrigatório
  fone varchar(15),                        -- Telefone do usuário, campo opcional
  login varchar(15) not null unique,       -- Nome de login, deve ser único
  senha varchar(250) not null,             -- Senha do usuário (geralmente criptografada), campo obrigatório
  perfil varchar(20) not null              -- Perfil do usuário (ex: 'admin', 'user'), campo obrigatório
);

-- Inserção de um usuário administrador inicial na tabela tbusuarios
insert into tbusuarios(iduser,usuario,login,senha,perfil) 
values(1,'Administrador','admin',md5('admin'),'admin');

-- Criação da tabela tbclientes para armazenar informações de clientes
create table tbclientes(
  idcli int primary key auto_increment,    -- Identificador único do cliente, auto_increment para gerar automaticamente
  nomecli varchar(50) not null,            -- Nome do cliente, campo obrigatório
  endcli varchar(100),                     -- Endereço do cliente, campo opcional
  fonecli varchar(15) not null,            -- Telefone do cliente, campo obrigatório
  emailcli varchar(50) unique              -- Email do cliente, campo único
);

-- Criação da tabela tbos para armazenar informações sobre ordens de serviço (OS)
create table tbos(
  os int primary key auto_increment,       -- Identificador único da OS, auto_increment
  data_os timestamp default current_timestamp, -- Data da OS com timestamp padrão no momento da criação
  tipo varchar(15) not null,               -- Tipo de serviço (ex: 'manutenção', 'instalação'), campo obrigatório
  situacao varchar(20) not null,           -- Situação da OS (ex: 'em andamento', 'concluída'), campo obrigatório
  equipamento varchar(150) not null,       -- Descrição do equipamento, campo obrigatório
  defeito varchar(150),                    -- Descrição do defeito (opcional)
  servico varchar(150),                    -- Descrição do serviço realizado (opcional)
  tecnico varchar(30),                     -- Nome do técnico responsável, opcional
  valor decimal(10,2),                     -- Valor do serviço, opcional
  idcli int not null,                      -- Chave estrangeira referenciando o cliente
  foreign key(idcli) references tbclientes(idcli) -- Relaciona a OS ao cliente na tabela tbclientes
);

