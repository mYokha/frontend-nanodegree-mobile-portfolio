## Website Performance Optimization portfolio project

Your challenge, if you wish to accept it (and we sure hope you will), is to optimize this online portfolio for speed! In particular, optimize the critical rendering path and make this page render as quickly as possible by applying the techniques you've picked up in the [Critical Rendering Path course](https://www.udacity.com/course/ud884).

To get started, check out the repository and inspect the code.

### Getting started

#### Part 1: Optimize PageSpeed Insights score for index.html

Some useful tips to help you get started:

1. Check out the repository
1. To inspect the site on your phone, you can run a local server

  ```bash
  $> cd /path/to/your-project-folder
  $> python -m SimpleHTTPServer 8080
  ```

1. Open a browser and visit localhost:8080
1. Download and install [ngrok](https://ngrok.com/) to the top-level of your project directory to make your local server accessible remotely.

  ``` bash
  $> cd /path/to/your-project-folder
  $> ./ngrok http 8080
  ```

1. Copy the public URL ngrok gives you and try running it through PageSpeed Insights! Optional: [More on integrating ngrok, Grunt and PageSpeed.](http://www.jamescryer.com/2014/06/12/grunt-pagespeed-and-ngrok-locally-testing/)

Profile, optimize, measure... and then lather, rinse, and repeat. Good luck!

#### Part 2: Optimize Frames per Second in pizza.html

To optimize views/pizza.html, you will need to modify views/js/main.js until your frames per second rate is 60 fps or higher. You will find instructive comments in main.js. 

You might find the FPS Counter/HUD Display useful in Chrome developer tools described here: [Chrome Dev Tools tips-and-tricks](https://developer.chrome.com/devtools/docs/tips-and-tricks).

### Optimization Tips and Tricks
* [Optimizing Performance](https://developers.google.com/web/fundamentals/performance/ "web performance")
* [Analyzing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/analyzing-crp.html "analyzing crp")
* [Optimizing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/optimizing-critical-rendering-path.html "optimize the crp!")
* [Avoiding Rendering Blocking CSS](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-blocking-css.html "render blocking css")
* [Optimizing JavaScript](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/adding-interactivity-with-javascript.html "javascript")
* [Measuring with Navigation Timing](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/measure-crp.html "nav timing api"). We didn't cover the Navigation Timing API in the first two lessons but it's an incredibly useful tool for automated page profiling. I highly recommend reading.
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/eliminate-downloads.html">The fewer the downloads, the better</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/optimize-encoding-and-transfer.html">Reduce the size of text</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/image-optimization.html">Optimize images</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching.html">HTTP caching</a>

### Customization with Bootstrap
The portfolio was built on Twitter's <a href="http://getbootstrap.com/">Bootstrap</a> framework. All custom styles are in `dist/css/portfolio.css` in the portfolio repo.

* <a href="http://getbootstrap.com/css/">Bootstrap's CSS Classes</a>
* <a href="http://getbootstrap.com/components/">Bootstrap's Components</a>

## How to run the app.

You can scroll up on this repo's page and click the green button "Clone or download" and, for example, download the .zip file. Then you just unpack the archieve and double click index.html. In case you want to run pizza app you can go to views folder and double click pizza.html.

The other way to open the app is following this [link](https://myokha.github.io/frontend-nanodegree-mobile-portfolio/).

In any case if you want to see one of my projects (which are placeholders just yet) click on link next to peroject's description.
If you want to run Cameron's pizza app, it is lised the last one in projects list... So click on it.

### Optimozations made to portfolio

1. As I don't need Analytics I've commented it's code. Anyway, if Iever wanted to use GA, there's `async` attribute on every `<script>` tag. Just in case.
2. I've unblocked html for rendering while loading css with `media` attr for `<link>` tag.
3. I've minified .css and .js files
4. Of course the images are compressed and none of them is larger than 4 kilobytes.
5. I've put some additional classes to html and used them in css to reach everything I need with just one selector.
6. I've deletet a lot of style rules which do not affect the way portffolio looks.
7. I also added favicon... I hate seeing errors in console.

This is mostly it. I decided not to use Gulp or Grunt for this project. It's a small one. So I easily managed all the operations by myself.
Actually I've done a lot of stuff here and one can see all the changes by following commits. But the most influential ones were described.

### Optimozations made to pizza app

Well, basically I've done just two things. Both were modifications to `main.js` file of views folder. And let's be clear, both of them are similar. It's a common thing that some canculations are being done inside the loops or function calls while being just some static thigs after being calculated.

In this project there are those kind of problems.
1. The first problem is far under 60fps of background pizzas movement while scrolling up and down. So I took some variables out of 'for' loop to prevent their recalculation each time loop runs:
```
var items = document.querySelectorAll('.mover'),
      itemsLength = items.length,
      phase,
      scroll = document.body.scrollTop / 1250;
```

2. The other problem was that when change the size of pizza it take way too much time to render stuff. So I took some static calculations out of 'for' loop again:
```
var pizzaContainer = document.querySelectorAll(".randomPizzaContainer");  
      var dx = determineDx(pizzaContainer[0], size);
      var newwidth = (pizzaContainer[0].offsetWidth + dx) + 'px';
```
Actually, those variables have been located inside of `hangePizzaSizes(size)`, so they've been recalculated a 100 times every time I switched the size of pizza, so I took them out of the function. So now they ace calculated just once everyy time I use the switch and `hangePizzaSizes(size)` can get those variables from outer function.

---
P.S. This project is a real challange because from the time the entire course has been recorded Chrome Dev Tools have changed massively!
