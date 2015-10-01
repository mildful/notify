# notify
notify est une librairie javascript permettant de créer et d'afficher des notifications. Elle est complètement **indépendante** et ne nécessite donc pas jQuery :).

## Sommaire
- [Bases](create)
- [Paramètres](tweak)
- [Avancés](tweak)

## <a name="how_to"></a>Bases
###_constructor
Pour créer une notification, il suffit d'instancier un objet de la classe Notify :
```javascript
new Notify('A random message here');
```
par défaut, la notification apparaîtra en haut à droite du navigateur et aura le style _info_.

Vous pouvez lier la notification à un élément HTML. Celle ci apparaîtra alors autour de l'élément sélectionné :
```javascript
var elem = document.getElementById('elemId');
new Notify(elem, {
	content: 'Your message here :)'
});
```

Le constructeur de Notify retourne l'id de la notification. Toutes les notifications sont sauvegardées dans un tableau _Notify.notifs_. Vous pouvez accèder à chacune d'entre elles en utilisant l'_id_ généré.
```javascript
var id = new Notify('foo');
console.log(Notify.notifs); // contient toutes les notifications
console.log(Notify.notifs[id]) // retourne l'objet Notify correspondant à la notification 'foo'
```
###Notify.clear()
Avec cet _id_ vous pouvez également supprimer une notification :
```javascript
var id = new Notify('foo');
Notify.clear(id);
OU
Notify.notifs[id].clear();
```

## <a name="create"></a>Paramètres
Lors de la création de la notification, vous pouvez passer en paramètres un objet pour personnaliser la notification.
Il existe de nombreux paramètres, les voici :

```javascript
var elem = document.getElementById('elemId');

new Notify(elem, {
  // le contenu de la notification
  // @default: null
  content: 'Your message here :)',
  // le titre de la notification
  // @default: null
  title: 'Your message here :)',
  // permet d'insérer une image dans la notification
  // @default: null
  image: 'path/to/image.jpg',
  // le style de la notification ('warn', 'error', 'success', 'info')
  // @default: 'info'
  className: 'warn',
  // la marge (en pourcent) qui sépare la notification d'un élément HTML
  // @default: 0
  gap: 4,
  // la marge (en pourcent) qui sépare la notification d'un des bord du navigateur
  // @default: 3
  gapWindow: 7,
  // l'animation d'entrée ('slideDown', 'fadeIn', 'swipeIn')
  // @default: 'slideDown'
  showAnimation: 'swipeIn',
  // l'animation de sortie ('slideUp', 'fadeOut', 'swipeOut')
  // @default: 'slideUp'
  hideAnimation: 'swipeOut',
  // la durée de l'animation d'entrée en ms
  // @default: 400
  showDuration: 500,
  // la durée de l'animation de sortie en ms
  // @default: 200
  hideDuration: 300,
  // activer/desactiver le clic sur la notification pour la faire disparaître
  // @default: true
  clickToHide: false,
  // activer/desactiver la disparition automatique de la notification après un delai
  // @default: true
  autoHide: false,
  // activer le clic sur la notification pour la faire disparaître
  // @default: 5000
  autoHideDelay: 8000,
  // url sur laquelle on est redirigé lorsque l'on clique sur la notification. On peut passer en valeur un array avec true en seconde clef afin d'ouvrir le lien dans un nouvel onglet
  // @default: null
  url: ['http://www.gog.com/', true],
});
```

## <a name="create"></a>Paramètres
#### position
Spécifie la position de la notification par rapport à un élèment HTML ou dans le navigateur

_default: 'top right'_
```javascript
new Notify("Hey, what's up dude ?", {
	position: 'top left'
});
```
La valeur à spécifier dépend de si la notification est liée à un élèment HTML ou si elle s'affiche de manière absolue dans la fenêtre du navigateur :

|positionement| window        | html element  |
|:-----------:| :-----------: |:-------------:|
|top left     | col 3 is      | right-aligned |
|top center   | col 2 is      | centered      |
|top right    | zebra stripes | are neat      |

Valeurs possibles :
top left, top center, top right, right top, right middle, right bottom, bottom right, bottom center, bottom left, left bottom, left middle, left top



#### cubicBezier
Spécifie le cubic-bezier à utiliser pour jouer les animations de sortie/entrée.

_default: 'ease'_
_values :_
- _[all jQueryUI easings](http://easings.net/fr)_
- _CSS3's named easings: "ease", "ease-in", "ease-out", and "ease-in-out"._
- _CSS3's bezier curves (refer to [cubic-bezier.com](http://cubic-bezier.com/))._
- _Spring physics: Pass a two-item array in the form of [ tension, friction ]. A higher tension (default: 500) increases total speed and bounciness. A lower friction (default: 20) increases ending vibration speed. Refer to [Spring Physics Tester](http://codepen.io/julianshapiro/pen/hyeDg) for testing values._
- _Step easing: Pass a one-item array in the form of [ steps ]. The animation will jump toward its end values using the specified number of steps. See [this article](https://css-tricks.com/clever-uses-step-easing/) to learn more about step easing._
```javascript
// example with CSS3's named easing :)
new Notify('Animations are cools', { cubicBezier: 'ease-out' });
```
