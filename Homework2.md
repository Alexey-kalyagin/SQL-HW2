USE HomeWork2;

CREATE TABLE HomeWork2.movies
(
`guid` INT NOT NULL AUTO_INCREMENT,
`name_film` VARCHAR(45) NOT NULL,
`released` INT NOT NULL,
`genre` VARCHAR(45) NOT NULL,
`Studios_UniqueID` VARCHAR(45) NOT NULL, 
`director`  VARCHAR(45) NOT NULL,
PRIMARY KEY (`guid`)
);

SELECT Studios_UniqueID as studio
FROM movies;

INSERT INTO `HomeWork2`.`movies` 
(`guid`, `name_film`, `released`, `genre`, `Studios_UniqueID`, `director`)
VALUES ('1', 'Голодные игры', '2012', 'фантастика, триллер', 'Lionsgate', 'Гэри Росс');
INSERT INTO `HomeWork2`.`movies`
(`guid`, `name_film`, `released`, `genre`, `Studios_UniqueID`, `director`)
VALUES ('2', 'Кот Барсик', '2022','мультфильм', 'Союзмультфильм', 'Андрей Колпин');
INSERT INTO `HomeWork2`.`movies`
(`guid`, `name_film`, `released`, `genre`, `Studios_UniqueID`, `director`)
VALUES ('3', 'Ламборгини: человек-легенда', '2022','биография, драма', 'Lambofilm, Zian Films', 'Роберт Мореско');
INSERT INTO `HomeWork2`.`movies`
(`guid`, `name_film`, `released`, `genre`, `Studios_UniqueID`, `director`)
VALUES ('4', 'Прибытие', '2016','фантастика, драма', 'Paramount Pictures', 'Дени Вильнёв');

SELECT * From HomeWork2.movies;

DELETE FROM movies 
WHERE guid = 2;
DELETE FROM movies 
WHERE guid = 3;

INSERT INTO `HomeWork2`.`movies`
(`guid`, `name_film`, `released`, `genre`, `Studios_UniqueID`, `director`)
VALUES ('2', 'Апгрейд', '2018','триллер, боевик', 'Blumhouse Productions', 'Ли Уоннелл');
INSERT INTO `HomeWork2`.`movies`
(`guid`, `name_film`, `released`, `genre`, `Studios_UniqueID`, `director`)
VALUES ('3', 'Аватар', '2009','фантастика, боевик', '20th Century Fox, Lightstorm Entertainment', 'Джеймс Кэммерон');

ALTER TABLE HomeWork2.movies ADD COLUMN budget INT;
ALTER TABLE HomeWork2.movies ADD COLUMN box_office INT;
ALTER TABLE HomeWork2.movies ADD COLUMN commentary VARCHAR(20);

UPDATE HomeWork2.movies SET budget = '78000000'
WHERE guid = '1';
UPDATE HomeWork2.movies SET box_office = '694394724'
WHERE guid = '1';

UPDATE HomeWork2.movies SET budget = '5000000'
WHERE guid = '2';
UPDATE HomeWork2.movies SET box_office = '16593554'
WHERE guid = '2';

UPDATE HomeWork2.movies SET budget = '23700000'
WHERE guid = '3';
UPDATE HomeWork2.movies SET box_office = '292370602'
WHERE guid = '3';

UPDATE HomeWork2.movies SET budget = '47000000'
WHERE guid = '4';
UPDATE HomeWork2.movies SET box_office = '203388186'
WHERE guid = '4';

SELECT box_office, budget, commentary,
CASE 
	WHEN box_office/budget > 5 THEN 'БЛОКБАСТЕР'
	WHEN box_office/budget > 3 THEN 'Хороший сбор'
	WHEN box_office/budget > 2 THEN 'Окупился'
	else 'Провалился в прокате'
END AS commentary
FROM movies;

CREATE TABLE HomeWork2.studios
(
`UniqueID` INT NOT NULL AUTO_INCREMENT,
`name_studio` VARCHAR(45) NOT NULL,
`founder` VARCHAR(45) NOT NULL,
PRIMARY KEY (`UniqueID`)
);

INSERT INTO `HomeWork2`.`studios` 
(`UniqueID`, `name_studio`, `founder`)
VALUES ('1', 'Blumhouse Productions', 'Джейсон Блум');
INSERT INTO `HomeWork2`.`studios`
(`UniqueID`, `name_studio`, `founder`)
VALUES ('2', 'Lionsgate', 'Фрэнк Гистра');
INSERT INTO `HomeWork2`.`studios`
(`UniqueID`, `name_studio`, `founder`)
VALUES ('3', 'Paramount Pictures', 'Джим Янопулос');
INSERT INTO `HomeWork2`.`studios`
(`UniqueID`, `name_studio`, `founder`)
VALUES ('4', '20th Century Fox', 'Алан Бергман');
INSERT INTO `HomeWork2`.`studios`
(`UniqueID`, `name_studio`, `founder`)
VALUES ('5', 'Союзмультфильм', 'Юлиана Слащёва');
INSERT INTO `HomeWork2`.`studios`
(`UniqueID`, `name_studio`, `founder`)
VALUES ('6', 'Lightstorm Entertainment', 'Джеймс Кэмерон');

ALTER TABLE HomeWork2.studios ADD COLUMN net_profit INT;
ALTER TABLE HomeWork2.studios ADD COLUMN commentary VARCHAR(20);

SELECT * FROM HomeWork2.studios;

UPDATE HomeWork2.studios SET net_profit = '422000000'
WHERE UniqueID = '1';
UPDATE HomeWork2.studios SET net_profit = '615000000'
WHERE UniqueID = '2';
UPDATE HomeWork2.studios SET net_profit = '621000000'
WHERE UniqueID = '3';
UPDATE HomeWork2.studios SET net_profit = '0'
WHERE UniqueID = '4';
UPDATE HomeWork2.studios SET net_profit = '1900000'
WHERE UniqueID = '5';
UPDATE HomeWork2.studios SET net_profit = '0'
WHERE UniqueID = '6';

SELECT name_studio, commentary,
IF (net_profit = 0, 'Данные о прибыли не известны', net_profit) AS 'Наличие прибыли'
FROM studios; 