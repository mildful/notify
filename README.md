# notify
notify est une librairie javascript permettant de crééer des notifications de manières simple et personnalisée.
Notez que jQuery n'est **pas** nécessaire ! ;)

## Sommaire
- [Utilisation](how_to)
  - [créer](create)
  - [paramètrer](tweak)  
  - [styliser](design)
- [Arborescence](hierarchy)

## <a name="how_to"></a>Utilisation
### <a name="create"></a>créer
Pour faire apparaître une notification, il suffit d'instancier un objet de la classe Notify :
```javascript
new Notify('A random message here');
```
par défaut, la notification apparaîtra en haut à droite du navigateur et aura le style _info_.

Vous pouvez faira apparaître la notification près d'un élèment HTML :
```javascript
var elem = document.getElementById('elemId');
new Notify(elem, {
	content: 'Your message here :)'
});
```

Le constructeur de Notify retourne l'id de la notification. Toutes les notifications sont sauvegardées dans un tableau _Notify.notifs_. Vous pouvez accèder à chacune d'entre elles en utilisant l'_id_ généré.
```javascript
console.log(Notify.notifs); // contient toutes les notifications

var id1 = new Notify('foo');
console.log(Notify.notifs[id]) // retourne l'objet Notify correspondant à la notification 'foo'
```

### <a name="create"></a>paramètrer
Lors de la création de la notification, vous pouvez passer en paramètres un objet pour personnaliser la notification.
```javascript
// exemple de personnalisation
new Notify('something wrong happened', {
    className: 'warn',
    position: 'bottom right',
    showAnimation: 'swipeIn',
    hideAnimation: 'swipeOut',
    hideDuration: 600
});
```


Il existe de nombreux paramètres, les voici :
#### content
Le contenu textuel de la notification. Surtout utile lorsque l'on veut faire apparaître la notification près d'un élèment HTML

_defaul: null_
```javascript
// étant donné que le premier argument n'est plus le message, on le passe via content
var elem = document.getElementById('elemId');
new Notify(elem, {
	content: 'Your message here :)'
});
```


#### title
Le titre de la notification

_default: null_
```javascript
new Notify('"Hey, what\'s up dude ?', {
	title: 'New message !'
});

```

#### image
Permet d'insérer une image dans la notification. Pour en savoir plus, lire [styliser](design)
_default: null_
```javascript
new Notify('"Hey, what\'s up dude ?', {
	image: 'path/to/image.jpg'
});
```


#### position
Spécifie la position de la notification par rapport à un élèment HTML ou dans le navigateur

_default: 'top right'_
```javascript
new Notify('"Hey, what\'s up dude ?', {
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


#### className
Permet de spécifier le style de notification à utiliser. Pour savoir comment créer vos propres classes, lire [styliser](design)

_default: 'info'_
```javascript
new Notify('The sky is blue', { className: 'info' });
new Notify('Care !', { className: 'warn' });
new Notify('The server is dead.', { className: 'error' });
new Notify('Your website is online !', { className: 'success' });
```


#### gap
La marge en pixel qui gère l'espacement entre les bords d'un élèment HTML et de la notification.

_default: 0_
```javascript
new Notify('The witcher 3 is amazing.', { gap: 10 });
```


#### gapWindow
Similaire à _gap_ mais permet de gérer l'espacement avec les bords de la fenêtre.

_default: 3_
```javascript
new Notify('The witcher 3 is amazing.', { gapWindow: 12 });
```


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


#### showAnimation
Nom de l'animation d'entrée.

_default: 'slideDown'_

_values: slideDown, fadeIn, swipeIn_
```javascript
new Notify('foobar', { showAnimation: 'swipeIn' });
```


#### hideAnimation
Nom de l'animation de sortie.

_default: 'slideUp'_

_values: slideUp, fadeOut, swipeOut_
```javascript
new Notify('foobar', { hideAnimation: 'swipeOut_' });
```


#### showDuration / hideDuration
Durée en milliseconde de l'animation d'entrée ou de sortie.

_default: 400 (showDuration) / 200 (hideDuration)_
```javascript
new Notify('foobar', { 
	showDuration: 320,
	hideDuration: 300
});
```


#### clickToHide
Permet de supprimer la notification lorsque l'utilisateur clique dessus.

_default: true_
```javascript
new Notify('foobar', { clickToHide: false });
```


#### autoHide
Permet de cacher automatiquement la notification après un délai _autoHideDelay_.

_default: true_
```javascript
new Notify('foobar', { autoHide: false });
```


#### autoHideDelay
Permet de gérer le delai avant l'autoHide

_default: 5000_
```javascript
// la notification restera 8 secondes à l'écran avant de disparaître.
new Notify('foobar', { autoHideDelay: 8000 });
```


### url
Permet de spécifier un lien sur lequel rediriger en _blank lors du clique sur la notification.

_default: null_
```javascript
// la notification restera 8 secondes à l'écran avant de disparaître.
new Notify('GO GOG', { url: 'https://www.gog.com/' });
```
