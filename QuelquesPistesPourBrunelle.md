# Quelques pistes pour Brunelle 

## Bonjour
Bonjour, je ne sais rien de vous, si ce n'est que nous sommes tous les deux auditeurs en UTC 503.
Je vais donc evoquer quelques points, qui me semblent saillants pour moi pour essayer de vous aider.
Je n'ai pas la prétention de faire un cours. Seulement faire pour moi un exercice de synthèse sur le langage Ocmal

## Comment faire du Ocaml ?
### mon éditeur de texte en ligne que j'aime bien...
Personnellement, j'aime bien avoir du concret : J'aime bien utiliser [try.ocamlpro.com](http:try.ocamlpro.com)
C'est un éditeur qui permet de voir ce qu'on fait, et une console qui permet te tester les fonctions.
(try.ocmal.pro.png)

### Un premier programme
on écrit un programme
```Ocaml
(* Mon premier commentaire, 
   au début de mon premier programme en Ocaml...*)
let coucou = "Coucou";;
(* Et histoire de voir qu'il se passe quelque chose...*)
print_string(coucou);;
```
On le lance avec le bouton "Evaluer le code" en bas, et on a le résultat de l'exécution dans la colonne de droite.
(fig2.png)

### Quelques règles à partir de cette exemple :

- Toute affectation (variable ou fonction, ce qui est pareil en Ocmal), commence par le clé `let`
- Pour écrire quelque chose, il faut faire appel à la fonction print_string() ou print_int() selon ce qu'on veut écrire !
- Les variables sont "unmutables", c'est à dire qu'on ne peut pas écrire coucou = coucou + " machin"

## Ecrire une fonction
### la base
```Ocaml
let f x = 2*x;;
print_int(f 3);;
```

Je n'y peut rien, c'est comme cela ! 
La fonction s'appelle f, le paramètre x, et la valeur renvoyée est 2 * 2.
Comme je veux travailler avec des entiers, je mets print_int().

Original mais pas très compliqué !
(fig3.png)

### Utilisation de la Console
Un petit truc sympa, c'est qu'une fois le code évalué je peux l'essayer dans la console (fig4.png)
Je tape 
```Ocaml
f 5
```
Et il me retourne
```Ocaml
- int = 10
```
### La "Force" de Ocmal (et du paradigme fonctionnel en général)
Ce qui est très fort, c'est l'appel récursif!
Par exemple je veux calculer n!. Appelons `fact n` la fonction qui va le faire
la méthode est toujours la même:
1) Quel est le plus petit cas ? ici, on prend n = 1, et 1! = 1, d'où fact 1 doit renvoyer 1.
2) On suppose que le programme tourne jusqu'à n-1... c'est à dire de fact (n-1) a du sens. Comment vais-je calculer fact n ? 
Assez clairement, pour moi, fact n = n * fact (n-1).

En python cela donerait cela 
```python
def fact(n:int)->int:
  if n == 1:
    return 1
  return n * fact(n-1)
  
print(fact(5))
```

Et bien en Ocmal, cela s'écrit
```Ocaml
let rec fact n = if n = 1 then 1 else n*fact (n-1);;
(* et pour voir le résultat... *)
print_int(fact 5);;
```

Ou si on veut faire joli...
```Ocaml
let rec fact n = 
  if n = 1 then 
    1 
  else 
    n * fact (n-1);;
    
(* et pour voir le résultat... *)
print_int(fact 5);;
```
### Quelques règles

- Ne pas oublier le mot clé `rec` qui marque que la fonction est récursive. Sinon, elle ne peut s'appeler elle-même
- Il faut impérativement traiter tous les cas ! Sinon le compilateur ava pas être très content...
Dans le cas présent, le prof m'a fait remaraquer que pour éviter n = 0 ou n < 0, on peut écrire
```Ocaml
let rec fact n = if n <= 1 then 1 else n*fact (n-1);;
(* et pour voir le résultat... *)
print_int(fact 5);;
```
Mais à notre petit niveau, on suppose que l'utilisateur n'écrit pas n'importe quoi ;-) Car le else traite bien tous les cas différents de n = 1. 


### Parenthèses, pas parenthèses ?
Cela peut être déroutant au départ, mais Ocmal n'a pas besoin de parenthèse, tant que cela se lit directement. Ici, seul (n-1) nécessite des parenthèses, car on veut avoir l'image de n - 1 par la fonction fact, et non 1 ôté à l'image de n par fact.
Là encore, c'est comme cela. On apprend, et on fait avec.
Toutefois, si on met des parenthèses partout, Ocaml

## Les tableaux en Ocaml

### Super simple...
```
let = tab[1; 2; 3];;
```
### Attention !
Tous les éléments doit avoir le même type.

## La manipulation des tableaux
### hum... Ocaml pas gentil...
On ne peut que prendre la premier élement, ou tout le reste ! C'est assez violent pour quelqu'un qui arrive d'un langage où on peut aller taper n'importe où dans le tableau... Mais c'est comme cela
Pour cela il y a deux fonctions dans le module `List`, qui gère les listes :

- `List.hd(tab)`, qui renvoie le premier terme
- `Liste.tl(tab)', qui renvoie tout le tableau, sauf le premier élément. (attention, si tab = [], cela plante !)

Pour comprendre, rien ne vaut un exemple :
```Ocaml
let tab = [1; 2; 3];;
let debut = List.hd(tab);;
let fin = List.tl(tab);;
```

on a `debut = 1` et `fin = [2; 3]`.

Alors comment faire pour manipuler un tableau ?

Avec conrage, on applique la méthode
on veut multipler tous les termes d'un tabelau par 2. Soit `double` cette fonction, qui a un tableau comme paramètre, et qui renvoie un tableau.
1. Le plus petit cas... le tableau vide [], et donc `double []` renvoie `[]`
2. On suppose que cela marche avec une liste de taille n-1, et que donc `double [...]` a du sens. Que se passe-t-il pour mon tableau de taille n ?
Et bien, je dis que le résultat c'est un premier tableau de 1 élément, le premier qui va être multiplié par 2, concaténé au tableau renvoyé par `double [...]`.
la concaténation se note "@" pour les listes et ^ pour string
On a donc cela 

```Ocaml
let double tab =
   if tab = [] then
      []
   else [List.hd(tab)] @ double List.tl(tab);;
``` 

Simple, non ?



