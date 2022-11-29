# Plain Text Note and Citation Management

_Captured: 2015-12-26 at 10:17 from [wcm1.web.rice.edu](http://wcm1.web.rice.edu/plain-text-citations.html)_

When I started the research for my second book project, I decided to rethink my writing and note-taking process from the ground up. After [switching to a plain-text writing workflow](http://wcm1.web.rice.edu/my-academic-book-in-plain-text.html) in the middle of writing my first academic book, I knew that I wanted to write and take notes exclusively in Markdown for this new project. I knew that I wanted to experiment with open notebook research by hosting all of my notes in an [online, version-controlled wiki](http://wiki.wcaleb.rice.edu). And I also wanted to be able to store, locate, and easily cite bibliographic information for secondary sources used in my research.

In this post, which serves as a sort of technical companion to my post on [Open Notebook History](http://wcm1.web.rice.edu/open-notebook-history.html), I will explain how I am managing my notes and citations using plain text files, [Gitit](http://gitit.net), and [Pandoc](http://johnmacfarlane.net/pandoc/index.html)--John MacFarlane's amazing open-source program for document conversion.

Dennis Tenen and Grant Wythoff have recently written for the Programming Historian about [how to write scholarship in Plain Text using Markdown and Pandoc](http://programminghistorian.org/lessons/sustainable-authorship-in-plain-text-using-pandoc-and-markdown), and my basic workflow is very similar to the one they describe, with one major difference. As Tenen and Wythoff explain, Pandoc allows you to [use a BibTex database to insert citations](http://programminghistorian.org/lessons/sustainable-authorship-in-plain-text-using-pandoc-and-markdown#working-with-bibliographies) into a Markdown document.[1](http://wcm1.web.rice.edu/plain-text-citations.html) Instead of maintaining _one_ `*.bib` file, however, my system stores BibTeX data and free-form notes for each secondary source in its own, separate file.

In other words, my method for managing citations is similar to my [plain-text GTD system](http://wcm1.web.rice.edu/plain-text-gtd.html). In my GTD system, every task gets its own text file. Similarly, in my research notebook, every secondary source--whether it is a book, an article, a book chapter, or a dissertation--gets _its_ own text file.

This method allows me to give every secondary source its own page in my [Gitit wiki](http://wiki.wcaleb.rice.edu), so that I can link to specific sources within wiki pages. When I am ready to process a Markdown file that has citation keys, I combine all of my BibTeX entries into a single bibliography file, at which point my process begins to look again like the one Tenen and Wythoff describe.

Before diving into the details of how and why I manage citations this way, it may help to view this screencast that shows what my note-taking and citation workflow looks like in real time:

As that screencast describes, for every new book, article, or dissertation I encounter, I create a new plain text file that becomes a page in my wiki. At the top of the file, I include bibliographic information about the source using the [BibTeX](http://www.bibtex.org) reference management software, and I wrap the citation block inside Pandoc's code block syntax, so that it looks like this:
    
    
    ~~~~~{.bib}
    @Book{ kerby1972,
        author = {Robert L. Kerby},
        title = {Kirby Smith's Confederacy: The Trans-{M}ississippi South, 1863--1865},
        address = {New York},
        publisher = {Columbia University Press},
        year = 1972,
    }
    ~~~~~

I then take notes about the source directly in that same text file, whose filename is the same as the BibTeX key.[2](http://wcm1.web.rice.edu/plain-text-citations.html) You can see what this looks like in the screencast, or [take a look at an example here](http://wiki.wcaleb.rice.edu/_showraw/kerby1972).

## Citing sources in Markdown

Pandoc allows you to insert citations using BibTeX keys like `kerby1972` in the above example. I'm using Pandoc version 1.12.1 in the screencast, and it's worth noting that some new features have been implemented in the latest version. But the [basic method for inserting citations](http://johnmacfarlane.net/pandoc/README.html#citations) still holds.[3](http://wcm1.web.rice.edu/plain-text-citations.html)

In order to convert the citations in a Markdown file into fully formatted footnotes, Pandoc needs both a bibliography file containing all the cited BibTeX entries and a CSL file to tell it which style manual to use.

The CSL file I use for most projects is [available in this Gist](https://gist.github.com/wcaleb/11329328); it's basically the standard [chicago-fullnote-bibliography-no-ibid](https://github.com/citation-style-language/styles/blob/master/chicago-fullnote-bibliography-no-ibid.csl) CSL file, with the exception of the change [described here](https://gist.github.com/wcaleb/6354288). That file goes in my `$HOME/.csl` folder so that Pandoc can find it later.

To create the bibliography file that Pandoc needs when processing my Markdown manuscript file, I use a [Python Pandoc filter and a shell script](https://gist.github.com/wcaleb/9fe0116169754763a3c2) to get the BibTeX entries out of each of my note files, add a "short title" in the "note" field, and append the entry to a single bibliography file.[4](http://wcm1.web.rice.edu/plain-text-citations.html)

Once I have generated the bibliography file, converting my Markdown manuscript means running a command that usually looks something like this:
    
    
    pandoc --bibliography=gitit.bib --csl=chicago.csl --output=manuscript.pdf manuscript.txt

Watch the screencast to see what an example output PDF looks like once Pandoc has processed all the citations. Changing the output filename to a `*.docx` file makes it possible to create a Microsoft Word file, too.

## Gitit customizations

As mentioned above, I go through the extra trouble of keeping my BibTeX entries in separate files so that each secondary source can get its own page in [my wiki](http://wiki.wcaleb.rice.edu). All of my notes are kept in a Git repository, and when I push new commits to the repo, my online wiki is updated so that changes are reflected there.

I have also written a [Haskell plugin](https://github.com/wcaleb/gitit-plugins/blob/master/Bibtex2Html.hs) that uses [Bibtex2Html](https://www.lri.fr/~filliatr/bibtex2html/) to convert the bibliographic block at the top of each page into a formatted citation whenever the page is loaded by a user.[5](http://wcm1.web.rice.edu/plain-text-citations.html) Though this is not an essential part of the workflow, it makes the pages on the wiki a bit more readable and means that a formatted citation for each of my secondary sources is always handy if I need it.

## Vim customizations

My citation management system is text editor independent. But I have created some shortcuts that make it easier for me to manage my notes in Vim.

For example, whenever I push a commit to my notes' Git repository, a post-commit hook generates a Vim dictionary file that contains all of the BibTeX keys in my Wiki:
    
    
    basename -s .page -a /Users/wcm1/Dropbox/wikidata/*.page | grep '^[a-z]\+[0-9]\{4\}$' > /Users/wcm1/.vim/dicts/bibtexpages.txt

This hook relies on the fact that the filenames for each of my secondary source notes is the same as the BibTeX keys. So getting a list of all of my BibTeX keys just means listing all of the files in the directory and finding filenames that start with a string and end with a four-digit number.[6](http://wcm1.web.rice.edu/plain-text-citations.html) Piping that list to a dictionary file means that I can [autocomplete BibTeX citations in Vim](http://vim.wikia.com/wiki/Dictionary_completions), as demonstrated in the screencast.

I also have a [Vim command that allows me to create a new page in my Wiki](https://github.com/wcaleb/dotfiles/blob/master/_vim/gitit.vimrc) just by typing the following at the command line:
    
    
    :Wiki lichtenstein1996

where `lichtenstein1996` is the name of the new Wiki page. Because of the way this command works, if I already have a page by that name in my wiki, Vim will just open that page. This prevents me from overwriting existing files or creating duplicate BibTeX keys, which would be more of a problem if I were keeping all of my entries in a single `*.bib` file.

To open already existing notes more easily, I use the [FuzzyFinder](http://www.vim.org/scripts/script.php?script_id=1984) plugin, together with a [mapping that binds a shortcut](https://github.com/wcaleb/dotfiles/blob/master/_vim/fuf.vimrc) to my `wikidata` directory.

My system also would not be sustainable if I had to remember proper BibTeX syntax every time I wanted to create a new citation. Fortunately, the [snipMate](http://www.vim.org/scripts/script.php?script_id=2540) plug-in for Vim allows me to create snippets--often-typed blocks of text that can be inserted into a Vim buffer just be typing a special trigger word and hitting `<Tab>`. I have written [pre-defined snippets](https://github.com/wcaleb/dotfiles/blob/master/_vim/snippets/pandoc.snippets) that insert BibTeX templates directly into my file and allow me to fill in each field by tabbing through the template, as demonstrated in the screencast.

These snippets also fill out some of the fields for me based on the name of the file. Since I name each file containing a source according to the BibTeX key I want to use, the snippet uses that filename to fill in the BibTeX key and determine the year of publication.[7](http://wcm1.web.rice.edu/plain-text-citations.html)

## Conclusion

Although this system took some thinking and tweaking to set up, using it has now become second nature, and I seldom have to touch the underlying scripts that hold it together. But I also like that the system could be easily adapted if I later decided that I wanted to use a program like [Zotero](https://www.zotero.org) or [BibDesk](http://bibdesk.sourceforge.net) to manage my citations. Since I will have kept my entries in BibTeX from the beginning, any citation software that interfaces with `*.bib` files (which is most of the ones currently on the market) will be able to accept my notes in the future. At the same time, I am not locked into any proprietary database file formats.[8](http://wcm1.web.rice.edu/plain-text-citations.html)

That's the beauty of plain text files that (ostensibly) justifies the lengths to which I've gone to make this system work. And whatever its quirks, it is a system that does exactly what I need it to do because, unlike larger bibliographic management programs written to suit every imaginable discipline and use case, it was designed specifically and exclusively for my needs. So far, so good!

  1. For other examples of scholars who do this, check out the Bib files maintained by [Jason Heppler](https://github.com/hepplerj/bib) and [Lincoln Mullen](https://github.com/lmullen/historybib). [Kieran Healy](http://kieranhealy.org/blog/archives/2014/01/23/plain-text/) also uses Pandoc and BibTex to publish sociology papers, and his write-up also details how to integrate statistics and figures into the workflow using R.[↩](http://wcm1.web.rice.edu/plain-text-citations.html)

  2. My method of mixing notes and BibTeX is similar to the one described by [John Lenz](http://blog.wuzzeb.org/posts/2012-06-14-reference-management.html) in a four-part series of blog posts, though my implementation is not quite the same as his.[↩](http://wcm1.web.rice.edu/plain-text-citations.html)

  3. Note that the screencast does not explain how I keep notes on primary sources, which is a subject for another day.[↩](http://wcm1.web.rice.edu/plain-text-citations.html)

  4. For more on Pandoc filters, check out John MacFarlane's tutorial on [scripting with Pandoc](http://johnmacfarlane.net/pandoc/scripting.html#but-i-dont-want-to-learn-haskell).[↩](http://wcm1.web.rice.edu/plain-text-citations.html)

  5. I got the idea for doing this from the aforementioned [John Lenz](http://blog.wuzzeb.org/posts/2012-06-26-bibtex-and-gitit.html) posts, but my own plugin is basically just a modified version of the [Dot.hs](https://github.com/jgm/gitit/blob/master/plugins/Dot.hs) plugin distributed with the Gitit source code.[↩](http://wcm1.web.rice.edu/plain-text-citations.html)

  6. If I were keeping all of my BibTeX entries in a single file and trying to extract a list of keys from it, I would probably use Lincoln Mullen's [bibkeys](https://github.com/lmullen/bibkeys) Gem.[↩](http://wcm1.web.rice.edu/plain-text-citations.html)

  7. If I were not using Vim, I could reproduce some of this functionality using a program like [TextExpander](https://smilesoftware.com/TextExpander/index.html).[↩](http://wcm1.web.rice.edu/plain-text-citations.html)

  8. I learned my lesson the hard way when I began taking my dissertation notes in a now-defunct program for PCs called Citation. When I switched from PC to Mac about six months into working on the thesis, I couldn't use Citation any more, and the only way to take my notes with me was to export them into one, gigantic Rich Text Format file that was impossible to sort in a reasonable way. Never again![↩](http://wcm1.web.rice.edu/plain-text-citations.html)
