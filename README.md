# Formulaire de contact HTML sans PHP ni serveur (tutoriel 2026)

Exemple complet et clonable : ajoutez un formulaire de contact fonctionnel à un site HTML statique en 5 minutes, sans PHP ni backend. Les emails arrivent directement dans votre boîte, données hébergées en France, grâce à [AirMess](https://airmess.fr/?utm_source=github&utm_medium=readme&utm_campaign=airmess-html-example&utm_content=intro).

Autres exemples : [Hugo](https://github.com/MaximeBranger/airmess-hugo-example) · [Astro](https://github.com/MaximeBranger/airmess-astro-example)

📖 Tutoriel complet : [https://airmess.fr/tutoriels/formulaire-contact-html](https://airmess.fr/tutoriels/formulaire-contact-html?utm_source=github&utm_medium=readme&utm_campaign=airmess-html-example&utm_content=tutoriel)

## Démarrage rapide

```bash
git clone https://github.com/MaximeBranger/airmess-html-example.git
cd airmess-html-example
```

1. Remplacez `VOTRE_ID` dans [index.html](index.html) par l'ID de votre formulaire AirMess.
2. Servez le dossier (par exemple `npx serve .` ou `python -m http.server 8000`) et ouvrez la page.
3. Ajoutez l'origine utilisée (ex. `http://localhost:8000`) à la liste des origines autorisées du formulaire.

## Le problème

Un formulaire HTML ne sait pas envoyer d'email tout seul. Sans PHP ni serveur, il reste deux options habituelles. La première est le lien `mailto:`, qui ouvre le client mail du visiteur, et encore, s'il en a un configuré. La seconde est d'écrire et d'héberger un backend. AirMess propose une troisième voie : votre formulaire envoie les données à une URL, et vous recevez un email.

## Étape 1 : créer le formulaire sur AirMess

Créez un compte sur [airmess.fr](https://airmess.fr/?utm_source=github&utm_medium=readme&utm_campaign=airmess-html-example&utm_content=creer-compte), puis un nouveau formulaire. Indiquez l'adresse qui recevra les messages et ajoutez votre domaine à la liste des origines autorisées. Copiez l'URL du formulaire.

## Étape 2 : ajouter le formulaire à votre page

```html
<form id="contact-form" action="https://airmess.fr/f/VOTRE_ID" method="POST">
  <label for="name">Nom</label>
  <input id="name" name="name" type="text" required>

  <label for="email">Email</label>
  <input id="email" name="email" type="email" required>

  <label for="message">Message</label>
  <textarea id="message" name="message" rows="5" required></textarea>

  <button type="submit">Envoyer</button>
  <p id="contact-status" role="status"></p>
</form>
```

## Étape 3 : envoyer sans recharger la page

Juste avant `</body>` :

```html
<script>
  const form = document.querySelector('#contact-form');
  const status = document.querySelector('#contact-status');

  form.addEventListener('submit', async (e) => {
    e.preventDefault();
    const button = form.querySelector('button');
    button.disabled = true;
    status.textContent = 'Envoi en cours…';

    try {
      const res = await fetch(form.action, {
        method: 'POST',
        body: new FormData(form), // si l'API attend du JSON : adapter ici
      });
      if (!res.ok) throw new Error(res.status);
      form.reset();
      status.textContent = 'Merci, votre message a bien été envoyé.';
    } catch {
      status.textContent = "L'envoi a échoué. Réessayez dans un instant.";
    } finally {
      button.disabled = false;
    }
  });
</script>
```

Le `role="status"` fait lire le message de confirmation aux lecteurs d'écran.

## En cas de problème

Si l'envoi échoue avec une erreur CORS dans la console, votre domaine n'est pas dans la liste des origines autorisées. Pensez-y aussi pour vos tests en local. Pour bloquer les robots, activez hCaptcha dans les réglages du formulaire.

## Licence

[MIT](LICENSE)
