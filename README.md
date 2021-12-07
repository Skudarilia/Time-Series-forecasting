# Time-Series forecasting
## 7 способов прогнозирования временных рядов

  Мы рассмотрим проблему, связанную с прогнозированием количества пассажиров JetRail, нового высокоскоростного железнодорожного сервиса от Unicorn Investors. 
  
  Нам предоставляются данные за 2 года (август 2012 г. - сентябрь 2014 г.), и с помощью этих данных мы должны прогнозировать количество пассажиров на ближайшие 7 месяцев.
  Первые 14 месяцев (август 2012 г. - октябрь 2013 г.) используются в качестве данных для __обучения__, а следующие 2 месяца (ноябрь 2013 г. - декабрь 2013 г.) - данные для __тестирования__.
____
  __Метод 1: Наивный подход__

Метод прогнозирования, который предполагает, что следующая ожидаемая точка равна последней наблюдаемой точке.
____
  __Метод 2: Простое среднее__

Метод прогнозирования, который прогнозирует ожидаемое значение, равное среднему значению всех ранее наблюдаемых точек.
____  
  __Метод 3: Скользящее среднее__

Использование цен начального периода сильно повлияет на прогноз на следующий период. Поэтому в качестве улучшения по сравнению с простым средним мы возьмем среднее значение цен только за последние несколько периодов времени. Очевидно, что мысль здесь заключается в том, что важны только последние цены. Методика прогнозирования, которая использует период времени для расчета среднего.
____  
  __Метод 4: Простое экспоненциальное сглаживание__

Прогнозы рассчитываются с использованием средневзвешенных значений, в которых веса экспоненциально уменьшаются по мере того, как наблюдения уходят в прошлое, наименьшие веса связаны с самыми старыми наблюдениями:

![image](https://user-images.githubusercontent.com/55200466/145033813-90b79c01-3810-4363-9bbd-333f89cd3ddd.png)

где 0≤ α ≤1 - параметр сглаживания. Прогноз на один шаг вперед для времени T + 1 является средневзвешенным значением всех наблюдений в серии y1,…, yT. Скорость, с которой снижаются веса, определяется параметром α.
____  
  __Метод 5: Метод линейного тренда Холта__

Каждый набор данных временного ряда может быть разложен на составляющие: тренд, сезонность и остаток. Любой набор данных, который следует за трендом, может использовать метод линейного тренда Холта для прогнозирования.
Холт расширил простое экспоненциальное сглаживание, чтобы позволить прогнозировать данные с трендом. Это не более чем экспоненциальное сглаживание, применяемое как к уровню (среднее значение в ряду), так и к тренду. Чтобы выразить это в математической записи, нам теперь нужно три уравнения: одно для уровня, одно для тренда и одно для объединения уровня и тренда, чтобы получить ожидаемый прогноз.

![image](https://user-images.githubusercontent.com/55200466/145034208-7006efd3-efea-4691-b1f1-1c9e9a21899c.png)

Значения, которые мы предсказали в вышеупомянутых алгоритмах, называются Уровнем. В приведенных выше трех уравнениях вы можете заметить, что мы добавили уровень и тренд для создания уравнения прогноза. Как и в случае простого экспоненциального сглаживания, уравнение уровня здесь показывает, что оно представляет собой средневзвешенное значение наблюдения и прогноз на один шаг впереди выборки. Уравнение тренда показывает, что оно представляет собой средневзвешенное значение оценочного тренда в момент времени t на основе ℓ (t) −ℓ (t − 1) и b (t − 1), предыдущей оценки тренда.
____  
  __Метод 6: Метод Холта-Винтера__

Метод Холта-Винтера будет лучшим вариантом среди остальных моделей из-за сезонности. Сезонный метод Холта-Винтера включает в себя уравнение прогноза и три уравнения сглаживания - одно для уровня ℓt, одно для тренда bt и одно для сезонной компоненты, обозначенной st, с параметрами сглаживания α, β и γ.

![image](https://user-images.githubusercontent.com/55200466/145034536-9e2adb6b-2e67-48da-bc75-4fd2c429bb0e.png)

где s - длина сезонного цикла, для 0 ≤ α ≤ 1, 0 ≤ β ≤ 1 и 0 ≤ γ ≤ 1.
Уравнение уровня показывает средневзвешенное значение между сезонно скорректированным наблюдением и несезонным прогнозом для времени t. Уравнение тренда идентично линейному методу Холта. Сезонное уравнение показывает средневзвешенное значение между текущим сезонным индексом и сезонным индексом того же сезона в прошлом году (т.е. периоды времени назад).
____  
  __Метод 7: ARIMA__

В то время как модели экспоненциального сглаживания основывались на описании тренда и сезонности в данных, модели ARIMA стремятся описать корреляции в данных между собой. Мы видим, что использование Seasonal ARIMA создает решение, похожее на метод Холта-Винтера.
____
  Мы можем сравнить эти модели на основе их баллов RMSE:
  
  ![image](https://user-images.githubusercontent.com/55200466/145034832-13ce42a9-6fee-4931-ba5a-9a4840e2881c.png)

  Как видно лучше всего подходят 2 модели для данного прогноза: __Метод Холта-Винтера__ и __ARIMA__
