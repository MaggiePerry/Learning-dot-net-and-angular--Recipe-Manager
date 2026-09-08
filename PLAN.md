# Recipe Manager - Project Plan

A full-stack recipe management app built with .NET 8 and Angular 18 to learn core backend and frontend concepts.

**Tech Stack:**
- **Backend:** .NET 8 Web API, C#, Entity Framework Core, SQL Server (LocalDB)
- **Frontend:** Angular 18, TypeScript, Angular Material
- **Auth:** JWT authentication with ASP.NET Identity
- **Testing:** xUnit (backend), Jasmine/Karma (frontend)

---

## Phase 1: Project Setup & Foundation (~3 hours)

### Backend Setup
- [ ] Install .NET 8 SDK, verify with `dotnet --version`
- [ ] Create solution: `dotnet new sln -n RecipeManager`
- [ ] Create Web API project: `dotnet new webapi -n RecipeManager.API`
- [ ] Create class library: `dotnet new classlib -n RecipeManager.Core` (models/interfaces)
- [ ] Create class library: `dotnet new classlib -n RecipeManager.Data` (EF Core/repositories)
- [ ] Add projects to solution and set up project references
- [ ] Install NuGet packages: EF Core, SQL Server provider, Identity, JWT Bearer

**C# concepts:** Solutions, project structure, namespaces, NuGet packages

### Frontend Setup
- [ ] Install Node.js (LTS) and Angular CLI: `npm install -g @angular/cli`
- [ ] Create Angular app: `ng new recipe-manager-ui --routing --style=scss`
- [ ] Install Angular Material: `ng add @angular/material`
- [ ] Set up folder structure: `core/`, `features/`, `shared/`
- [ ] Configure proxy for API calls during development (`proxy.conf.json`)

**Angular concepts:** CLI, project structure, modules, Angular Material setup

### Verification
- [ ] Backend runs and returns default weather forecast endpoint
- [ ] Frontend runs and shows default Angular page
- [ ] Frontend can proxy requests to backend

---

## Phase 2: Data Models & Database (~3 hours)

### Backend - Models (RecipeManager.Core)
- [ ] Create `Recipe` model (Id, Title, Description, ImageUrl, PrepTime, CookTime, Servings, CreatedAt, UpdatedAt)
- [ ] Create `Ingredient` model (Id, Name, Quantity, Unit, RecipeId)
- [ ] Create `Step` model (Id, Instruction, OrderNumber, RecipeId)
- [ ] Create `Category` model (Id, Name) with many-to-many relationship to Recipe
- [ ] Create DTOs: `RecipeDto`, `CreateRecipeDto`, `UpdateRecipeDto`

**C# concepts:** Classes, properties, data annotations, access modifiers, collections, DTOs

### Backend - Database (RecipeManager.Data)
- [ ] Create `AppDbContext` inheriting from `DbContext`
- [ ] Configure entity relationships with Fluent API (one-to-many, many-to-many)
- [ ] Add connection string to `appsettings.json`
- [ ] Create initial migration: `dotnet ef migrations add InitialCreate`
- [ ] Apply migration: `dotnet ef database update`
- [ ] Create seed data (5-10 sample recipes)

**C# concepts:** Entity Framework Core, DbContext, migrations, Fluent API, LINQ, connection strings

### Frontend - Models
- [ ] Create TypeScript interfaces: `Recipe`, `Ingredient`, `Step`, `Category`
- [ ] Create environment config for API URL

**TypeScript concepts:** Interfaces, type safety, enums, environment configuration

---

## Phase 3: API Layer - CRUD Operations (~3 hours)

### Backend - Repository Pattern
- [ ] Create `IRecipeRepository` interface
- [ ] Implement `RecipeRepository` with EF Core
- [ ] Methods: GetAll, GetById, Create, Update, Delete, Search, GetByCategory
- [ ] Register repository in DI container (`Program.cs`)

**C# concepts:** Interfaces, dependency injection, repository pattern, async/await, LINQ queries

### Backend - Controllers
- [ ] Create `RecipesController` with `[ApiController]` attribute
- [ ] GET `/api/recipes` - list all (with pagination)
- [ ] GET `/api/recipes/{id}` - get single recipe with ingredients and steps
- [ ] POST `/api/recipes` - create new recipe
- [ ] PUT `/api/recipes/{id}` - update recipe
- [ ] DELETE `/api/recipes/{id}` - delete recipe
- [ ] GET `/api/recipes/search?q=` - search recipes
- [ ] GET `/api/categories` - list categories
- [ ] Add model validation with Data Annotations
- [ ] Add proper error handling with try/catch and status codes
- [ ] Configure CORS in `Program.cs`

**C# concepts:** Controllers, routing, HTTP methods, model binding, validation, action results, CORS, middleware

### Backend - AutoMapper
- [ ] Install AutoMapper
- [ ] Create mapping profiles (Entity <-> DTO)

**C# concepts:** Object mapping, profiles, NuGet libraries

---

## Phase 4: Angular Core Features - Recipe List & Detail (~3 hours)

### Frontend - Services
- [ ] Create `RecipeService` using `HttpClient`
- [ ] Methods matching each API endpoint (getAll, getById, create, update, delete, search)
- [ ] Add error handling with RxJS `catchError`
- [ ] Create a shared `ApiResponse` interface for typed responses

**Angular concepts:** Services, HttpClient, dependency injection, Observables (RxJS), error handling

### Frontend - Recipe List Page
- [ ] Generate component: `ng generate component features/recipes/recipe-list`
- [ ] Display recipes in a responsive card grid (Angular Material cards)
- [ ] Add search bar with debounced input (RxJS `debounceTime`, `switchMap`)
- [ ] Add category filter chips
- [ ] Add pagination (Angular Material paginator)
- [ ] Create a loading spinner component

**Angular concepts:** Components, templates, data binding, *ngFor, *ngIf, pipes, Angular Material components

### Frontend - Recipe Detail Page
- [ ] Generate component: `ng generate component features/recipes/recipe-detail`
- [ ] Set up route: `/recipes/:id`
- [ ] Display full recipe with ingredients and steps
- [ ] Add edit and delete buttons
- [ ] Use `ActivatedRoute` to read route params

**Angular concepts:** Routing, route parameters, component lifecycle (ngOnInit), async pipe

### Frontend - Navigation
- [ ] Create header/navbar component with Angular Material toolbar
- [ ] Set up routes: home, recipe list, recipe detail
- [ ] Add active route highlighting

**Angular concepts:** Router, routerLink, routerLinkActive

---

## Phase 5: Angular Forms - Create & Edit Recipes (~3 hours)

### Frontend - Recipe Form
- [ ] Generate component: `ng generate component features/recipes/recipe-form`
- [ ] Build reactive form with `FormBuilder`
- [ ] Fields: title, description, imageUrl, prepTime, cookTime, servings
- [ ] Dynamic `FormArray` for ingredients (add/remove rows)
- [ ] Dynamic `FormArray` for steps (add/remove, drag to reorder)
- [ ] Category multi-select dropdown
- [ ] Add validators: required, min/max length, number ranges
- [ ] Display validation error messages
- [ ] Reuse form for both create and edit modes

**Angular concepts:** Reactive forms, FormBuilder, FormGroup, FormArray, Validators, two-way binding, conditional rendering

### Frontend - UX Polish
- [ ] Add success/error toast notifications (Angular Material snackbar)
- [ ] Add confirmation dialog before delete (Angular Material dialog)
- [ ] Add loading states on form submit
- [ ] Navigate back to list/detail after save

**Angular concepts:** Material dialogs, snackbars, Router navigation, component communication

---

## Phase 6: Authentication (~3 hours)

### Backend - Auth
- [ ] Add ASP.NET Identity to the project
- [ ] Create `ApplicationUser` extending `IdentityUser`
- [ ] Create `AuthController` with Register and Login endpoints
- [ ] Configure JWT token generation (access token)
- [ ] Add `[Authorize]` attribute to create/update/delete endpoints
- [ ] Allow anonymous access to GET endpoints
- [ ] Add UserId to Recipe model (recipes belong to users)

**C# concepts:** Identity, JWT, authentication middleware, authorization attributes, claims

### Frontend - Auth
- [ ] Create `AuthService` (login, register, store token, logout)
- [ ] Create login and register components with reactive forms
- [ ] Create an HTTP interceptor to attach JWT token to requests
- [ ] Create a route guard (`AuthGuard`) to protect create/edit routes
- [ ] Show/hide nav items based on auth state
- [ ] Store token in localStorage

**Angular concepts:** HTTP interceptors, route guards, localStorage, conditional UI, auth patterns

---

## Phase 7: Testing & Final Polish (~2-3 hours)

### Backend Tests
- [ ] Create `RecipeManager.Tests` xUnit project
- [ ] Write 3-5 unit tests for `RecipeRepository` (using in-memory database)
- [ ] Write 2-3 integration tests for `RecipesController`
- [ ] Test validation, not-found, and success scenarios

**C# concepts:** xUnit, Arrange-Act-Assert, mocking, in-memory database, test project setup

### Frontend Tests
- [ ] Write 2-3 component tests (recipe list renders, form validates)
- [ ] Write 1-2 service tests (mock HttpClient)
- [ ] Run tests: `ng test`

**Angular concepts:** Jasmine, Karma, TestBed, component testing, service mocking

### Final Polish
- [ ] Review error handling across both projects
- [ ] Make sure all TypeScript types are strict (no `any`)
- [ ] Add a simple README with setup instructions
- [ ] Do a final run-through of all features

---

## Key Concepts Checklist

### .NET / C#
- [ ] Project structure (solution, multiple projects)
- [ ] Classes, interfaces, properties, access modifiers
- [ ] Dependency Injection
- [ ] Entity Framework Core (code-first, migrations, LINQ)
- [ ] Web API controllers, routing, model binding
- [ ] Async/await
- [ ] DTOs and AutoMapper
- [ ] Validation and error handling
- [ ] Authentication (Identity + JWT)
- [ ] Repository pattern
- [ ] Unit and integration testing

### Angular / TypeScript
- [ ] Components, templates, data binding
- [ ] Services and dependency injection
- [ ] HttpClient and Observables (RxJS)
- [ ] Routing (params, guards, navigation)
- [ ] Reactive forms (FormBuilder, FormArray, validators)
- [ ] Angular Material UI components
- [ ] HTTP interceptors
- [ ] TypeScript interfaces and strict typing
- [ ] Component lifecycle hooks
- [ ] Pipes (built-in and custom if time allows)
- [ ] Component testing

---

## Estimated Timeline

| Phase | Hours | Focus |
|-------|-------|-------|
| 1 - Setup | ~3h | Project scaffolding |
| 2 - Data | ~3h | Models, EF Core, database |
| 3 - API | ~3h | CRUD endpoints, repository pattern |
| 4 - UI List/Detail | ~3h | Angular components, routing, services |
| 5 - UI Forms | ~3h | Reactive forms, validation |
| 6 - Auth | ~3h | JWT auth, guards, interceptors |
| 7 - Testing | ~2-3h | xUnit, Jasmine, polish |
| **Total** | **~20h** | |

## Notes
- Each phase builds on the previous one - don't skip ahead
- Commit code at the end of each phase
- If stuck, complete what you can and move on - circle back later
- The goal is breadth of concepts, not production-readiness
