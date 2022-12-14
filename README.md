# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #5 выполнил:
- Гусамов Артур Филаритович
- РИ210950
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
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
Интеграция экономической системы в проект Unity и обучение ML-Agent

## Подготовка к лабораторной работе
- Создать виртуальное пространство![image](https://user-images.githubusercontent.com/102403656/206916820-9759662e-c4ff-4505-be42-d695d6c20a52.png)![image](https://user-images.githubusercontent.com/102403656/206916838-71fe568e-3ba7-4bfb-b10e-a29d74732ac3.png)
- Активировать пространство![image](https://user-images.githubusercontent.com/102403656/206916903-d2a0c904-c937-49ab-ae14-cdfead80663e.png)
- Установить нужные пакеты командами:
  - pip install mlagents==0.28.0
  - pip install torch~=1.7.1 -f https://download.pytorch.org/whl/torch_stable.html
- Перейти в папку с проектом и запустить MLAgent![image](https://user-images.githubusercontent.com/102403656/206923625-d5526800-e004-4e82-bd9e-8d6d0043d841.png)
- Запускаем сцену в Unity и наблюдаем за обучением![image](https://user-images.githubusercontent.com/102403656/206923707-767b9794-405d-4cfa-91d8-2e3cf02ea0c3.png)
- Устанавливаем и запускаем TensorFlow![image](https://user-images.githubusercontent.com/102403656/207005496-c162d5af-310b-4ce9-9b95-03116995161a.png)![image](https://user-images.githubusercontent.com/102403656/207005605-9fde31e6-5687-403d-9178-344181850f89.png)


## Задание 1
### Измените параметры файла. yaml-агента и определить какие параметры и как влияют на обучение модели.
- Cтартовые значения и результат:
	 ```c#
	behaviors:
	  Economic:
	    trainer_type: ppo
	    hyperparameters:
	      batch_size: 1024
	      buffer_size: 10240
	      learning_rate: 3.0e-4
	      learning_rate_schedule: linear
	      beta: 1.0e-2
	      epsilon: 0.2
	      lambd: 0.95
	      num_epoch: 3      
	    network_settings:
	      normalize: false
	      hidden_units: 128
	      num_layers: 2
	    reward_signals:
	      extrinsic:
		gamma: 0.99
		strength: 1.0
	    checkpoint_interval: 500000
	    max_steps: 750000
	    time_horizon: 64
	    summary_freq: 5000
	    self_play:
	      save_steps: 20000
	      team_change: 100000
	      swap_steps: 10000
	      play_against_latest_model_ratio: 0.5
	      window: 10
	```
	![image](https://user-images.githubusercontent.com/102403656/207007066-5edb63f0-fc57-4e3b-94e6-e52d24c18a72.png)
	![image](https://user-images.githubusercontent.com/102403656/207007111-d96d6520-904d-488d-b321-983df301b2d1.png)
- Далее я пробовал изменять, как мне показалось, наиболее весомые значения:

Economics1
```
learning_rate: 2.0e-4
gamma: 0.4
strength: 0.4
```
Economics2
```
lambd: 0.1
num_epoch: 6
num_layers: 15
summary_freq: 10000
```
Economics3
```
batch_size: 2048
buffer_size: 5000
epsilon: 0.5
```
![image](https://user-images.githubusercontent.com/102403656/207023581-6dfd5b6f-ee75-4acc-8b9e-0019cd14c2bb.png)
![image](https://user-images.githubusercontent.com/102403656/207023657-1dd45da1-301f-4c3e-b194-a97ecd946a16.png)

## Задание 2
### Опишите результаты, выведенные в TensorBoard.
- Cumulative Reward. Это график общего вознаграждения, к максимизированию которого и стремиться MLAgent
- Episode Length. По большому показывает, какова была длина эпизодов при обучении. Чем короче, тем быстрее было произведено обучение
- Politic loss. Показывает величину изменение политики(траектории) обучения
- Value loss. Моделирует, как хорошо MLAgent прогнозирует своё будущее значение
- Policy. Графики в группе Policy отвечают за оценку кацчества действий
## Выводы

В ходе выполнения лаб. работы я научился сравнивать и анализировать результирующие данные из работы самообучаемой модели, освежил знания по работе с MLAgent-ом

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
