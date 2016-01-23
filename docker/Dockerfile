FROM node:0.12-slim
MAINTAINER Damien Cuenot <cdams@outlook.fr> 

RUN apt-get update && apt-get install -y git
RUN groupadd -r slides && useradd -r -g slides slides

RUN git clone https://github.com/hakimel/reveal.js.git /revealjs
RUN mkdir -p /revealjs/md

WORKDIR /revealjs

RUN npm install -g grunt-cli && npm install
RUN sed -i Gruntfile.js -e "s/files: \[ 'index\.html'\]/files: [ 'pres\/**' ]/"

COPY index.html /revealjs/
COPY custom.css /revealjs/css/
COPY title.js /revealjs/plugin/
COPY test_slides.md /revealjs/pres/slides.md
COPY amtheme.css /revealjs/css/theme/
ONBUILD ADD slides.md /revealjs/md/

EXPOSE 8000
VOLUME ["/revealjs/md/"]
CMD ["grunt", "serve"]
