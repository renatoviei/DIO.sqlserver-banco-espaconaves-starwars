# DIO.sqlserver-banco-espaconaves-starwars
<h2>Scripts de criação e utilização do banco relacional e das tabelas que compõem a estrutura do banco dados EstrelaDaMorte baseado na API de Star Wars: https://swapi.dev/<h2>
  
<h2>Script de utilização do banco:</h2>
  
```
use EstrelaDaMorte
```
  
<h2>Script de criação da tabela Planetas:</h2>
      
```
create table Planetas(
	IdPlaneta int NOT NULL,
	Nome varchar(50) NOT NULL,
	Rotacao float NOT NULL, 
	Orbita float NOT NULL,
	Diametro float NOT NULL,
	Clima varchar(50) NOT NULL,
	Populacao int NOT NULL,
)
go
alter table Planetas add constraint PK_Planetas primary key (IdPlaneta);
```
  
<h2>Script de criação da tabela Naves:</h2>
      
```
create table Naves(
	IdNave int NOT NULL,
	Nome varchar(100) NOT NULL,
	Modelo varchar(150) NOT NULL,
	Passageiros int NOT NULL,
	Carga float NOT NULL,
	Classe varchar(100) NOT NULL,
)
go
alter table Naves add constraint PK_Naves primary key (IdNave);
```
  
<h2>Script de criação da tabela Pilotos:</h2>
  
```
create table Pilotos(
	IdPiloto int NOT NULL,
	Nome varchar(200) NOT NULL,
	AnoNascimento varchar(10) NOT NULL, 
	IdPlaneta int NOT NULL,
)
go
alter table Pilotos add constraint PK_Pilotos primary key (IdPiloto);
go
alter table Pilotos add constraint FK_Pilotos_Planetas foreign key (IdPlaneta)
references Planetas (IdPlaneta);
```
  
<h2>Script de criação da tabela PilotosNaves:</h2>
  
```
create table PilotosNaves(
	IdPiloto int NOT NULL,
	IdNave int NOT NULL,
	FlagAutorizado bit NOT NULL,
)
go
alter table PilotosNaves add constraint PK_PilotosNaves primary key (IdPiloto, IdNave);
go
alter table PilotosNaves add constraint FK_PilotosNaves_Pilotos foreign key (IdPiloto)
references Pilotos (IdPiloto);
go
alter table PilotosNaves add constraint FK_PilotosNaves_Naves foreign key (IdNave)
references Naves (IdNave);
go 
alter table PilotosNaves add constraint DF_PilotosNaves_FlagAutorizado default (1) for FlagAutorizado
```
  
<h2>Script de criação da tabela HistoricoViagens:</h2>
  
```
create table HistoricoViagens(
    IdNave int NOT NULL,
	IdPiloto int NOT NULL,	
	DtSaida datetime NOT NULL,
	DtChegada datetime NULL
)
go
alter table HistoricoViagens add constraint FK_HistoricoViagens_PilotosNaves foreign key (IdPiloto, IdNave)
references PilotosNaves (IdPiloto, IdNave) ;
go
alter table HistoricoViagens check constraint FK_HistoricoViagens_PilotosNaves 
```
  

  
