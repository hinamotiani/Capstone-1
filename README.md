# Capstone-1
USE restaurant_ratings;
SELECT  Consumer_ID
FROM consumer_preferences;
SELECT DISTINCT Consumer_ID
FROM consumer_preferences;

SELECT *
FROM consumers;
-- How many restaurants allow drinking and smoking services?
SELECT * 
FROM restaurants;
SELECT *
FROM consumers;
SELECT *
FROM consumer_preferences;
SELECT DISTINCT Smoking_Allowed FROM restaurants;
SELECT DISTINCT Alcohol_Service FROM restaurants;
-- Ans
SELECT COUNT(Smoking_Allowed) AS number_of_smokers ,COUNT(*) AS number_of_drinkers
FROM restaurants 
WHERE Smoking_Allowed IN ("Yes","Smoking Section") OR Alcohol_Service IN ("Full Bar","Wine & Beer");

-- How many restaurants get low and high rating ?
SELECT Overall_Rating,COUNT(*)
FROM restaurants
INNER JOIN ratings
ON restaurants.ï»¿Restaurant_ID=ratings.Restaurant_ID
WHERE Overall_Rating IN (0,2)   
GROUP BY Overall_Rating;
-- How many restaurants get low and high rating and by which consumers?
SELECT Overall_Rating,COUNT(*)
FROM restaurants
INNER JOIN ratings
ON restaurants.ï»¿Restaurant_ID=ratings.Restaurant_ID
INNER JOIN consumers
ON ratings.ï»¿Consumer_ID=consumers.ï»¿Consumer_ID
WHERE Overall_Rating IN (0,2)
GROUP BY Overall_Rating;


-- Select all restaurants where public parking is available and their budget is low?
SELECT Name,Parking,Price
FROM restaurants
WHERE Parking="Public" AND Price ="Low";

-- What can you learn from the highest rated restaurants? Do consumer preferences have an effect on ratings?
SELECT Name,COUNT(Overall_Rating)
FROM restaurants;
SELECT * FROM ratings;
SELECT * FROM consumer_preferences;
SELECT MAX(Overall_Rating) FROM ratings;
-- ANs
SELECT Name,COUNT(Overall_Rating)
FROM restaurants
INNER JOIN ratings 
ON restaurants.ï»¿Restaurant_ID=ratings.Restaurant_ID
WHERE Overall_Rating=2 AND Food_Rating=2 AND Service_Rating=2
GROUP BY Name
ORDER BY COUNT(Overall_Rating) DESC;
