# lab5
flask reg

        import requests
        from flask import Flask, render_template, request, redirect
        import psycopg2




        app = Flask(__name__)

        conn = psycopg2.connect(database="service_db",
                        user="postgres",
                        password="1234",
                        host="localhost",
                        port="5432")
        cursor = conn.cursor()

        @app.route('/login/', methods=['GET'])
        def index():
           return render_template('login.html')

        @app.route('/registration/', methods=['POST', 'GET'])
        def registration():
            if request.method == 'POST':
                name = request.form.get('name')
                login = request.form.get('login')
                password = request.form.get('password')

        cursor.execute('INSERT INTO service.users (full_name, login, password) VALUES (%s, %s, %s);',
                       (str(name), str(login), str(password)))
        conn.commit()

        return redirect('/login/')

    return render_template('registration.html')




        @app.route('/login/', methods=['POST', 'GET'])
        def login():
            if request.method == 'POST':
                if request.form.get("login"):
                    username = request.form.get('username')
                    password = request.form.get('password')
                    cursor.execut        e("SELECT * FROM service.users WHERE login=%s AND password=%s", (str(username), str(password)))
                    records = list(cursor.fetchall())

            return render_template('account.html', full_name=records[0][1])
        elif request.form.get("registration"):
            return redirect("/registration/")

    return render_template('login.html')
    
LOGIN

    <!DOCTYPE html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <title>Login</title>
    </head>
    <body>
    <form action="" method="post">
        <p>
     <label for="username">Username</label>
     <input type="text" name="username">
     </p>
     <p>
         <label for="password">Password</label>
     <input type="password" name="password">
     </p>
     <p>
         <input type="submit" value="login" name="login">
      <input type="submit" value="registration" name="registration">
     </p>

     </form>

    </body>
    </html>

ACOOUNT

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        <form action="" method="post">
            {% if full_name %}
            <p>Hello, {{full_name}}! </p>
            {% endif %}

	</p>

    </form>
        </head>
    <body>

    </body>
    </html>

REGISTRATION

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Registration</title>
    </head>
    <body>
        <form action="" method="post">
          <p>
        <label for="name">Your name:</label>
        <input type="text" name="name">
         </p>
            <p>
	        <label for="login">Login:</label>
	        <input type="text" name="login">
	         </p>
	    <p>
	        <label for="password">Password:</label>
	        <input type="password" name="password">
    	</p>
	    <p>
	        <input type="submit" value="Sign In">
    	</p>
        </form>

    </body>
    </html>

