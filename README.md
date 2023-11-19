# GeneticLab

Для начала был сгенерирован набор зашумленных данных без использования видеокарты.
Далее распишем непосредственно генетический алгоритм. В качестве генов выступают числа типа float - коэффициенты при соответствующей степени многочлена. Сам алгоритм не параллелится, так как каждая следующая итерация зависит от предыдущей. Однако, части этого алгоритма все же можно распараллелить. Далее это будет указано в соответствующих пунктах.

0. Генерация стартовой популяции
1. Кроссовер. Берем половину популяции с наилучшими результатами и формируем новую популяцию. Для этого случайным образом выбираем crosspoint и какая половина генов от какого родителя достанется. Далее формируем наследника. Данный фрагмент можно легко распараллелить, так как скрещивания происходят независимо друг от друга. Так, каждая нить будет формировать одного наследника.
2. Мутация. В качестве мутации мы будем просто увеличивать или уменьшать случайные гены и случайных индивидов на случайное число. Данный фрагмент нет смысла параллелить, так как количество мутаций мало по сравнению с объемом популяции.
3. Fitness. Далее вычисляем ошибку для каждой особи. Это фрагмент также легко параллелится - каждая нить будет вычислять fitness для своей особи.
4. Выбор лучшего варианта на текущей итерации.

В качестве погрешности использовался максимум среди модулей отклонения по точкам.
