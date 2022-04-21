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
  let coucou = "Coucou";;
  print_string(coucou);;
```
On le lance avec le bouton "Evaluer le code" en bas, et on a le résultat de l'exécution dans la colonne de droite.
(fig2.png)
Encore là ?

### Quelques règles à partir de cette exemple :

- Toute affectation (variable ou fonction, ce qui est pareil en Ocmal), commence par le clé `let`
- Pour écrire quelque chose, il faut faire appel à la fonction print_string() ou print_int() selon ce qu'on veut écrire !
- Les variables sont "unmutables", c'est à dire qu'on ne peut pas écrire coucou = coucou + " machin"




