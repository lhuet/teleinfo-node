Module teleinfo
===============
Module node.js pour décoder les trames téléinfo.
Il devrait fonctionner avec tous les tarifs et sur tout matériel compatible node avec un port série
(Testé sur Raspberry Pi avec tarif bleu).

Dépendance avec le module serialport.

Utilisation
-----------

Installer le module :

    npm install teleinfo

Importer le module :

```javascript
var teleinfo = require('teleinfo');
```

Récupérer l'instance d'EventEmitter du module en appelant la fonction teleinfo qui prend en paramètre le port série :

```javascript
// Exemple d'utilisation sur Raspberry Pi
var trameEvents = teleinfo.teleinfo('/dev/ttyAMA0');
```

Les trames téléinfo sont envoyées sous forme d'évènements :
* trame : trames brutes non vérifiées (utile uniquement à des fins de debug)
* tramedecodee : trames sous forme d'un objet (checksums validés pour chaque propriété)

Exemple :

```javascript
trameEvents.on('tramedecodee', function (data) {
  console.log(util.inspect(data));
});
```

Objet récupéré (data) du type :

```javascript
    { ADCO: '000000000000',
      OPTARIF: 'BASE',
      ISOUSC: 30,
      BASE: 6366719,
      PTEC: 'TH..',
      IINST: 1,
      IMAX: 30,
      PAPP: 300,
      MOTDETAT: '000000' }
```

