# Backend Workshop

*August 11, 2022*

Kappa Theta Pi Technical Development

with Neha Desaraju

---

## What is a backend?

Why is it needed? What problems does it solve?

<!-- .slide: data-auto-animate -->

--

## What is a backend?

Why is it needed? What problems does it solve?

* Persistence (e.g. Docs)
* Hides proprietary algorithms or data (e.g. Shazam)
* Offloads work from client to server (e.g. online games)

<!-- .slide: data-auto-animate -->

---

## Backends IRL

* Both web app and mobile app interact with the same APIs
* Most are REST APIs (follow the REST constraints)
  * Each response from the server is standalone (stateless)
  * E.g. client asks "What is the list of tasks for this user to do?"

--

## In practice

* Client makes four main types of requests: GET, POST, PUT, DELETE
  * Request may include headers, parameters, and request bodies
* Server gives response + response code that indicates status
  * E.g. 404 = not found, 401 = unauthorized, 200 = OK

--

### Example - GET

1. Front end makes a GET request with TODO in the header/parameter
2. Back end responds with code 200 and a JSON string:
```json
{
    "items": [
        "Go Shopping",
        "Add API",
        "Add tests"
    ]
}
```

--

### Example - POST

1. Front end makes POST request with request body:
```json
{
    "name": "My new item!",
    "position": 1
}
```
2. Back end responds with 201 (created) code

---

## Create your own backend! <!-- .element: class="r-fit-text" -->

---

## Brief intro to Flask

In **app.py**:

```python [1|3|5-8|11-12]
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    # return your index.html here!
    pass


if __name__ == '__main__':
    app.run(host="localhost", port="8000", debug=True)
```

--

Run your app by typing

```shell
flask run
```

into the terminal, and navigate to the URL it displays (typically **https://localhost:8000**).

--

Now we'll create our first route.

```python
@app.route('/hello')
def hello_world():
    return "Hello world!"
```

Go to **https://localhost:8000/hello**! You should see **Hello world!** at the top of the screen.

--

You can also return an `html` file instead of just text. Let's change our index route to display our home page.

```python [1|3-5]
from flask import Flask, render_template

@app.route('/')
def index():
    return render_template('index.html')
```

`index.html` must be in a folder called *templates* for it to work.

---

## Getting started - URL shortener

1. Go to Replit or Glitch and import the [template repo](https://github.com/texaskappathetapi/backend-demo)
2. Make sure you've installed required dependencies
```shell
pip install Flask Flask-SQLAlchemy Flask-Migrate
```

--

### Files

* **main.py** initializes db and imports the Flask app as a *package*
* **config.py** sets Flask configuration (you can change based on env variables)
* **app/__init__.py** initializes *app* as a package
* **app/models.py** contains database structure object

--

### Editing the routes

First we need to add POST request handling in **routes.py**. HTML form submitted = POST request to server

```python [1|3-5|18-22|24]
@app.route('/', methods=['GET', 'POST'])
def index():
    if request.method == 'POST':
        url = request.form['url']
        short_id = request.form['custom_id']

        if short_id and ShortURLs.query.filter_by(short_id=short_id).first() is not None:
            flash('Please enter different custom id!')
            return redirect(url_for('index'))

        if not url:
            flash('The URL is required!')
            return redirect(url_for('index'))

        if not short_id:
            short_id = generate_short_id(8)

        new_link = ShortURLs(
            original_url=url, short_id=short_id, created_at=datetime.now())
        db.session.add(new_link)
        db.session.commit()
        short_url = request.host_url + short_id

        return render_template('index.html', short_url=short_url)

    return render_template('index.html')
```
<!-- .element: class="fragment" -->

<!-- .slide: data-auto-animate -->

--

### Editing the routes

Second, we need to redirect a short URL (GET request) to the long URL.

```python [1-2|]
@app.route('/<short_id>')
def redirect_url(short_id):
    link = ShortURLs.query.filter_by(short_id=short_id).first()
    if link:
        return redirect(link.original_url)
    else:
        flash('Invalid URL')
        return redirect(url_for('index'))
```

<!-- .element: class="fragment" -->

<!-- .slide: data-auto-animate -->

---

This presentation was made with ❤️ and `revealjs` by Neha Desaraju.