## Описание playbook

Playbook устанавливает и настраивает:
- **ClickHouse** — колоночную СУБД
- **Vector** — агент для сбора и обработки логов
- **LightHouse** — веб-интерфейс для ClickHouse (через Nginx)

## Структура репозитория
playbook/
├── site.yml              # Основной playbook
├── inventory/
│   └── prod.yml          # Inventory production-окружения
├── group_vars/
│   ├── clickhouse/
│   │   └── vars.yml      # Переменные ClickHouse
│   ├── vector/
│   │   └── vars.yml      # Переменные Vector
│   └── lighthouse/
│       └── vars.yml      # Переменные LightHouse
└── templates/
└── nginx.conf.j2     # Шаблон конфигурации Nginx
plain

## Параметры

| Компонент | Параметры | Файл |
|-----------|-----------|------|
| ClickHouse | `clickhouse_version` | `group_vars/clickhouse/vars.yml` |
| Vector | `vector_version`, `vector_install_dir`, `vector_config_dir` | `group_vars/vector/vars.yml` |
| LightHouse | `lighthouse_vcs`, `lighthouse_dir` | `group_vars/lighthouse/vars.yml` |

## Теги

Playbook содержит три play:
- `Install Clickhouse` — группа `clickhouse`
- `Install Vector` — группа `vector`
- `Install Lighthouse` — группа `lighthouse`

## Как запустить

```bash
# Проверка синтаксиса
ansible-lint site.yml

# Прогон в режиме check
ansible-playbook -i inventory/prod.yml site.yml --check

# Установка с показом diff
ansible-playbook -i inventory/prod.yml site.yml --diff
