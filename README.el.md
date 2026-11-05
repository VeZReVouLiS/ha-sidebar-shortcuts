# HA Sidebar Shortcuts

[English](README.md) | **Ελληνικά**

Επαναφέρει στο sidebar του Home Assistant τις σελίδες διαχείρισης που χρησιμοποιείς καθημερινά, ένα κλικ μακριά:

| Item | Ανοίγει |
|---|---|
| Εργαλεία προγραμματιστή | `/developer-tools/yaml` |
| Συσκευές & υπηρεσίες | `/config/integrations/dashboard` |
| Αυτοματισμοί & σκηνές | `/config/automation/dashboard` |
| Εφαρμογές | `/config/apps/installed` |
| Marketplace | `/marketplace` |

Είναι ένα αρχείο ρυθμίσεων για το [Custom Sidebar](https://github.com/elchininet/custom-sidebar) που προσαρμόζεται μόνο του:

- **Μόνο για διαχειριστές.** Οι admin βλέπουν τις συντομεύσεις. Οι υπόλοιποι χρήστες κρατούν το κανονικό τους sidebar.
- **Αυτόματη γλώσσα.** Τα ονόματα ακολουθούν τη γλώσσα του προφίλ κάθε χρήστη. Περιλαμβάνονται αγγλικά και ελληνικά, και [η προσθήκη νέας γλώσσας](#προσθήκη-γλώσσας) είναι μία γραμμή ανά item. Όσες γλώσσες λείπουν δείχνουν αγγλικά.
- **Μόνο ό,τι υπάρχει.** Οι "Εφαρμογές" κρύβονται σε εγκαταστάσεις χωρίς apps (Container/Core). Το "Marketplace" κρύβεται σε εκδόσεις πριν το 2026.11.

## Προϋποθέσεις

Έλεγξέ τες πριν την εγκατάσταση:

| Προϋπόθεση | Γιατί |
|---|---|
| Home Assistant **2026.8 ή νεότερο** (προτείνεται 2026.11+) | Το Custom Sidebar v17 θέλει 2026.8+. Το Marketplace item θέλει 2026.11+. |
| Λογαριασμός **διαχειριστή** (admin) | Μόνο οι admin εγκαθιστούν από το Marketplace και αλλάζουν το `configuration.yaml`. |
| **[Custom Sidebar](https://github.com/elchininet/custom-sidebar) v17 ή νεότερο** | Αυτό το αρχείο είναι ρύθμιση για αυτό το plugin. Χωρίς αυτό δεν γίνεται τίποτα. |
| Τρόπος να **αλλάζεις αρχεία** στο `/config` | Για παράδειγμα τα apps File editor, Studio Code Server, Samba share ή Terminal & SSH. |
| Ένα **restart** του Home Assistant | Το plugin φορτώνεται με `extra_module_url`, που διαβάζεται μόνο στην εκκίνηση. |

## Εγκατάσταση

### Βήμα 1: Εγκατάσταση του Custom Sidebar

[![Άνοιγμα του Custom Sidebar στο Home Assistant σου](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=elchininet&repository=custom-sidebar&category=plugin)

Το κουμπί ανοίγει το Custom Sidebar στο Marketplace σου (σε Home Assistant 2026.10 ή παλαιότερο, στο HACS). Πάτα **Install**.

Παράλειψε το βήμα αν έχεις ήδη το Custom Sidebar.

### Βήμα 2: Φόρτωση του Custom Sidebar σε κάθε σελίδα

Πρόσθεσε αυτό στο `configuration.yaml`. Αν έχεις ήδη ενότητα `frontend:`, πρόσθεσε μόνο το κομμάτι `extra_module_url`:

```yaml
frontend:
  extra_module_url:
    - /local/community/custom-sidebar/custom-sidebar-plugin.js
```

Σε Home Assistant 2026.10 ή παλαιότερο με HACS, βάλε `/hacsfiles/custom-sidebar/custom-sidebar-plugin.js`.

Το Marketplace μπορεί να προσθέσει το Custom Sidebar και ως dashboard resource. Αυτό μόνο του δεν φτάνει: τα dashboard resources φορτώνουν μόνο όταν ανοίγει ένα dashboard, ενώ το sidebar χρειάζεται το plugin σε κάθε σελίδα.

### Βήμα 3: Κατέβασμα του αρχείου ρυθμίσεων

[![Κατέβασμα του custom-sidebar-config.yaml](https://img.shields.io/badge/%CE%9A%CE%B1%CF%84%CE%AD%CE%B2%CE%B1%CF%83%CE%BC%CE%B1-custom--sidebar--config.yaml-41BDF5?style=for-the-badge&logo=homeassistant&logoColor=white)](https://github.com/VeZReVouLiS/ha-sidebar-shortcuts/releases/latest/download/custom-sidebar-config.yaml)

Αποθήκευσέ το ως **`/config/www/custom-sidebar-config.yaml`**. Το όνομα και ο φάκελος πρέπει να είναι ακριβώς αυτά, γιατί το Custom Sidebar διαβάζει μόνο αυτή τη διαδρομή.

Έχεις ήδη δικό σου `custom-sidebar-config.yaml`; Μην το αντικαταστήσεις. Αντίγραψε τα items κάτω από το `order:` από το αρχείο που κατέβασες στο δικό σου.

### Βήμα 4: Restart και ανανέωση

1. Κάνε restart το Home Assistant (**Settings** > μενού με τις τρεις τελείες > **Restart Home Assistant**).
2. Κάνε hard refresh στον browser (**Ctrl+F5**, ή **Cmd+Shift+R** σε Mac). Στο companion app: **Settings** > **Companion app** > **Debugging** > **Reset frontend cache**.

Αν ο φάκελος `www` δεν υπήρχε πριν το βήμα 3, το restart του βήματος 4 είναι αυτό που τον κάνει διαθέσιμο.

## Προσθήκη γλώσσας

Όλα τα ονόματα βρίσκονται σε ένα σημείο, στην αρχή του αρχείου, κάτω από `js_variables` > `trans`. Πρόσθεσε μία γραμμή με τον κωδικό της γλώσσας σου κάτω από κάθε item. Για παράδειγμα, γαλλικά:

```yaml
    developer_tools:
      en: 'Developer Tools'
      el: 'Εργαλεία προγραμματιστή'
      fr: 'Outils de développement'
```

Ο κωδικός είναι το πρώτο κομμάτι της γλώσσας του προφίλ σου (`fr` για γαλλικά, `de` για γερμανικά, `pt` και για τις δύο εκδοχές των πορτογαλικών). Όσα items δεν έχουν τη γλώσσα σου δείχνουν αγγλικά. Pull requests με νέες γλώσσες είναι ευπρόσδεκτα.

## Ενημερώσεις

Είναι αρχείο ρυθμίσεων, οπότε δεν ενημερώνεται μόνο του. Για να μαθαίνεις για νέες εκδόσεις, πάτα **Watch** > **Custom** > **Releases** πάνω σε αυτή τη σελίδα. Για ενημέρωση, κατέβασε ξανά το αρχείο (βήμα 3) και ανανέωσε τον browser. Για τις ενημερώσεις δεν χρειάζεται restart.

Η έκδοση που έχεις φαίνεται στην πρώτη γραμμή του αρχείου.

## Απεγκατάσταση

Σβήσε το `/config/www/custom-sidebar-config.yaml` και ανανέωσε τον browser. Για να φύγει και το Custom Sidebar, αφαίρεσε τη γραμμή `extra_module_url`, απεγκατάστησέ το από το Marketplace και κάνε restart.

## Αντιμετώπιση προβλημάτων

| Πρόβλημα | Λύση |
|---|---|
| Δεν αλλάζει τίποτα | Έλεγξε ότι το Custom Sidebar είναι στο `extra_module_url` (βήμα 2), κάνε restart και hard refresh. |
| Λείπουν οι συντομεύσεις σε έναν χρήστη | Είναι μόνο για διαχειριστές. Έλεγξε τον χρήστη στο **Settings** > **People**. |
| Τα ονόματα είναι στα αγγλικά | Η γλώσσα έρχεται από το προφίλ του χρήστη (**Profile** > **Language**). Δικά τους ονόματα έχουν μόνο οι γλώσσες που υπάρχουν στο αρχείο, δες [Προσθήκη γλώσσας](#προσθήκη-γλώσσας). |
| Λείπουν οι "Εφαρμογές" | Η εγκατάστασή σου δεν έχει apps (Home Assistant Container ή Core). Είναι αναμενόμενο. |
| Λείπει το "Marketplace" | Το Home Assistant σου είναι παλαιότερο από 2026.11. Εκεί το HACS έχει δικό του item στο sidebar. |

## Ευχαριστίες

Ευχαριστώ τον [elchininet](https://github.com/elchininet) για το Custom Sidebar και για την ιδέα να βρίσκονται όλες οι μεταφράσεις σε ένα σημείο.

## Άδεια

[MIT](LICENSE)
