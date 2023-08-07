# Ayyads_portfolio
data analyst portfolio (video_games_analysis)

SELECT * FROM vcon

SELECT DISTINCT name, SUM(globalsales) AS copysales, AVG(userscore) AS avgscore, SUM(usercount) AS totalfeedback
FROM vcon 
WHERE year BETWEEN 2000 AND 2021
GROUP BY name
ORDER BY copysales DESC

SELECT DISTINCT publisher, SUM(globalsales) AS psales
FROM vcon
WHERE publisher IS NOT NULL
GROUP BY publisher
ORDER BY psales DESC
LIMIT 5

SELECT DISTINCT year, SUM(globalsales) AS total_sales
FROM vcon
WHERE year IS NOT NULL
GROUP BY year 
ORDER BY year 

SELECT DISTINCT year, SUM(globalsales) AS total_sales
FROM vcon
WHERE year IS NOT NULL
GROUP BY year 
ORDER BY total_sales DESC



SELECT * FROM vcon
WHERE platform IS NULL

SELECT DISTINCT platform, SUM(nasales) AS NA_SALES, SUM(eusales) AS EU_SALES, SUM(jpsales) AS JP_SALES, SUM(othersales) AS OTHER_SALES, SUM(globalsales) AS GLOBAL_SALES
FROM vcon
GROUP BY platform
ORDER BY GLOBAL_SALES DESC 
