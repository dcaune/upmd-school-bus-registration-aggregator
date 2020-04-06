# UPMD School Bus Registration Aggregator

L'[Union des Parents d'Élèves](https://www.upmd.fr) du [Lycée Français International Marguerite Duras](http://lfiduras.com) met en place un formulaire en ligne permettant aux parents d'enregistrer leur(s) enfant(s) au transport scolaire.

Ce formulaire est décomposé en plusieurs sections dynamiques permettant à une famille d'inscrire jusqu'à 4 enfants, en référençant 1 ou 2 parents :

| Accueil                                           | Premier Enfant                                    | Premier Parent                                    | Cotisation Obligatoire                            | Confirmation de la Soumission                     |
| ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- |
| ![](doc/upmd_school_bus_registration_form_01.png) | ![](doc/upmd_school_bus_registration_form_02.png) | ![](doc/upmd_school_bus_registration_form_03.png) | ![](doc/upmd_school_bus_registration_form_04.png) | ![](doc/upmd_school_bus_registration_form_05.png) |

Ce formulaire en ligne est décliné en 4 langues :

- [Anglais](https://forms.gle/BPkmA9X2dGeuJmTX6)
- [Coréen](https://forms.gle/FE9iAGEfq4ksRCrY7)
- [Français](https://forms.gle/NH9g2W8xEXx3kBgd9)
- [Vietnamien](https://forms.gle/hSr5wPwrUGXqVuwr5)

L'UPMD utilise 4 Google Forms pour implémenter ces 4 formulaires dynamiques. Ces 4 formulaires sont configurés pour enregistrer les réponses des parents dans un document Google Sheets. Cependant, chaque formulaire Google Forms enregistre les réponses dans une feuille séparée du document Google Sheets.

![Réponses des Formulaires d'Inscription](doc/upmd_school_bus_registration_forms_response.png)

Le script en ligne de commande (CLI) `aggregate_bus_registration` permet d'aggréger les réponses aux formulaires en un seul jeu de données.

## Installation

L'application **UPMD School Bus Registration Aggregator** est un script [Python(https://fr.wikipedia.org/wiki/Python_(langage))] de type [_interface en ligne de commande_](https://fr.wikipedia.org/wiki/Interface_en_ligne_de_commande).

Cette application est [displonible en ligne](https://pypi.org/project/upmd-schoolbus-registration-aggregator/) comme [paquet](<https://fr.wikipedia.org/wiki/Paquet_(logiciel)>) dans le [dépôt](https://fr.wikipedia.org/wiki/D%C3%A9p%C3%B4t_(informatique) tiers officiel [_Python Package Index_](https://pypi.org/) recensant tous les paquets Python [libres](https://fr.wikipedia.org/wiki/Logiciel_libre).

Son installation s'effectue en ligne de commande via l'outil [`pipenv`](https://pipenv.pypa.io/en/latest/) :

```bash
$ pipenv install upmd-schoolbus-registration-aggregator
```

_Note: vous prendrez soin d'installer préalablement les programmes [`pip`](https://en.wikipedia.org/wiki/Pip_(package*manager)) et `pipenv`.*

Par exemple :

```bash
# Create a Python virtual environment
$ pipenv shell --three
Creating a virtualenv for this project...
Pipfile: /Users/dcaune/.local/bin/upmd/Pipfile
Using /usr/local/bin/python3.7 (3.7.3) to create virtualenv...
⠋ Creating virtual environment...Using base prefix '/usr/local/Cellar/python/3.7.3/Frameworks/Python.framework/Versions/3.7'
New python executable in /Users/dcaune/.virtualenvs/upmd-2tdys9Pu/bin/python3.7
Also creating executable in /Users/dcaune/.virtualenvs/upmd-2tdys9Pu/bin/python
Installing setuptools, pip, wheel...done.
Running virtualenv with interpreter /usr/local/bin/python3.7

✔ Successfully created virtual environment!
Virtualenv location: /Users/dcaune/.virtualenvs/upmd-2tdys9Pu
Creating a Pipfile for this project...
WARNING: Executing a script that is loading libcrypto in an unsafe way. This will fail in a future version of macOS. Set the LIBRESSL_REDIRECT_STUB_ABORT=1 in the environment to force this into an error.
Launching subshell in virtual environment...

The default interactive shell is now zsh.
To update your account to use zsh, please run `chsh -s /bin/zsh`.
For more details, please visit https://support.apple.com/kb/HT208050.
bash-3.2$  . /Users/dcaune/.virtualenvs/upmd-2tdys9Pu/bin/activate

# Install UPMD School Bus Registration Aggregator application
(upmd) bash-3.2$ pipenv install upmd-schoolbus-registration-aggregator
Installing upmd-schoolbus-registration-aggregator…
Adding upmd-schoolbus-registration-aggregator to Pipfile's [packages]…
✔ Installation Succeeded
Pipfile.lock not found, creating…
Locking [dev-packages] dependencies…
Locking [packages] dependencies…
✔ Success!
Updated Pipfile.lock (a01b6b)!
Installing dependencies from Pipfile.lock (a01b6b)…
  🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 45/45 — 00:00:12
```

## Configuration

Vous aurez besoin d'autoriser cette application à utiliser l'API Google Sheets. Pour ce faire vous aurez besoin d'enregister un nouveau _Cloud Platform_ ce qui activera automatiquement l'API Google Sheets pour ce projet. Rendez-vous à l'adresse [https://developers.google.com/sheets/api/quickstart/python](https://developers.google.com/sheets/api/quickstart/python) et cliquez sur le bouton **Enable the Google Sheets API** :

|                                              |                                              |                                              |
| -------------------------------------------- | -------------------------------------------- | -------------------------------------------- |
| ![](doc/enable_the_google_sheets_api_01.png) | ![](doc/enable_the_google_sheets_api_02.png) | ![](doc/enable_the_google_sheets_api_03.png) |

## Execution

```bash
$ aggregate_bus_registration --help
usage: aggregate_bus_registration [-h] [-f FILE] [-l LOCALE] [-c FILE] [-i ID]
                                  [-o ID] [--smtp-hostname SMTP_HOSTNAME]
                                  [--smtp-username SMTP_USERNAME]
                                  [--smtp-port SMTP_PORT]
                                  --email-template-path EMAIL_TEMPLATE_PATH

School Data Importer

optional arguments:
  -h, --help            show this help message and exit
  -f FILE, --file FILE  specify the path and name of the CSV file containing
                        information about children and parents
  -l LOCALE, --locale LOCALE
                        specify the locale (ISO 639-3 code) corresponding to
                        the language of the registration form
  -c FILE, --google-credentials FILE
                        absolute path and name of the Google credentials file
  -i ID, --input-google-spreadsheet_id ID
                        specify the identification of the Google spreadsheet
                        containing the responses to the registration forms
  -o ID, --output-google-spreadsheet_id ID
                        specify the identification of the Google spreadsheet
                        to populate children and parents from the registration
                        forms
  --smtp-hostname SMTP_HOSTNAME
                        specify the host name of the machine on which the SMTP
                        server is running.
  --smtp-username SMTP_USERNAME
                        Specify the username/email address to connect to the
                        SMTP server.
  --smtp-port SMTP_PORT
                        specify the TCP port or the local Unix-domain socket
                        file extension on which the SMTP server is listening
                        for connections.
  --email-template-path EMAIL_TEMPLATE_PATH
                        specify the absolute path name of the localized HTML
                        e-mail templates.
```