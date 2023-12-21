# ��������� ������ � 2
� ��������� ��ᒺ���� ��������� �������������� �� ����: �LINQ�

## ���������� ����ײ

1.	��������� ����������: github.com/IlonaShevchenko/Practice_Linq.git 
2.	��������� ���������� ������ Query1(), Query2(), ..., Query10(), ������� ��� ������ ����� � �����. �������� (������ ��� ���������) ���. � ������ ��������� �� ������� ������. ��� ������ � ������� ����� �� ���� ����������� ���� �� ����� ���������� ������ (������� ���������� ������ ���. ���� output.txt).
3.	��� ������ �� ���� ��������� ������� ��������� � ��������� ���������. ϳ��� ��������� ������� ������ QueryN() ��������� ������ ����, �������� ����� N ������������ ������.
4.	��������Readme.md ����. 

## �̲�� �²��
-	��������� ����� 
-	���������� �������� 
-	��������� ������ (������� ������������ ������ � ���� ��������� �� ��������� LINQ) 
-	��� �������� 
-	��������� ������ �������� 
-	������ ���������� ����������

## ղ� ������
**��������� ������**
1.	������� �� �����, �� �������� � ����� � 2012 ����.
```
var selectedGames = games.Where(UKgameIN2012 => UKgameIN2012.Country == "Ukraine" && UKgameIN2012.Date.Year == 2012);
```

2.	������� Friendly ����� ����� ���볿, �� ���� ������� � 2020 ����.
```
var selectedGames = games.Where(FrgameIT2020 => FrgameIT2020.Tournament == "Friendly" && FrgameIT2020.Date.Year >= 2020 && (FrgameIT2020.Home_team == "Italy" || FrgameIT2020.Away_team == "Italy"));
```
3.	������� �� ������ ����� ����� ������� �� 2021 ��, �� ���� ������ � ����.
```
var selectedGames = games.Where(DrawFRgame2021 => DrawFRgame2021.Date.Year == 2021 && DrawFRgame2021.Country == "France" && (DrawFRgame2021.Home_team == "France") && DrawFRgame2021.Home_score == DrawFRgame2021.Away_score);
```
4.	������� �� ����� ����� ������ � 2018 ���� �� 2020 �� (�������), � ���� ���� �� ���� ��������.
```
var selectedGames = games.Where(DEgame18_20LOSER => DEgame18_20LOSER.Date.Year >= 2018 && DEgame18_20LOSER.Date.Year <= 2020 && DEgame18_20LOSER.Away_team == "Germany" && DEgame18_20LOSER.Home_score > DEgame18_20LOSER.Away_score);
```
5.	������� �� ������������ ����� (UEFA Euro qualification), �� �������� � ��� �� � ������, � ����� �� ����� �������� ��������� �����.
```
var selectedGames = games.Where(UK_Win_Cvalification_UEFA => UK_Win_Cvalification_UEFA.Tournament == "UEFA Euro qualification" && (UK_Win_Cvalification_UEFA.City == "Kyiv" || UK_Win_Cvalification_UEFA.City == "Kharkiv") && UK_Win_Cvalification_UEFA.Home_team == "Ukraine" && UK_Win_Cvalification_UEFA.Home_score > UK_Win_Cvalification_UEFA.Away_score);
```
6.	������� �� ����� ���������� ��������� ���� � ������� (FIFA World Cup), ��������� � ������������.
```
var selectedGames = games.Where(LSTWrldCUP => LSTWrldCUP.Tournament == "FIFA World Cup").OrderByDescending(u => u.Date).Take(8);
```
7.	������� ������ ���� � 2023 ����, � ����� ����� ������ �������.
```
FootballGame g = games.FirstOrDefault(FSTgameUKwinIN2023 => FSTgameUKwinIN2023.Date.Year == 2023 && ((FSTgameUKwinIN2023.Away_team == "Ukraine" && FSTgameUKwinIN2023.Away_score > FSTgameUKwinIN2023.Home_score) || (FSTgameUKwinIN2023.Home_team == "Ukraine" && FSTgameUKwinIN2023.Home_score > FSTgameUKwinIN2023.Away_score)));
```
8.	����������� �� ����� ����-2012 (UEFA Euro), �� �������� � �����, �� ����� � ���������� �������������.
```
var selectedGames = games.Where(Convertation => Convertation.Tournament == "UEFA Euro" && Convertation.Date.Year == 2012 && Convertation.Country == "Ukraine").Select(x => new
{
    MatchYear = x.Date.Year,
    Team1 = x.Home_team,
    Team2 = x.Away_team,
    Goals = x.Away_score + x.Home_score
});
```
9.	����������� �� ����� UEFA Nations League � 2023 ���� �� ����� � ���������� �������������.
```
var selectedGames = games.Where(convertUEFANL2023 => convertUEFANL2023.Tournament == "UEFA Nations League" && convertUEFANL2023.Date.Year == 2023).Select(x => new
{
    MatchYear = x.Date.Year,
    Game = $"{x.Home_team} - {x.Away_team}",
    Result = x.Home_score == x.Away_score ? "Draw" : (x.Home_score > x.Away_score ? "Win" : "Loss")
});
```
10.	������� � 5-�� �� 10-��� (�������) ����� Gold Cup, �� �������� � ���� 2023 �.
```
var selectedGames = games.Where(GoldCUPgameJULY2023 => GoldCUPgameJULY2023.Tournament == "Gold Cup" && GoldCUPgameJULY2023.Date.Year == 2023 && GoldCUPgameJULY2023.Date.Month == 7).Skip(4).Take(6);
```

**��� ��������**
[����������� ���](src/Program.cs)

**��������� ������ ��������**
��������� ������ 1-5 �� �����
![1-5](https://github.com/Yarik-Za/OOP_Linq_Practice_2/1-5.jpg)

��������� ������ 6-10 �� �����
![6-10](https://github.com/Yarik-Za/OOP_Linq_Practice_2/6-10.png)

### ������ ���������� ���������� 
https://github.com/Yarik-Za/OOP_Linq_Practice_2