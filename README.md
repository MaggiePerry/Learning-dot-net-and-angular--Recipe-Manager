# Recipe Manager - .NET + Angular Learning Project

A full-stack recipe management web application built to learn core .NET/C# and Angular/TypeScript concepts.

## About This Project

This is an AI-assisted learning project. The project plan, task breakdown, and issue definitions were created collaboratively with AI (Claude), but **all programming and implementation is done by me**. The AI serves as a planning and learning partner — not a code generator.

### How AI Was Used
- **Project planning:** Claude helped structure the 7-phase learning plan with clear milestones
- **Task breakdown:** Each phase was broken into focused GitHub issues with acceptance criteria
- **Concept mapping:** Each task identifies the specific .NET/Angular concepts it covers
- **Code:** Written by me to build real understanding of the technologies

## What It Does

A web app where users can create, browse, search, and organize recipes. Each recipe has a title, description, ingredients, steps, cook time, category, and an optional image URL.

## Tech Stack

- **Backend:** .NET 8 Web API, C#, Entity Framework Core, SQL Server (LocalDB)
- **Frontend:** Angular 18, TypeScript, Angular Material
- **Auth:** JWT authentication with ASP.NET Identity
- **Testing:** xUnit (backend), Jasmine/Karma (frontend)

## Project Structure

See [PLAN.md](PLAN.md) for the full project plan with phases and checklists.

See [ISSUES.md](ISSUES.md) for the GitHub issue definitions broken out by sub-section.

## Setup Instructions

*(To be completed as each phase is implemented)*

### Prerequisites
- .NET 8 SDK
- Node.js (LTS)
- Angular CLI
- SQL Server LocalDB

### Backend
```bash
cd RecipeManager.API
dotnet restore
dotnet ef database update
dotnet run
```

### Frontend
```bash
cd recipe-manager-ui
npm install
ng serve
```

The frontend runs on `http://localhost:4200` and proxies API requests to the backend at `https://localhost:5001`.
