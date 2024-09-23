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
Este repositório contém um exemplo de criação de tabelas para um sistema de cadastro de ID 

``` java 
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.sql.Statement;

public class DatabaseSetup {
    private static final String URL = "jdbc:mysql://localhost:3306/seu_banco_de_dados";
    private static final String USER = "seu_usuario";
    private static final String PASSWORD = "sua_senha";

    public static void main(String[] args) {
        try (Connection connection = DriverManager.getConnection(URL, USER, PASSWORD)) {
            createTables(connection);
            insertAdminUser(connection);
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static void createTables(Connection connection) throws SQLException {
        String createUsuariosTable = "CREATE TABLE tbusuarios (" +
                "iduser INT PRIMARY KEY, " +
                "usuario VARCHAR(15) NOT NULL, " +
                "fone VARCHAR(15), " +
                "login VARCHAR(15) NOT NULL UNIQUE, " +
                "senha VARCHAR(250) NOT NULL, " +
                "perfil VARCHAR(20) NOT NULL" +
                ");";

        String createClientesTable = "CREATE TABLE tbclientes (" +
                "idcli INT PRIMARY KEY AUTO_INCREMENT, " +
                "nomecli VARCHAR(50) NOT NULL, " +
                "endcli VARCHAR(100), " +
                "fonecli VARCHAR(15) NOT NULL, " +
                "emailcli VARCHAR(50) UNIQUE" +
                ");";

        String createOsTable = "CREATE TABLE tbos (" +
                "os INT PRIMARY KEY AUTO_INCREMENT, " +
                "data_os TIMESTAMP DEFAULT CURRENT_TIMESTAMP, " +
                "tipo VARCHAR(15) NOT NULL, " +
                "situacao VARCHAR(20) NOT NULL, " +
                "equipamento VARCHAR(150) NOT NULL, " +
                "defeito VARCHAR(150), " +
                "servico VARCHAR(150), " +
                "tecnico VARCHAR(30), " +
                "valor DECIMAL(10,2), " +
                "idcli INT NOT NULL, " +
                "FOREIGN KEY (idcli) REFERENCES tbclientes(idcli)" +
                ");";

        try (Statement statement = connection.createStatement()) {
            statement.executeUpdate(createUsuariosTable);
            statement.executeUpdate(createClientesTable);
            statement.executeUpdate(createOsTable);
            System.out.println("Tabelas criadas com sucesso!");
        }
    }

    private static void insertAdminUser(Connection connection) throws SQLException {
        String insertAdmin = "INSERT INTO tbusuarios (iduser, usuario, login, senha, perfil) VALUES (?, ?, ?, MD5(?), ?)";
        
        try (PreparedStatement preparedStatement = connection.prepareStatement(insertAdmin)) {
            preparedStatement.setInt(1, 1);
            preparedStatement.setString(2, "Administrador");
            preparedStatement.setString(3, "admin");
            preparedStatement.setString(4, "admin");
            preparedStatement.setString(5, "admin");
            preparedStatement.executeUpdate();
            System.out.println("Usuário administrador inserido com sucesso!");
        }
    }
}


