# DH-SQL-exercicios

#### Selecione o código dos países que falam português
````
select country_code from country_language
where language = "portuguese";
````

#### Selecione o nome das cidades com menos de 10.000 habitantes
````
select name from country
where population <10000;
````
#### Selecione o nome das cidades com até 10.000 habitantes
````
select name from country
where population <=10000;
````
#### Selecione os países com mais de 10 milhões de habitantes
````
select name from country
where population > 10000000;
````
#### Selecione o nome e a população dos países da Asia e Europa
````
select name, population from country
where continent = "Asia" or "Europe"
````
#### Selecione o nome dos estados brasileiros em ordem alfabética
````
select name from city
where country_code = 'BRA'
order by name
````
#### Liste os países de cada continente por ordem decrescente de PIB
````
select name,gnp from country
order by gnp desc
````
#### Encontre os 5 países com menor densidade populacional do mundo
````
select name,population from country
order by population ASC 
limit 5
````
#### Liste todos os países asiáticos com área maior que um milhão de kilômetros quadrados
````
select population,name,surface_area from country
where continent = "ASIA"
and surface_area > 1000000
order by name
````
#### Consulte os países que possuem um idioma oficial falado por menos de 10% de sua população, e liste seus códigos e tais idiomas.
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
#### Liste os países independentes há menos de 40 anos. 
````
select name, continent, indep_year, Year(curdate()) - indep_year as anos_indep  from country
where Year(curdate()) - indep_year < 40
````
#### Qual continente concentra a maior parte desses paises?
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
#### Liste os países com muito espaço! Para isso, vamos definir que esses países são os que têm menos de 10 pessoas por kilômetro quadrado ou que tem uma superfície maior que 8 milhões de metros quadrados.
````
select name, surface_area, population, population/surface_area as densidade
from country
where population/surface_area <10
or surface_area > 8000000
order by densidade Desc;
````
#### Vamos supor que a coluna GNP da tabela country guarde o PIB do ano de 2001, e que a coluna GNP_old guarde o PIB do ano 2000. Calcule a variação (em porcentagem) do PIB per cápita dos países da América. Você pode calcular a variação com a seguinte fórmula: variação = (valor_novo / valor_antigo - 1) * 100
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

