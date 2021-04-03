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
select city.name, country.name from city
join country
ON city.country_code = country.code;
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
