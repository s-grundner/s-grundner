# Pandoc-moderncv

_Captured: 2015-11-28 at 10:09 from [barraq.github.io](http://barraq.github.io/pandoc-moderncv/)_

Pandoc facilities for typesetting modern curriculums vitae. Inspired by the well known Latex ModernCV, it is fairly customizable, allowing you to use predefined themes and to define your own style by changing colors, fonts, etc.

**Pandoc-ModernCV** is a Pandoc facilities for typesetting modern curriculums vitae. Inspired by the well known Latex ModernCV, it is fairly customizable, allowing you to use predefined themes and to define your own style by changing colors, fonts, etc.

With **Pandoc-ModernCV** simply write your CV in _Markdown_, compile it and publish it in a snap.

Pandoc-ModernCV currently supports _pdf_ and _html5_ export formats. The html5 output is responsive and supports rendering for small to large screens.

##  Preview & Screenshots

Live **html5** preview [here](http://barraq.github.io/pandoc-moderncv/preview/cv.html)

![Pandoc-ModernCV large-screen preview ](https://raw.github.com/barraq/pandoc-moderncv/gh-pages/media/images/large-screen.png)

> _Screenshot of the HTML scaffold CV taken for a large screen._

Live **pdf** preview [here](http://barraq.github.io/pandoc-moderncv/preview/cv.pdf)

![Pandoc-ModernCV PDF export preview ](https://raw.github.com/barraq/pandoc-moderncv/gh-pages/media/images/cv-pdf.png)

> _Screenshot of the PDF scaffold CV._

Notice the QR-Code

##  Requirements

For building your CV in html you need:

For exporting your CV to pdf you need:

  * wkpdf or wkhtmltopdf: 
  * exiftool, [http://www.sno.phy.queensu.ca/~phil/exiftool/](http://www.sno.phy.queensu.ca/%7Ephil/exiftool/)

##  Installation

Install **Compass** and **Susy**:
    
    
    $ gem install compass
    $ gem install susy
    

Install **wkpdf** or **wkhtmltopdf**. If on MacOSX please check Troubleshooting section for installing correctly wkpdf.

Install **Pandoc** by using your package manager or by using the provided installer <http://johnmacfarlane.net/pandoc/installing.html> (or using _cabal_)

Install **exiftool** by using your package manager (use [brew](http://brew.sh/) on Mac)

**rsync** should already be installed... if not, install it using your package manager.

You are done!

##  Getting Started

The simplest way to get started with _pandoc-moderncv_ is to use the provided scaffold. In a terminal just do:
    
    
    $ make scaffold
    $ make html
    

What it does it that it creates a scaffold _cv_ located in the /cv directory and builds an html version of it. To open the generated cv just do:
    
    
    $ open dist/cv.html
    

To export the CV to pdf just do:
    
    
    on MacOS X
    $ make pdf
    
    on Linux/Windows
    $ make pdf HTMLTOPDF=wkhtmltopdf
    

Hit the link to [preview the generated pdf](https://github.com/barraq/pandoc-moderncv/raw/gh-pages/preview/cv.pdf)

There you are!

##  Customize

###  Metadata

Your CV can be customized with metadata. Metadata are located between two --- separators at the top of the cv.md file and are formated using the YAML format:
    
    
    ---
    lang: en
    title: Résumé Title
    firstname: Firstname
    lastname: Lastname
    photo: images/picture.png
    email: contact@yoursite.com
    mobile: '+1 (234) 567 890'
    address:
      city: City 
      country: Country
    settings:
      protect-mobile: true
      protect-email: true
    ---
    
    put here your *CV* data
    

Currently Pandoc-MordernCV supports the following metadata:

key type value

lang
string
en

title
string
Resume Title

firstname
string
Firstname

lastname
string
Lastname

photo
url
path/to/photo.png

qrcode
url
images/qrcode.png

contact
url
<http://contact.yoursite.com>

homepage
url
<http://yoursite.com>

email
email
[contact@yoursite.com](mailto:contact@yoursite.com)

mobile
string
'+1 (234) 567 890'

phone
string
'+2 (345) 678 901'

fax
string
'+3 (456) 789 012'

footer
markdown
**custom** _markdown_ text

**address**
map

city
string
City

country
string
Country

**settings**
map

protect-email
boolean
true/false (default: false)

protect-mobile
boolean
true/false (default: false)

protect-phone
boolean
true/false (default: false)

protect-fax
boolean
true/false (default: false)

display-lastupdate
boolean
true/false (default: false)

###  Private & Public CV

It is often handy to hide/show specific informations in your CV depending on where it is published/sent. Pandoc-ModernCV supports **public** and **private** cv:

  * when **public**: 
    * protected metadata are removed.
    * _cv/public.md_ is displayed just after the header and before the CV body.
  * when **private**: 
    * protected metadata are displayed.
    * _cv/private.md_ is displayed just after the header and before the CV body.

####  Protecting Metadata

Currently Pandoc-ModernCV can protect the following metadata:

  * email
  * mobile
  * phone
  * fax

Metadata can be (un)protected independently as follow:
    
    
    ---
    ...
    settings:
      protect-mobile: true # this protect *mobile*
      protect-email: false # this unprotect *email*
    ---
    

####  Building Private/Public CV

To build a public CV just do:
    
    
    $ make html public-cv=true
    or
    $ make pdf public-cv=true
    

To build a private CV just do:
    
    
    $ make html private-cv=true
    or
    $ make pdf private-cv=true
    

Currently pandoc-moderncv supports a single theme: classic.

> Feel free to contribute and send me your custom theme!

###  Colors, Fonts, Icons

All themes can be customized through variables defined in _stylesheets/_settings.scss_. Currently the variables are:
    
    
    $base-font-size: 18px;
    $base-line-height: 23px;
    
    $photo-width: 182px;
    $qrcode-width: 100px;
    
    // Size
    $h1-font-size:      $base-font-size*2;
    $h1-line-multiple:  2;
    $h2-font-size:      $base-font-size*1.5;
    $h2-line-multiple:  1.5;
    $h3-font-size:      $base-font-size*1.2;
    $h3-line-multiple:  1;
    
    // Colors
    $firstname-color: rgb(0, 0, 0);
    $familyname-color: rgb(0, 0, 0);
    $title-color: rgb(89, 89, 89);
    $address-color: rgb(0, 0, 0);
    $quote-color: rgb(0, 0, 0);
    $section-rectangle-color: rgb(191, 191, 191);
    $section-title-color: rgb(89, 89, 89);
    $subsection-color: rgb(0, 0, 0);
    $hint-color: rgb(0, 0, 0);
    
    // Icons
    $external-link-icon: $fa-var-external-link;
    $email-icon: $fa-var-envelope-o;
    $phone-icon: $fa-var-phone;
    $mobile-icon: $fa-var-mobile;
    $fax-icon: $fa-var-print;
    

#  Troubleshooting

##  Cannot load such file -- sass/script/node (LoadError)

For some reasons there is a bug when installing the latest version of Compass... your install of Sass get messed up (I didn't have time to investigate: if you have a better workaround/explanation let me know).

To get over it just uninstall sass and install it again:
    
    
    $ gem uninstall sass
    $ gem install sass
    

##  Cannot load RubyCocoa library

When trying to install wkpdf on MacOsx you may be told that _wkpdf requires that RubyCocoa is installed..._ The fact is that using wkpdf with non-default Ruby installations is not supported.

You must install wkpdf with the native ruby packaged on your mac:

You can use _rvm_ or simply do:
    
    
    $ sudo /System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/bin/gem install wkpdf
    

To check if your install is correct be sure that the first line of _/usr/bin/wkpdf_ file looks like the following:
    
    
    #!/System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/bin/ruby
    
