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
| Total        |  3h45min       |      3h32min           |   |    |

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
    
        Composant pour la page d'accueil, servant de point d'entrée visuel à l'application. (Fait appel au fichier Quizform.vue)

- QuizForm.vue : 
    
        Composant interactif pour poser des questions, collecter des réponses, et gérer un quiz.Ainsi, il est conçu pour interagir avec l'utilisateur via un formulaire (dans ce cas, notre quiz). Il gère aussi la logique d'intéraction comme la validation des réponses, le calcul de score ou de résultats, la soumission des données.


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
|  QuestionCheckbox | 30min |  1h05min |  compter le score avec le choix multiple| Aucune pour l'instant |Même si je réponds à toutes les réponses justes, il ne valide que 3 réponses justes, et jamais le checkbox car je ne peux pas mettre plusieurs réponses. 
|  API | 1h | 20min |aucune  | | Je pensais que ce serait plus long
|Modification des questions| 15min | 16 min| | |je voulais personnaliser un peu le Quiz
| Raport | 30min | 40min  |  | | |
| Total        |   2h55min     |     3h31min            |   |    |


# Explications et réflexions sur le code
Quelle est la différence entre un prop et un modèle (v-model) ?

        Un prop est un mécanisme qui permet de transmettre des données du composant parent vers le composant enfant. Ces données sont en lecture seule dans l'enfant, ce qui signifie que l'enfant ne peut pas directement les modifier. Les props sont souvent utilisées pour configurer ou personnaliser le comportement d'un composant enfant avec des valeurs statiques ou dynamiques. Par exemple, un composant de bouton peut recevoir une prop pour définir son libellé ou sa couleur.

        Le modèle (v-model), quant à lui, est une fonctionnalité qui établit une liaison bidirectionnelle entre une donnée du parent et le composant enfant. Cela signifie que les données circulent dans les deux sens : le parent peut transmettre une valeur initiale à l'enfant (comme avec un prop), et l'enfant peut mettre à jour cette valeur dans le parent grâce à un événement automatique. Cela est particulièrement utile dans des situations dynamiques, comme les champs de formulaire ou les composants interactifs, où l'utilisateur modifie les données.

Comment rendre la propriété placeholder optionnelle ?

        Pour rendre la propriété placeholder optionnelle, il suffit de la déclarer dans les props avec un type défini et de lui attribuer une valeur par défaut, comme une chaîne vide.

# Semaine 3.
| Tâche  | Temps estimé| Temps passé | Difficulté rencontrée | Solution | commentaire|
| ------------ | ----| ----------- | ---------------------|----- | --- |
|   Réponse | 1h   | 55min   |   | | |
|  Score | 30min | 50min  |    totalScore ne calculait pas le score maximal possible.   | il fallait modifier la définition de totalScore pour qu'elle utilise Object.keys() sur correctAnswersData car avant j'essayais de calculer la valeur totalScore en utilisant la propriété length sur un objet, ce qui n'est pas valide.| J'ai demandé de l'aide à ChatGPT mais il modifiait des choses qu'il fallait pas donc j'ai passé beaucoup de temps à trier la bonne information.|
| Raport | 30min | 50min  |  | ||
| Total        |  2h     |  2h35               |   |    |

# Explications et réflexions sur le code
À quoi sert l'option immediate: true dans le watch ? Que se passe-t-il si on l'enlève ou si on met immediate: false ?

- Comportement de immediate: true

        Lorsque immediate: true est défini, la fonction de rappel (ici updateCorrectAnswers) est exécutée immédiatement une fois que le watch est défini, avant même qu'une des propriétés observées ne change. Cela permet d'initialiser ou de synchroniser des valeurs dès que le composant est monté, en tenant compte de l'état initial des propriétés observées.

        Dans mon code, immediate: true garantit que la fonction updateCorrectAnswers est exécutée immédiatement, ce qui remplit initialement la valeur de correctAnswers avec une évaluation basée sur l'état actuel des réponses utilisateurs (toutes initialisées à null ou []).

- Si on enlève immediate: true ou si on met immediate: false

        La fonction updateCorrectAnswers ne sera pas appelée automatiquement après que le watch soit configuré.
        Elle ne sera exécutée qu'en réponse à des modifications ultérieures des propriétés observées (MachuPicchu, Gastronomie, oiseau, attractions_Perou).
        Donc, la valeur initiale de correctAnswers restera dans son état par défaut ([false, false, false, false]) jusqu'à ce que l'utilisateur commence à interagir avec les champs.
        Si on affiche des résultats basés sur correctAnswers avant une interaction, ils seront incorrects ou non pertinents (par exemple, affichant "Réponse correcte : false" pour toutes les questions dès le début).

Proposer une autre manière de calculer le score (réécrire la fonction du computed) et comparer les deux méthodes.

- Méthodes: 

        La méthode utilisée est donc filter pour extraire les valeurs true dans le tableau correctAnswers.value, puis utilise length pour compter le nombre de réponses correctes.

        const score = computed<number>(() => correctAnswers.value.filter((value) => value).length);

        Une autre manière de calculer le score serait d'utiliser "reduce", donc: 

        const score = computed<number>(() => correctAnswers.value.reduce((acc, value) => acc + (value ? 1 : 0), 0));

        Cette méthode prend une fonction de rappel et un accumulateur initial (ici, 0). Pour chaque élément de correctAnswers.value, la fonction de rappel ajoute 1 à l'accumulateur si l'élément est true, sinon elle ajoute 0. À la fin, "reduce" retourne le total des valeurs, c'est-à-dire le score.

- Comparasion:

        Les deux méthodes ont des performances comparables pour la plupart des cas d'utilisation courants. Cependant, reduce peut être légèrement plus performant dans certaines situations, car il effectue l'itération en une seule passe et ajoute un résultat directement, tandis que filter crée un nouveau tableau.

        filter est plus déclarative et directe, ce qui rend cette méthode plus simple à comprendre. Par contre,la méthode avec "reduce" est un peu plus complexe, surtout si on n'est pas habitué à reduce. Il faut comprendre comment fonctionne l'accumulateur et comment il est mis à jour à chaque itération. Cependant, une fois compris, reduce est une méthode très puissante et flexible car il permet d'appliquer n'importe quelle logique à chaque élément (surtout si les calculs deviennent plus complexes).

- En conclusion:

        Pour les petits tableaux et si le but est d'avoir une solution simple et facile à comprendre, il faut utiliser filter + length, ce qui est généralement suffisant.
        Pour les tableaux plus grands ou s'il faut effectuer des calculs plus complexes sur chaque élément, reduce peut être plus performant et plus flexible.
        Dans notre code, les deux méthodes donnent le même résultat: le score calculé en fonction des réponses correctes.


# Semaine 4.

| Tâche  | Temps estimé| Temps passé | Difficulté rencontrée | Solution | commentaire|
| ------------ | ----| ----------- | ---------------------|----- | --- |
|   Etats |  1h15min  |  58min |   | | |
|  Boutons | 50 min |  41min |    | | les reponses ne se vident toujours po
|  Réponses immuables|  10 min  |  2min |   | | |
| Raport | 45min |  30min |  | ||
| Total        |  3h     |    2h11min            |   |    |

# Explications et réflexions sur le code


Comment pourrait-on réécrire la ligne suivante sans l'opérateur ternaire (avec des if et else) ?
model.value =
  value.value === props.answer ? QuestionState.Correct : QuestionState.Wrong;


        on peut écrire:
        if (value.value === props.answer) {
        model.value = QuestionState.Correct;
        } else {
        model.value = QuestionState.Wrong;
        }


Comment pourrait-on réécrire autrement la logique du watch sur value ?

        On peut simplemement utiliser un computed: 
        const model = {
        value: computed(() => {
        return value.value === null ? QuestionState.Empty : QuestionState.Fill;
        }),
        };
        Plus besoin d'utiliser un watch pour synchroniser model.value, car computed le met à jour automatiquement.

# Semaine 5.

| Tâche  | Temps estimé| Temps passé | Difficulté rencontrée | Solution | commentaire|
| ------------ | ----| ----------- | ---------------------|----- | --- |
|   Réponse détaillée |  30min  |  10min |   | | |
|  Style | 10min | 2min  |    | |
| Raport | 40min | 25min  |  | ||
| Total        |  1h20min    |  37min              |   |    |

# Explications et réflexions sur le code

Ajouter ce computed dans QuestionRadio.vue :
const answerText = computed<string>(
  () =>
    props.options.find((option) => option.value === props.answer)?.text ??
    props.answer,
);
Remplacer {{ props.answer }} par {{ answerText }} dans le template.

Expliquer pourquoi on a fait ce changement ainsi que le code du computed.


        On souhaite rechercher, dans props.options, une option qui correspond à la valeur de props.answer. Si une correspondance est trouvée, cette option est retournée. En utilisant un computed, on crée une propriété réactive qui sera recalculée automatiquement dès que props.answer ou props.options sera modifié.


Que se passe-t-il lorsqu'on ne met pas de valeur à answer-detail ? Est-ce satisfaisant ? Si ce n'est pas le cas, proposer une amélioration.


        Si aucune valeur n'est fournie à answer-detail, la propriété sera indéfinie, ce qui peut entraîner des comportements inattendus ou des affichages vides. Pour améliorer cela, on peut définir une valeur par défaut dans les props (par exemple, une chaîne vide) ou rendre la propriété obligatoire avec required: true. Une autre option est de gérer ce cas dans le template en affichant un message alternatif comme "Aucune information disponible".



# Semaine 6.

| Tâche  | Temps estimé| Temps passé | Difficulté rencontrée | Solution | commentaire|
| ------------ | ----| ----------- | ---------------------|----- | --- |
|   Déploiement | 15min |  |   | ||
|  Amélioration QuestionText.vue | 1h |  1h |    | | 
| Amélioration Trivia | 2h |  58min |    || pas fini car je suis fatigué| 
| Raport | 45min | 1h30min  |  | ||
| Vérification du code et problèmes à régler   |  1h     |     4h           |  Beaucoup, plus de détail à la fin du report |    | Pleins de fautes accumulées avec le temps.
| Total        |  3h     |                |   |    |



# Améliorations

QuestionCheckbox.vue : Sélectionner plusieurs réponses.

- Pourquoi avez-vous choisi ces améliorations ? 
        
        Je l'avais déjà commencé en cours donc j'ai juste décidé de le finir.

- Comment les avez-vous implémentées ? 

        C'était pareil que radio, il fallait aujouter une liste de réponses et un watch qui surveillait les réponses.

- Quels problèmes avez-vous rencontrés ? 
        
        Le bouton "terminer" ne s'activait jamais, j'ai passé des semaines à essayer de comprendre le pourquoi, je ne sais pas pourquoi mais j'ai décidé d'effacer la question "checkbox" et tout marcahait comme prévu. Après avoir analysé le code mille fois, je me suis rendu compte que je n'avais  pas changé le type à checkbox, j'avais laissé type="radio". Aussi, le fait de créer une liste de réponses et pas une seule était difficile à comprendre, j'ai demandé de l'aide à une camarade et m'a dit qu'il fallait juste changer le type de answer et par conséquent le watch aussi
- Quelles améliorations pourriez-vous encore apporter ? 

        Je ne sais vraiment pas, juste styliser pour que ce soit plus beau.

Accepter plusieurs réponses possibles pour QuestionText.vue (par exemple, "2" ou "deux").

- Pourquoi avez-vous choisi ces améliorations ? 

        C'est celle qui semblait le plus facile.

- Comment les avez-vous implémentées ?

        Answer est aussi une liste, mais cette fois le watch aussi devait être changé, si newModel est égal à QuestionState.Submit, il faut vérifier si la réponse de l'utilisateur correspond à une des réponses possibles (props.answer).

- Quels problèmes avez-vous rencontrés ? 

        Pas vraiment de problème, c'était assez simple. Juste, faire la liste de LIMA. lima. ou Lima c'était pas fifou, donc j'ai décidé de faire que le programme convertisse la réponse donnée par l'utilisateur en minuscule.

- Quelles améliorations pourriez-vous encore apporter ?

        Accepter les réponses qui sont en un autre langage je suppose. 

Adapter le Trivia pour pouvoir y jouer.

- Pourquoi avez-vous choisi ces améliorations ? 

        ça avait l'air compliqué donc j'ai décidé de tester.

- Comment les avez-vous implémentées ? 

        J'ai surtout copié collé beaucoup d'infos qui y sont déjà sur Questionradio car c'est des QCM avec une seule réponse. Les boutons je l'ai pris de quizform.

- Quels problèmes avez-vous rencontrés ? 

        Pour l'instant aucun.

- Quelles améliorations pourriez-vous encore apporter ? 

        Comme c'est des questions au hasard, j'aimerais bien ajouter un bouton pour avoir des nouvelles questions.


# Diffultés en général

J'ai passé beaucoup de temps les premières semaines à comprendre ce que je faisais, souvent je comprenais même pas, cela est devenu un problème quand mon code ne marchait plus alors que je fasais tout "juste", des petites choses comme le type ou le model restaient des concepts assez abstraits pour que je puisse comprendre complètement. Après avoir passé énormément de temps sur le projet, j'ai commencé à comprendre, surtout en enlevant et en rajoutant des lignes. J'ai remarqué qu'il y avait beaucoup de choses inutiles, je me suis beaucoup aidé de chatgpt au début et je comprenais l'explication donnée de chaque élément individuel, mais l'ensemble restait flou. Je n'avais aucun guide (ou c'est ce que je pensais) et j'avais mis un tableau comparatif afin de donner les bonnes réponses à la machine. J'avais une const AnswerDataUpdate car cela me parassait trè logique. Puis j'ai remarqué que answer était déjà indiqué dans la propre question: id="oiseau" v-model="questionStates[2]"et là il y  answer='Condor', je sais pas pourquoi ça m'a pris du temps alors que ça reste très logique. J'avais quand mêmê peur d'effacer le tableau, jusqu'à que un ami me dise que sur le site github il y a le code exemple de l'enseignant (je savais déjà mais je pensais pas qu'il y avait vraiment le code, je pensais qu'il y avait juste le lien du site comme exemple). Avec ce code j'ai réglé toutes les petites fautes et j'ai mieux adapté questionradio et questiontext, ce qui m'a aidé pour régler mon problème sur Chekbox.

Aussi, je ne sais pas pourquoi quand j'appuie sur réinitialiser, les questions radio ne se vident pas, pourtant, l'état affiche "empty". J'ai regardé plusieurs fois si la function ou le button étaient bien écrit mais tout est correct. Je n'ai toujours pas trouvé de solution, je suppose (et j'espère) que c'est juste un beug de mon ordi.

# Commentaire
Actuellement, je me vois capable de faire plus d'amélioration (comme Trivia ou questionselect.vue) mais je suis très fatigué de ce projet. Je suis satisfait du résultat et fier de moi, mais je n'ai pas prévu de passer plus de temps que ça (j'ai d'autres choses à réviser). Par contre, c'est hyper sympa d'avoir appris à créer un site, je le referai probablement, mais pas dans un future proche.