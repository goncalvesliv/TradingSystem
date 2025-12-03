# 🧾 Asset Trading System
**Project Demo Video:** : https://drive.google.com/file/d/1K3fkBF4rF2gVY9Iq74HIibx0Nbuoiu1v/view?usp=sharing

## 📌 Description

This project is an asset trading system built with a distributed architecture. It simulates order submission and processing for buy and sell orders, performs order matching, and stores executed trades in a SQL Server database.

##The solution is composed of the following components:

-OrderAPI – API responsible for submitting and retrieving orders.
-OrderProcessor – Service that consumes messages from RabbitMQ, performs order matching, and saves the results to the database.
-OrderUI – Windows Forms interface for viewing orders and executed trades.
-OrderCommonModels – Library containing shared data models.
-OrderApi.Tests – Unit test project using XUnit and Moq.

## ⚙️ Technologies Used

- .NET 6 / .NET 8  
- C#  
- Windows Forms  
- RabbitMQ  
- Docker  
- SQL Server  
- XUnit + Moq  


## 🚀 How to Run the Project

### 1. Clone the repository

bash
git clone https://github.com/goncalvesliv/SistemaDeNegociacao.git
cd SistemaDeNegociacao

### 2. Configure the database connection string
In the OrderAPI and OrderProcessor projects, edit the appsettings.json file with your connection string:

"ConnectionStrings": {
  "NegociacoesDb": "Server=SEU_SERVIDOR;Database=NomeBanco;User Id=SEU_USUARIO;Password=SENHA;"
}

Then create the two required tables in SQL Server:

CREATE TABLE Negocios (
    Id INT IDENTITY(1,1) PRIMARY KEY,
    NomeAtivo NVARCHAR(50) NOT NULL,
    Preco DECIMAL(18,6) NOT NULL,
    Quantidade INT NOT NULL,
);

CREATE TABLE OrdemProcessada (
    Id INT IDENTITY(1,1) PRIMARY KEY,
    TipoOrdem NVARCHAR(1) NOT NULL,
    NomeAtivo NVARCHAR(50) NOT NULL,
    Preco DECIMAL(18,6) NOT NULL,
    Quantidade INT NOT NULL,
    Status NVARCHAR(30) NOT NULL,
);

### 3. Run RabbitMQ with Docker
To allow the API to publish orders and the processor to consume them, RabbitMQ must be running.

Steps:
Ensure Docker is installed.
Use the docker-compose.yml file located in the project root.
Run: docker-compose up -d

Access the management interface:
URL: http://localhost:
User: guest
Password: guest

### 4. Run the Projects
OrderAPI - dotnet run
OrderProcessor (requires RabbitMQ running)) - dotnet run
Then run the OrderUI interface.
