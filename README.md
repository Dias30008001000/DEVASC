# Проверка версии Python и обновление системы
python3 -V
sudo apt-get update

# Создание скрипта, назначение прав на выполнение и смена владельца
echo "ls ../Desktop" > myfile.sh
chmod +x myfile.sh
sudo chown root myfile.sh
./myfile.sh

# Поиск и фильтрация с помощью регулярных выражений (grep)
grep devasc /etc/passwd
grep '^root' /etc/passwd
grep 'false$' /etc/passwd


firstName = input("What is your first name? ")
lastName = input("What is your last name? ")
location = input("What is your location? ")
age = input("What is your age? ")

print("Hi " + firstName + " " + lastName + "! Your location is " + location + " and you are " + age + " years old.")



aclNum = int(input("What is the IPv4 ACL number? "))
if aclNum >= 1 and aclNum <= 99:
    print("This is a standard IPv4 ACL.")
elif aclNum >= 100 and aclNum <= 199:
    print("This is an extended IPv4 ACL.")
else:
    print("This is not a standard or extended IPv4 ACL.")



while True:
    x = input("Enter a number to count to: ")
    if x == 'q' or x == 'quit':
        break
    x = int(x)
    y = 1
    while True:
        print(y)
        y = y + 1
        if y > x:
            break




# Чтение данных из файла в список
devices = []
file = open("devices.txt", "r")
for item in file:
    item = item.strip()
    devices.append(item)
file.close()
print(devices)

# Добавление новых элементов в файл
file = open("devices.txt", "a")
while True:
    newItem = input("Enter device name: ")
    if newItem == "exit":
        print("All done!")
        break
    file.write(newItem + "\n")
file.close()



# Создание виртуального окружения и установка пакетов
python3 -m venv devfun
source devfun/bin/activate
pip3 install requests
pip3 freeze > requirements.txt
deactivate

# Развертывание окружения из файла зависимостей
python3 -m venv devnew
source devnew/bin/activate
pip3 install -r requirements.txt
deactivate




# Глобальная настройка Git
git config --global user.name "Dias30008001000"
git config --global user.email "chokubashev.dias@gmail.com"

# Инициализация и первый коммит
git init
echo "I am on my way to passing the Cisco DEVASC exam" > DEVASC.txt
git add DEVASC.txt
git commit -m "Committing DEVASC.txt to begin tracking changes"

# Работа с ветками
git branch feature
git checkout feature
echo "This text was added originally while in the feature branch" >> DEVASC.txt
git add DEVASC.txt
git commit -m "Added a third line in feature branch"

# Слияние веток
git checkout master
git merge feature
git branch -d feature

# Интеграция с удаленным репозиторием GitHub
git remote add origin https://github.com/Dias30008001000/DEVASC.git
git push -u origin master




class Location:
    def __init__(self, name, country):
        self.name = name
        self.country = country
    
    def myLocation(self):
        print("Hi, my name is " + self.name + " and I live in " + self.country + ".")

loc1 = Location("Tomas", "Portugal")
loc1.myLocation()

loc2 = Location("Ying", "China")
loc2.myLocation()

loc3 = Location("Amare", "Kenya")
loc3.myLocation()

your_loc = Location("Chokubashev Dias", "Kyrgyzstan")
your_loc.myLocation()



class Circle:
    def __init__(self, radius):
        self.radius = radius

    def circumference(self):
        pi = 3.14
        circumferenceValue = pi * self.radius * 2
        return circumferenceValue

    def printCircumference(self):
        myCircumference = self.circumference()
        print("Circumference of a circle with a radius of " + str(self.radius) + " is " + str(myCircumference))

circle1 = Circle(2)
circle1.printCircumference()

circle2 = Circle(5)
circle2.printCircumference()

circle3 = Circle(7)
circle3.printCircumference()




from test_data import *

ret_val = []
def json_search(key, input_object):
    def inner_function(key, input_object):
        if isinstance(input_object, dict):
            for k, v in input_object.items():
                if k == key:
                    temp = {k: v}
                    ret_val.append(temp)
                if isinstance(v, dict):
                    inner_function(key, v)
                elif isinstance(v, list):
                    for item in v:
                        if not isinstance(item, (str, int)):
                            inner_function(key, item)
        else:
            for val in input_object:
                if not isinstance(val, (str, int)):
                    inner_function(key, val)
    inner_function(key, input_object)
    return ret_val




import unittest
from recursive_json_search import json_search
from test_data import *

class json_search_test(unittest.TestCase):
    def test_search_found(self):
        self.assertTrue([] != json_search(key1, data))

    def test_search_not_found(self):
        self.assertTrue([] == json_search(key2, data))

    def test_is_a_list(self):
        self.assertIsInstance(json_search(key1, data), list)

if __name__ == '__main__':
    unittest.main()




import xml.etree.ElementTree as ET
import re

xml = ET.parse("myfile.xml")
root = xml.getroot()

ns = re.match('{.*}', root.tag).group(0)
editconf = root.find("{}edit-config".format(ns))
defop = editconf.find("{}default-operation".format(ns))
testop = editconf.find("{}test-option".format(ns))

print("The default-operation contains: {}".format(defop.text))
print("The test-option contains: {}".format(testop.text))



import json
import yaml

with open('myfile.json', 'r') as json_file:
    ourjson = json.load(json_file)

print("The access token is: {}".format(ourjson['access_token']))
print("The token expires in {} seconds.".format(ourjson['expires_in']))

print("\n\n---")
print(yaml.dump(ourjson))



import json
import yaml

with open('myfile.yaml', 'r') as yaml_file:
    ouryaml = yaml.safe_load(yaml_file)

print("The access token is {}".format(ouryaml['access_token']))
print("The token expires in {} seconds.".format(ouryaml['expires_in']))

print("\n\n")
print(json.dumps(ouryaml, indent=4))
