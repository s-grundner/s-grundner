# Homoglyph Detection

_Captured: 2017-09-05 at 20:54 from [codebox.net](https://codebox.net/pages/homoglyph-detection)_

[Homoglyphs](https://en.wikipedia.org/wiki/Homoglyph) are characters with different meanings, that look similar/identical to each other - like the digit '0' and the capital letter 'O' for example.

Homoglyphs within a single alphabet tend to be rare for obvious reasons; these days, however, the internet runs on Unicode which means that it is possible to mix the letters from [many different languages](http://www.unicode.org/cldr/charts/latest/supplemental/languages_and_scripts.html) together in one place.

For example, each of the characters shown below are different, with their own unique Unicode codepoint values, but they all look more-or-less like the capital letter 'A':

A Α А Ꭺ ᗅ ᴀ ꓮ Ａ 𐊠 𝐀 𝐴 𝑨 𝒜 𝓐 𝔄 𝔸 𝕬 𝖠 𝗔 𝘈 𝘼 𝙰 𝚨 𝛢 𝜜 𝝖 𝞐

As well as creating general confusion, homoglyphs can cause particular problems for software developers. For example, if a social media website wants to protect its users from offensive language it may create a 'black-list' of forbidden words, and block any content that contains them. However, someone wishing to use one of the black-listed words could replace one of its letters with a homoglyph - the word would no longer match the one on the black-list, but its meaning would still be apparent to anyone who saw it.

The list below shows some examples of this technique (hover over the words to reveal where regular letters have been replaced with homoglyphs)

I have tried to compile a list of all the homoglyphs I could find, and to make the list useful by processing it in various ways to make it easier to use in software. The list of homoglyphs I used is based on [the one that appears on the Unicode Consortium website](http://www.unicode.org/Public/security/8.0.0/confusables.txt) however this list, although long, was incomplete, so I added some further pairs found thanks to [homoglyphs.net](http://homoglyphs.net/). I have packaged the list into Java and JavaScript libraries, and also created some resources that may be useful to those developing in other languages:

### JavaScript Quick Start

Include the Homoglyph library in your JavaScript project by downloading it from NPM:
    
    
    npm install homoglyph-search
    

Then call the module's `search()` function with the text you want to search, and the word/s you want to search for:
    
    
    var homoglyphSearch = require('homoglyph-search');
    
    var bannedWords = ['credit'];
    var textToSearch = 'Get free ϲrеdiᴛ';
    
    var results = homoglyphSearch.search(textToSearch, bannedWords);
    

### JavaScript and Unicode

Unfortunately, [JavaScript has a unicode problem](https://mathiasbynens.be/notes/javascript-unicode) \- string processing code that works perfectly well with regular English characters can behave in unexpected ways when more exotic ones are used.

In the example below the string 'FOUR' has a length value of '4' as we would expect, however when the letters are replaced with high-value homoglyphs the length is reported as '8'. This problem occurs for any character with a Unicode codepoint value higher than U+FFFF:
    
    
        >'FOUR'.length
        4
        >'𐊇𐊒𝐔𝐑'.length
        8
    

This can cause problems when attempting to process Strings in order to detect homoglyph substitutions; however the homoglyph-search library mentioned above uses the new [ECMAScript 6 for...of](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Statements/for...of) construct which correctly extracts individual characters from a piece of text to allow a search to be performed.

### Java Quick Start

Include the Homoglyph library in your Java project by downloading it from Maven Central:
    
    
    <dependency>
        <groupId>net.codebox</groupId>
        <artifactId>homoglyph</artifactId>
        <version>1.0.2</version>
    </dependency>
    

Then use the `HomoglyphBuilder` class to build a `Homoglyph` object, and call its `search()` method with the text you want to search, and the word/s you want to search for:
    
    
    String textToSearch = "Get free ϲrеdiᴛ";
    String[] bannedWords = new String[]{"credit"};
    
    Homoglyph homoglyph = HomoglyphBuilder.build();
    
    List<SearchResult> results = homoglyph.search(textToSearch, bannedWords);
    

### Java and Unicode

Unfortunately, [Java also has a Unicode problem!](https://docs.oracle.com/javase/tutorial/i18n/text/unicode.html) \- when the language was designed, the Unicode standard only used 16-bits to encode each character, and so the corresponding Java `char` data type was specified to have 16-bits as well. The Unicode standard has since been updated to add many more different characters, and more than 16 bits are required to represent them all. This means that we must [be careful when handling Strings that contain high-value characters](https://docs.oracle.com/javase/tutorial/i18n/text/design.html), we can't rely, for example, on the `.length()` method returning the correct number of characters in a String.

The Java library described above provides a homoglyph-aware search function, that correctly handles high-value Unicode characters by using the 32-bit `int` datatype to represent codepoint values.

### Other Resources

  * Here is a [sorted text file with one group of homoglyphs on each line](https://github.com/codebox/homoglyph/blob/master/raw_data/chars.txt)
  * Here is a similar file which contains [ the Unicode codepoint hexadecimal values for each character](https://github.com/codebox/homoglyph/blob/master/raw_data/char_codes.txt)
