# From Jack to Blender

Проект для курса Nand->Tetris. 
В рамках проекта сначала была идея разработать скринсейвер, но потом идея переросла в движок для 3D-рендера.
Для запуска необходимо открыть папку /vm в VMEmulator.

## Интерфейс:
При запуске приложения вы можете видеть название текущей просматриаемой фигуры и
собственно саму фигуру. Управление в сцене:
    1. Стрелочки влево-вправо: движение камеры по оси Y;
    2. Цифры: переключение фигур.
    
    (PgUp/PgDown и стрелочки вверх/вниз были выпилены из-за критической недопиленности
    и отсутствия возможности адекватно починить)
    
Доступные фигуры:
    1. Куб;
    2. Прямоугольный параллелипипед (не прямоугольник :) );
    3. Пирамида;
    4. Треугольная призма;
    5. Шестиугольная призма

## Trivia:
Как это дело работает?

Вся математика держится на классах Fraction (обыкновенные дроби) и 
PointVector3D (набор координат в пространстве). В свою очередь с помощью PV3D
реализован класс отрезка Segment, из которых состоят фигуры Shape (Array of Segment, в сущности).
    
Когда создаётся сцена с фигурой в ней, для каждого отрезка в фигуре проводится луч, соединяющий 
камеру и его концы. Затем вычисляются координаты точек пересечения этих лучей с плоскостью экрана.

Затем координаты точек в пространстве раскладываются по базису сторон экрана, приводятся в рамки
уже физического экрана платформы Hack, после чего используется Screen.drawLine(), чтобы нарисовать 
на экране проекцию отрезка. Так рисуются все отрезки фигуры и получается так называемый Wireframe Viewport, 
или же изображение фигуры без граней, только с рёбрами.

## Что интересное можно посмотреть?
Самое интересное находится в классах 

**Fraction**, где реализована логика дробей (и тысяча и одна фича, созданные 
в попытках обойти переполнение жалкого 16-тибитного инта XD ),

**PointVector3D**, где описана математика векторов, 

и **Scene**, где описан сам процесс рендера.
    
Код этих классов (особенно, само собой, Scene) местами плохо читаем из-за большого количества манипуляций 
над временными переменными и диспозами, но это сделано во избежание ошибок переполнения стека.

## Над проектом работали:

[Бойко Владимир](https://github.com/Xoka74),
[Федоров Иван](https://github.com/fed1v),
[Хрусталев Дмитрий](https://github.com/Daemetry)

_Stay sharp and math!_
