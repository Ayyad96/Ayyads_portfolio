# Ayyads_portfolio
First_Portfolio
data analyst portfolio (video_games_analysis)

/* Checking all of the columns available in the database */ 

SELECT * FROM vcon;

/* Selecting the highest selling video games in global market */ 

SELECT DISTINCT name, SUM(globalsales) AS copysales, AVG(userscore) AS avgscore, SUM(usercount) AS totalfeedback
FROM vcon 
GROUP BY name
ORDER BY copysales DESC;



<img width="635" alt="sum_of_global_sales_by_name" src="https://github.com/Ayyad96/Ayyads_portfolio/assets/140683898/8edfafff-950c-4fbd-8ce9-f53472482a51">




/* Selecting the highest selling video games in global market for the last 10 years */

SELECT DISTINCT name, SUM(globalsales) AS copysales, AVG(userscore) AS avgscore, SUM(usercount) AS totalfeedback
FROM vcon 
WHERE year BETWEEN 2010 AND 2020
GROUP BY name 
ORDER BY copysales DESC 
LIMIT 10;

/* Identifying the best video games that has the highest average score of user experience for the last 10 years */

SELECT name, AVG(userscore)
FROM vcon
WHERE userscore IS NOT NULL AND year >= 2010 AND year <= 2020
GROUP BY name
ORDER BY AVG(userscore) DESC
LIMIT 10;

/* Identifying the best publisher in terms of collecting the highest revenue in selling video games copies globally */

SELECT DISTINCT publisher, SUM(globalsales) AS psales
FROM vcon
WHERE publisher IS NOT NULL
GROUP BY publisher
ORDER BY psales DESC
LIMIT 5;

/* Identifying which year contributes to the highest selling of video games copies anually in this consoles games industry */

SELECT DISTINCT year, SUM(globalsales) AS total_sales
FROM vcon
WHERE year IS NOT NULL
GROUP BY year 
ORDER BY total_sales DESC;

/* Checking the selling rate by year of this industry globally */

SELECT DISTINCT year, SUM(globalsales) AS total_sales
FROM vcon
WHERE year IS NOT NULL
GROUP BY year 
ORDER BY year;

/* Getting more insight to identify the market pattern in the database by platform and year column */ 

SELECT * FROM vcon
WHERE platform IS NULL;

SELECT DISTINCT platform, SUM(nasales) AS NA_SALES, SUM(eusales) AS EU_SALES, SUM(jpsales) AS JP_SALES, SUM(othersales) AS OTHER_SALES, SUM(globalsales) AS GLOBAL_SALES
FROM vcon
GROUP BY platform
ORDER BY GLOBAL_SALES DESC;

/* Getting confused of a certain data under platform column, proceed making some research */

SELECT * FROM vcon WHERE platform = '2600';

/* Instead of getting the market trends through platform column only, had to expand on the company market trends throughout the upgraded and newest consoles gaming platform they created each and every year available */
/* Had to run a few research and proceeding to create a new column in the table based on the platform column in the vcon table */

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

 /* Jumping on the market trend of each platform for each company */

SELECT DISTINCT company, platform, SUM(globalsales)
FROM vcon 
GROUP BY company, platform
ORDER BY company, SUM(globalsales) DESC;

/* Based on the trend of each company each time a new upgraded version of console gaming platform, we saw a downfall in video games copies sales eventhough the company launch new upgraded version of gaming platform */
/* Seeing the market trend, this industry are moving towards market collapsing based on this data, however the data is having a bias and defect since we're getting a lot of null values and some of the year are missing in this dataseset */


