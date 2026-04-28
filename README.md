# Умные ассистенты, агенты и многоагентные системы в Yandex Cloud

В этом репозитории содержится пример создания интеллектуального ассистента по продаже вин в Yandex Cloud, а также создания многоагентной системы для подбора ужина из основного блюда и вина на основе пожеланий пользователя. Мы по шагам рассматриваем следующие понятия:

### Умные ассистенты: [advanced-assistant.ipynb](advanced-assistant.ipynb)
* Использование языковых моделей в Yandex Cloud на базе Responses API и [OpenAI SDK](https://github.com/openai/openai-python) (в ранних версиях - на базе [Yandex Cloud ML SDK](https://github.com/yandex-cloud/yandex-cloud-ml-sdk))
* Простейшие ассистенты для поддержания контекста диалога
* Понятие [Function Calling](https://yandex.cloud/ru/docs/foundation-models/concepts/yandexgpt/function-call) в генеративных моделях и его использование с ассистентами
* Вызов удалённых функций на основе Model Context Protocol
* Подключение текстовой базы знаний (индекса) к модели для реализации RAG
* Умное чанкование и индексирование таблиц Markdown
* Реализация агента с документным индексом и поддержкой нескольких функций: поиск в базе данных, вызов оператора, добавление покупок в корзину
* Многоагентное тестирование модели с помощью диалога двух агентов
* Реализация телеграм-бота на основе ассистента, с поддержкой нескольких пользователей

### ReAct агенты
* Агенты и агентное взаимодействие в OpenAI Agents SDK - [adk.ipynb](adk.ipynb)
* ReAct-агенты в Smolagents - [code-agent.ipynb](code-agent.ipynb)

### Agentic Workflows: [langgraph-agent.ipynb](langgraph-agent.ipynb)
* Создание Agentic Workflow с помощью LangGraph поверх Responses API
* Тестирование Agentic Workflow с помощью фреймворка RAGAS

## Запуск примера

Для работы с примером рекомендуется:
* Клонировать репозиторий (на своём ноутбуке или в проекте Yandex Datasphere)
* Для авторизации в облаке:
  - Создать сервисный аккаунт, имеющий права `ai.editor`, `serverless.mcpGateways.anonymousInvoker` и `serverless.mcpGateways.invoker`
  - [ИЛИ] Получить для этого аккаунта ключ авторизации, сохранить его в файл `authorized_key.json` в домашнюю директорию проекта, в этот файл добавить поле `folder_id`
  - [ИЛИ] Получить для этого аккаунта API-ключ и установить в проекте датасферы секреты `folder_id`, `api_key` (либо установить соответствующие переменные окружения)
* Установить секрет `tg_token`, если вы планируете тестировать телеграм-бота
* Открыть соответствующий ноутбук [advanced-assistant.ipynb](advanced-assistant.ipynb) (Создание ассистента), [adk.ipynb](adk.ipynb) (Агенты в OpenAI Agent SDK), [langgraph-agent.ipynb](langgraph-agent.ipynb) (построение Agentic Workflow) и [code-agent.ipynb](code-agent.ipynb) (ReAct-агент на основе кодогенерации)
* Для работы MCP потребуется развернуть MCP-сервера одним из следующих способов:
  - На виртуальной машине, запустив код из этого репозитория:
    ```
    fastmcp run mcp-wine-shop.py -t sse -p 8000 --host 0.0.0.0`
    fastmcp run mcp-rest.py -t sse -p 8001 --host 0.0.0.0
    ```
  - На [FastMCP Cloud](https://fastmcp.cloud/), используя репозиторий [https://github.com/yandex-datasphere/advanced-assistant-mcp](https://github.com/yandex-datasphere/advanced-assistant-mcp). Необходимо развернуть два MCP-сервера, указав в качестве скрипта запуска `mcp-wine-shop.py` и `mcp-rest.py`
