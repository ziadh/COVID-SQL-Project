# COVID-19 Data Analysis SQL Queries

This repository contains SQL queries for analyzing COVID-19 data. The queries are designed to extract specific information from the `PortfolioProject..CovidDeaths` table and perform various calculations and comparisons. The queries provide insights into COVID-19 cases, deaths, population percentages, vaccination rates, and more. The skills demonstrated in this repository include SQL querying, data manipulation, aggregation, and joining.

## Queries


- Select Data that we are going to be starting with
```sql
SELECT *
FROM PortfolioProject..CovidDeaths
WHERE continent IS NOT NULL 
ORDER BY 3, 4
```

- Total Cases vs Total Deaths
- Shows likelihood of dying if you contract covid in your country
```

SELECT Location, date, total_cases, new_cases, total_deaths, population
FROM PortfolioProject..CovidDeaths
WHERE continent IS NOT NULL 
ORDER BY 1, 2
```



- Total Cases vs Population
- Shows what percentage of population infected with Covid
```

SELECT Location, date, total_cases, total_deaths, (total_deaths / total_cases) * 100 AS DeathPercentage
FROM PortfolioProject..CovidDeaths
WHERE location LIKE '%states%' AND continent IS NOT NULL 
ORDER BY 1, 2
```


- Countries with Highest Infection Rate compared to Population
```

SELECT Location, Population, MAX(total_cases) AS HighestInfectionCount, MAX((total_cases / population)) * 100 AS PercentPopulationInfected
FROM PortfolioProject..CovidDeaths
--WHERE location LIKE '%states%'
GROUP BY Location, Population
ORDER BY PercentPopulationInfected DESC
```




- Countries with Highest Death Count per Population
```

SELECT Location, MAX(CAST(Total_deaths AS INT)) AS TotalDeathCount
FROM PortfolioProject..CovidDeaths
--WHERE location LIKE '%states%'
WHERE continent IS NOT NULL 
GROUP BY Location
```


Note: The actual execution of these queries depends on the specific database structure and data availability. Please make sure to modify the queries according to your database schema and table names.

