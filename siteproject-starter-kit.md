## Initialization, Performance, and Health Audit

[WHyWHat](#whywhat)

[The Protocol](#theprotocol)

* [Drupal General Settings](#drupal-general-settings)

* [Logging and monitoring](#log)

* [Server Settings](#server-settings)

* [Customer docs](#customer-docs)[Admin UX and UI](#admin-ux-and-ui)

* [User Permissions](#user-permissions)

* [3rd party services \(if relevant\)](#3rd-party-services)

* [Site Down Procedure](#site-down-procedure)

* [Admin UX and UI](#admin-ux-and-ui)

* [SEO](#seo)

#### WHyWHat {#whywhat}

At Gizra, we are at a point where we insist on minimum quality checks and procedures when starting to work on a new project for either inherited websites or websites built from scratch. We internally understand the importance of these activities and the challenge is communicating and aligning expectations with the clients.

Client expectations are that Gizra takes care of all the required technical aspects to make sure their website runs smoothly, fast, and is secure. In most cases, clients are only happy to hand it over and forget about it. However, this means that they may not always understand the importance or urgency of technical initilaziation and maintenance activities. It is our responsibility to advocate for these procedures and activities, even if they are not sexy to our clients like a new feature or design change.

The time \(and budget\) to go through the following list of checks and activities is reflected in several ways in our engagement with the client.

* New project - applicable parts reflected in the project price estimate

* Maintenance - “Support Services Retainer”

  * The first month reflects ~10 hours to apply the checks and procedures.

  * Follow-up issues \(with timebox\) opened based on the checklist findings and are planned into the roadmap per urgency and importance.

* Maintenance - “Technical Maintenance Services” - Set amount of monthly budget for ongoing checks and technical maintenance activities determined by Gizra to ensure the website runs smoothly, fast, and is secure.

Some of the following checks provide useful information in times of urgency. Therefore, make sure to document the details, add a link to the specific issue from the [common file](https://docs.google.com/spreadsheets/d/1GrFjvMkp-9zv-8U59Mtg4gQPnZXICRhbQDnsOIjLPeM/edit?usp=sharing) and create each of the mentioned wiki entry.

We should know which tools are available for each site, especially when we are in a rush.

### The Protocol {#theprotocol}

#### Drupal General Settings {#drupal-general-settings}

* [ ] Set a site email and contact us mail \(if relevant\)

* [ ] Change the default/previous admin password

* [ ] Update favicon

* [ ] Make sure non-live environments are not sending mails to users \(probably would like to have them redirected to a QA / AM address for checks\). For Pantheon, [read here](https://pantheon.io/docs/guides/rerouting-outbound-email/).

* [ ] Install the Honeypot module, or consider disabling the user/1 account, Due to [this kind of real-world scenarios](https://www.drupal.org/project/drupal/issues/2939720).

* [ ] Add a "developer" role to the project which has all the permissions that user/1 would have.

* [ ] Consider assigning each developer and PM a user with the developer role with an identifiable name \(such as, gizranoam\).

#### Logging and Monitoring {#loggingandmonitoring}

* [ ] Install [http\_log](https://www.drupal.org/project/logs_http) and setup setting for [Rollbar](https://rollbar.com/). Remember to add Rollbar for both \`test\` and \`live\` environments. Set the required alerts to your email/Slack/other medium for TL / AM. Better enable Rollbar to open issues on Github.

* [ ] Install StatusCake : Include 3 checks: Authenticated, Drupal Caching, CDN Caching. Use location optimization if the site justifies it.

* [ ] Ensure the live environment StatusCake is connected to the Gizra SiteHealth channel.

#### Server Settings {#server-settings}

* [ ] Connect live domain to [pantheon](https://pantheon.io/docs/articles/sites/domains/) \(or another hosting service\) and to [CloudFlare](https://www.cloudflare.com/) \(or another CDN\), and document the chosen one. For CDN, Pantheon is first choice, than if hosted not on pantheon CloudFlare should be the CDN, for DNS management we always use CloudFlare.

* [ ] Validate/Install SSL and Redirect Http traffic to Https.

* [ ] [Redirect www / non-www](https://pantheon.io/docs/articles/sites/code/redirect-incoming-requests/)- set canonical domain name, if relevant.

* [ ] [Enable native caching](https://pantheon.io/docs/drupal-cache/) and test http caching \([Varnish](http://www.isvarnishworking.com/) or [Pantheon Cache](https://pantheon.io/features/advanced-caching)\). Most important check is for the Homepage.

* [ ] Automatic daily periods backup for a month.

#### Customer Docs {#customer-docs}

* [ ] Create a basic written user guide manual. Remember it will keep being updated as you add more and more tasks and features to the project.

* [ ] Add a wiki entry, add a link to the written user guide.

* [ ] Add another wiki entry, named “Hosting and Monitoring Direct Links”, with direct links to

  * Hosting service

  * CDN

  * Monitoring services

  * Google Analytics

  * Google Search Console

  etc... \(wait, think about any other relevant services to document in the wiki before moving on!\)

#### User Permissions {#user-permissions}

* [ ] Create a matrix of content types with the following criteria:

* view/edit/delete per content type

* /node \(should be blocked\)

* /rss.xml \(should be blocked\)

* define the expected result of each combination for anonymous users

* verify it works as expected, and open a follow up issue if not. For example:

![](https://lh3.googleusercontent.com/c7z5TDukvyXgAroCd34SapK-Nrd3GLs9K5BgF14upv-KIOXehin8buwtqteygZsKCT1UlF4edcAx9Wvat-1bBMQ906ZktZMmzIxur25kesmeIbTZUXaZDmmOUCX-1NLemcJS6Lsh)

#### 

#### 3rd Party Services \(if relevant\) {#3rd-party-services}

* [ ] connect a facebook app

* [ ] connect a twitter account

* [ ] Set custom variables

#### 

#### Site Down Procedure {#site-down-procedure}

* [ ] Create a [Site Down Procedure](https://docs.google.com/spreadsheets/d/1kPEXR7zYNi-cyPhVPGSfaTlncVYzLfCufipNIs5j-Mg/edit?usp=sharing) for Gizra Team, document it on Wiki

* [ ] Consider creating a [Site Status Page](https://uptime.statuscake.com/?TestID=Pejzmr6d2j) for client usage, or consider adding client to the StatusCake email alerts.

* [ ] Create and share Site Down Procedure for Client, document it on Wiki \(see an[Example Template](https://docs.google.com/document/d/19T6j0a6MjUhXiKx1eNuojXLW8W_H1FCcJnz06OhCUdE/edit?usp=sharing)for the wiki entry\)

#### Admin UX and UI {#admin-ux-and-ui}

1. [ ] If it's new project build from scratch, the admin UI/UX is part of the project tasks, and needs to be open as development issues, according to UI/UX repo. [Contact Liat](mailto:liat@gizra.com) for recommended checks and issues.

2. [ ] If it is existing project, open an issue with 5h \(5 hours\) timebox to learn the admin UI and how things was build there and then recommend of possible improvements.

#### SEO {#seo}

* [ ] Connect and get permissions to the [Google Search Console](https://www.google.com/webmasters/#?modal_active=none).

* [ ] Set an analytics ID and get permissions to the [Google Analytics](https://www.google.com/analytics/#?modal_active=none). Create a basic dashboard report and set yourself ongoing updates \(consider using[ this starter template](https://analytics.google.com/analytics/web/template?uid=WTQUny71Sq-rYVJUXEccqw)\).

##### On-Page \(or on-site\) optimization:

* [ ] Title Tag, Meta descriptions.

* [ ] Search for headings inconsistency in the pages \(h2 should be under h1\).

* [ ] Search for content duplications in site \(use [siteliner](http://www.siteliner.com/)\).

* [ ] Check site URL structure \([read more](https://moz.com/learn/seo/url)\).

* [ ] Check Crawl Error Resolutions using Google Webmaster Tools.

* [ ] Check and document the current site speed \(using [Google Page Speed Insight](https://developers.google.com/speed/pagespeed/insights/)\).

* [ ] Perform a Keyword Research. [See this issue](https://github.com/Gizra/CRI/issues/728) for more details and ideas.

##### Technical Optimization

* [ ] XML Sitemap - Install and test.

* [ ] Check Your Robots.txt File: make sure no key pages are being blocked from being crawled by the search engines. Block admin panels and low-quality pages.

* [ ] Verify appropriate usage of redirects.[See this issue](https://github.com/Gizra/CRI/issues/726) for more details.

* [ ] Use [Google Search Console](https://www.google.com/webmasters/tools/home?hl=en) to recognize potential soft 404s. Also ask site owner how did they handle old content that has been removed.

* [ ] Consider 404 page improvements, to include useful links \(both users and robots will use it\), keep general site look and feel, display error message to explain what happened. Also better include a call for action + homepage link + search box \(in site\).

* [ ] Check if site is mobile friendly \(use [Google Mobile-Friendly Text](https://search.google.com/test/mobile-friendly)\).

##### And all that jazz...

* [ ] Perform a quick SEO Audit, see [this issue for more details](https://github.com/Gizra/CRI/issues/724#issue-286587906).

* [ ] Open a discussion/future issue with client regarding possible off-site optimizations. [See this issue for more details](https://github.com/Gizra/CRI/issues/727).



