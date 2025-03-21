# zafiyetli-proje
import sqlite3

conn = sqlite3.connect(":memory:")
cursor = conn.cursor()

cursor.execute("CREATE TABLE users (id INTEGER PRIMARY KEY, username TEXT, password TEXT)")
cursor.execute("INSERT INTO users (username, password) VALUES ('admin', 'password123')")

def login(username):
    query = f"SELECT * FROM users WHERE username = '{username}'"
    cursor.execute(query)
    user = cursor.fetchone()
    if user:
        print(f"Giriş başarılı! Hoş geldin {user[1]}")
    else:
        print("Geçersiz kullanıcı adı!")

username_input = input("Kullanıcı adınızı girin: ")
login(username_input)
#Bu kodda:
#Kullanıcı giriş yaparken SQL Injection açığı bulunuyor.
#Örneğin "admin' --" girilirse şifresiz giriş yapılabilir.
