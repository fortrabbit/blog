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
wip: true
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

:Quote{ author="Melvin E. Conway" text="Organizations which design systems are constrained to produce designs which are copies of the communication structures of these organizations." }

## Images

![Manage landing page](/images/action-ui.png)

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
AuthUserFile /srv/app/{{app-env-id}}/htdocs/.htpasswd
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
