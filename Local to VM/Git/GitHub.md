Voici les commandes pour **mettre à jour ton dépôt GitHub** avec les nouvelles modifications :

### 📌 **Étape 1 : Vérifier l'état du dépôt**

Ouvre ton terminal et place-toi dans le dossier de ton projet :

```bash
cd /chemin/vers/ton/repo
git status
```

Cela te montrera les fichiers modifiés, ajoutés ou supprimés.

---

### 📌 **Étape 2 : Ajouter les fichiers mis à jour**

Ajoute **tous** les fichiers modifiés :

```bash
git add .
```

Ou ajoute un fichier spécifique :

```bash
git add nom_du_fichier
```

---

### 📌 **Étape 3 : Committer les modifications**

Ajoute un message clair pour expliquer les changements :

```bash
git commit -m "Mise à jour des configurations pfSense et schémas"
```

---

### 📌 **Étape 4 : Pousser les modifications sur GitHub**

Si tu es sur la branche `main` ou `master` :

```bash
git push origin main
```

Si tu es sur une autre branche :

```bash
git push origin nom_de_la_branche
```

---

### 📌 **==Bonus== : Si c’est la première mise à jour après un clone**

Si tu as cloné ton repo récemment et que tu veux être sûr d’être à jour avant de pousser :

```bash
git pull origin main
```

Cela synchronisera ton repo local avec les dernières versions sur GitHub.

---

💡 **Astuce :**  
Si Git te demande tes identifiants à chaque push, tu peux configurer l’authentification avec un **token GitHub** ou utiliser SSH.

Dis-moi si tu rencontres un problème ! 🚀

## **First Push from a New Device or After Cloning**
The `git push origin main` step happens **every time you want to push changes** from your local repository to the remote repository. However, depending on the situation, you may need to set the upstream branch the **first time** you push from a new device. Here’s how it works:



If you cloned an existing repository and made changes, you usually just run:

```bash
git push origin main
```

However, if Git asks you to set the upstream branch (especially on a new device or after cloning), you need to run:

```bash
git push --set-upstream origin main
```

This command establishes a tracking relationship between your local branch (`main`) and the remote branch.

### **Subsequent Pushes**

Once the upstream is set, you can simply use:

```bash
git push
```

This will push the changes to the correct branch without needing to specify `origin main` each time.

### **Summary**

- **First push from a new device:** `git push --set-upstream origin main`
- **Regular push after that:** `git push`
- If you are switching devices, make sure to first pull the latest changes using:
    
    ```bash
    git pull origin main
    ```
    
    before making new changes and pushing.

Would you like a more automated way to handle this when switching devices?