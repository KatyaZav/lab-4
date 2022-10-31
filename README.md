# Доработка интерактивного приложения и его подготовка к сборке.
Отчет по лабораторной работе #4 выполнила:
- Завьялова Екатерина Николаевна
- РИ300023
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения.
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения.
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения.
- Выводы.

## Цель работы
интеграция интерфейса пользователя в разрабатываемое интерактивное приложение.

## Задание 1
### Используя видео-материалы практических работ 1-5 повторить реализацию приведенного ниже функционала:
1) Практическая работа «Создание анимации объектов на сцене»
2) Практическая работа «Создание стартовой сцены и переключение
между ними»
3) Практическая работа «Доработка меню и функционала с остановкой
игры»
4) Практическая работа «Добавление звукового сопровождения в игре»
5) Практическая работа «Добавление персонажа и сборка сцены для
публикации на web-ресурсе»

Ход работы:
1) Дбавить анимацию вагонетки.

Этот пункт был выполнен в самой первой лабораторной работе. Была добавлена анимация вагонетки и восклицательного знака.

![Фото](https://github.com/KatyaZav/lab-4/blob/main/Screens/1%20task/1.gif)

2) Создать стартовую сцену и добавить перемещение между сценами.

Для простоты кода я сделала отдельный класс MainMenu, тут будут функции паузы, переключения сцен, настройка звука.
Сейчас напишу реализацию переключения между сценами:

```c#
public class MainMenu : MonoBehaviour
{

    AudioSource manager;
    public static float VolumeMusic=1;
    public static float VolumeSounds=1;

    private void Start()
    {
        manager = GetComponent<AudioSource>();
    }
    public void LoadScene(int number)
    {
        Statistics.EndGame();
        SceneManager.LoadScene(number);
    }
}
```

Итого все выглядит так:

![Видео](https://github.com/KatyaZav/lab-4/blob/main/Screens/1%20task/2.gif)

3) Создание механики паузы
Добавлю в скрипт метод паузы.

```c#
public void MakePause(bool isPause)
    {
        if (isPause)
            Time.timeScale = 0;
        else
            Time.timeScale = 1;
    }
```

Главное не забыть добавить этот скрипт кнопке.

![Видео](https://github.com/KatyaZav/lab-4/blob/main/Screens/1%20task/3.gif)

4) Добавить звук и мелодию.

Сначала эти звуки надо найти. Я искала их в открытых и бесплатных источниках (не асетах юнити). 

Потом надо добавить элементам эти звуки, но к сожалению звуки тут не слышны...

![Видео](https://github.com/KatyaZav/lab-4/blob/main/Screens/1%20task/4.1.jpg)

Важно: для задания 3 придется полностью переделывать систему звука, если об этом не позаботиться заранее! Я сделала пустой элемент, который в определенных условиях будет производить нужный звук. Этот элемент будет помечен определенным тегом. Музыка будет в камере (она есть на всех сценах и у нее есть свой тег).

```c#
public class SoundManager : MonoBehaviour
{
    [SerializeField] AudioClip ButtonClick;
    [SerializeField] AudioClip GoldCatched;
    [SerializeField] AudioClip GoldDrop;

    [SerializeField]AudioSource sourse;

    void Start()
    {
        sourse = GetComponent<AudioSource>();

        Statistics.UpdateGameCount += Count;
        Statistics.LosedPoint += Lose;
    }

    private void Count(int x)
    {
        sourse.PlayOneShot(GoldCatched);
    }

    private void Lose()
    {
        sourse.PlayOneShot(GoldDrop);
    }

    public void ButtonSound()
    {
        sourse.PlayOneShot(ButtonClick);
    }
}
```

![Видео](https://github.com/KatyaZav/lab-4/blob/main/Screens/1%20task/4.2.gif)

5) Cделать билд сцен.

Добавлять персонажа на сцену мне не нужно, поэтому перейду к созданию билда. Перехожу в Build Settings, и запускаю процесс билда.

![Видео](https://github.com/KatyaZav/lab-4/blob/main/Screens/1%20task/5.jpg)


## Задание 2
### Привести описание того, как происходит сборка проекта проекта под другие платформы. Какие могут быть особенности?

Ход работы:
1) Посмотреть какие бывают стандартные сборки:
- Мобильное устройства
- Веб
- ПК

Из неосновных:
- VR
- PS4, например

Каждый из этих варантов запускается только на определенном устройстве (для веба нужен сервер, для запуска надо загрузить на платформу или выбрать "build and run").

![фото](https://github.com/KatyaZav/lab-4/blob/main/Screens/2%20task/1.jpg)

## Задание 3
### Добавить в меню Option возможность изменения громкости (от 0 до 100%) фоновой музыки в игре.

Ход работы:
1) Дополнить код класса для слайдера-настройки звукового проигрывателя.

```c#
public class _Slider : MonoBehaviour
{
    Slider slider;
    public bool isMusic;

    MainMenu soundManager;

    private void OnEnable()
    {
        if (slider == null)
            Start();

        //Debug.Log("enable");
        if (isMusic)
            slider.value = MainMenu.VolumeMusic;
        else
            slider.value = MainMenu.VolumeSounds;
    }

    void Start()
    {
        soundManager = GameObject.FindGameObjectWithTag("SoundManager").GetComponent<MainMenu>();
        slider = GetComponent<Slider>();

        if (isMusic)
            slider.value = MainMenu.VolumeMusic;
        else
            slider.value = MainMenu.VolumeSounds;
    }

    public void UpdateSoundsVolume()
    {
        MainMenu.VolumeSounds = slider.value;
        soundManager.UpdateVolume();
    }

    public void UpdateMusicVolume()
    {
        MainMenu.VolumeMusic = slider.value;
        soundManager.UpdateVolume();
    }
}
```

Осталось все скрипты повесить на объекты.

![фото](https://github.com/KatyaZav/lab-4/blob/main/Screens/3%20task/1.gif)

## Выводы

Я попыталась сделать базовую навигацию кнопок, научилась работать со звуками и музыкой, поработала со слайдерами.

Так же я посмотрела возможные платформы для билда.

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
