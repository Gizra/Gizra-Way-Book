# GitBook & GitHub Workflow

The following chapter assumes you are working with GitBook UI. As a developer you may feel comfortable working with your text editor and command line. Both ways are fine, as long as the end results will be a GitHub pull request.

GitBook's repository is automatically synced to GitHub, so you may make changes on either of them, and it is guaranteed to be reflected in the other.

As a privileged user, start by [editing](https://www.gitbook.com/book/amitaibu/the-gizra-way/details) the book



![](images/gitbook/image1.jpg)

Create a new branch, you will work on a side branch, which will not immediately be reflected in the official book. This allows you to go wild with your edits, without the fear of breaking the live site.

![](images/gitbook/image2.jpg)

![](images/gitbook/image3.jpg)

GitBook shows you which branch you are currently editing. It is also reflected in the URL. For example, the URL for the `who-we-are` branch would be `https://www.gitbook.com/book/amitaibu/the-gizra-way/edit#/edit/who-we-are/`

![](images/gitbook/image4.jpg)

You are now on the new branch. You can go ahead and create new articles, update existing ones, or delete. Be Bold.

![](images/gitbook/image5.jpg)

On GitHub, open a [Pull Request](http://www.thegizraway.com/pull_requests.html), which will make your work visible to other, and allow an easier review.

![](images/gitbook/image6.jpg)

Once the review is done, and all comments have been addressed, the PR may be merged into the `master` branch which will automatically update the official book. It may take a minute or two for the [site](http://www.thegizraway.com/) to show the new content.
![](images/gitbook/image7.jpg)