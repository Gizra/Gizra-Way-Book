# Features module: how to share site’s config with others?

If you already had a chance to build one or two Drupal sites,  you probably know Drupal site consists of three parts:
**Code** (modules, themes…) stored in files, **Configuration**  (content types, views, panels…) stored in the database, and **Content** (nodes, terms…) stored in the database.

When we are collaborating in the project, building the site together, we want to share our work. As we build Drupal site, define content types, setup Views and Panels, we end up making a lot of configuration changes. These changes stored in DB. Code is easy to share, but there is no easy way to merge changes to DB. So here come our challenge: how to share site’s config with others?

Optional solution: Document all the configuration we made and do them again in the new environment. Well, It's not a very clever way of working. It takes a lot of time and can lead to many mistakes along the way. Lucky for us, there is a way to manually export/import configuration in code, as you can see for example in View options:

![](images/features/export_view.png)

Views, content types, panels and some other modules provide this export/import option, But not every modules gives us this option. Additionally, working this way doesn't provide us the ability to know the dependencies of our configuration. For example, when we export View, we need to export also the content type it depends on, otherwise the View won't work. And when the View is complex, there can be more and more configurations that it relies on, how can we be sure we won't miss anythings?
That is exactly why we have Features module!

Features simply package up all of that configuration (components) into a module, and we can use it like any other Drupal module. In another words: Features is a module that creates modules.

Take a look on a simple example: I created a web page that display list of blog post. It was built from Content type called Blog, and a View.
Now I want to export my work and move it to another environment. I simply create a module (using features module) that contain my configurations (Content type and View). 
Let's do it together:

Go to `admin/structure/features/create`.
Give the feature a name. This will be the name of the module, so we always use the project name (Dynamic example in this case) and a reasonable name that tell us what this module use for (Blog in this case). Also write a description that tells more about this module.
In the right area on the screen you need to select the components that should be include in the module (in this case Content type=Blog and View=Blog).
As you can see, Features automatically select for us all the dependencies our module needs to work properly. You can add your own dependencies as you want.

![](images/features/create_feature.png)




What should be “featurize”? What can’t be “featurize”? How we decide what to “featurize”? 


Do it in practice - 
- Create feature (add component and dependencies).
- Enable feature (how do we make sure the feature works?)
- Update feature 
- Feature state (default, override, conflict)




