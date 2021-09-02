
.PHONY: slides display

default: slides display

slides:
	 pandoc -s -t revealjs -o index.html -V theme=simple ruby-saas.md metadata.yaml

display:
	open index.html
