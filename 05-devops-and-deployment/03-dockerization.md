# Dockerization

Containerization ensures your app works on every machine.

## 1. Dockerfile (Node/Express)
Create a `Dockerfile` in your server root.

```dockerfile
# Stage 1: Build
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

## 2. Dockerfile (React)
React needs to be built into static HTML/JS/CSS files and served by Nginx.

```dockerfile
# Stage 1: Build
FROM node:18-alpine as builder
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Serve
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

## 3. Docker Compose
Orchestrate everything.

```yaml
version: '3.8'
services:
  server:
    build: ./server
    ports:
      - "3000:3000"
    environment:
      - DATABASE_URL=postgres://user:pass@db:5432/pern_app
    depends_on:
      - db
      
  client:
    build: ./client
    ports:
      - "80:80"

  db:
    image: postgres:15-alpine
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
      POSTGRES_DB: pern_app
    volumes:
      - pgdata:/var/lib/postgresql/data

volumes:
  pgdata:
```
