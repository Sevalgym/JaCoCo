Задача №1 - Синдром 100% Легенда Вы попали в команду максималистов, которые хотят, чтобы те авто-тесты, которые вы пишете, покрывали код на 100%.

Но вот незадача:

Непонятно, что такое 100% Непонятно, как это сделать Вспоминаем: покрытием кода у нас занимается JaCoCo, но он просто "сигнализирует" о том, что конкретно пошло не так.

Большинство подобных плагинов помимо целей отчётности (report) содержат ещё цель check, которая обрушает сборку, если не выполнены определённые проверки.

Что вам нужно:

Изучить документацию на плагин (а конкретно на цель check) Внедрить эту цель в фазу verify (обратите внимание, что эта цель итак публикуется в эту фазу) Настроить правила по покрытию на 100% (при этом нужно изучить разницу между счётчиками INSTRUCTION, LINE, BRANCH, COMPLEXITY) Выбрать один из счётчиков и добиться 100% покрытия тестами Важно: использовать можно только один из следующих:

INSTRUCTION LINE BRANCH По шагам:

Скачиваете проект с лекции Мы просили плагин выполнить цель report для генерации отчёта, вам надо по аналогии с ним добавить ещё один execution, только не забыв заменить в нём report на check. Если не получается, см. как в подсказке ниже. Изучаете документацию, экспериментируете со счётчиками (INSTRUCTION, LINE, BRANCH) Выбираете один из счётчиков (на ваше усмотрение из первых трёх: INSTRUCTION, LINE, BRANCH) Запускаете, удостоверяетесь, что сборка падает, делаете push в GitHub (так, чтобы в логах осталось, что сборка падала в CI) Анализируете отчёт JaCoCo, смотрите что осталось непокрытым Дописываете тесты, чтобы обеспечить 100% по выбранному счётчику, делаете push в GitHub (так, чтобы в логах осталось, что сборка зелёная в CI) Итого: у вас должен быть репозиторий на GitHub, в котором расположен ваш Java-код.

Подсказка №1 Подсказка №2 (пример настройки) Важно: если вы используете Lombok, то покрытие сгенерированных им методов (например, getter/setter'ы тоже учитываются). Это не всегда бывает нужно.

Варианта тут два:

Вы читаете документацию на excludes, которая позволяет вам исключать целые классы из рассмотрения (не наш вариант) Игнорируете сгенерированные Lombok'ом методы (для этого создайте файл lombok.config в корне проекта со следующим содержимым: lombok.addLombokGeneratedAnnotation = true и не забудьте сделать mvn clean)