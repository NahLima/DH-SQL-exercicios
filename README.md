# DH-SQL-exercicios

#### 1 Selecione o código dos países que falam português
````
select country_code from country_language
where language = "portuguese";
````

#### 2 Selecione o nome das cidades com menos de 10.000 habitantes
````
select name from country
where population <10000;
````
#### 3 Selecione o nome das cidades com até 10.000 habitantes
````
select name from country
where population <=10000;
````
#### 4 Selecione os países com mais de 10 milhões de habitantes
````
select name from country
where population > 10000000;
````
#### 5 Selecione o nome e a população dos países da Asia e Europa
````
select name, population from country
where continent = "Asia" or "Europe"
````
#### 6 Selecione o nome dos estados brasileiros em ordem alfabética
````
select name from city
where country_code = 'BRA'
order by name
````
#### 7 Liste os países de cada continente por ordem decrescente de PIB
````
select name,gnp from country
order by gnp desc
````
#### 8 Encontre os 5 países com menor densidade populacional do mundo
````
select name,population from country
order by population ASC 
limit 5
````
#### 9 Liste todos os países asiáticos com área maior que um milhão de kilômetros quadrados
````
select population,name,surface_area from country
where continent = "ASIA"
and surface_area > 1000000
order by name
````
#### 10 Consulte os países que possuem um idioma oficial falado por menos de 10% de sua população, e liste seus códigos e tais idiomas.
````
select coutry_code, language, percentage, name from country_language
join country on country_language.country_code=country.code
where is_official = 'T' and percentage <10
order by country_code

// ou

select country_code, language 
from country_language
where is_official IN ('T')
and percentage < 10
````
#### 11 Liste os países independentes há menos de 40 anos. 
````
select name, continent, indep_year, Year(curdate()) - indep_year as anos_indep  from country
where Year(curdate()) - indep_year < 40
````
#### 12 Qual continente concentra a maior parte desses paises?
````
select
	continent, 
	count(population) as numero_de_paises 
from 
	country
where 
	year(curdate())-indep_year < 40
group by continent
order by numero_de_paises Desc
limit 1;
````
#### 13 Liste os países com muito espaço! Para isso, vamos definir que esses países são os que têm menos de 10 pessoas por kilômetro quadrado ou que tem uma superfície maior que 8 milhões de metros quadrados.
````
select name, surface_area, population, population/surface_area as densidade
from country
where population/surface_area <10
or surface_area > 8000000
order by densidade Desc;
````
#### 14 Vamos supor que a coluna GNP da tabela country guarde o PIB do ano de 2001, e que a coluna GNP_old guarde o PIB do ano 2000. Calcule a variação (em porcentagem) do PIB per cápita dos países da América. Você pode calcular a variação com a seguinte fórmula: variação = (valor_novo / valor_antigo - 1) * 100
````
SELECT 
    continent,
    name,
    gnp,
    gnp_old,
    CONCAT(ROUND(((gnp / gnp_old) - 1) * 100, 2),'%') AS 'taxa_de_crescimento%',
    ((gnp / gnp_old) - 1) AS 'taxa_de_crescimento'
FROM
    country
WHERE
    continent LIKE '% America'
ORDER BY taxa_de_crescimento DESC;
````

#### 15 Selecionar os nomes e códigos dos países
````
select name,code from country;
````
#### 16 Selecionar todas as colunas da tabela de países
````
select * from country;
````
#### 17 Selecionar todas as colunas da tabela de cidades
````
select * from city;
````
#### 18 Selecione os 50 primeiros registros da tabela de países
````
select * from country
limit 50;
````
#### 19 Selecione os registros de 51 à 60 da tabela de países
````
select * from country
limit 51,9;
````
#### 20 Encontre os 5 países cujo PIB mais cresceu
````
select name, (gnp - gnp_old) as PIB from country
order by PIB desc
limit 5;
````
#### 21 Selecione os 10 primeiros registros  das cidades com mais de 10.000 habitantes da tabela cidades
````
select * from city
Where population >10000 
order by population desc
limit 10;
````
#### 22 Selecione os registros de 11 à 20 com até 10.000 habitantes da tabela cidades e ordene alfabeticamente pelo nome das cidades
````
select * from city
Where population <=10000 
order by name 
limit 11,9;
````
#### 23 Selecione as cidades que o nome destas começa com a letra A
````
select name from city
where name like 'A%';
````
#### 24 Selecione as cidades que possuem entre 10.000 e 20.000 habitantes
````
select name, population FROM city
where population >10000 and population <20000
order by population asc;
````
#### 25 Selecione países que seus nomes terminam com a letra A
````
select name FROM country
where name like '%a'
````
#### 26 Selecione os países em que as regiões pertencem ao Caribe
````
SELECT name, region FROM country
Where region = "Caribbean";
````
#### 27 Selecione os países em que as regiões pertencem ao Caribe
````
SELECT name, region FROM country
Where region = "Caribbean";
````
#### 28 Selecionar os nomes e códigos dos países, renomeando as colunas com suas traduções em português
````
select name as nome, code as código from country;
````
#### 29 Liste os nomes das cidades ao lado do nome de seu respectivo país
````
select city.name as City_Name, country.name as Country_Name from city
join country
ON city.country_code = country.code
order by country.name;
````
#### 30 Listar os nomes dos países lado a lado com os idiomas falados neles
````
select country.name, country_language.language country from country
join country_language
ON country_language.country_code = country.code
order by country.name;
````
#### 31 Listar os nomes dos países lado a lado com os idiomas falados neles e acrescentar a porcentagem da população de cada idioma
````
select country.name, country_language.language, country_language.percentage
from country 
join country_language  
ON country_language.country_code = country.code
order by country.name;
````
#### 32 Calcule a população de cada continente
````
SELECT continent, SUM(population) AS pop_continental from country
group by continent;
````
#### 33 Mostre os códigos dos países com pelo menos 3 idiomas oficiais
````
SELECT 
    country_code,
    count(language) As contagem,
    group_concat(language order by language separator '  |  ' ) as linguas 
FROM
    country_language
GROUP BY country_code
having contagem >= 3; 
````
#### 34 Liste os nomes das cidades ao lado dos nomes dos países cujo nome começa com o nome da cidade
````
SELECT 
    city.name AS city_name, country.name AS country_name
FROM
    city,
    country
WHERE
    country.name LIKE CONCAT(city.name, '%')
    and country.code = city.country_code


// ou 

SELECT 
    city.name AS city_name, country.name AS country_name
FROM
    city
join country on 
country.name LIKE CONCAT(city.name, '%')
and country.code = city.country_code;
````
#### 35 Repita a query acima, mas mostre o nome de todas as cidades mesmo que não haja "match" com nenhum país
````
SELECT 
    city.country_code AS city_country_code,
    city.name AS city_name,
    country.code AS country_code,
    country.name AS country_name
FROM
    city
        LEFT JOIN
    country ON country.code = city.country_code
        AND country.name LIKE CONCAT(city.name, '%')
    
````
#### 36 Liste países. Adicione somente as cidades que tem população maior do que 3 milhões de habitantes

````
SELECT 
    country.name, 
    city.name, 
    city.population
FROM country
	LEFT JOIN city 
	ON city.country_code = country.code
	AND city.population > 3000000
    order by country.name asc
    
````
#### 37 Calcular a quantidade de pessoas que fala cada um desses idiomas

````
select 
	country.code, 
	country.population, 
    country_language.language, 
    country_language.percentage,
    (round(((country_language.percentage / 100) * country.population/ 100) *100 ,0)) As population_by_language
from country
join country_language 
on country.code = country_language.country_code
````
#### 38 Selecionar os nomes das diferentes regiões do mundo

````
SELECT DISTINCT region
FROM country
ORDER BY region;
````
#### 39 Selecionar os nomes das distintas regiões do mundo que possuem países com mais de 100 milhões de habitantes

````
SELECT DISTINCT
    (region), name, population
FROM
    country
where population >= 100000000
````
#### 40 Listar códigos dos países que possuem ao menos um idioma oficial falado por uma população maior que 2% e menor que 9% do país

````
SELECT 
    code,
    country_language.language,
    country_language.is_official population,
    country_language.percentage
FROM
    country
        JOIN
    country_language
WHERE
    is_official = 'T' AND percentage >= 2
        AND percentage <= 9;
````
#### 41 Utilizando o COALESCE trabalhe os valores NULL da tabela COUNTRY e substitua-os por um valor que deseja

````
select name, coalesce(indep_year, null,  1980 )  from country;
````
#### 42 Mostre o pais e a data calculada de 7  dias antes o ultimo dia do mes de fevereiro do ano de independencia
````
SELECT 
    name,
    indep_year,
    DATE_ADD(LAST_DAY(MAKEDATE(indep_year, 34)),
        INTERVAL - 7 DAY) - '7 ultimo dia de fevereiro'
FROM
    country
````
#### 43 Crie uma consulta que concatene o nome do país e da cidade
````
select country.name as país, count(city.name) as contagem_cidades,
group_concat(country.name, ' - ' ,city.name separator ' | ') as cidadePaisConcat
from country
join city
on country.code = city.country_code
GROUP BY country_code
````
#### 44 Crie uma consulta que concatene o nome do país e da cidade
````
select country.name as país, count(city.name) as contagem_cidades,
group_concat(country.name, ' - ' ,city.name separator ' | ') as cidadePaisConcat
from country
join city
on country.code = city.country_code
GROUP BY country_code

-- ou 

select country.name as país, count(city.name) as contagem_cidades,
group_concat(city.name separator ' | ') as cidadePaisConcat
from country
join city
on country.code = city.country_code
GROUP BY country_code;
````
#### 45 Substitua o nome de uma das cidades da Europa por São Paul   --> pesquisar melhor isso.
````
UPDATE city
SET name = 'São Paulo'
WHERE name = 'Kabul'; 
````
#### 46 Encontre qual o maior nome de cidade da Ásia
````
SELECT 
    Distinct(LENGTH(city.name)) AS contagem, city.name, country.continent
FROM city
JOIN country
where continent = 'Asia'
ORDER BY contagem DESC
Limit 3;
````
#### 47 Crie uma regra que avalie a quantidade de habitantes de uma localidade. Se essa localidade possuir mais de 5 milhões de habitantes, retorne como "Populosa".  Se for menor que 5 milhões de habitantes, retorne como "Ainda tem espaço"
````
select name as cidade , population as qtd_pessoas , 
	(Select case
	when population > 5000000 then 'Populosa'
    when population < 5000000 then 'Ainda tem espaço'
    end) as retorno
from city
order by qtd_pessoas Desc;
````
#### 48 Calcule a população de cada continente E Mostre a população dos continentes por ordem decrescente
````
select sum(city.population) as contagem_pop,country.continent from city
join country
on city.country_code = country.code
group by continent
order by  contagem_pop desc;
````
#### 49 Encontre os 5 distritos mais populosos do mundo
````
select district, population from city
order by population desc
limit 5;
````
#### 50 Buscar os nomes dos distritos com população maior que 10 milhões de habitantes
````
select district, population from city
order by population desc
limit 5;
````
#### 51 Crie uma tabela simples, contendo 3 colunas de texto e 3 colunas numéricas. Os tamanhos dos campos podem ser diversos
````

CREATE TABLE clientes (
    id_cliente INTEGER AUTO_INCREMENT PRIMARY KEY,
    nome_cliente VARCHAR(80) NOT NULL,
    endereço_cliente VARCHAR(20)  NOT NULL,
    telefone_cliente INTEGER NOT NULL,
    sexo VARCHAR(30) NOT NULL,
    email_cliente VARCHAR(100) UNIQUE NOT NULL,
    cpf_cliente INTEGER  NOT NULL
);
    
````
#### 52 Inclua uma coluna na tabela
   
````
Alter table clientes
    add column nome_conjuge varchar(200);
````
#### 53 Elimine a tabela que criou por completo
````
    DROP table clientes;
````
