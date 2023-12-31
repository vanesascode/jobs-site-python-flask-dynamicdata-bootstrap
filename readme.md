# Jobs site using Python Flask stack with Dynamic Data for database management (BACKEND + FRONTEND)

In the link below you can see how it looks and what it does. Notice this app is still in development stage running on a local domain. It is a learning project and you can find all my notes during the process, which helped me understand everything better. 👇👇👇

## https://dev-jobs-by-vanesascode.onrender.com/

![Captura](https://github.com/vanesascode/jobs-site-python-flask-mysql-bootstrap/assets/131259155/d4ff4d32-e7f2-4ca2-815f-7bcf6bab9f1b)

The combination of `Python, Flask, and Data` is commonly used in web development to create a full-stack application. Flask is a lightweight web framework in Python.

Together, they allow developers to build dynamic and scalable web applications, handling both the front-end and back-end aspects of the application. 

# To run the app:

1. In the terminal run: `python app.py` If you are in VSCode, within the file app.py just click on the triangle button on the top right.
2. Open http://localhost:4000/ in the browser.

Here you can see the Database in JSON:
http://localhost:4000/api/jobs

# 💥 BACKEND 💥

How to start:

- [x] run: `pip install Flask`
- [ ] import Flask in app.py: `from flask import Flask`
- [ ] start the Flask app: `app = Flask(__name__)`
- [ ] run the Flask app in the browser:

```
if __name__ == "__main__":
    app.run(debug=True, port=4000)
```

The previous code is checking if the current module is being run directly (as opposed to being imported by another module). If it is being run directly, it runs the Flask application with debug mode enabled and listens on port 4000.

## Route handlers

This is our main route handler, since we only have a page in this app:

```
@app.route("/")
def home():
    return render_template("home.html", jobs=JOBS, company_name="Dev")
```

When a user accesses the root URL ("/"), the home() function is executed.

The function returns the rendered template "home.html" using the render_template() function from Flask. It passes the JOBS variable (the name of the database, in fact) as a parameter to the template, which can be accessed within the template. Additionally, it passes the value "Dev" as the company_name parameter to the template.


## Deployment

In order to deploy it into an Internet URL, I created a file called requirements.txt in which I indicate the apps that need to be installed for production stage, and added it to the project folder. Then, in [render.com](https://dashboard.render.com/) I uploaded the Github repository as a Web Service (free option). You set the Runtime as `Python 3`, the Build Command as `pip install -r requirements.txt` and the start command as `gunicorn app:app`.


# 💥 FRONTEND 💥

## Templates

In Flask, templates are used to generate dynamic HTML pages. Templates allow you to separate the structure of your web pages from the logic in your Python code. Flask uses a templating engine called `Jinja2` by default.

We then render these templates using the `render_template`(see it imported in the app.py file) function provided by Flask. This function takes the name of the template file as an argument and can also accept additional parameters to pass data to the template (for example, the value "Dev" as the company_name parameter, as seen in the route handler above).

Jinja2 is inspired by Django's template engine but offers more flexibility and features. It allows you to generate dynamic content by combining HTML code with expressions, control structures, and filters.

As mentioned before, in this particular project we just have a page (home, "/"). However, inside this home template, we include the 'nav' template like this, thanks to the Jinja2 syntax:

`{% include "nav.html" %}`

We can also get every item from the fetched 'jobs' MySQL table like this:

`{% for job in jobs %} {% include "jobitems.html" %} {% endfor %}`

The construction of every item in the jobs table is going to be indicated in the template 'jobitems'

## CSS and pictures

In Flask, the "static" folder is a special directory where you have to store static files such as CSS stylesheets, JavaScript files, images, and other assets that are used by your web application

It is typically placed in the root directory of your Flask project alongside the application code. Flask automatically recognizes and serves the files from this folder when they are requested by the client.

You import a CSS file like this in the head of your html file:

```
<link
      rel="stylesheet"
      type="text/css"
      href="{{ url_for('static', filename='transitions.css') }}"
    />
```

## SASS & Bootstrap customization

I made most of the styling with Bootstrap, but I had to adapt certain details with SASS in order to customize the components as I wanted. To get ready to do so, follow these steps:

- [x] Create a package.json file if you haven't one yet. (In the terminal run `npm init -y`)
- [ ] Install Bootstrap: `npm install bootstrap@5.3.0`
- [ ] Create a file called: 'styles.scss' in the 'static folder'
- [ ] Import Bootstrap in the file: `@import "../node_modules/bootstrap/scss/bootstrap.scss";`
- [ ] Install extension 'Live Sass Compiler' by Ritwick Dey in VsCode.
- [ ] Press the button at the bottom that says 'Watch Sass' and save something in your scss file. You'll see that a styles.css file and a styles.css.map files are created. Sass has been compiled into a CSS file and now we can import it into our project.

## Mailto links

In every position from the jobs table there is a button that says 'Apply'. The mailto link it contains opens the user's default email client with a new email composition window, with the recipient's email address, subject line, and optionally, the body of the email pre-filled.

In this case it has been done with the app https://mailtolink.me/:

```
href="mailto:devjobs@devjobs.com?subject=Application%20to%20{{ job['title']|urlencode }}&body=My%20name%3A%0D%0A%0D%0AMy%20CV%3A%0D%0A%0D%0AMy%20Linkedin%3A"
```

- Mailto:devjobs@devjobs.com" specifies the recipient's email address (it is invented)
- The "{{ job['title']|urlencode }}" part is a placeholder that will be replaced with the URL-encoded version of the job title.
- "|urlencode" is used in URL encoding. It is used to ensure that URLs are properly formatted and can be transmitted correctly over the internet.

## See all your pip packages installed and versions: 

- [x] Run: `py -m pip list`
