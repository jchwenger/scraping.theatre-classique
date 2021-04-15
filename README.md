# Scraping Théâtre Classique

Extracting all plays from [Théâtre Classique](http://www.theatre-classique.fr/pages/programmes/PageEdition.php).

Using Python 3, [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) and [regex](https://pypi.org/project/regex/).

```bash
$ python scrape.py
$ python dataset.py
```

The first script will produce the folder `théâtre-classique-source`, containing
all the scraped html pages. The second one will process them into a dataset
saved in the folder `théâtre-classique-dataset`, removing introductory contents
(character lists for instance), and surrounding each theatre lines (one
character speaking, possible didascalia, and the text) with the markers `<|s|>`
and `<|e|>`, that will be used to identify these points when training a neural
net on it.

The scripts will first check whether files are present, and skip them. For a
re-download or re-processing, erase the files or directories first.

---

```bash
$ python scrape.py --help

usage: scrape.py [-h] [-d DELAY] [-t TRY_FOR_TXT]

Downloading all books by one author from Théâtre Classique: http://www.theatre-classique.fr

optional arguments:
  -h, --help            show this help message and exit
  -d DELAY, --delay DELAY
                        The delay to wait between each download, default: 1 second
  -t TRY_FOR_TXT, --try_for_txt TRY_FOR_TXT
                        Attempt to download the txt version if available, default: False
```

```bash
$ python dataset.py --help

usage: dataset.py [-h] [-d DIR] [-o OUT_DIR] [-s START] [-e END]

Turning Théâtre Classique scraped html files into a dataset (notably: adding
<|s|> and <|e|> other other markers.

optional arguments:
  -h, --help            show this help message and exit
  -d DIR, --dir DIR     The directory containing the .txt files, defaults to théâtre-classique-source
  -o OUT_DIR, --out_dir OUT_DIR
                        The directory containing the .txt files, defaults to théâtre-classique-clean
  -s START, --start START
                        The start of speech delimiter. Default: <|s|>
  -e END, --end END     The end of speech delimiter. Default: <|e|>
```
