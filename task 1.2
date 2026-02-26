import requests

urls = [
    "https://github.com/",
    "https://www.binance.com/en",
    "https://tomtit.tomsk.ru/",
    "https://jsonplaceholder.typicode.com/",
    "https://moodle.tomtit-tomsk.ru/"
]

print("Проверка доступности сайтов\n")

for url in urls:
    try:
        response = requests.get(url, timeout=10)
        status = response.status_code

        if status == 200:
            availability = "доступен"
        elif status == 403:
            availability = "вход запрещён"
        elif status == 404:
            availability = "не найден"
        elif 400 <= status < 500:
            availability = "ошибка клиента"
        elif 500 <= status < 600:
            availability = "ошибка сервера"
        else:
            availability = "нестандартный ответ"

        print(f"{url} – {availability} – код {status}")

    except requests.Timeout:
        print(f"{url} – недоступен (превышено время ожидания) – таймаут")
    except requests.ConnectionError:
        print(f"{url} – недоступен (ошибка соединения)")
    except requests.RequestException as e:
        print(f"{url} – недоступен (ошибка запроса: {e})")
