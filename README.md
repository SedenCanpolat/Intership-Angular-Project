# Internship Angular Project
My internship project was developed using Angular in front-end web development.  
You can find the PDF version of the report, which contains all the details of the project I submitted at the end of my internship, in the files under the name Internship-Report.pdf.

## Key Technical Implementations

### 1. Authentication with Angular Signals

Reactive front-end authentication implemented using **Angular Signals** for state tracking:

```typescript
@Injectable({ providedIn: 'root' })
export class AuthGuard {
  private isAuthenticated = signal(false);

  login(username: string, password: string): boolean {
    if (username === 'admin' && password === '1234') {
      this.isAuthenticated.set(true);
      localStorage.setItem('isLoggedIn', 'true');
      return true;
    }
    return false;
  }

  checkAuth(): boolean {
    this.isAuthenticated.set(localStorage.getItem('isLoggedIn') === 'true');
    return this.isAuthenticated();
  }
}
```

**Highlights**
- Angular Signals for reactive authentication state  
- UI-level access control using conditional rendering in `AppComponent`  
- Session persistence with `localStorage`  
- Authentication state validation via boolean checks  

### 2. Type-Safe API Integration

REST API consumption using TypeScript interfaces for structured data handling:

```typescript
export interface ApiData {
  name: string;
  country: string;
  alpha_two_code: string;
  web_pages: string;
  domains: string[];
}

this.http
  .get<ApiData[]>('http://universities.hipolabs.com/search?name=middle')
  .subscribe(data => {
    this.universitiesList = data;
  });
```

**Highlights**
- Strongly typed HTTP requests  
- RxJS Observables for asynchronous data handling  
- Data fetching on component initialization  

### 3. Nested Routing Architecture

Parent–child routing structure for organized navigation:

```typescript
export const routes: Routes = [
  { path: '', redirectTo: '/university', pathMatch: 'full' },
  { path: 'university', component: UniversityComponent, children: universityRoutes }
];

export const universityRoutes: Routes = [
  { path: '', redirectTo: '', pathMatch: 'full' },
  { path: 'main', redirectTo: '' },
  { path: 'info', component: InfoUniversityComponent },
  { path: 'html', component: TableUniversityDetailsComponent },
  { path: 'prime', component: PrimeTableComponent },
  { path: 'api-html', component: ApiExampleComponent },
  { path: 'api-prime', component: ApiPrimengComponent }
];
```

**Highlights**
- Modular and scalable routing structure  
- Clear parent–child navigation hierarchy  
- Clean and readable URLs  

### 4. Standalone Components (Modern Angular)

Angular standalone components implemented without `NgModule`s:

```typescript
@Component({
  selector: 'app-root',
  standalone: true,
  imports: [UniversityComponent, LoginComponent, CommonModule, RouterModule],
})
export class AppComponent {}

bootstrapApplication(AppComponent, {
  providers: [provideRouter(routes), provideAnimations()]
});
```

**Highlights**
- Modern Angular standalone API  
- Explicit per-component dependency management  
- Simplified project structure  

### 5. TypeScript Data Modeling

Strongly typed interfaces used throughout the project:

```typescript
export interface UniversityCountries {
  name: string;
  country: string;
}

export interface ApiData {
  name: string;
  country: string;
  alpha_two_code: string;
  web_pages: string;
  domains: string[];
}
```

**Why It Matters**
- Prevents runtime errors  
- Improves readability and maintainability  
- Better IDE support and autocomplete  

### 6. UI Development with PrimeNG

Professional UI components built using **PrimeNG**:

```html
<p-table [value]="universitiesList">
  <ng-template pTemplate="header">
    <tr><th>Name</th></tr>
  </ng-template>
</p-table>

<p-sidebar [(visible)]="visibleSidebar">
  <ul>
    <li><a routerLink="info">University Info</a></li>
  </ul>
</p-sidebar>
```

**Highlights**
- PrimeNG `p-table` for data presentation  
- PrimeNG `p-sidebar` for navigation  
- Template-driven UI rendering  

## Installation and Setup

```bash
git clone https://github.com/SedenCanpolat/Intership-Angular-Project.git
cd Intership-Angular-Project
npm install
ng serve
```

### Login Credentials

- **Username:** admin  
- **Password:** 1234  

## Application Structure

```text
src/app/
├── api-data.ts                     # API response interface
├── api-example/                    # HTML table with API data
├── api-primeng/                    # PrimeNG table with API data
├── auth.guard.ts                   # Front-end authentication service
├── login/                          # Login component
├── side/                           # Sidebar navigation (PrimeNG)
├── table-university-details/       # Static HTML table
├── prime-table/                    # Static PrimeNG table
├── university/                     # Main container component
│   └── university-routing.module.ts# Child route definitions
└── app-routing.module.ts           # Root routing configuration
```


