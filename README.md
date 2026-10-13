# Dropyour — plugin Claude Code

Publish micro-apps from your AI with no account; operate them as real apps. Data stored in the EU.

```
claude plugin marketplace add dropyour/dropyour-plugin
claude plugin install dropyour@dropyour
```

**Pas de compte, pas de clé, pas d'OAuth.** Le premier appel publie. C'est ce qui distingue Dropyour
des plateformes qui offrent le même cycle de vie : chez elles, installer le plugin déclenche une
authentification avant le premier octet.

## Ce que ton agent gagne

- **Publier** une page à une URL stable, sans compte.
- **Opérer** ensuite : versions, retour arrière, réglages, données — le même protocole du début à la fin.
- **Faire grandir** en vraie app (palier 4) : code serveur, magasin interrogeable, horloge, secrets,
  visiteurs connectés, fichiers, temps réel.

Hébergé en Europe. Export à tout moment, et une app graduée peut être redéployée sur ton propre compte d'hébergement : partir n'est pas une négociation.

## Les 34 outils

| Outil | Ce qu'il fait |
|---|---|
| `dropyour_whoami` | Check my Dropyour tier |
| `dropyour_publish` | Publish a new drop |
| `dropyour_replace` | Replace a drop's content |
| `dropyour_update_settings` | Change a drop's settings |
| `dropyour_secret_set` | Store a secret for an app |
| `dropyour_secret_delete` | Delete an app secret |
| `dropyour_logs` | Read an app's log |
| `dropyour_egress_deny` | Cut an outbound domain for an app |
| `dropyour_secrets_list` | List secret names |
| `dropyour_graduate` | Graduate a drop into a real app |
| `dropyour_import` | Import an existing app |
| `dropyour_read_app_files` | Read a graduated app's files |
| `dropyour_call` | Call one of my app's routes |
| `dropyour_schedule` | Read, set, or trigger my app's clock |
| `dropyour_status` | Check a drop's status |
| `dropyour_read_content` | Read a drop's content |
| `dropyour_read_data` | Read a drop's stored data |
| `dropyour_write_data` | Write a drop's stored data |
| `dropyour_list_versions` | List a drop's versions |
| `dropyour_rollback` | Roll a drop back to a version |
| `dropyour_milestone` | Set a milestone on a system of linked apps, and roll them all back to it |
| `dropyour_records_summary` | Summarize an app's records |
| `dropyour_records_list` | Query an app's records |
| `dropyour_autonomy` | Set how much this app's agent may do alone |
| `dropyour_link` | Link one app to another, and state what it relies on |
| `dropyour_rotate_token` | Rotate a drop's management token |
| `dropyour_patch` | Patch part of a drop |
| `dropyour_app_tools` | Declare your app's MCP tools |
| `dropyour_records_visibility` | Set who reads a collection |
| `dropyour_records_write` | Write one row in the app store |
| `dropyour_release` | Publish, verify, and roll back on failure |
| `dropyour_delete` | Delete a drop |
| `dropyour_delegate` | Share access to one of my apps |
| `dropyour_list` | List my drops |

## Les skills

| Skill | Quand il se déclenche |
|---|---|
| `dropyour-publier` | mettre une page en ligne depuis le chat |
| `dropyour-serveur` | écrire le code serveur d'une app graduée |
| `dropyour-reparer` | une app est cassée : lire le journal, revenir en arrière |

## Ce dépôt

Il ne contient **que la couche distribution** : manifestes, déclaration MCP, skills. Le produit vit
ailleurs et reste privé. Toute la matière ici est **générée** depuis les sources du produit — un
chiffre ou une surface écrits à la main y vieilliraient sans que personne le voie.

MIT. Documentation : <https://dropyour.io/fr/docs>
