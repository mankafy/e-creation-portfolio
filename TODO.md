# TODO — E-Creation Portfolio

Cocher au fur et à mesure. Ajouter ici tout nouveau chantier.

## Contenu (config/site.ts)

- [x] Renseigner l'e-mail réel (`contact@ecreation-mg.com`, boîte Zimbra OVH)
- [ ] Renseigner le WhatsApp (`contact.whatsapp`)
- [x] Ajouter la page Facebook (`socials`)
- [ ] Ajouter les autres réseaux (LinkedIn…) quand ils existent
- [x] Remplacer les projets de démo par de vraies réalisations (technologies, `caseStudyHref` si page)
- [x] Passer `demoMode` à `false`

## SEO

- [x] Passer l'URL du site sur https://ecreation-mg.com (`.env.production`)
- [x] `app/robots.ts` (bloquer `/api/`, lien vers le sitemap)
- [x] `app/sitemap.ts` (lister chaque page)
- [x] URL canonique dans les metadata (`app/layout.tsx`)
- [x] Favicon / icône (`app/icon.tsx` ou fichier)
- [x] Image Open Graph 1200×630 (`app/opengraph-image.tsx` ou visuel fourni)
- [x] Données structurées JSON-LD `Organization` (uniquement des infos confirmées)
- [x] Une page par service (`/services/[slug]`), à enrichir avec du contenu réel (types de projets, délais)
- [x] FAQ sur les pages de services (`site.faq` + `faq` par service, JSON-LD `FAQPage`)
- [ ] Préciser la FAQ : durée de la garantie de corrections, hébergement, anglais, moyens de paiement
- [x] Étoffer chaque page de service : section « Pour quels projets ? » (`audience`, `useCases`)
- [x] Inscrire le site dans Google Search Console et y soumettre `/sitemap.xml`
- [ ] Valider le JSON-LD avec le test des résultats enrichis de Google une fois en ligne
- [x] Confirmer la ville pour le SEO local (Antananarivo, `address` dans le JSON-LD)
- [x] Intégrer Poppins dans les images Open Graph
- [x] Page création de site web : vitrine, e-commerce, « site internet », clients en France (Search Console : requêtes « création site web Madagascar » en position 70-100)
- [ ] Créer la fiche Google Business Profile (Antananarivo) et y mettre le lien du site
- [ ] Obtenir des liens vers le site : page Facebook, annuaires d'entreprises malgaches, « réalisé par E-Creation » sur les sites clients
- [ ] Mi-décembre 2026 : relire Search Console (position des requêtes « création site web Madagascar »)

## Légal

- [ ] Page Mentions légales (`legal.legalHref`)
- [x] Page Politique de confidentialité (`/confidentialite`), liée au formulaire et au pied de page
- [ ] Faire relire la politique de confidentialité (durée de conservation notamment)
- [x] Ajouter les pages légales au sitemap (automatique via `legal`)

## Formulaire de contact

- [x] Créer un compte Resend, vérifier le domaine d'envoi et définir `RESEND_API_KEY`, `CONTACT_TO_EMAIL`, `CONTACT_FROM_EMAIL` dans Cloudflare (Variables and Secrets du Worker)
- [x] Limite d'envois sur `/api/contact` (binding `CONTACT_LIMITER` du Worker)

## Déploiement Cloudflare Workers

- [x] Créer le Worker relié au dépôt
- [x] Réglages Cloudflare : build `npm run build`, déploiement `npx wrangler deploy` / `npx wrangler preview`
- [ ] Déconnecter Vercel du dépôt (il build encore chaque push)
- [x] Brancher le domaine ecreation-mg.com (et www) sur le Worker
- [x] Rediriger www.ecreation-mg.com vers ecreation-mg.com (Redirect Rule Cloudflare)
- [x] Activer « Always Use HTTPS » (SSL/TLS → Edge Certificates)
- [x] Vérifier que Workers Builds suit bien `mankafy/e-creation-portfolio` depuis le transfert du dépôt (dépôt rendu public)
- [x] Désactiver l'adresse `*.workers.dev` du Worker (`workers_dev: false`)
- [ ] Vérifier après déploiement : `curl -I` sur `/icon` et `/opengraph-image` (type `image/png`), `/sitemap.xml`, `/robots.txt`, 404

- [x] Anti-robot Turnstile sur le formulaire (secret `TURNSTILE_SECRET_KEY` dans Cloudflare)

## E-mail

- [x] DMARC en `p=quarantine`
- [ ] Passer DMARC en `p=reject` si aucun vrai mail ne tombe en spam d'ici fin novembre 2026

## UX / UI / qualité

- [x] Audit Lighthouse (17/11/2026, mobile accueil : perf 79, accessibilité 100, bonnes pratiques 93, SEO 100) : h1 affiché sans attendre le JS, Turnstile chargé à l'approche du formulaire, 5 polices préchargées au lieu de 10
- [ ] Relancer Lighthouse mobile sur l'accueil après déploiement (objectif : LCP < 2,5 s)
- [x] Autoriser Cloudflare Web Analytics dans la CSP et le mentionner dans la politique de confidentialité
- [ ] Vérifier après déploiement que Web Analytics reçoit des visites (tableau de bord Cloudflare)
- [x] Vérifier le responsive de 320px à grand écran (aucun débordement à 320/375/768/1280px)
- [x] Vérifier la navigation clavier et les contrastes (texte ≥ 4.5:1, contours de champs ≥ 3:1)
