 # R Studio
 
   Integrates into a single window:
 -   R console (CLI)
 -  text editor
 -    file/environment/history/help browser(s)
 -    graphic viewer
 
  Makes it easy to dive into R!

# What is [R Markdown](http://rmarkdown.rstudio.com/)?

+  Plain text formatting syntax (markup language)
+ Originally designed for creating web documents
+  Easy-to-read and easy-to-write
+ Allows you to focus on content, rather than layout
+ Can be converted into virtually any format, e.g. `.pdf`, `.html`, `.doc`

# The step by step guide to RmarkDown (courtsey of Charles Belinsky!)

# For Windows Users:

+ Issues:

You need a LaTeX program (we will use MikTex)

MikTex needs to be installed for all users (this is not the default)

MiKTeX needs privileges to install packages on-the-fly (also, not the default)
 

+ Procedures:

1. Go to MiKTex website and click Download

2. Click on the downloaded file to install

3. Accept the MikTeX copying conditions and click Next

4. Change Installation Scope to Install MiKTeX for anyone who uses this computer

5. Installation directory can stay to same ... click Next

6. Settings options:
Preferred Paper: 90% of the world uses A4 but the United States uses Letter

7. Install missing packages on-the-fly: switch to Yes

8. Click Next

9. Review: click Start

Note: the first time you use execute RMarkDown Knit-to-PDF will take a LOOOONG time because MiKTeX is downloading many missing packages

# For Mac Users: 

The easiest way is to download MacTex here:

http://www.tug.org/mactex/

… click on MacTex Download

 

MacTex is straightforward – just download and install using all defaults. But MacTex is over 4GB – the network would throw a bit of a fit if everyone in the class was downloading this at the same time.

 

Note: The smaller LaTeX software linked on the page, BasicTeX, does not work with RMarkDown.

 

I tested this on Mac 10.12 (Sierra) and Mac 10.14 (Mojave). 

 

Mac 10.15 (Catalina) is being released this September.  Students should avoid upgrading to Catalina because setups like what this class demands are notorious for not working right on the first iteration of a new Mac OS. 



# To learn more see:
 
- [Using R Markdown for Class Reports](http://www.stat.cmu.edu/~cshalizi/rmarkdown/) by Cosma Shalizi
- [Markdown Basics](https://markdown-guide.readthedocs.io/en/latest/basics.html), which describes the most commonly used markdown constructs.
- [R Code Chunks](https://rmarkdown.rstudio.com/lesson-3.html), which goes into more depth on customizing the behavior of embedded R code.
- [R Markdown Cheat Sheet (PDF)](https://www.rstudio.com/wp-content/uploads/2015/02/rmarkdown-cheatsheet.pdf), a quick guide to the most commonly used markdown syntax, knitr options, and output formats.
- [R Markdown Reference Guide (PDF)](https://www.rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf), a more comprehensive reference guide to markdown, knitr, and output format 
- [Compiling Notebooks](https://support.rstudio.com/hc/en-us/articles/200552276-Creating-Notebooks-from-R-Scripts), which describes how to compile HTML, PDF, or MS Word notebooks from R scripts.
Document output formats: HTML, PDF, Word
- [Having installed R and RStudio before installing MikTeX?](https://medium.com/@sorenlind/create-pdf-reports-using-r-r-markdown-latex-and-knitr-on-windows-10-952b0c48bfa9)
- Note:  *TinyTex* is a custom LaTeX distribution based on TeX Live that is small in size but functions well in most cases, especially for `R` users.  *TinyTex* is easier to install than *MikTex* and works well with Rstudio. More detail about *TinyTex* can be found in: https://yihui.name/tinytex/  


[Back](https://github.com/younghhk/STAT_COMP/)
