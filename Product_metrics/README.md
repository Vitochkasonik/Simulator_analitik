###  Анализ продуктовых метрик
**Задача 1:**    проанализировать и сравнить Retention двух групп пользователей:   
пришедших через платный трафик (source = 'ads') и пришедших через органические каналы (source = 'organic')   
 
**Реализация:**   
- [SQL запрос в Redash на расчёт Retention пользователей по разным группам трафика](https://github.com/Vitochkasonik/Simulator_analitik/blob/main/Product_metrics/Retention_2023_10_10.jpg)  
- [Создание визуализации](https://github.com/Vitochkasonik/Simulator_analitik/blob/main/Product_metrics/Retention_2023_10_10_chart.jpg)     
    
- Ответ на вопрос: отличается ли характер использования приложения у взятых групп пользователей будет положительный.    
    Отмечу, что характер использования приложений у групп пользователей, пришедших через разные виды трафика похож. Тренд нисходящий, со второго дня использования резко падает по количеству пользователей.    
    Интересно, что изначально количество пользователей пришедших по рекламным каналам выше, чем пришедших органически, но уже со второго дня соотношение меняется и сохраняется в течение всего исследуемого периода.
    В долгосрочной перспективе пользователи, которые пришли в приложение органическим путём, чаще становятся постоянными, конверсия органического источника выше.
    
**Задача 2:** проанализировать результат рекламной кампании, в результате которой в приложение пришло много новых пользователей.  Есть сомнение в качестве трафика, вопрос: то стало с рекламными пользователями в дальнейшем, как часто они продолжают пользоваться приложением?

**Реализация:**
Акция прошла 11.10.2023, считаем Retention для пользователей пришедших впервые в эту дату по рекламному трафику.  

- [SQL запрос](https://github.com/Vitochkasonik/Simulator_analitik/blob/main/Product_metrics/Retention_2023_10_11.jpg)
- [Визуализация](https://github.com/Vitochkasonik/Simulator_analitik/blob/main/Product_metrics/retention-%D0%B4%D0%BB%D1%8F-%D0%BA%D0%BE%D0%B3%D0%BE%D1%80%D1%82%D1%8B-11-10-23_chart.jpg)

  Даже визуально видно, что подавляющее большинство рассматриваемых пользователей больше в приложение не зашли.
  
- Дополнительно можно посмотреть сравнение метрики Retention для когорты следующего дня, пришедшей в приложение также по рекламному трафику:
  
  [Сравнение Retention](https://github.com/Vitochkasonik/Simulator_analitik/blob/main/Product_metrics/retention-11-10%20%D0%B8%2012-10.jpg)
  
  Отличия в характере Retention отчётливо заметны, данная рекламная акция не оправдывает затрат на рекламу.

   **Задача 3:** найти причины внезапного падения активности пользователей в приложении 20.10.2023.

  **Реализация:**
  - Смотрим данные по BI-системе (в данном случае наш основной дашборд в Superset), исключаем такие причины падения как неисправности у пользователей одной из операционных системы (падение есть и на iOS и на Android), потерю пользователей одного из источников трафика (падение произошло и среди пользователей, пришедших по рекламному пути, и по естественному), смотрим географию и видим падение произошло только у пользователей из России:
     
    [По географии](https://github.com/Vitochkasonik/Simulator_analitik/blob/main/Product_metrics/geografic.jpg)
  - Составляем SQL запрос и выводим список городов, пользователи из которых не смогли попасть в приложение 20.10.2023

     [SQL запрос](https://github.com/Vitochkasonik/Simulator_analitik/blob/main/Product_metrics/SQL_cities.jpg)
  
### Основная идея: для ответов на подобные вопросы удобно использовать и BI-систему, и SQL запросы - оба инструмента дополняют возможности друг друга
