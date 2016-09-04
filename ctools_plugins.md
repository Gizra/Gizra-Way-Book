# CTools plugins

Our working method is to build a static site with jekyll and then make it dynamic, by copying HTML and CSS to the Drupal site, and replacing the static parts with dynamic content. You can read more about this method in [Gizra blog](http://www.gizra.com/content/custom-css-as-contrib-with-jekyll/).

In this training we will focus on a particular part of the implementation of this method, by using two powerful drupal’s modules: [CTools](https://www.drupal.org/project/ctools) and [Panels](https://www.drupal.org/project/panels).

One of the great tools of CTools is the Plugins.
CTools plugin is a piece of code located in small file (.inc), which help us to extend any module functionality.
Panels provides content areas exposed as block or page. We use the panel as a container to display our plugin.
In this post we'll go through a few steps, show how to create and use CTools plugins with Panels.


### 1 - Recognize the plugin in the Markup
First we need to look at the Markup and recognize the piece of code that we going to make a plugin for.
For example, look at this page:

![](markup.png)

We can identify three parts: **header**, **footer** and **content**. The content area contains two items lists: one is a list view and the second is a grid view. Header and footer repeat on every page, so they will be part of our layout. Every item in the list is a piece of code that repeat itself, so we can look at one list as a plugin. In this page we have two lists, so we will create separate plugin for each list.

The final code for the examples below can be found in [this repository](https://github.com/Gizra/dynamic_example/tree/lesson1).

Let’s look at the code in the static site. 
Go to ```/static/src/hello-world/index.html``` and open the file.

```
---
layout: default
label: Hello-world
---

<div class="ui segment stacked">
  <div class="ui very relaxed items">

    {% include single_item.html %}
    {% include single_item.html %}
    {% include single_item.html %}


  </div>
</div>

<div class="ui link cards">


  {% include card.html %}
  {% include card.html %}
  {% include card.html %}
  {% include card.html %}
  {% include card.html %}
  {% include card.html %}
  
</div>
```

We see that the code for the item in the list view is in ```single_item.html``` - it will be the first plugin, and the code for the item in the grid view is in ```card.html``` - it will be the second plugin.
Also we can see the layout for this page is ```default```. So let’s take a look at the layout. Go to ```/static/src/_layouts/default.html```.

```
<body>

    {% include header.html %}

    <main class="ui container">
      {{ content }}
    </main>

    {% include footer.html %}

    <script src="/assets/javascript/script.js"></script>
  </body>
```
Here, inside the ```<body>``` tag, we see first the **header** (which his code is in ```header.html```), then the **content** (inside the ```<main>``` tag), and final the **footer** (which his code is in ```footer.html```)

Now, after we saw the parts of the page, and identified the plugins, we can go ahead and start building them.


### 2 - Create new theme.
In the project directory, within the theme directory, create a folder called 'MYTHEME' (replace MYTHEME with the name of the new theme). Within this folder create MYTHEME.info file which contain some simple instructions to help Drupal identify and use our theme. For example you can look at ```dynamic_example/themes/dynamic_example_theme/dynamic_example_theme.info``` 

Next, within MYTHEME folder create folder called ```templates```.
Inside this folder we need to place the ```page.tpl.php``` file. This file is the default template file to display a single Drupal page. Copy it from ```/www/modules/system/page.tpl.php``` and paste it into ```templates``` folder.


```
theme/
    MYTHEME/
        MYTHEME.info
        templates/
             page.tpl.php
```

Now, let’s go back to our markup. Remember we recognized three parts of the page: **header**, **footer** and **content**. That is the layout of the page, so we need to replace the ```page.tpl.php``` default code with the HTML of this layout. 
But, before we do any changes in our ```page.tpl.php```, we need to make sure Drupal reads this file from our theme folder. To check this, all we need to do is to delete all the file’s content (don’t worry, it can be reversible), and write something like ‘*My theme*’. Then go to the browser and clear cache of your Drupal site. If you see the words ‘*My theme*’ it means Drupal notice to ```page.tpl.php``` in our theme folder. Undo deletion (by cmd+z).


### 3 - Edit page.tpl.php file.
As we said, we need to place the HTML from the Markup layout into Drupal site. 
In the project directory, go to ```/static/src/_includes/header.html```. Copy the content of this file and paste it in the top of your ```page.tpl.php``` file.
Then copy the ```<main>``` tag and all it contains from ```/static/src/_layouts/default.html```.
Finally go to ```/static/src/_includes/footer.html``` and copy it’s content too.
The result should be look like this:

```
<header class="ui container header">
  <h2 class="ui header">
    <a href="/"><i class="home icon"></i></a>
    <a href="/">Brand</a>
  </h2>
</header>

<main class="ui container">
  {{content}}
</main>

<footer class="ui inverted vertical footer segment">
  <div class="ui container">
    Copyright ...
  </div>
</footer>
```

This code now is in our drupal page, but it’s completely static, exactly like our markup. Let’s replace the static parts with a dynamic content. In the original ```page.tpl.php``` code, find the line where Drupal prints the content. Cut and paste this line inside the ```<main>``` tag, where the content should be print. Additionally we want to see the drupal messages, so cut the relevant line and paste it above the ```<main>``` tag. Now your code should look like this:

```
<header class="ui container header">
  <h2 class="ui header">
    <a href="/"><i class="home icon"></i></a>
    <a href="/">Brand</a>
  </h2>
</header>

<?php print $messages; ?>

<main class="ui container">
  <?php print render($page['content']); ?>
</main>

<footer class="ui inverted vertical footer segment">
  <div class="ui container">
    Copyright ...
  </div>
</footer>
```

That’s all we need. Delete the rest of the original code in ```page.tpl.php```.


### 4 - Create Panel page
In drupal site, go to ```/admin/structure/pages``` and create a page. Give it title and path, choose 1 column layout and leave content empty for now. Later we will add the plugin to the content area.
Save the panel page and export it by Features. Put the module in ```/modules/custom/MYMODULE```. Don’t forget to enable the module.




