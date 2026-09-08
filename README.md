# Jeu Pour ou Contre - 100% IMMO

Régie de plateau du jeu « Pour ou Contre / Vrai ou Faux » : les experts votent
depuis leur tablette (QR code, temps réel Supabase), la régie affiche le mur des
experts, la question de la manche et le verdict.

Une seule page autonome, `index.html` : tout est embarqué, sauf la musique de
diffusion `beat.mp3` et les Google Fonts. `test-realtime.html` est une page de
diagnostic du temps réel, exclue du déploiement par `.vercelignore`.

## Mise en ligne

Déploiement Vercel sans build, projet `jeu-pour-contre`, alias
<https://jeu-pour-contre.vercel.app> :

```bash
vercel deploy --prod
```

## Enregistrement pour le montage

Une case « Enregistrer le MP4 », décochée par défaut, est posée à côté du bouton
Diffusion. Décochée, le plateau se déroule normalement. Cochée, le bouton
Diffusion devient une prise de vue : partage de l'onglet, invite de lancement,
régie recadrée en 16/9 exact, curseur masqué, son pris en sortie du lecteur,
puis `Échap` termine et télécharge un 1920x1080 H.264.

Deux pièges de Chrome sont traités dans le code, ne pas les défaire :

- Chrome confine une page à son onglet tant qu'il la capte, donc le plein écran
  système n'est pas disponible pendant une prise. Sans effet sur le fichier, qui
  est recadré sur la régie seule.
- Le cadre capté doit faire un 16/9 exact en pixels écran, sinon Chrome arrondit
  aux dimensions paires inférieures (1918x1080, 1920x1078) et Premiere étire le
  fichier dans une timeline 1080.
