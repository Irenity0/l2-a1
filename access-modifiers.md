In TypeScript, access modifiers control how we access class properties and methods. They help us protect data, control visibility, and define how classes interact with each other.

TypeScript provides three main access modifiers: `public`, `private`, and `protected`. It also provides `readonly`, which controls whether a property can be modified after initialization.

## 1. Public

The `public` modifier allows us to access properties and methods from anywhere: inside the class, outside the class, and from child classes.

It is the default access modifier in TypeScript, so we don't need to explicitly write it.

Example:

typescript

```typescript
class User {
  public name: string;

  constructor(name: string) {
    this.name = name;
  }
}

const user = new User("John");

console.log(user.name); // John

user.name = "David"; // Allowed
```

Here, we can access and modify `name` directly from outside the class.

When to use it: When we want a property or method to be accessible throughout our application.

## 2. Private

The `private` modifier restricts access to a property or method to the class where it is declared. We cannot access it directly from outside the class or from child classes.

Example:

typescript

```typescript
class BankAccount {
  private balance: number = 1000;

  public getBalance(): number {
    return this.balance;
  }

  public deposit(amount: number): void {
    this.balance += amount;
  }
}

const account = new BankAccount();

console.log(account.getBalance()); // 1000

account.deposit(500); // Allowed

// Error: Property 'balance' is private
console.log(account.balance);
```

Here, `balance` is private, so we cannot access it directly. Instead, we use public methods such as `getBalance()` and `deposit()` to interact with it.

When to use it: When we want to protect internal data and prevent unintended direct access or modifications.

Important: TypeScript's `private` is enforced during compile-time type checking. JavaScript's native `#private` fields provide runtime privacy.

## 3. Protected

The `protected` modifier allows access to a property or method inside its own class and its child classes. However, it cannot be accessed directly from outside the class.

Example:

typescript

```typescript
class Employee {
  protected salary: number = 5000;
}

class Manager extends Employee {
  public showSalary(): void {
    console.log(this.salary); // Allowed
  }
}

const manager = new Manager();

manager.showSalary(); // 5000

// Error: Property 'salary' is protected
console.log(manager.salary);
```

Here, `Manager` inherits from `Employee`, so it can access the protected `salary` property. However, external code cannot access it directly.

When to use it: When we want to share properties or methods with child classes while keeping them inaccessible to external code.

## 4\. Readonly

The `readonly` modifier prevents a property from being reassigned after it has been initialized. We can assign its value when declaring it or inside the class constructor, but we cannot change it afterward.

Example:

typescript

```typescript
class User {
  readonly id: number;

  constructor(id: number) {
    this.id = id;
  }
}

const user = new User(101);

console.log(user.id); // 101

// Error: Cannot assign to 'id'
user.id = 202;
```

Here, the `id` property can be initialized in the constructor, but we cannot reassign it afterward.

When to use it: When we want to ensure that certain properties, such as IDs or creation dates, cannot be reassigned.

## Quick comparison

| Modifier | Inside class | Child class | Outside class | Reassignment |
| --- | --- | --- | --- | --- |
| `public` | Yes | Yes | Yes | Allowed |
| `private` | Yes | No | No | Allowed |
| `protected` | Yes | Yes | No | Allowed |
| `readonly` | Yes | Yes | Yes (read only) | Not after initialization |

## Practical recommendation

As a general rule, we should use:

- Public: For properties and methods that need to be accessible everywhere.
- Private: For internal data that should only be accessed within the class.
- Protected: For properties and methods that should be shared with child classes.
- Readonly: For properties whose values should not be reassigned after initialization.

Key takeaway: Access modifiers help us achieve encapsulation in OOP. They allow us to control how data is accessed and modified, making our TypeScript applications more maintainable, predictable, and easier to manage.