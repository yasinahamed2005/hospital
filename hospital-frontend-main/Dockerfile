# ---------- Build stage ----------
FROM node:18 AS build-stage
WORKDIR /app

# copy project files
COPY package*.json ./
COPY . .

RUN npm install
RUN npm run build

# ---------- Runtime stage (Tomcat) ----------
FROM tomcat:9-jdk17

# clean default apps
RUN rm -rf /usr/local/tomcat/webapps/*

# Deploy React/Vite build as ROOT app
COPY --from=build-stage /app/dist /usr/local/tomcat/webapps/ROOT

EXPOSE 8080
CMD ["catalina.sh", "run"]
