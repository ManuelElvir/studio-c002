# Studio C002 — contexte pour Claude Code

Maquette 3D (three.js r128, un seul fichier `index.html`) de l'aménagement d'un studio de 35 m² en location à Pierre-Bénite (69).
Publiée sur GitHub Pages : https://manuelelvir.github.io/studio-c002/

## Règles de conception (à respecter dans toute modification)
- **Locataire : aucun perçage.** Tout est posé, à pression (sol-plafond, tringles télescopiques, supports serrés sur les coffres de volets) ou en adhésif repositionnable.
- **Palette** : blanc (principal, murs), chêne (secondaire), terre cuite `#B5755A` mat (accent). Pas de noir sur les nouveaux meubles et luminaires.
- Garder des passages d'au moins ~75 cm ; ne pas bloquer radiateurs (électriques, ne jamais les couvrir), tableau électrique, portes et placard du ballon d'eau chaude.
- Asymétrie équilibrée plutôt que symétrie parfaite.

## Repères du fichier
- Coordonnées en mètres : `x` vers les fenêtres (mur est à `W=5.21`), `z` vers la cuisine (mur sud à `D=5.51`), `y` vers le haut (plafond `H=2.5`). Salle d'eau et WC côté `x < 0` (jusqu'à `X0=-1.3`).
- Helpers : `B(x0,x1,y0,y1,z0,z1,mat,parent,shadow)` (boîte), `C(x,z,r,y0,y1,mat,parent,seg,rTop)` (cylindre), `S(x,y,z,sx,sy,sz,mat,parent)` (sphère), `art()` pour les cadres.
- Groupes de murs masqués automatiquement selon la caméra : `north`, `south`, `east`, `west` ; masqués par vue : `bath`, `wc`.
- Vues : objet `views` (position caméra, cible, texte de légende, `hide`). Boutons dans `<nav class="views">`.
- Ambiances : objet `levels` (`jour`, `soir`, `cine`, `travail`) appliquées par `applyLights()`.

## Vérification avant commit
```bash
python3 -c "import re;s=open('index.html').read();open('/tmp/a.js','w').write(re.findall(r'<script>(.*?)</script>',s,re.S)[0])" && node --check /tmp/a.js
```
Attention aux constantes utilisées avant leur déclaration (ex. `tcMat` est défini dans la section « Coin nuit ») : `node --check` ne les détecte pas, tester aussi dans le navigateur.
