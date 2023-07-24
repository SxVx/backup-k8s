FROM nginx:alpine

# Copia el archivo index.html desde ./src en el contenedor
COPY ./src/index.html /usr/share/nginx/html/index.html

# Verifica si el archivo se copió correctamente
RUN ls -l /usr/share/nginx/html
