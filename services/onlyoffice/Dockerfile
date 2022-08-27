FROM onlyoffice/documentserver:6.3.1
COPY winfont /usr/share/fonts/winfont
RUN fc-cache -f -v
EXPOSE 80
CMD bash -C '/app/onlyoffice/run-document-server.sh';'bash'