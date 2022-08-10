# Personal Website & Portfolio Workshop

*August 10, 2022*

Kappa Theta Pi Technical Development

with Neha Desaraju

---

## Content

1. Work experience
2. Projects
3. Personalization

--

### Work experience

* Don't repeat your resume, add value
* Aim to give a brief demonstration of your skills and knowledge <!-- .element: class="fragment" -->
* Only list the most impactful/recent ones <!-- .element: class="fragment" -->

--

### Projects

* Have fun with it!
* Develop things that are unique and meaningful to you <!-- .element: class="fragment" -->
* Stay up to date & read a lot to get inspiration <!-- .element: class="fragment" -->
* A project can always turn into something bigger but doesn't have to! <!-- .element: class="fragment" -->

--

### Personalization

* Add your hobbies or fun things you like to do
* Showcase your personality <!-- .element: class="fragment" -->
* Sets yourself apart from just a standard resume <!-- .element: class="fragment" -->

---

## How to build it

If you're a software developer, code your own portfolio from scratch to showcase your
skills. If you're a UX designer or anyone else, you can choose to go with a no-code
website builder.

---

### Tools & technologies

* Webflow, Squarespace, or Wix (no code)
  * May have costs to use
  * Try applying for student discounts
* HTML & CSS (and optionally Javascript)
* More advanced JS frameworks like React or Ionic
  * Good for demonstrating front-end knowledge
* CSS frameworks such as Boostrap

--

#### HTML

```html [|3-6|7-9]
<!DOCTYPE html>
<html>
    <head>
        <title>My Personal Website</title>
        <link rel="stylesheet" href="styles.css" />
    </head>
    <body>
        <h1>Welcome to my website!</h1>
    </body>
</html>
```

--

#### CSS

```css
h1 {
    text-align: center;
    color: red;
    font-family: Times New Roman, serif;
}
```

---

### Hosting your website

--

#### Github Pages

For static websites only (uses only HTML, CSS, and client-side JS):

1. Create a repo titled `<username>.github.io` in your Github account (each user gets a free .github.io domain!)
2. Have a file called `index.html`. You can include everything else you need to run the site in this repo too, like CSS and JS scripts.
3. Go to `https://<username>.github.io` to see your site!

--

**Bonus**: You can also host your (static) portfolio projects on a .github.io site, if you have one published. For example, if your project repo is called `my-project` and has an `index.html` file, you can see it at `<username>.github.io/my-project`!

--

#### For non-static sites

If you're creating with anything that needs to be built server-side (or otherwise can't be built through GH Pages):

* Netlify
* GCP/AWS
* Heroku

They will all have cloud server costs associated with them, but many have a generous free tier and you may be eligible for free student credits or through organizations. Check their pricing!

--

#### Custom domain name

* You'll have to purchase a domain name if you want a custom one
* Use your student email to qualify for GH Student Developer pack and get a free .me domain for a year
* You may also get free domain names for a year by attending hackathons!
* NameCheap, GoDaddy, & Google Domains have domain name solutions

---

## Inspiration

* [Short list of creative portfolios](https://github.com/iRaul/creative-portfolios)
* [Long list of dev portfolios](https://github.com/emmabostian/developer-portfolios)
* [Httpster](https://httpster.net/)
* [Awwwards](https://www.awwwards.com/)
* Search `portfolio template` on Github to find repos with templates you can use

---

## Example time!

Let's walk through how I built my portfolio with HTML, CSS, & jQuery. Find the repo [here](https://github.com/estaudere/estaudere.github.io)!

--

### index.html

```html [3-8|14-19|24-29]
<!DOCTYPE html>
<html lang="en">
<head>
    ...
    <title>Neha Desaraju</title>
    <!-- Google Fonts, CSS frameworks, + custom CSS -->
    ...
</head>
<body>
    <div class="container home">
        <!-- about me -->
        ...
        <div class="row">
            <div id="connect" class="column">
                <h3>Connect</h3>
                <ul>
                    <!-- each item is a li -->
                </ul>
            </div>
            
            <!-- the currently column, made similarly to the connect column -->
            ...
        </div>
        <div id="projects">
            <h3>Projects</h3>
            <ul>
                <!-- each item is a li with class project -->
            </ul>
        </div>
    </div>

    <!-- Custom JS -->
    <script src="./script.js"></script>

</html>
``` 

--

### data.json

```json [|]
{
    "socials": [
        {
            "title": "Mail",
            "link": "mailto:neha.desaraju@gmail.com",
            "icon": "fa fa-envelope"
        },
        {
            "title": "Github",
            "link": "https://github.com/estaudere",
            "icon": "fa-brands fa-github"
        },
```

--

### script.js

```js [|2|3|10-14]
$(document).ready(function() {
  $.getJSON("https://raw.githubusercontent.com/estaudere/estaudere.github.io/master/data.json", function(data) {
    addSocials(data.socials);
    addCurrently(data.currently['2021'], '2021');
    addCurrently(data.currently['2022'], '2022');
    addProjects(data.projects);
  })
});

function addSocials(socials) {
  $.each(socials, function(i, val) {
    $("#connect > ul").append("<li><a href='" + val.link + "' target='_blank' rel='noreferrer noopener'><i class='" + val.icon + "'></i>" + val.title + "</a></li>");
  })
}

// more functions
```

---

This presentation was made with ❤️ and `revealjs` by Neha Desaraju.