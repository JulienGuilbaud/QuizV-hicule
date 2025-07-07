# Quiz de Recommandation de VTT pour Enfants

## 🎯 Objectif de l'application

Ce projet est un quiz interactif conçu pour aider les clients du site [Mic Performance](https://www.micperformance.com/) à choisir le 4-roues (VTT) le plus adapté pour leur enfant. En répondant à une série de questions simples, l'utilisateur reçoit une recommandation de produit personnalisée, le guidant ainsi vers le meilleur achat possible.

L'objectif principal est d'améliorer l'expérience utilisateur, de simplifier le processus de décision et d'augmenter les conversions en dirigeant les clients vers les produits les plus pertinents.

## ✨ Fonctionnalités

*   **Interface simple et engageante** : Un parcours utilisateur fluide, de la première question au résultat.
*   **Questionnaire progressif** : L'utilisateur répond à des questions sur l'âge de l'enfant, le type de terrain, le style souhaité et le budget.
*   **Barre de progression visuelle** : L'utilisateur voit où il en est dans le quiz.
*   **Recommandation personnalisée** : Affiche le produit le plus pertinent avec une image, une description, ses caractéristiques principales et un lien direct vers la page du produit.
*   **Suivi analytique (UTM)** : Les liens de recommandation incluent des paramètres UTM pour suivre l'efficacité du quiz dans des outils comme Google Analytics.
*   **Entièrement en JavaScript natif** : Aucune dépendance à des frameworks lourds, garantissant une performance optimale.
*   **Stylé avec Tailwind CSS** : Un design moderne et responsive qui s'adapte à tous les écrans.

## 🔧 Comment ça fonctionne ?

La logique de recommandation est basée sur un système de points simple :

1.  **Données** : Deux tableaux JavaScript principaux contiennent la logique :
    *   `quizData` : Définit les questions et les options proposées à l'utilisateur.
    *   `productRecommendations` : Contient la liste de tous les VTT, chacun avec ses caractéristiques et ses critères de correspondance (`match`).

2.  **Calcul du score** :
    *   Pour chaque produit, un score est initialisé à 0.
    *   Les réponses de l'utilisateur sont comparées aux critères `match` de chaque produit.
    *   Des points sont attribués en fonction de la pertinence des réponses (ex: +5 points si l'âge correspond, +2 si le budget correspond, etc.).

3.  **Résultat** :
    *   Le produit ayant obtenu le score le plus élevé est sélectionné comme la meilleure recommandation.
    *   Si aucun produit n'atteint un score minimum (actuellement 11 points), une carte par défaut est affichée, invitant l'utilisateur à contacter le service client.

## 🚀 Comment personnaliser le quiz ?

Toute la configuration du quiz se trouve dans le fichier `index.html`, à l'intérieur de la balise `<script>`.

### Modifier les questions

Pour changer, ajouter ou supprimer des questions, modifiez le tableau `quizData`. Chaque objet question doit avoir la structure suivante :

```javascript
{
    question: "Quel âge a votre enfant ?", // Le texte de la question
    key: 'age', // Une clé unique pour cette réponse
    options: [
        { text: "Moins de 4 ans", value: "0-3" },
        // ... autres options
    ],
    multiple: false // Laisser à false pour l'instant
}
```

### Modifier les produits

Pour gérer le catalogue de produits, modifiez le tableau `productRecommendations`. Chaque produit doit suivre ce format :

```javascript
{
    id: 'Minitron', // Un identifiant unique
    name: "VTT Minitron (eQuad S)", // Nom du produit
    description: "Le point de départ parfait...", // Description
    link: "https://...", // Lien vers la page du produit
    image: "https://...", // Lien vers l'image du produit
    features: ["36 Volts", "500 Watts", ...], // Liste des caractéristiques
    match: { // Critères pour la recommandation
        age: ['0-3'],
        budget: ['low'],
        terrain: ['yard'],
        look: ['sport','any']
    }
}
```

**Important** : Les valeurs dans `match` (ex: `'0-3'`, `'low'`, `'yard'`) doivent correspondre exactement aux `value` des options dans `quizData`.

## 🛠️ Technologies utilisées

*   **HTML5**
*   **Tailwind CSS** - Pour un design rapide et responsive.
*   **JavaScript (ES6+)** - Pour toute la logique du quiz, sans aucune bibliothèque externe.


