import json
import requests
from datetime import datetime

DATA_URL = "https://www.cbr-xml-daily.ru/daily_json.js"
SAVE_FILE = "save.json"

def load_groups():
    try:
        with open(SAVE_FILE, encoding="utf-8") as f:
            return json.load(f)
    except:
        return {}

def save_groups(groups):
    with open(SAVE_FILE, "w", encoding="utf-8") as f:
        json.dump(groups, f, ensure_ascii=False, indent=2)

def get_currency_data():
    try:
        r = requests.get(DATA_URL, timeout=8)
        r.raise_for_status()
        data = r.json()
        return data["Valute"], data["Date"]
    except:
        print("Не удалось загрузить данные с ЦБ РФ...")
        return {}, None

def show_all_rates(valute):
    if not valute:
        print("Данных нет...")
        return
    print(f"Курсы на {datetime.now().strftime('%Y-%m-%d %H:%M')}")
    print("-" * 48)
    for code, item in sorted(valute.items()):
        print(f"{code:7}  {item['Name']:28}  {item['Value']:>10.4f} ₽")

def show_one_rate(valute, code):
    if code.upper() in valute:
        item = valute[code.upper()]
        print(f"{code.upper():7}  {item['Name']:28}  {item['Value']:>10.4f} ₽")
    else:
        print(f"Валюта {code.upper()} не найдена...")

def show_groups(groups):
    if not groups:
        print("Пока что групп нет...")
        return
    for name, codes in groups.items():
        print(f"Группа: {name}")
        if codes:
            for c in sorted(codes):
                print(f"  • {c}")
        else:
            print("  (ничего нет (＞︿＜))")
        print()

def main():
    groups = load_groups()

    while True:
        print("\n" + "═" * 50)
        print("Мониторинг курсов ЦБ РФ")
        print("1. Показать все курсы")
        print("2. Показать курс одной валюты")
        print("3. Показать все группы")
        print("4. Создать новую группу")
        print("5. Добавить валюту в группу")
        print("6. Удалить валюту из группы")
        print("7. Удалить группу")
        print("0. Выход")
        print("═" * 50)

        action = input("→ ").strip()

        valute, _ = get_currency_data()

        if action == "1":
            show_all_rates(valute)

        elif action == "2":
            code = input("Код валюты (USD, EUR и т.д.): ").strip()
            show_one_rate(valute, code)

        elif action == "3":
            show_groups(groups)

        elif action == "4":
            name = input("Название новой группы: ").strip()
            if name and name not in groups:
                groups[name] = []
                save_groups(groups)
                print(f"Группа «{name}» создана")
            else:
                print("Такое название уже есть/пробел не считается...")

        elif action == "5":
            show_groups(groups)
            group_name = input("В какую группу добавить? ").strip()
            if group_name not in groups:
                print("Нет такой группы...")
                continue
            code = input("Код валюты: ").strip().upper()
            if code in valute and code not in groups[group_name]:
                groups[group_name].append(code)
                save_groups(groups)
                print(f"{code} добавлен в группу «{group_name}»")
            else:
                print("Такой валюты нет/она уже добавлена...")

        elif action == "6":
            show_groups(groups)
            group_name = input("Из какой группы удалить? ").strip()
            if group_name not in groups:
                print("Такой группы нет...")
                continue
            code = input("Код валюты: ").strip().upper()
            if code in groups[group_name]:
                groups[group_name].remove(code)
                save_groups(groups)
                print(f"{code} удалён из группы «{group_name}»")
            else:
                print("Такой валюты тут нет...")

        elif action == "7":
            show_groups(groups)
            name = input("Какую группу удалить? ").strip()
            if name in groups:
                del groups[name]
                save_groups(groups)
                print(f"Группа «{name}» удалена")
            else:
                print("Нет такой группы...")

        elif action in ("0", "q", "выход"):
            print("Пака")
            break

        else:
            print("Нет такого...")

if __name__ == "__main__":
    main()
