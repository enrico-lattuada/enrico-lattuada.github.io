# Add a reveal.js presentation

Clone the reveal repository

```
git clone https://github.com/hakimel/reveal.js.git
```
Take note of the version used.

Create a directory for slides in the static folder.
Copy the required files into the new directory from the reveal repository.

```
mkdir .reveal.js
cp reveal.js/index.html .reveal.js/index.html
cp -r reveal.js/css .reveal.js/css
cp -r reveal.js/dist .reveal.js/dist
cp -r reveal.js/js .reveal.js/js
cp -r reveal.js/plugin .reveal.js/plugin
```

(Check also [here](https://dbafromthecold.com/2021/02/21/creating-presentations-with-reveal-and-github-pages/) for more information.)

Create a dedicated folder for each presentation.
Create a new ``index.html`` file (or copy one of the examples from the reveal.js repository).
Link the ``index.html`` file from the post by adding its path (from the static directory) to the ``url_slides`` field.
For instance, to link slides defined in ``static/slides/example/index.html``, do

```
url_slides: "slides/example/"
```