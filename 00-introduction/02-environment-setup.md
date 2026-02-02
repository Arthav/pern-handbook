# Environment Setup

Before writing code, we need a professional development environment.

## 1. Node.js
Install the Long Term Support (LTS) version. This ensures stability.
*   **Windows/Mac/Linux**: Use `nvm` (Node Version Manager) to manage versions. This is a senior best practice to switch between project requirements easily.

```bash
# Install nvm (Linux/Mac)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash

# Install Node LTS
nvm install --lts
nvm use --lts
```

## 2. PostgreSQL
You can run Postgres locally or use Docker (Recommended for keeping your OS clean).

### Option A: Docker (The "Senior" Way)
Create a `docker-compose.yml` file in your root for your database. We will cover this in depth later, but for now:

```yaml
version: '3.8'
services:
  db:
    image: postgres:15-alpine
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: pern_app
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data

volumes:
  pgdata:
```
Run `docker-compose up -d` to start it.

### Option B: Local Installation
Download the installer from [postgresql.org](https://www.postgresql.org/download/).
*   **PGAdmin**: Usually comes with the installer. A GUI tool to view your DB.
*   **DBeaver**: A universal database tool (Highly Recommended alternative to PGAdmin).

## 3. Visual Studio Code Setup
Extensions required for maximum productivity:

1.  **ESLint & Prettier**: For code formatting and linting.
2.  **PostgreSQL (by Microsoft)**: Connect to your DB directly inside VS Code.
3.  **Thunder Client** or **Postman**: For API testing.
4.  **Tailwind CSS IntelliSense**: If using Tailwind.
5.  **ES7+ React/Redux/React-Native snippets**: For fast component creation.

## 4. Terminal
Use a Unix-based terminal.
*   **Windows**: Use WSL2 (Windows Subsystem for Linux). Do not use Command Prompt for serious dev work.
*   **Mac/Linux**: Default terminal is fine. I recommend `zsh` with `oh-my-zsh` for better autocomplete.

## 5. Global Packages
Install strictly necessary global tools:
```bash
npm install -g pnpm nodemon
```
*   **pnpm**: Faster, disk-efficient alternative to npm.
*   **nodemon**: Automatically restarts your node application when files change.

---
[← Previous Section](./01-what-is-pern.md) | [Next Section →](./03-javascript-refresher.md)
