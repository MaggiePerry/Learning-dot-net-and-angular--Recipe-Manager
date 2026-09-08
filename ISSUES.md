# GitHub Issues

Issues to create for the Recipe Manager project, organized by phase and sub-section.

---

## Issue 1: Phase 1 - Backend Setup

**Title:** Phase 1: Backend project setup (.NET 8 solution structure)

**Body:**
Set up the .NET 8 backend project structure with proper solution organization.

### Tasks
- [ ] Install .NET 8 SDK, verify with `dotnet --version`
- [ ] Create solution: `dotnet new sln -n RecipeManager`
- [ ] Create Web API project: `dotnet new webapi -n RecipeManager.API`
- [ ] Create class library: `dotnet new classlib -n RecipeManager.Core` (models/interfaces)
- [ ] Create class library: `dotnet new classlib -n RecipeManager.Data` (EF Core/repositories)
- [ ] Add projects to solution and set up project references
- [ ] Install NuGet packages: EF Core, SQL Server provider, Identity, JWT Bearer
- [ ] Verify backend runs and returns the default weather forecast endpoint

### C# Concepts Covered
Solutions, project structure, namespaces, NuGet packages

### Acceptance Criteria
- Solution compiles and runs
- Three projects exist: API, Core, Data
- Project references are correctly wired (API -> Core, API -> Data, Data -> Core)
- `dotnet run` on the API project returns the weather forecast sample endpoint

---

## Issue 2: Phase 1 - Frontend Setup

**Title:** Phase 1: Frontend project setup (Angular 18 with Angular Material)

**Body:**
Set up the Angular 18 frontend project with Angular Material and development proxy.

### Tasks
- [ ] Install Node.js (LTS) and Angular CLI: `npm install -g @angular/cli`
- [ ] Create Angular app: `ng new recipe-manager-ui --routing --style=scss`
- [ ] Install Angular Material: `ng add @angular/material`
- [ ] Set up folder structure: `core/`, `features/`, `shared/`
- [ ] Configure proxy for API calls during development (`proxy.conf.json`)
- [ ] Verify frontend runs and shows default Angular page
- [ ] Verify frontend can proxy requests to backend

### Angular Concepts Covered
CLI, project structure, modules, Angular Material setup

### Acceptance Criteria
- `ng serve` runs without errors
- Angular Material is installed and a Material component can be rendered
- Proxy config forwards `/api/*` requests to the .NET backend

---

## Issue 3: Phase 2 - Backend Models

**Title:** Phase 2: Create data models and DTOs (RecipeManager.Core)

**Body:**
Define the domain models and DTOs that represent the recipe data structure.

### Tasks
- [ ] Create `Recipe` model with properties: Id, Title, Description, ImageUrl, PrepTime, CookTime, Servings, CreatedAt, UpdatedAt
- [ ] Create `Ingredient` model with properties: Id, Name, Quantity, Unit, RecipeId
- [ ] Create `Step` model with properties: Id, Instruction, OrderNumber, RecipeId
- [ ] Create `Category` model (Id, Name) with many-to-many relationship to Recipe
- [ ] Create DTOs: `RecipeDto`, `CreateRecipeDto`, `UpdateRecipeDto`

### C# Concepts Covered
Classes, properties, data annotations, access modifiers, collections, DTOs

### Acceptance Criteria
- All models are in the `RecipeManager.Core` project
- Models use appropriate data annotations for validation
- DTOs exist for create, update, and read operations
- Solution still compiles

---

## Issue 4: Phase 2 - Database Setup with EF Core

**Title:** Phase 2: Set up database with Entity Framework Core

**Body:**
Configure Entity Framework Core with DbContext, migrations, and seed data.

### Tasks
- [ ] Create `AppDbContext` inheriting from `DbContext`
- [ ] Configure entity relationships with Fluent API (one-to-many for Ingredients/Steps, many-to-many for Categories)
- [ ] Add connection string to `appsettings.json` (SQL Server LocalDB)
- [ ] Create initial migration: `dotnet ef migrations add InitialCreate`
- [ ] Apply migration: `dotnet ef database update`
- [ ] Create seed data with 5-10 sample recipes

### C# Concepts Covered
Entity Framework Core, DbContext, migrations, Fluent API, LINQ, connection strings

### Acceptance Criteria
- Database is created via migration
- Seed data populates the database on first run
- Relationships are correct (Recipe has many Ingredients, many Steps, many-to-many with Categories)

---

## Issue 5: Phase 2 - Frontend TypeScript Models

**Title:** Phase 2: Create TypeScript interfaces and environment config

**Body:**
Define TypeScript interfaces matching the backend models and configure the API URL.

### Tasks
- [ ] Create TypeScript interfaces: `Recipe`, `Ingredient`, `Step`, `Category`
- [ ] Create environment config for API URL

### TypeScript Concepts Covered
Interfaces, type safety, enums, environment configuration

### Acceptance Criteria
- Interfaces match the backend DTOs
- Environment files have the correct API base URL configured

---

## Issue 6: Phase 3 - Repository Pattern

**Title:** Phase 3: Implement repository pattern for data access

**Body:**
Create the repository interface and implementation for recipe data access using EF Core.

### Tasks
- [ ] Create `IRecipeRepository` interface in `RecipeManager.Core`
- [ ] Implement `RecipeRepository` in `RecipeManager.Data` with EF Core
- [ ] Implement methods: GetAll (with pagination), GetById, Create, Update, Delete, Search, GetByCategory
- [ ] Register repository in DI container (`Program.cs`)

### C# Concepts Covered
Interfaces, dependency injection, repository pattern, async/await, LINQ queries

### Acceptance Criteria
- `IRecipeRepository` defines all CRUD + search methods
- `RecipeRepository` implements all methods using EF Core and LINQ
- Repository is registered in `Program.cs` as a scoped service
- All methods are async

---

## Issue 7: Phase 3 - API Controllers

**Title:** Phase 3: Build REST API controllers with CRUD endpoints

**Body:**
Create the RecipesController and CategoriesController with full CRUD operations, validation, and error handling.

### Tasks
- [ ] Create `RecipesController` with `[ApiController]` attribute
- [ ] Implement GET `/api/recipes` - list all with pagination
- [ ] Implement GET `/api/recipes/{id}` - get single recipe with ingredients and steps
- [ ] Implement POST `/api/recipes` - create new recipe
- [ ] Implement PUT `/api/recipes/{id}` - update recipe
- [ ] Implement DELETE `/api/recipes/{id}` - delete recipe
- [ ] Implement GET `/api/recipes/search?q=` - search recipes
- [ ] Implement GET `/api/categories` - list categories
- [ ] Add model validation with Data Annotations
- [ ] Add error handling with try/catch and proper status codes
- [ ] Configure CORS in `Program.cs`

### C# Concepts Covered
Controllers, routing, HTTP methods, model binding, validation, action results, CORS, middleware

### Acceptance Criteria
- All endpoints return correct status codes (200, 201, 204, 400, 404)
- Validation errors return 400 with details
- Swagger UI shows all endpoints and they work correctly
- CORS allows the Angular frontend origin

---

## Issue 8: Phase 3 - AutoMapper Setup

**Title:** Phase 3: Configure AutoMapper for entity-to-DTO mapping

**Body:**
Set up AutoMapper to handle conversion between EF Core entities and DTOs.

### Tasks
- [ ] Install AutoMapper NuGet package
- [ ] Create mapping profiles (Recipe <-> RecipeDto, CreateRecipeDto -> Recipe, etc.)
- [ ] Register AutoMapper in `Program.cs`

### C# Concepts Covered
Object mapping, profiles, NuGet libraries

### Acceptance Criteria
- Mapping profiles cover all entity-to-DTO and DTO-to-entity conversions
- Controllers use AutoMapper instead of manual mapping

---

## Issue 9: Phase 4 - Recipe Service (Angular)

**Title:** Phase 4: Create Angular RecipeService with HttpClient

**Body:**
Build the Angular service layer that communicates with the .NET API.

### Tasks
- [ ] Create `RecipeService` using `HttpClient`
- [ ] Implement methods: getAll, getById, create, update, delete, search
- [ ] Add error handling with RxJS `catchError`
- [ ] Create a shared `ApiResponse` interface for typed responses

### Angular Concepts Covered
Services, HttpClient, dependency injection, Observables (RxJS), error handling

### Acceptance Criteria
- Service methods return typed Observables
- Error handling catches HTTP errors and provides meaningful messages
- Service is provided in root

---

## Issue 10: Phase 4 - Recipe List Page

**Title:** Phase 4: Build recipe list page with search and filtering

**Body:**
Create the recipe list component with a card grid, search, category filtering, and pagination.

### Tasks
- [ ] Generate component: `ng generate component features/recipes/recipe-list`
- [ ] Display recipes in a responsive card grid using Angular Material cards
- [ ] Add search bar with debounced input (RxJS `debounceTime`, `switchMap`)
- [ ] Add category filter chips
- [ ] Add pagination using Angular Material paginator
- [ ] Create a loading spinner component

### Angular Concepts Covered
Components, templates, data binding (interpolation, property, event), *ngFor, *ngIf, pipes, Angular Material components

### Acceptance Criteria
- Recipe cards display title, description, cook time, and image
- Search filters results as the user types (with debounce)
- Category chips filter by selected category
- Pagination works with the API's paginated response
- Loading spinner shows while data is being fetched

---

## Issue 11: Phase 4 - Recipe Detail Page

**Title:** Phase 4: Build recipe detail page with routing

**Body:**
Create the recipe detail component that displays a full recipe with ingredients and steps.

### Tasks
- [ ] Generate component: `ng generate component features/recipes/recipe-detail`
- [ ] Set up route: `/recipes/:id`
- [ ] Display full recipe with all fields, ingredients list, and ordered steps
- [ ] Add edit and delete buttons
- [ ] Use `ActivatedRoute` to read route params

### Angular Concepts Covered
Routing, route parameters, component lifecycle (ngOnInit), async pipe

### Acceptance Criteria
- Navigating to `/recipes/1` loads and displays recipe with id 1
- Ingredients and steps are displayed in order
- Edit button navigates to the edit form
- Delete button removes the recipe (with confirmation)

---

## Issue 12: Phase 4 - Navigation Component

**Title:** Phase 4: Create navigation bar and configure routing

**Body:**
Set up the app's navigation structure with Angular Material toolbar and route configuration.

### Tasks
- [ ] Create header/navbar component with Angular Material toolbar
- [ ] Set up routes: home, recipe list (`/recipes`), recipe detail (`/recipes/:id`)
- [ ] Add active route highlighting with `routerLinkActive`

### Angular Concepts Covered
Router, routerLink, routerLinkActive

### Acceptance Criteria
- Navbar displays app name and navigation links
- Active route is visually highlighted
- All routes navigate correctly

---

## Issue 13: Phase 5 - Recipe Form Component

**Title:** Phase 5: Build reactive recipe form with dynamic arrays

**Body:**
Create the recipe form component using Angular reactive forms with dynamic ingredient and step arrays.

### Tasks
- [ ] Generate component: `ng generate component features/recipes/recipe-form`
- [ ] Build reactive form with `FormBuilder`
- [ ] Add fields: title, description, imageUrl, prepTime, cookTime, servings
- [ ] Implement dynamic `FormArray` for ingredients (add/remove rows)
- [ ] Implement dynamic `FormArray` for steps (add/remove, drag to reorder)
- [ ] Add category multi-select dropdown
- [ ] Add validators: required, min/max length, number ranges
- [ ] Display validation error messages inline
- [ ] Reuse form for both create (`/recipes/new`) and edit (`/recipes/:id/edit`) modes

### Angular Concepts Covered
Reactive forms, FormBuilder, FormGroup, FormArray, Validators, two-way binding, conditional rendering

### Acceptance Criteria
- Form validates all required fields before submission
- Ingredients and steps can be dynamically added and removed
- Form pre-populates when editing an existing recipe
- Validation messages appear when fields are touched and invalid
- Form submits to the correct API endpoint (POST for create, PUT for edit)

---

## Issue 14: Phase 5 - UX Polish (Notifications, Dialogs, Loading States)

**Title:** Phase 5: Add toast notifications, confirmation dialogs, and loading states

**Body:**
Polish the user experience with feedback mechanisms across the app.

### Tasks
- [ ] Add success/error toast notifications using Angular Material snackbar
- [ ] Add confirmation dialog before delete using Angular Material dialog
- [ ] Add loading states on form submit (disable button, show spinner)
- [ ] Navigate back to list/detail after successful save

### Angular Concepts Covered
Material dialogs, snackbars, Router navigation, component communication

### Acceptance Criteria
- Success message appears after creating/updating/deleting a recipe
- Error messages appear when API calls fail
- Delete action requires confirmation before proceeding
- Submit button is disabled while request is in progress

---

## Issue 15: Phase 6 - Backend Authentication

**Title:** Phase 6: Implement JWT authentication with ASP.NET Identity

**Body:**
Add user authentication to the backend using ASP.NET Identity and JWT tokens.

### Tasks
- [ ] Add ASP.NET Identity to the project
- [ ] Create `ApplicationUser` class extending `IdentityUser`
- [ ] Create `AuthController` with Register and Login endpoints
- [ ] Configure JWT token generation (access token with claims)
- [ ] Add `[Authorize]` attribute to create/update/delete endpoints
- [ ] Allow anonymous access (`[AllowAnonymous]`) to GET endpoints
- [ ] Add UserId foreign key to Recipe model (recipes belong to users)
- [ ] Update migration for the new user relationship

### C# Concepts Covered
Identity, JWT, authentication middleware, authorization attributes, claims

### Acceptance Criteria
- Users can register with email/password
- Users can login and receive a JWT token
- Protected endpoints return 401 without a valid token
- GET endpoints remain publicly accessible
- Recipes are associated with the user who created them

---

## Issue 16: Phase 6 - Frontend Authentication

**Title:** Phase 6: Implement frontend auth (login, register, guards, interceptor)

**Body:**
Build the Angular authentication flow including login/register forms, token management, and route protection.

### Tasks
- [ ] Create `AuthService` with login, register, store token, and logout methods
- [ ] Create login component with reactive form
- [ ] Create register component with reactive form
- [ ] Create an HTTP interceptor to attach JWT token to outgoing requests
- [ ] Create a route guard (`AuthGuard`) to protect create/edit routes
- [ ] Show/hide nav items based on authentication state
- [ ] Store JWT token in localStorage

### Angular Concepts Covered
HTTP interceptors, route guards, localStorage, conditional UI, auth patterns

### Acceptance Criteria
- Users can register and login from the UI
- JWT token is automatically attached to API requests
- Unauthenticated users are redirected to login when accessing protected routes
- Nav shows Login/Register when logged out, and Logout when logged in
- Token persists across page refreshes

---

## Issue 17: Phase 7 - Backend Tests

**Title:** Phase 7: Write backend unit and integration tests with xUnit

**Body:**
Add test coverage for the repository layer and API controllers using xUnit.

### Tasks
- [ ] Create `RecipeManager.Tests` xUnit project
- [ ] Write 3-5 unit tests for `RecipeRepository` using in-memory database
- [ ] Write 2-3 integration tests for `RecipesController`
- [ ] Cover scenarios: validation errors, not-found (404), and successful CRUD

### C# Concepts Covered
xUnit, Arrange-Act-Assert, mocking, in-memory database, test project setup

### Acceptance Criteria
- All tests pass with `dotnet test`
- Tests cover happy path and error scenarios
- In-memory database is used (no dependency on real SQL Server for tests)

---

## Issue 18: Phase 7 - Frontend Tests

**Title:** Phase 7: Write frontend component and service tests

**Body:**
Add basic test coverage for key Angular components and services.

### Tasks
- [ ] Write 2-3 component tests (recipe list renders correctly, form validates)
- [ ] Write 1-2 service tests (mock HttpClient, verify correct API calls)
- [ ] Ensure all tests pass: `ng test`

### Angular Concepts Covered
Jasmine, Karma, TestBed, component testing, service mocking

### Acceptance Criteria
- All tests pass with `ng test`
- Tests verify component rendering and form validation behavior
- Service tests mock HTTP calls and verify request URLs/methods

---

## Issue 19: Phase 7 - Final Polish

**Title:** Phase 7: Final review, cleanup, and documentation

**Body:**
Final pass to ensure code quality, type safety, and complete documentation.

### Tasks
- [ ] Review error handling across both backend and frontend
- [ ] Ensure all TypeScript types are strict (no `any` types)
- [ ] Update README with complete setup and run instructions
- [ ] Do a full run-through of all features end-to-end
- [ ] Verify all phases are committed cleanly

### Acceptance Criteria
- No TypeScript `any` types in the codebase
- README contains setup instructions for both backend and frontend
- All features work end-to-end: browse, search, create, edit, delete, login, register
