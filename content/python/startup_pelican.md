Title: Как я поднял блог с помощью Pelican
Summary: Моё первое впечатление от Pelican
Date: 2023-07-17 16:00
Tags: python, pelican, blog
Url: startup-pelican
Slug: startup-pelican

###Имеем на входе:
- Старый блог на Jekyll
- Уже готовый дизайн(html+css)
- Знания Python, Jekyll, Django и Jinja

<br/>

###Почему я выбрал Pelican:
- Свежий проект, сообщество активно контрибьютит
- Страницы генерируются на основе markdown, как и Jekyll
- В темплейтах используется Jinja2

<br/>

###Мой HowTo:
1.) Делаем первый шаг [**отсюда**](https://docs.getpelican.com/en/latest/install.html). Устанавливаем Pelican, дополнительные пакеты и выполняем:

```
    pelican-quickstart
```

2.) После создания минимальной структуры проекта я полез в *pelicanconf.py*. Помимо основных настроек я прописал свой, к примеру TELEGRAM_USERNAME. Вид моего конфига:

```
    AUTHOR = "dkurchigin"
    SITENAME = "Типичный Python разработчик"
    SITESUBTITLE = "О программировании, мелочах жизни и многом другом..."
    SITEURL = "https://dkurchigin.github.io/"
    PATH = "content"
    TIMEZONE = "Europe/Moscow"
    DEFAULT_LANG = "Russian"
    TELEGRAM_USERNAME = "dirty_rotten_imb"
    GITHUB_USERNAME = "dkurchigin"
    EMAIL = "kurchigin.dmitry@yandex.ru"
    DEFAULT_PAGINATION = 10
    THEME = ""
``` 

3.) Для смены стандартной схемы создал [**следующую структуру**](https://docs.getpelican.com/en/latest/themes.html#structure) в корне проекта

![pelican_structure]({static}/theme/images/pelican_structure.JPG)

4.) Подсмотреть базовый синтаксис и логику темплейтов можно в [**стандартной теме**](https://github.com/getpelican/pelican/tree/master/pelican/themes).

5.) Для локального дебага делаю **make html**, а затем **make serve**.

6.) Для публикации на **Github Pages** делаю так:

```
    make html
    ghp-import output -b gh-pages
    git push origin gh-pages
```

7.) В настройках репозитория во вкладке **Pages** указываю, что необходимо забирать контент из ветки **gh-pages**:

![github_pages_settings]({static}/theme/images/github_pages_settings.JPG)

8.) **ENJOY!**