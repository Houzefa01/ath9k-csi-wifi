# ath9k-csi — capture du CSI Wi-Fi avec le pilote ath9k

Pilote Linux **ath9k** (Qualcomm Atheros 802.11n) modifié pour capturer les données
brutes de **Channel State Information (CSI)** de chaque trame reçue. Cible de test :
carte **AR9565** sous noyau 6.19 (Arch Linux).

## Principe

- `ath9k.h` : ajout d'une structure `csi_state` dans `ath_softc`
  (tampon de 4096 octets, spinlock, wait-queue, horodatage `timespec64`, entrée debugfs)
- `recv.c` : dans le chemin de réception des trames, copie des données
  (`chains × 56` octets) dans le tampon CSI, horodatage, puis réveil des lecteurs en attente
- `debug.c` : exposition du tampon via **debugfs** pour une lecture depuis l'espace utilisateur
- `Makefile` / `Kbuild` : compilation hors arbre (module externe)

Le fichier **`ath9k-csi.patch`** contient le diff complet par rapport au pilote ath9k
d'origine.

## Compilation

```bash
cd ath9k-csi
make -C /lib/modules/$(uname -r)/build M=$PWD modules
```

## État

Prototype de recherche. La dernière compilation enregistrée échouait encore contre les
en-têtes 6.19, donc le module n'est pas validé. Le chargement d'un pilote réseau modifié
peut figer la machine : testez-le dans une VM ou sur une machine dédiée.

> L'archive d'origine (`csi-wifi.7z`) contient aussi l'arbre complet des sources du noyau
> Linux et les objets compilés. Ils ne sont pas versionnés ici.

Licence : ISC / GPL-2.0, comme le pilote ath9k d'origine.
