# ATIVIDADE trigger
## METODOLOGIA 

 Essa atividade tem o propósito da utilização do trigger, que foi apresentado durante a aula de Banco de Dados e proposto pelo tutor.

 ## PASSO 1 - REPRODUZA O CÓDIGO SUGERIDO

 create table Pedido(
IDpedido int auto_increment primary key,
DataPedido datetime,
NomeCliente varchar(100)
);

insert into Pedido (DataPedido, NomeCliente) values ('2005-04-15', 'Matheus');
insert into Pedido (DataPedido, NomeCliente) values ('2005-04-15', 'Laia');
insert into Pedido (DataPedido, NomeCliente) values ('1986-09-12', 'Ricardo');

 ![image](https://github.com/MatheusLaiaa/trigger/assets/144149403/3f9fdfa3-3fa8-43bd-a62f-1ee63675c767)

 ## PASSO 2 - EXECUTAR A PRÓXIMA ETAPA E VERIFICAR O RESULTADO 

 Inserir aqui
DELIMITER $
create trigger RegistroDataCriacaoPedido
before insert on Pedido
for each row 
begin 

set New.DataPedido = now();
end;
$
DELIMITER ;

insert into Pedido (NomeCliente) values ('Maria');

select * FROM PEDIDO; 

![image](https://github.com/MatheusLaiaa/trigger/assets/144149403/88f442fc-64bb-4c5e-8962-897870250860)

## PASSO 3 - ADICIONAR FILMES E ID E MINUTOS

inserir aqui
create table Filmes(
id int  primary key auto_increment,
titulo varchar(100),
minutos int 
); 

delimiter $ 
create trigger chk_minutos before insert on filmes 
for each row 
begin
if new.minutos < 0 then 
set new.minutos = null;
end if;
end$

delimiter ;


Inserir aqui

insert into Filmes (titulo, minutos) values ('The terrible trigger', 120);
insert into Filmes (titulo, minutos) values ('O alto da campadecida', 135);
insert into Filmes (titulo, minutos) values ('Faroeste Caboclo', 240);
insert into Filmes (titulo, minutos) values ('The matrix', 90);
insert into Filmes (titulo, minutos) values ('Blade runner ', -88);
insert into Filmes (titulo, minutos) values ('O labirinto do fauno', 110);
insert into Filmes (titulo, minutos) values ('Metropole', 0);
insert into Filmes (titulo, minutos) values ('A lista', 120);

![image](https://github.com/MatheusLaiaa/trigger/assets/144149403/67284afa-9aea-46dc-9d81-8c14bab0e1b8)

## PASSO 4 - ADICIONAR cnk_minutos

Inserir aqui
delimiter $ 
create trigger chk_minutos before insert on Filmes
for each row 
begin
if new.minutos < 0 then 

signal sqlstate '45000'
set message_text = "Valor inváilido para minutos", 
mysql_errno = 2022; 

end if;
end$ 

delimiter ;

## PASSO 5 - ADICIONAR Log_deletion

Inserir aqui
create table Log_deletion(
id  int  primary key  auto_increment,
titulo varchar(60),
quando datetime,
quem varchar(40)
);

delimiter $ 
create trigger Log_deletion after delete on Filmes 
for each row 
begin
insert into log_deletion values (null, old.titulo, sysdate(), user());
end$ 
delimiter ; 

delete from Filmes where id = 2;
delete from Filmes where id = 4;

select * from log_deletion;

![image](https://github.com/MatheusLaiaa/trigger/assets/144149403/bb5ebd85-0839-47b8-978f-1f6779f85f62)

# ALUNO - RA - EMAIL 

Matheus Ferreira De Laia - 236012 - matheuslaia664@gmail.com




