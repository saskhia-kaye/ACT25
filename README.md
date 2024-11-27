# ACT25
SOLID PRINCIPLES

S - Single Responsibility Principle (SRP)

Definition: A class should have only one reason to change. It should focus on a single responsibility.

Implementation in Angular:

Divide components, services, and modules based on their distinct responsibilities.

// Violating SRP
@Component({
  selector: 'app-dashboard',
  templateUrl: './dashboard.component.html',
})
export class DashboardComponent {
  fetchData() {
    // Fetch API logic here
  }

  renderChart() {
    // Chart rendering logic here
  }
}

// Following SRP
@Component({
  selector: 'app-dashboard',
  templateUrl: './dashboard.component.html',
})
export class DashboardComponent {
  constructor(private dataService: DataService) {}

  ngOnInit() {
    this.dataService.fetchData();
  }
}

@Injectable({
  providedIn: 'root',
})
export class DataService {
  fetchData() {
    // Fetch API logic here
  }
}


Real-World Use Case:

In a large Angular project, separating concerns ensures smoother testing and updates when the API or charting library changes.

O - Open/Closed Principle (OCP)

Definition: Software entities should be open for extension but closed for modification.

Implementation in Angular:

Use Angular’s dependency injection and inheritance for extending functionality without altering existing code.

// Adding a new feature without modifying existing logic
@Injectable({
  providedIn: 'root',
})
export class NotificationService {
  sendEmailNotification(message: string) {
    // Email logic
  }
}

@Injectable({
  providedIn: 'root',
})
export class AdvancedNotificationService extends NotificationService {
  sendPushNotification(message: string) {
    // Push notification logic
  }
}


Real-World Use Case:

Adding SMS notifications without modifying the existing notification services.

L - Liskov Substitution Principle (LSP)

Definition: Objects of a superclass should be replaceable with objects of a subclass without affecting the application.

Implementation in Angular:

Ensure derived components or services behave as expected.

export abstract class Shape {
  abstract area(): number;
}

export class Rectangle extends Shape {
  constructor(private width: number, private height: number) {
    super();
  }
  area() {
    return this.width * this.height;
  }
}

export class Square extends Shape {
  constructor(private side: number) {
    super();
  }
  area() {
    return this.side * this.side;
  }
}


Real-World Use Case:

For geometric calculations, replacing a Rectangle object with a Square object should not break the calculation logic.

I - Interface Segregation Principle (ISP)

Definition: A class should not be forced to implement interfaces it does not use.

Implementation in Angular:

Split large interfaces into smaller, more specific ones.

// Violating ISP
export interface User {
  id: number;
  name: string;
  email: string;
  sendEmail(email: string): void;
}

// Following ISP
export interface UserDetails {
  id: number;
  name: string;
  email: string;
}

export interface EmailSender {
  sendEmail(email: string): void;
}


Real-World Use Case:

Avoid overloading user models with methods unrelated to their primary purpose.

D - Dependency Inversion Principle (DIP)

Definition: High-level modules should not depend on low-level modules. Both should depend on abstractions.

Implementation in Angular:

Leverage dependency injection for decoupling dependencies.

@Injectable({
  providedIn: 'root',
})
export class HttpService {
  getData(url: string) {
    return fetch(url);
  }
}

@Injectable({
  providedIn: 'root',
})
export class DataService {
  constructor(private httpService: HttpService) {}

  fetchData() {
    return this.httpService.getData('https://api.example.com');
  }
}


Real-World Use Case:

Easily swap the HttpService with another library like Axios without changing DataService

