
I have created a flask app which will return "Test" string. This string can be modified from admin panel.

Below is the code for the same:

app.py

from flask import Flask, render_template, request, jsonify
import mysql.connector

app = Flask(__name__)

@app.route('/')
def index():
   return render_template('index.html')

@app.route('/test', methods=['GET'])
def test():
   db = mysql.connector.connect(
      host="localhost",
      user="root",
      passwd="",
      database="mydatabase"
   )
   cursor = db.cursor()
   cursor.execute("SELECT * FROM test")
   result = cursor.fetchall()
   return jsonify(result)

if __name__ == '__main__':
   app.run(debug = True)

index.html

<html>
   <body>
      <h1>Test API</h1>
      <a href = "/test">Click here to get "Test" string</a>
   </body>
</html>

 Admin panel can be created using flask-admin.

Below is the code for the same:

from flask import Flask
from flask_admin import Admin
from flask_admin.contrib.sqla import ModelView

app = Flask(__name__)
admin = Admin(app)

@app.route('/')
def index():
   return '<a href="/admin/">Click me to get to Admin!</a>'

if __name__ == '__main__':
   app.run()
