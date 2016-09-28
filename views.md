# Views

Simply, Views module is a query builder. But it is not simple at all, In fact, Views is a very powerful and complex tool, have a lot of options that sometimes can be very confusing. But don’t you worry, when you understand the basic logical, it becomes more easy to dive into it.

As a query builder, behind it there is a SQL query. For these who want to watch the query in the UI, during building the view, go to `admin/structure/views/settings` and check the `Show the SQL query` option.

In this training we will create a view that display list of blog titles.

I created content type called `Blog` with basic fields: Title and Body, and generate some demo content.

To start build new View, go to `admin/structure/views/add`.

This form give us some main View definitions. Set the View name and description (be kind and describe it shortly and clearly, so others can understand what this View shows), then, in ‘show’ field define what kind of information the View will show. This selection determine the main table in DB that the View will use to retrieve data and it cannot be changed later.

![](images/views/first_view_form.png)

In this View we want to display list of blog’s titles, so we select to show `Content` (nodes). Since we chose Content, we get also the option to select which content type. Although we know we need to choose the `Blog` content type, let’s leave it `All` for now, because I want to show you how to define that filter in the edit View page.

There is also the possibility to create a page and a block in this form. Our Blog list will display on a page, but we will create it at the next step (just for you to see how we define this in the edit View page.), So leave the page checkboxes unchecked.
We finished here, click `Continue and edit` button.


