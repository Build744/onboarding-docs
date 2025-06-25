# Introduction to Testing in C# with xUnit

## Objective of the Document

This document aims to provide a clear and practical introduction to unit testing in C# using the xUnit framework. It is intended for beginner or intermediate developers who want to understand the basics of automated testing and practice the core concepts with concrete examples.

## Table of Contents

1. Why Write Tests?
2. Overview of xUnit
3. Installing xUnit
4. Structure of a Test with xUnit and the AAA Pattern
5. Common Assertions
6. Parameterized Tests
7. Exception Handling
8. Best Practices
9. Practical Examples

---

## 1. Why Write Tests?

Unit tests allow you to:

- Verify that the code works as expected
- Reduce the risk of regression when making changes
- Document the expected behavior of the system
- Gain confidence during refactoring

## 2. Overview of xUnit

xUnit is a modern unit testing framework for .NET. It is widely used and supported by the community. It succeeds other frameworks like NUnit and MSTest.
## 3. Installing xUnit

### Using Visual Studio GUI (Option 1)

1. Open Visual Studio > Create a new project.
2. Choose **Class Library (.NET)** for your business logic project.
3. Create a second project using **xUnit Test Project (.NET)**.
4. Add a reference from the test project to the business logic project: right-click on the test project > "Add" > "Project Reference" > check the business project.
5. Manage NuGet packages if needed (right-click > Manage NuGet Packages > search for xUnit if not pre-installed).

### Using .NET CLI (Option 2)

```bash
# Create a solution and a test project
dotnet new sln -n DemoTests
cd DemoTests

dotnet new classlib -n DemoApp
dotnet new xunit -n DemoApp.Tests
dotnet sln add DemoApp/DemoApp.csproj
dotnet sln add DemoApp.Tests/DemoApp.Tests.csproj
dotnet add DemoApp.Tests/DemoApp.Tests.csproj reference DemoApp/DemoApp.csproj
```

## 4. Structure of a Test with xUnit and the AAA Pattern

When writing unit tests, it's best practice to follow the **AAA pattern**: **Arrange, Act, Assert**. This pattern helps make tests clear and maintainable by dividing each test into three sections:

- **Arrange**: Set up the objects, data, and prerequisites needed for the test.
- **Act**: Perform the action or call the method under test.
- **Assert**: Verify that the outcome is as expected.

### Example Using AAA with xUnit

```csharp
public class Calculator
{
    public int Add(int a, int b) => a + b;
}
```

```csharp
public class CalculatorTests
{
    [Fact]
    public void Add_ReturnsCorrectSum()
    {
        // Arrange
        var calculator = new Calculator();

        // Act
        int result = calculator.Add(2, 3);

        // Assert
        Assert.Equal(5, result);
    }
}
```

**Benefits of the AAA Pattern:**
- Improves readability by clearly separating setup, execution, and verification.
- Makes it easier to identify what is being tested and why a test might fail.
- Encourages writing focused and concise tests.

## 5. Common Assertions

Here are the most used assertions in xUnit:

- `Assert.Equal(expected, actual)`: checks that two values are equal.
- `Assert.NotEqual(notExpected, actual)`: checks that two values are different.
- `Assert.True(condition)`: checks that a condition is true.
- `Assert.False(condition)`: checks that a condition is false.
- `Assert.Null(object)`: checks that an object is null.
- `Assert.NotNull(object)`: checks that an object is not null.
- `Assert.Throws<TException>(() => { })`: checks that an exception of type `TException` is thrown.
- `Assert.IsType<T>(object)`: checks that an object is of a specific type.
- `Assert.Contains(substring, string)`: checks that a string contains a substring.

## 6. Parameterized Tests

```csharp
public class CalculatorTests
{
    [Theory]
    [InlineData(1, 2, 3)]
    [InlineData(-1, -1, -2)]
    [InlineData(0, 0, 0)]
    public void Add_WorksForMultipleInputs(int a, int b, int expected)
    {
        var calculator = new Calculator();

        var result = calculator.Add(a, b);

        Assert.Equal(expected, result);
    }
}
```

## 7. Exception Handling

```csharp
public class StringProcessor
{
    public string GetFirstCharacter(string input)
    {
        if (string.IsNullOrEmpty(input))
            throw new ArgumentException("Input cannot be null or empty");

        return input[0].ToString();
    }
}

public class StringProcessorTests
{
    [Fact]
    public void GetFirstCharacter_ThrowsException_WhenInputIsEmpty()
    {
        var processor = new StringProcessor();

        Assert.Throws<ArgumentException>(() => processor.GetFirstCharacter(""));
    }
}
```

## 8. Best Practices

- Name tests clearly (e.g., Method_Condition_ExpectedResult)
- Keep a single `Assert` per test when possible
- Separate Arrange / Act / Assert phases
- Isolate tests (avoid external dependencies)
- Use mocks for dependencies (with libraries like Moq)

## 9. Practical Examples

### Example 1: Email Validation

#### Code to Test

```csharp
public class EmailValidator
{
    public bool IsValid(string email)
    {
        return !string.IsNullOrWhiteSpace(email)
               && email.Contains("@")
               && email.IndexOf('.') > email.IndexOf('@');
    }
}
```

#### Tests

```csharp
public class EmailValidatorTests
{
    private readonly EmailValidator _validator = new EmailValidator();

    [Fact]
    public void IsValid_ReturnsTrue_ForValidEmail()
    {
        Assert.True(_validator.IsValid("test@example.com"));
    }

    [Fact]
    public void IsValid_ReturnsFalse_ForMissingAt()
    {
        Assert.False(_validator.IsValid("testexample.com"));
    }

    [Fact]
    public void IsValid_ReturnsFalse_ForMissingDot()
    {
        Assert.False(_validator.IsValid("test@examplecom"));
    }
}
```

### Example 2: User Management

#### Code to Test

```csharp
public class UserManager
{
    private readonly HashSet<string> _usernames = new HashSet<string>();

    public void AddUser(string username)
    {
        if (string.IsNullOrWhiteSpace(username))
            throw new ArgumentException("Username cannot be empty");

        if (!_usernames.Add(username))
            throw new InvalidOperationException("Username already exists");
    }
}
```

#### Tests

```csharp
public class UserManagerTests
{
    [Fact]
    public void AddUser_ThrowsException_WhenUsernameIsEmpty()
    {
        var manager = new UserManager();

        Assert.Throws<ArgumentException>(() => manager.AddUser(" "));
    }

    [Fact]
    public void AddUser_ThrowsException_WhenUsernameAlreadyExists()
    {
        var manager = new UserManager();
        manager.AddUser("fad");

        Assert.Throws<InvalidOperationException>(() => manager.AddUser("fad"));
    }

    [Fact]
    public void AddUser_AddsUser_WhenValid()
    {
        var manager = new UserManager();

        var ex = Record.Exception(() => manager.AddUser("fad.ouro"));

        Assert.Null(ex);
    }
}
```

---

## Conclusion

Unit testing is a fundamental pillar of modern software development. xUnit provides a clear, powerful, and .NET-integrated approach to testing your applications efficiently. Regular testing practice improves code quality and maintainability.

This document gives you the essential tools to get started. It is recommended to follow up this introduction with advanced topics like mocking, async tests, integration tests, and code coverage.