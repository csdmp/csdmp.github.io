###
### Makefile for building and pushing site
###

GITHUB_PAGES_BRANCH=gh-pages
THEME = toc
THEME19 = toc19

MARKDOWN = python3 -m markdown
BASEDIR = .
LATEXDIR = $(BASEDIR)/latex
DOCSDIR = $(BASEDIR)/docs
PAGEDIR = $(BASEDIR)/content/
LATEXIFY = python3 $(LATEXDIR)/utils/latexify.py

html:
	hugo --theme=$(THEME)

develop:
	sleep 1 && echo "Opening local browser..." &&  open http://localhost:1313 &
	hugo server --theme=$(THEME) --buildDrafts --watch

github: html
	cp -r ./docs/* ./public/docs/
	cp -r ./public/* ../
	git add -A :/; git commit -m "Rebuilt site" ; git push

toc.sty:
	pandoc --read=markdown+raw_tex --template=./latex/toc.template ./latex/temp-latex.md -o ./docs/test.tex
	echo 'manually extract from test.tex'

pledge.pdf: $(PAGEDIR)/pledge.md
	$(LATEXIFY) $< > $(LATEXDIR)/temp-latex.md
	pandoc --read=markdown+raw_tex --template=$(LATEXDIR)/tocbig.template $(LATEXDIR)/temp-latex.md -o $(DOCSDIR)/$@


%.pdf: $(PAGEDIR)/%.md
	$(LATEXIFY) $< > $(LATEXDIR)/temp-latex.md
	pandoc --read=markdown+raw_tex --template=$(LATEXDIR)/toc.template $(LATEXDIR)/temp-latex.md -o $(DOCSDIR)/$@

%.pdf: $(PAGEDIR)/post/%.md
	$(LATEXIFY) $< > $(LATEXDIR)/temp-latex.md
	pandoc --read=markdown+raw_tex --template=$(LATEXDIR)/toc.template $(LATEXDIR)/temp-latex.md -o $(DOCSDIR)/$@

.PHONY: html clean develop
