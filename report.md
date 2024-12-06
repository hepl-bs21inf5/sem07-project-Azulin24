# Journal de bord
| Tâche  | Temps estimé| Temps passé | Commentaire |
| ------------ | ----| ----------- | ---------------------|
| Journal de bord| 10min  |   20min| je ne savais pas comment le structurer (pour que ce soit lisible) |


# Semaine 1, début du projet.

| Tâche  | Temps estimé| Temps passé | Difficulté rencontrée | Solution | commentaire|
| ------------ | ----| ----------- | ---------------------|----- | --- |
| Vue.js       | 1h    |  19min    |   | | Je pensais que ça allait être plus long|
| Bootstrap| 1h20min |   18min |           |  | Je pensais que ça allait être plus long|
|  Quiz | 1h | 1h 57min | 1.- Je ne savais pas comment faire pour afficher le score à la fin du quiz. La boucle for sur Javascript toujours pas maîtrisée au 100% 2.- je ne trouvais pas nav, je le cherchais sur le document html |  1.-l'ajouter la variable "let score" recommandé par chatgpt. 2.- l'enseigant m'a dit où il se trouvait |
| Raport | 25min |  58min |  | | Aucune difficultée rencontrée, je pensais juste que ça allait être plus rapide avec des réponses courtes. 
| Total        |  3h25min       |                 |   |    |

# Explications et réflexions sur le code

Le rôle de:

- main.ts: 
    
        Le fichier initialise l'application Vue.js, charge les styles globaux, configure les plugins (comme Vue Router), monte l'application.

- main.css : 
    
        Contient les règles CSS globales pour l'application, permettant de définir les polices, les couleurs, les marges, des ajustements pour harmoniser les styles tiers (comme Bootstrap). Il est aussi importé dans main.ts pour être disponible dans toute l'application.

- App.vue : 
    
        C'est le composant racine, il englobe toute l'application et rend les vues via <router-view>.

- router/index.ts : 
    
        Configure la navigation entre les pages grâce à Vue Router.

- AboutView.vue : 
    
        Composant pour la page "À propos", affichant des informations sur l'application.

- HomeView.vue : 
    
        Composant pour la page d'accueil, servant de point d'entrée visuel à l'application.

- QuizForm.vue : 
    
        Composant interactif pour poser des questions, collecter des réponses, et gérer un quiz.Ainsi, il est conçu pour interagir avec l'utilisateur via un formulaire. Il gère aussi la logique d'intéraction comme la validation des réponses, le calcul de score ou de résultats, la soumission des données.


Dans le fichier QuizForm.vue :

Quelles sont les similarités et les différences entre ref et computed ?

    Similarités: 

    - Tous deux sont des fonctionnalités de Vue 3 Composition API utilisées pour gérer des 
    données réactives.

    - Ils déclenchent une mise à jour du DOM chaque fois que leurs valeurs changent.

    - Ils sont utilisés dans le même but général : gérer des états réactifs et dépendants.

    Différences:

    - Ref a une valeur réactive qui peut être directement modifiée, tandis que Computed a une valeur calculée basée sur d'autres valeurs réactives.

    - Ref stocke un état brut ou une donnée observable, tandis que Computed génère un état dérivé automatiquement.

    - Ref peut être modifié directement (ref.value = ...), tandis que Computed ne peut pas être modifié directement, car il est calculé.

    - Ref suit une valeur entrée par l'utilisateur, tandis que Computed calcule si tous les champs d'un formulaire sont remplis.

Que se passe-t-il lorsqu'on clique sur le bouton "Terminer" ?

    La fonction submit est exécutée: elle empêche le rechargement, calcule un score basé sur les réponses, et affiche une alerte avec le résultat.

Qu'est-ce qu'un v-model ?

    Une directive pour lier bidirectionnellement un champ HTML à une variable réactive (ref) afin de synchroniser automatiquement les données. Si l'utilisateur modifie la valeur dans l'interface, le v-model met à jour automatiquement la variable associée.
    Par exemple: Quand l'utilisateur saisit "4" dans la question "Combien de pattes a un chat ?", la valeur de chat est automatiquement mise à jour.


À quoi sert le :class="{ disabled: !filled }" ?

    La syntaxe :class="{ disabled: !filled }" permet une liaison dynamique de classe CSS. Elle ajoute ou retire la classe disabled en fonction de la valeur de l'expression !filled.

    La propriété filled retourne true si toutes les questions ont été répondues.
    Si filled est false (au moins une réponse est manquante), la classe disabled est appliquée au bouton "Terminer". Cette classe peut modifier son apparence (par exemple, le griser) ou désactiver son clic, si elle est stylisée ainsi dans le CSS.


# Suite du projet

Il es possible de modifier les questions afin de personnaliser le projet. On peut aussi ajouter plus de choix, ou même des cases vides à remplir.

# Semaine 2.

| Tâche  | Temps estimé| Temps passé | Difficulté rencontrée | Solution | commentaire|
| ------------ | ----| ----------- | ---------------------|----- | --- |
|   Question radio | 20min   | 20min   |   | | |
|  QuestionText | 20min | 50min  |    je ne savais pas quoi écrire sur QuestionText.vue pour que ça  marche correctement    | J'ai demandé de l'aide à chatgpt afin de compléter mon code| J'ai passé quelques 1.5-2.5 heures supplémentaires à comprendre chaque changement que l'IA me recommendait de faire (je triais le plus important)|
|  QuestionCheckbox | 30min |  1h05min |  compter le score avec le choix multiple| Aucune pour l'instant |Même si je réponds à toutes les réponses justes, il ne valide que 3 réponses justes, les réponses du choix multiple ne sont jamais prises en compte. 
|  API | 1h | 20min |aucune  | | Je pensais que ce serait plus long
|Modification des questions| 15min | 16 min| | |je voulais personnaliser un peu le Quiz
| Total        |   2h25min     |     2h51min            |   |    |


# Explications et réflexions sur le code
Quelle est la différence entre un prop et un modèle (v-model) ?

        Un prop est un mécanisme qui permet de transmettre des données du composant parent vers le composant enfant. Ces données sont en lecture seule dans l'enfant, ce qui signifie que l'enfant ne peut pas directement les modifier. Les props sont souvent utilisées pour configurer ou personnaliser le comportement d'un composant enfant avec des valeurs statiques ou dynamiques. Par exemple, un composant de bouton peut recevoir une prop pour définir son libellé ou sa couleur.

        Le modèle (v-model), quant à lui, est une fonctionnalité qui établit une liaison bidirectionnelle entre une donnée du parent et le composant enfant. Cela signifie que les données circulent dans les deux sens : le parent peut transmettre une valeur initiale à l'enfant (comme avec un prop), et l'enfant peut mettre à jour cette valeur dans le parent grâce à un événement automatique. Cela est particulièrement utile dans des situations dynamiques, comme les champs de formulaire ou les composants interactifs, où l'utilisateur modifie les données.

Comment rendre la propriété placeholder optionnelle ?

        Pour rendre la propriété placeholder optionnelle, il suffit de la déclarer dans les props avec un type défini et de lui attribuer une valeur par défaut, comme une chaîne vide.

# Semaine 3.
| Tâche  | Temps estimé| Temps passé | Difficulté rencontrée | Solution | commentaire|
| ------------ | ----| ----------- | ---------------------|----- | --- |
|   Réponse | 20min   |    |   | | |
|  Score | 20min |   |      | | |
| Total        |       |                 |   |    |
