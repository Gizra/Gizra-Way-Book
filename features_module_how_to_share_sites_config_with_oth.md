# Features module: how to share site’s config with others?

If you already had a chance to build one or two Drupal sites,  you probably know Drupal site consists of three parts:
**Code** (modules, themes…) stored in files, **Configuration**  (content types, views, panels…) stored in the database, and **Content** (nodes, terms…) stored in the database.

When we are collaborating in the project, building the site together, we want to share our work. As we build Drupal site, define content types, setup Views and Panels, we end up making a lot of configuration changes. These changes stored in DB. Code is easy to share, but there is no easy way to merge changes to DB. So here come our challenge: how to share site’s config with others?


Optional solutions:
- Document all the configuration we did and do them again in the new environment (cons: takes time and can cause a lots of mistakes).
- Manually export/import configuration, like views, content types, panels (cons: not everything is exportable, we can’t track the diff between what we import and what is already in DB, no easy way to know the dependencies).  
- Move the configuration from DB to code -  use Features Module.


How Features works?
Take components (for example: Blog content type, Blog view, Blog taxonomy) and turn them into module. We can use it like any other drupal module (install it and expand it with additional code).


What should be “featurize”? What can’t be “featurize”? How we decide what to “featurize”? 


Do it in practice - 
- Create feature (add component and dependencies).
- Enable feature (how do we make sure the feature works?)
- Update feature 
- Feature state (default, override, conflict)




