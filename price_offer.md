# Price offer

* [Price offer Template](http://bit.ly/price-offer-template)
* [Webinar](http://www.gizra.com/content/gizra-way-webinar-budget-goggles/)

## Migration estimation

As migration is a bigger task, which is hard to split into smaller tasks, nor is there
much value to split it to the field level, we are taking a formula approach:


| Item  | Hours |
| -- | -- |
| Each table | 2 |
| Each field | 0.5 |
| Each taxonomy term/ reference/ image/ file field  | 0.5 |
| Another table with data in another language  | 10 |
| Table with content in mixed languages  | 5 |
| Testing  | 5 |

### Examples

A `{content}` table with title, body and reference to an existing `{tags}` table

| Item | Number of items | Total hours |
| -- | -- | -- |
| Table (`{content}`) | 1 | 2 |
| Fields (`title`, `body`, and `tags_reference`) | 3 | 1.5 |
| Reference field (`tags_reference`) | 1 |  5 |
| Testing | 1 |  5 |

**Total: 13.5 hours**

A `{posts_spanish}` and `{posts_english}` table with title, body.

| Item | Number of items | Total hours |
| -- | -- | -- |
| Table (`{content}`) | 1 | 2 |
| Fields (`title`, `body`) | 2 | 1 |
| Another table with data in another language  | 1 | 10 |
| Testing | 1 |  5 |

**Total: 18 hours**

### Pre-processing data

There are cases that for example the body field may hold internal links or media
that needs to be attached. Often times some massaging is needs, however we don't have a specific formula for this
as it's a custom that may differ from site to site. It is important to be aware of
this, and add it to the estimation.
