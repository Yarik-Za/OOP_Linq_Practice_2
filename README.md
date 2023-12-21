# Практична робота № 2
з дисципліни «Об’єктно орієнтоване програмування» на тему: «LINQ»

## ПОСТАНОВКА ЗАДАЧІ

1.	Клонувати репозиторій: github.com/IlonaShevchenko/Practice_Linq.git 
2.	Необхідно реалізувати методи Query1(), Query2(), ..., Query10(), шаблони цих методів наявні в проєкті. Завдання (запити для реалізації) див. у вигляді коментарів до кожного методу. Крім запиту у кожному методі має бути реалізований вивід на екран результатів запиту (приклад оформлення виводу див. файл output.txt).
3.	Для проєкту має бути створений власний локальний і віддалений репозиторії. Після реалізації кожного методу QueryN() необхідно робити коміт, вказуючи номер N реалізованого запиту.
4.	ОформитиReadme.md файл. 

## ЗМІСТ ЗВІТУ
-	Титульний аркуш 
-	Постановка завдання 
-	Реалізація запитів (навести формулювання запиту і його реалізацію за допомогою LINQ) 
-	Код програми 
-	Результат роботи програми 
-	Адреса віддаленого репозиторію

## ХІД РОБОТИ
**Реалізація запитів**
1.	Вивести всі матчі, які відбулися в Україні у 2012 році.
```
var selectedGames = games.Where(UKgameIN2012 => UKgameIN2012.Country == "Ukraine" && UKgameIN2012.Date.Year == 2012);
```

2.	Вивести Friendly матчі збірної Італії, які вона провела з 2020 року.
```
var selectedGames = games.Where(FrgameIT2020 => FrgameIT2020.Tournament == "Friendly" && FrgameIT2020.Date.Year >= 2020 && (FrgameIT2020.Home_team == "Italy" || FrgameIT2020.Away_team == "Italy"));
```
3.	Вивести всі домашні матчі збірної Франції за 2021 рік, де вона зіграла у нічию.
```
var selectedGames = games.Where(DrawFRgame2021 => DrawFRgame2021.Date.Year == 2021 && DrawFRgame2021.Country == "France" && (DrawFRgame2021.Home_team == "France") && DrawFRgame2021.Home_score == DrawFRgame2021.Away_score);
```
4.	Вивести всі матчі збірної Германії з 2018 року по 2020 рік (включно), в яких вона на виїзді програла.
```
var selectedGames = games.Where(DEgame18_20LOSER => DEgame18_20LOSER.Date.Year >= 2018 && DEgame18_20LOSER.Date.Year <= 2020 && DEgame18_20LOSER.Away_team == "Germany" && DEgame18_20LOSER.Home_score > DEgame18_20LOSER.Away_score);
```
5.	Вивести всі кваліфікаційні матчі (UEFA Euro qualification), які відбулися у Києві чи у Харкові, а також за умови перемоги української збірної.
```
var selectedGames = games.Where(UK_Win_Cvalification_UEFA => UK_Win_Cvalification_UEFA.Tournament == "UEFA Euro qualification" && (UK_Win_Cvalification_UEFA.City == "Kyiv" || UK_Win_Cvalification_UEFA.City == "Kharkiv") && UK_Win_Cvalification_UEFA.Home_team == "Ukraine" && UK_Win_Cvalification_UEFA.Home_score > UK_Win_Cvalification_UEFA.Away_score);
```
6.	Вивести всі матчі останнього чемпіоната світу з футболу (FIFA World Cup), починаючи з чвертьфіналів.
```
var selectedGames = games.Where(LSTWrldCUP => LSTWrldCUP.Tournament == "FIFA World Cup").OrderByDescending(u => u.Date).Take(8);
```
7.	Вивести перший матч у 2023 році, в якому збірна України виграла.
```
FootballGame g = games.FirstOrDefault(FSTgameUKwinIN2023 => FSTgameUKwinIN2023.Date.Year == 2023 && ((FSTgameUKwinIN2023.Away_team == "Ukraine" && FSTgameUKwinIN2023.Away_score > FSTgameUKwinIN2023.Home_score) || (FSTgameUKwinIN2023.Home_team == "Ukraine" && FSTgameUKwinIN2023.Home_score > FSTgameUKwinIN2023.Away_score)));
```
8.	Перетворити всі матчі Євро-2012 (UEFA Euro), які відбулися в Україні, на матчі з наступними властивостями.
```
var selectedGames = games.Where(Convertation => Convertation.Tournament == "UEFA Euro" && Convertation.Date.Year == 2012 && Convertation.Country == "Ukraine").Select(x => new
{
    MatchYear = x.Date.Year,
    Team1 = x.Home_team,
    Team2 = x.Away_team,
    Goals = x.Away_score + x.Home_score
});
```
9.	Перетворити всі матчі UEFA Nations League у 2023 році на матчі з наступними властивостями.
```
var selectedGames = games.Where(convertUEFANL2023 => convertUEFANL2023.Tournament == "UEFA Nations League" && convertUEFANL2023.Date.Year == 2023).Select(x => new
{
    MatchYear = x.Date.Year,
    Game = $"{x.Home_team} - {x.Away_team}",
    Result = x.Home_score == x.Away_score ? "Draw" : (x.Home_score > x.Away_score ? "Win" : "Loss")
});
```
10.	Вивести з 5-го по 10-тий (включно) матчі Gold Cup, які відбулися у липні 2023 р.
```
var selectedGames = games.Where(GoldCUPgameJULY2023 => GoldCUPgameJULY2023.Tournament == "Gold Cup" && GoldCUPgameJULY2023.Date.Year == 2023 && GoldCUPgameJULY2023.Date.Month == 7).Skip(4).Take(6);
```

**Код програми**
[Переглянути код](src/Program.cs)

**Результат роботи програми**
Виведення запитів 1-5 на екран
![1-5](https://github.com/Yarik-Za/OOP_Linq_Practice_2/1-5.jpg)

Виведення запитів 6-10 на екран
![6-10](https://github.com/Yarik-Za/OOP_Linq_Practice_2/6-10.png)

### Адреса віддаленого репозиторію 
https://github.com/Yarik-Za/OOP_Linq_Practice_2