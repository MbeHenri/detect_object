# Stufe 1: Build-Stufe
FROM node:16 AS build

# Arbeitsverzeichnis festlegen
WORKDIR /app

# Package.json und yarn.lock kopieren
COPY package*.json yarn.lock ./

# Abhängigkeiten installieren
RUN yarn install

# Den gesamten Code kopieren
COPY . .

# Build-Prozess starten
RUN yarn build

# Stufe 2: Production-Stufe
FROM nginx:alpine

# Arbeitsverzeichnis für Nginx konfigurieren
WORKDIR /usr/share/nginx/html

# Standard Nginx static assets entfernen
RUN rm -rf ./*

# Vom vorherigen Build den erstellten Code kopieren
COPY --from=build /app/build .

# Nginx-Konfiguration kopieren (optional, falls nötig)
# COPY nginx.conf /etc/nginx/nginx.conf

# Exponieren des Ports
EXPOSE 80

# Nginx starten
CMD ["nginx", "-g", "daemon off;"]

