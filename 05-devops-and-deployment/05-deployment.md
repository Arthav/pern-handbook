# Deployment Strategies

## 1. Cloud PaaS (Platform as a Service)
The easiest way for beginners/intermediates.
*   **Frontend**: Vercel or Netlify. Connect your GitHub, zero config.
*   **Backend**: Render or Railway. Upload your Node code.
*   **Database**: Neon (Serverless Postgres) or Supabase.

## 2. VPS (Virtual Private Server) - The Senior Way
Cheaper, more control, but you manage the OS.
*   **Providers**: DigitalOcean, Hetzner, AWS EC2.
*   **Tools**: Nginx (Reverse Proxy), PM2 (Process Manager), Certbot (SSL).

### Nginx Config (Reverse Proxy)
Used to serve your React API and proxy API requests to Node.

```nginx
server {
    listen 80;
    server_name myapp.com;

    location / {
        root /var/www/client;
        try_files $uri $uri/ /index.html;
    }

    location /api {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
    }
}
```

### PM2
Keeps your Node app alive forever.
```bash
npm install -g pm2
pm2 start server.js --name "my-api"
pm2 startup
pm2 save
```
