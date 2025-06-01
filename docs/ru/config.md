# ⚙️ Конфигурация
## 🧩 "Core"-настройки
Настройки, которые определяют поведение, компиляцию и парсинг Langrinder
Они описываются прямиком в `langrinder.Langrinder.__init__(...)`:
- `generator: type[LangrinderBaseGenerator] = LangrinderTranslationsGenerator` - практически самый главный параметр.
    Генерирует `output_file`, а также парсит `.mako` файлы под капотом (через `parser`)
- `parser: type[LangrinderBaseParser] = LangrinderSyntaxParser` - парсер блоков и строк текста.
    Важно: все форматирование происходит только за счет Mako, парсер лишь собирает текст!
- `node_template: str = "{LANGRINDER_PATH}/generator/templates/node.mako"` - шаблон для базовой ноды
- `translation_template: str = "{LANGRINDER_PATH}/generator/templates/translation.mako"` - шаблон для ноды перевода
- `translation_name: str = "Translation"` - имя класса перевода
- `node: type[Node] = ConstLanguageCode` - нода для получения локали
- `logger: logging.Logger | None = None`- логгер (описывает действия генератора при уровне DEBUG)

## 👀 Настройки поведения
Они описываются в `telegrinder.tools.global_context.GlobalContext("langrinder")`:
```python
ctx = GlobalContext("langrinder")
ctx["foo"] = "bar" 
```
- `locale` - дефолтная локаль (также используемая для `ConstUserLocale`)
- `tz` - часовой пояс. Указывается в формате *"Europe/Moscow"*
- `args` - глобальные аргументы, передаваемые в локаль всегда (возможно, конфиг, ссылки или названия чего-либо)
- `gender_generator` - генератор форм, зависимых от пола. Дефолтный: `langrinder.tools.GenderGenerator`
- `plural_generator` - генератор форм, зависимых от количества. Дефолтный: `langrinder.tools.PluralGenerator`

**[◀️ К оглавлению](./index.md)**