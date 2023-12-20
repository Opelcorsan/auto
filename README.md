# auto
elektron
import obd

# Инициализация соединения с адаптером OBD-II (порт COM4 для Windows, /dev/ttyUSB0 для Linux)
connection = obd.OBD(portstr="COM4")

# Получение и вывод списка всех поддерживаемых команд
commands = connection.supported_commands
print("Supported OBD-II commands:")
for cmd in commands:
    print(cmd.name)

# Получение и вывод данных по конкретной команде (например, скорость автомобиля)
speed_command = obd.commands.SPEED
response = connection.query(speed_command)
if response.is_null():
    print(f"Unable to get speed data. Response: {response}")
else:
    print(f"Vehicle Speed: {response.value} {response.unit}")

# Закрытие соединения
connection.close()
