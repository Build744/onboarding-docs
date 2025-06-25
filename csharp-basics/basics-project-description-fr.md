# CSharp Basics Project Description
## 🔧 Consigne générale – Programmation Orientée Objet (POO)

Pour chacun des exercices suivants, vous devez **implémenter une solution en utilisant les principes de la programmation orientée objet**. Cela signifie que :

- Vous devez **modéliser les entités** pertinentes sous forme de **classes** ;
- Vos classes doivent avoir des **attributs** et des **méthodes** adaptés au problème ;
- Vous devez **instancier des objets** si besoin pour utiliser les fonctionnalités définies ;
- Votre code doit **favoriser l'encapsulation, la réutilisabilité et la lisibilité**.

---

## 1. 🧠 Exercice : **FizzBuzz**

### 🔎 Contexte  
Le FizzBuzz est un exercice classique souvent utilisé pour évaluer la compréhension de la logique conditionnelle.

### 🎯 But  
Renvoyer une chaîne de caractères en fonction de la divisibilité d’un nombre entier.

### 📝 Règles métier  
- Si le nombre est divisible par **3 et 5** → retourner `"FizzBuzz"`.
- Si le nombre est divisible **seulement par 3** → retourner `"Fizz"`.
- Si le nombre est divisible **seulement par 5** → retourner `"Buzz"`.
- Sinon → retourner le nombre en chaîne (`"7"`).

### 🧪 Cas de test  
| Entrée | Sortie attendue |
| ------ | --------------- |
| 15     | "FizzBuzz"      |
| 9      | "Fizz"          |
| 10     | "Buzz"          |
| 7      | "7"             |

---

## 2. 📞 Exercice : **North America Phone Number Parser**

### 🔎 Contexte  
Dans les pays d’Amérique du Nord (comme les États-Unis et le Canada), les numéros de téléphone sont standardisés sous le format **NPA-NXX-XXXX** (10 chiffres). Cet exercice consiste à manipuler des chaînes et gérer des exceptions pour vérifier la validité d’un numéro.

### 🎯 But  
Analyser un numéro à 10 chiffres et le formater sous forme `(NPA)NXX-XXXX`.

### 📝 Règles métier  
#### `Parse(string number)`  
- Découper la chaîne en :
  - **NPA (Area code)** : 3 premiers chiffres
  - **NXX (Central Office code)** : 3 chiffres suivants
  - **XXXX (Line Number)** : 4 derniers chiffres  
- Vérifications :
  - Le numéro doit contenir exactement **10 chiffres**.


#### `ToString()`  
- Retourne la version formatée : **`(NPA)NXX-XXXX`**

### 🧪 Cas de test  
| Entrée `Parse` | Sortie `ToString()` |
| -------------- | ------------------- |
| "5145551234"   | "(514)555-1234"     |
| "2120007890"   | "(212)000-7890"     |


---

## 3. 📐 Exercice : **Résolution d'Équation Quadratique**

### 🔎 Contexte  
Les équations du second degré apparaissent souvent en mathématiques et en sciences. Cet exercice permet de s’exercer à l’implémentation de formules mathématiques, à la manipulation de types numériques, ainsi qu’à la gestion de plusieurs cas de sortie (0, 1 ou 2 solutions).

### 🎯 But  
Écrire une fonction qui permet de résoudre une équation du second degré de la forme suivante :

```
ax² + bx + c = 0
```
où `a`, `b` et `c` sont des nombres réels fournis par l’utilisateur.

### 📝 Règles métier  

#### 🔢 Étapes à suivre :

1. **Calcul du discriminant (Δ)**  
   Utiliser la **formule complète** :
   ```
   Δ = b² - 4ac
   ```

2. **Résolution en fonction de Δ :**
   - Si **Δ > 0**  
     → Deux racines réelles :  
     ```
     x1 = (-b + √Δ) / (2a)
     x2 = (-b - √Δ) / (2a)
     ```
     → Retourner `[x1, x2]`
   - Si **Δ == 0**  
     → Une racine réelle :  
     ```
     x = -b / (2a)
     ```
     → Retourner `[x]`
   - Si **Δ < 0**  
     → Pas de racines réelles  
     → Retourner `[]` (tableau vide)

3. **Cas particulier :**
   - Si `a == 0`, ce n’est **pas une équation quadratique**.

### 🧪 Cas de test  

| a   | b   | c   | Discriminant (Δ) | Résultat           |
| --- | --- | --- | ---------------- | ------------------ |
| 1   | -3  | 2   | 1                | [2, 1]             |
| 1   | 2   | 1   | 0                | [-1]               |
| 1   | 1   | 1   | -3               | []                 |
| 0   | 2   | 1   | —                | Exception attendue |

---

## 4. 🌡️ Exercice : **Convertisseur de Température**

### 🔎 Contexte  
Comprendre les formules de conversion entre **Kelvin**, **Celsius** et **Fahrenheit** permet de s’entraîner aux fonctions mathématiques, à la gestion des unités, et à l’écriture de méthodes claires.

### 🎯 But  
Convertir une température donnée entre les trois unités suivantes : **Kelvin**, **Celsius** et **Fahrenheit**.

### 📝 Règles métier  

#### 🔁 Conversions

- `Celsius -> Fahrenheit` : `(C × 9/5) + 32`
- `Celsius -> Kelvin` : `C + 273.15`
- `Kelvin -> Celsius` : `K - 273.15`
- `Fahrenheit -> Kelvin` : `((F - 32) × 5/9) + 273.15`
- `Kelvin -> Fahrenheit` : `((K - 273.15) × 9/5) + 32`

#### 📌 Contraintes
- Température en **Kelvin** ne peut pas être < 0 

### 🧪 Cas de test  
| Type conversion | Entrée | Sortie attendue |
| --------------- | ------ | --------------- |
| C → F           | 0°C    | 32°F            |
| F → C           | 212°F  | 100°C           |
| C → K           | 100°C  | 373.15 K        |
| K → F           | 0 K    | -459.67°F       |
| F → K           | 32°F   | 273.15 K        |
| K invalide      | -10 K  | Exception       |
