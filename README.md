# archive_org_audiobooks
Explore audiobooks on Internet Archive for downloading them with ia cli.
[https://www.kaggle.com/code/yuliakr/audiobooks-and-poetry/](https://www.kaggle.com/code/yuliakr/audiobooks-and-poetry/)

## Context

**[Internet Archive](https://archive.org)** is an amazing free source of media. I'm particularly interested in good quality audiobooks. 
Here I describe how to collect book IDs for 128kbps audiobooks using the **[Advanced Search](https://archive.org/advancedsearch.php)** option and pass them to **[ia cli](https://archive.org/developers/internetarchive/cli.html)** for bulk download.

## Usage
1. Get search results from the [Internet Archive](https://archive.org) in .CSV format using [Advanced Search returning JSON, XML, and more](https://archive.org/advancedsearch.php). From "Fields to return" include at least identifier, language, mediatype and format. (Or more, if needed.)
2. Explore the data - available languages, formats...
3. Filter the data for your preferences.
4. Write filtered identifiers to a .txt file.
5. Download items using **[ia](https://archive.org/developers/internetarchive/cli.html)**
```
ia download --itemlist {YOUR_LIST_OF_IDENTIFIERS}.txt --glob=”*128kb.mp3”
```
or **wget**
``` 
wget -r -H -nc -np -nH --cut-dirs=3 -A ”*128kb.mp3” -R .zip  -e robots=off -i “{YOUR_LIST_OF_IDENTIFIERS}.txt” -B 'http://archive.org/download/' --method=HEAD
```


   


### Observation
Advanced Search gives unexpected results when you try to do search in a specific language. For example, search "collection:audio_bookspoetry AND mediatype:audio AND language:French" shows 1073 results on the search results page. But advanced search with these parameters gives only 6 results. Analysis of the search result show that "language" field in archive.org dataset is messed up. It's usable if you know what language values are there.
