Title: FastAPI использование dependency_overrides 
Summary: Как замокать зависимости в FastAPI в автотестах
Date: 2024-01-26 16:00
Tags: python, fastapi, web, testing
Url: fastapi-mock-dependency
Slug: fastapi-mock-dependency

Всем привет!

Столкнулся с проблемой использования моков для автотестов в приложении **FastAPI**.

Есть клиент аутентификации, который используются во вьюхах. Попытки использовать **unittest.patch/monkeypatch** не произвели никакого эффекта. 
Но оказалось есть выход - использовать **dependency_overrides**. 

Вот как это можно использовать:

```
    async def authenticate(request: Request) -> Authentication:
    """ Основная функция для аутентификации, которую нужно замокать """
       ...
       return Authentication(**resp)
```

```
    async def _mock_authentication() -> Authentication:
    """ Переопределяет возвращаемое значение функции проверки сессии """
    data = {
        'user': 'test_user',
        ...
        'test': 'test'
    }
    return Authentication(**data)
```

```
    def create_test_app() -> FastAPI:
    """ Приложение для использование в тестах """
        app = FastAPI(title='app for tests')
        app.dependency_overrides[authenticate] = _mock_authentication
        ...
        return app
```