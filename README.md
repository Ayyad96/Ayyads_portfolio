# Ayyads_portfolio
data analyst portfolio (video_games_analysis)

SELECT * FROM vcon

SELECT DISTINCT name, SUM(globalsales) AS copysales, AVG(userscore) AS avgscore, SUM(usercount) AS totalfeedback
FROM vcon 
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

SELECT * FROM vcon WHERE platform = '2600'

ALTER TABLE vcon
ADD company VARCHAR(50);

UPDATE vcon
SET company =
	CASE 
		WHEN platform IN ('PS','PS2','PS3','PS4','PSP','PSV') THEN 'Sony'
		WHEN platform IN ('NES','SNES','N64','GC','Wii','WiiU','DS','3DS','GBA','GB') THEN 'Nintendo'
		WHEN platform IN ('XB','X360','XOne') THEN 'Microsoft'
		WHEN platform IN ('GEN','SCD','32X','SAT','DC','GG') THEN 'Sega'
		WHEN platform IN ('2600') THEN 'Atari'
		WHEN platform IN ('NG') THEN 'SNK'
		WHEN platform IN ('WS') THEN 'Bandai'
		WHEN platform IN ('TG16','PCFX') THEN 'NEC'
		WHEN platform IN ('3DO') THEN 'The 3DO Company'
		ELSE 'PC'
	END;
