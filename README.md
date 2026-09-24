# Formulaire de contact HTML sans PHP ni serveur (tutoriel 2026)

Ajoutez un formulaire de contact fonctionnel à un site HTML statique en 5 minutes, sans PHP ni backend. Emails reçus directement, données hébergées en France.

Exemple complet et clonable, à utiliser avec [AirMess](https://airmess.fr/?utm_source=github&utm_medium=readme&utm_campaign=airmess-html-example&utm_content=intro).

Autres exemples : [Hugo](https://github.com/MaximeBranger/airmess-hugo-example) · [Astro](https://github.com/MaximeBranger/airmess-astro-example)

📖 Tutoriel complet : [https://airmess.fr/tutoriels/formulaire-contact-html](https://airmess.fr/tutoriels/formulaire-contact-html?utm_source=github&utm_medium=readme&utm_campaign=airmess-html-example&utm_content=tutoriel)

## Démarrage rapide

```bash
git clone https://github.com/MaximeBranger/airmess-html-example.git
cd airmess-html-example
```

1. Remplacez `VOTRE_TOKEN` dans [index.html](index.html) par le jeton de votre formulaire AirMess.
2. Servez le dossier (par exemple `npx serve .` ou `python -m http.server 8000`) et ouvrez la page.
3. Ajoutez l'origine utilisée (ex. `http://localhost:8000`) à la liste des origines autorisées du formulaire.

[avec-fetch.html](avec-fetch.html) montre la variante sans rechargement de page.

## Le problème

Un formulaire HTML ne sait pas envoyer d'email tout seul. Sans PHP ni serveur, il reste deux options habituelles. La première est le lien `mailto:`, qui ouvre le client mail du visiteur, et encore, s'il en a un configuré. La seconde est d'écrire et d'héberger un backend. AirMess propose une troisième voie : votre formulaire envoie les données à une URL, et vous recevez un email.

## Étape 1 : créer le formulaire sur AirMess

Créez un compte sur [AirMess](https://airmess.fr/?utm_source=github&utm_medium=readme&utm_campaign=airmess-html-example&utm_content=creer-compte), puis un nouveau formulaire. Indiquez l'adresse qui recevra les messages et ajoutez votre domaine à la liste des origines autorisées. Copiez l'URL du formulaire.

## Étape 2 : ajouter le formulaire à votre page

```html
<form action="https://airmess.fr/api/submit/VOTRE_TOKEN" method="POST">
  <label for="name">Nom</label>
  <input id="name" name="name" type="text" required>

  <label for="email">Email</label>
  <input id="email" name="email" type="email" required>

  <label for="message">Message</label>
  <textarea id="message" name="message" rows="5" required></textarea>

  <button type="submit">Envoyer</button>
</form>
```

C'est tout : ce formulaire fonctionne sans JavaScript. À l'envoi, le navigateur quitte la page et le visiteur arrive sur une page de confirmation hébergée par AirMess. Pour le ramener sur votre site, renseignez « URL de redirection après envoi » dans les réglages du formulaire, par exemple votre page `/merci`.

Vous préférez que le visiteur reste sur la page et voie un message de confirmation à la place du formulaire ? Suivez le tutoriel [Formulaire de contact sans rechargement de page (fetch)](https://airmess.fr/tutoriels/formulaire-contact-sans-rechargement?utm_source=github&utm_medium=readme&utm_campaign=airmess-html-example&utm_content=tutoriel-lie).

## En cas de problème

Si l'envoi est refusé (page d'erreur ou erreur 403), votre domaine n'est pas dans la liste des origines autorisées. Pensez-y aussi pour vos tests en local. Pour bloquer les robots, activez hCaptcha dans les réglages du formulaire.

## Licence

[MIT](LICENSE)
