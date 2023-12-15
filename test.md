---
author: fl
figure:
  text: TEST 1 2
  emoji: 🍓
  caption: You can feed the figure 'image', 'icon' (Icones), 'text', 'emoji' and 'caption'
title: Testing article
lead: This article tests various features of content display.
intro: TESTING page to show features
created: 2029-11-30 11:37:22
draft: true
links:
  - title: Test
    intro: to external link
    type: external
    route: https://test.com
tag:
  - chronicles
head:
  meta:
    - name: 'keywords'
      content: 'TANKY TANK'
---

Did you know? We can see this DRAFT locally, but not in production.

## Lists

1. one
2. two
3. three
   a. 3a
   b. 3b

- bullet
- bullet
- bullet
  - indented
  - indented
    - indented

## Emphasis

_This text will be italic_  
_This will also be italic_

**This text will be bold**  
**This will also be bold**

_You **can** combine them_

## Tables

| Left columns | Right columns |
| ------------ | :-----------: |
| left foo     |   right foo   |
| left bar     |   right bar   |
| left baz     |   right baz   |

## MD Blockquote

> No passion in the world is equal to the passion to alter someone else's draft.  
> — H.G. Wells

## MDC Blockquote

::BlockQuote{text: "I just wanted to say that the documentation that you guys have and the service you provided me while I was initially setting everything up was probably the best I've encountered in my 20-ish years of front-end web development. Your dashboard is super simple and it has all of the right things for someone like me; good enough at this stuff to be slightly dangerous, and none of the other stuff that is fluff and not necessary. The fact that there is no cPanel is so refreshing! If there is a public place to leave a review, I'd be happy to do so.", time: '2023', source: 'customer support chat', author: { name: 'Scott Cooper' }, link: { name: 'www.wscottcooper.com', href: '<http://www.wscottcooper.com/>'}}::

## Code highlighting

```js [src/index.js] {1, 2-3}
const a = 4;
const b = a + 3;
const c = a * b;
```

```php [index.php]
class A {
  private Traversable&Countable $countableIterator;

  public function setIterator(Traversable&Countable $countableIterator): void {
    $this->countableIterator = $countableIterator;
  }

  public function getIterator(): Traversable&Countable {
    return $this->countableIterator;
  }
}
```

```apache [.htaccess]
Authtype Basic
AuthName "Welcome to my awesome project. Please Login."
AuthUserFile /srv/app/{{app-env-slug}}/htdocs/.htpasswd
Require valid-user
```

```yml
links:
  - title: Test
    intro: to external link
    type: external
```

```json
{
  "squadName": "Super hero squad",
  "homeTown": "Metro City",
  "formed": 2016,
  "secretBase": "Super tower",
  "active": true,
  "members": [
    {
      "name": "Molecule Man",
      "age": 29,
      "secretIdentity": "Dan Jukes",
      "powers": ["Radiation resistance", "Turning tiny", "Radiation blast"]
    },
    {
      "name": "Madame Uppercut",
      "age": 39,
      "secretIdentity": "Jane Wilson",
      "powers": ["Million tonne punch", "Damage resistance", "Superhuman reflexes"]
    }
  ]
}
```

```twig [src/templates/partials/navigation.twig]
{% for item in navigation %}
  <li><a href="{{ item.href }}">{{ item.caption }}</a></li>
{% endfor %}
```

links:

- title: Test
  intro: to external link
  type: external
  route: <https://test.com>
