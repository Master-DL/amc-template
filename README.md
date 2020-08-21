# Template pour auto-multiple-choice et amc2moodle

## [Installation](https://github.com/nennigb/amc2moodle#installation) (testé sous GNU/Linux Debian 9)

* `sudo apt-get update`
* `sudo apt-get install imagemagick latexml xmlindent python3-pip`
* `sudo pip3 install --upgrade pip`
* `latexml --VERSION`
* Si cette commande déclenche l'erreur "Assuming NOT a POSIX class since there is no terminating ']' in regex […] at /usr/share/perl5/LaTeXML/Common/Error.pm line 364" (testé avec LaTeXML 0.8.1), faire :  
    `sudo patch -Nbp1 /usr/share/perl5/LaTeXML/Common/Error.pm < .../`[`Error.pm.patch`](./Error.pm.patch)  
	puis à nouveau `latexml --VERSION`
* `git clone` [`https://github.com/nennigb/amc2moodle`](https://github.com/nennigb/amc2moodle)
* `cd amc2moodle`
* `sudo pip3 install .`

## Utilisation

* Copier/renommer le fichier [`main.tex`](./main.tex) (par exemple `ue.tex`), y ajouter des questions et mettre à jour la macro `\ue`.
* En supposant que le nom du groupe de questions à exporter soit `2020` :
    * Vérifier que le fichier `ue.tex` contienne les commandes LaTeX adéquates (notamment `\restituegroupe{2020}`)
	* Exécuter `amc2moodle -o ue_2020.xml -c 2020 -p ue.tex`
	* Ouvrir la banque de questions Moodle (`xdg-open https://moodle.univ-tlse3.fr/question/edit.php?courseid=$NumUE`)
	* Supprimer les questions de la catégorie `2020` si besoin (en cas de réimportation pour mettre à jour les questions)
	* Cliquer sur `Importer → Format XML Moodle`, cocher `Faire correspondre les notes : Note la plus proche si elle n'est pas listée` et téléverser le fichier `ue_2020.xml`.
