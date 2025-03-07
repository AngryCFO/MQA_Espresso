Домашнее задание к занятию «2.5. Espresso»
В рамках выполнения задания сделано:
Задание. Реализация теста на проверку главного экрана
Склонирован и запущен тестовый проект в Android Studio.

Добавлены необходимые зависимости в файл /app/build.gradle в блок dependencies {:

testImplementation 'junit:junit:4.13.2'
androidTestImplementation 'androidx.test.ext:junit:1.1.3'
androidTestImplementation 'androidx.test:rules:1.4.0'
androidTestImplementation 'androidx.test:runner:1.4.0'
androidTestImplementation 'androidx.test.espresso:espresso-core:3.4.0'
При возникновении проблем с запуском приложения был разрешен конфликт в структуре проекта (Project Structure) путем обновления следующих версий. Обновления были необходимы для обеспечения совместимости и стабильной работы приложения:
Android Gradle Plugin Version 7.4.2
Gradle Version 7.5
Создан новый класс в директории /app/src/androidTest/java/ru/abujor/simpleappforespresso/.

Добавлено аннотирование @RunWith над именем класса для указания на использование AndroidJUnit в тестах.

@RunWith(AndroidJUnit4.class)
public class ...
Задано правило MainActivity внутри класса. Вместо ActivityTestRule использован ActivityScenarioRule, чтобы облегчить управление состоянием активности и улучшить совместимость с новыми версиями Android. Это также позволяет более эффективно тестировать жизненный цикл активности.
@Rule
public ActivityScenarioRule<MainActivity> activityRule =
new ActivityScenarioRule<>(MainActivity.class);
Для написания теста было запущено приложение, после чего проведен анализ иерархии элементов с помощью Layout Inspector, в результате которого был обнаружен элемент с текстом This is home fragment и его ID.

Написан тест, проверяющий, что у найденного ID текст This is home fragment.

Вынесен текст кода в отдельную переменную, что улучшит читаемость кода и облегчит его поддержку. Если нужно будет изменить текст в будущем, это можно сделать это в одном месте, а не искать его по всему коду.
private static final String homeFragmentText = "This is home fragment";
Использование private static final String обеспечит неизменяемость значения, что повысит безопасность кода и уменьшит вероятность ошибок, связанных с изменением текста в разных местах.

Во время попытки запуска теста через консоль в режиме сборщика Gradle была успешно решена проблема с правами доступа к файлу gradlew путем выполнения команды:
chmod +x ./gradlew
Запущен тест в режиме сборщика Gradle, проверено его успешное завершение.
./gradlew connectedAndroidTest
Запущен тест, нажав кнопку запуска возле метода теста, произведен экспорт отчета теста в HTML-файл, отчёт добавлен в issues репозитория.

Для покрытия большинства потребностей добавлен Allure Report

Установлен Allure на ПК для требований системы отчетов.
brew install allure
allure --version
Добавлена необходимая Allure зависимость в файл /app/build.gradle в блок dependencies {:
androidTestImplementation 'io.qameta.allure:allure-kotlin-android:2.4.0'
В тесте в аннотирование @RunWith(AndroidJUnit4.class) над именем класса добавленно Allure и сделан импорт:
@RunWith(AllureAndroidJUnit4.class)
Запущен тест, проверено его успешное завершение.
В Android Studio в разделе Device Explorer по пути data/data/имя_проекта/files найдена и выгружена в проект папка allure-results с генерируемым отчетом.
Для запуска отчета в консоли выполнена команда:
allure serve
Скриншот отчёта добавлен в issues репозитория.