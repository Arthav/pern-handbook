# Capstone Project: "TaskFlow" (Project Management Tool)

To graduate to Senior status, build this.

## Features
1.  **Auth**: JWT, Registers/Login, Password Reset (Email).
2.  **Workspaces**: Users can create organizations.
3.  **Real-time**: Updates using Socket.io (drag and drop tasks).
4.  **Roles**: Admin, Member, Viewer (RBAC).
5.  **Performance**: Infinite scroll for tasks, Optimistic UI updates.

## Architecture
*   **DB**: Schema with `Users`, `Workspaces`, `Projects`, `Tasks` (Columns).
*   **Backend**: Node/Express with Layered Architecture (Controller/Service/Repo).
*   **Frontend**: React + TanStack Query + Zustand + Tailwind CSS.
*   **DevOps**: Dockerized and deployed to a VPS with Nginx.

## Implementation Steps
1.  Draw the Database Schema (ERD).
2.  Setup the Monorepo (client/server folders).
3.  Build the Auth API first.
4.  Build the Workspace CRUD.
5.  Connect Frontend Auth.
6.  Implement Tasks with simple CRUD.
7.  Add Socket.io for real-time updates.
8.  Dockerize and Deploy.

If you can build this *cleanly*, properly typed, and with tests... **You are hired.**
