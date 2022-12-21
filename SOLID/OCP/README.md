# Open-Closed-Principle
## Overview
The open-closed principle is a principle in object-oriented design that states that software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification. This means that you should be able to add new functionality to a class or module without changing its existing code.

## Example
In the incorrect implementation, the `PaymentProcessor` class processes a payment based on a string input that specifies the payment type. This means that if you want to add a new payment method, you need to modify the `ProcessPayment()` method to include a new `if` statement for that method. This violates the open-closed principle, as you are required to modify the existing code in order to add new functionality.
```c#
IPaymentMethod creditCard = new CreditCardPayment();
PaymentProcessor processor = new PaymentProcessor(creditCard);
processor.ProcessPayment(100);
```

```c#
// Incorrect implementation
public class PaymentProcessor
{
    public void ProcessPayment(string paymentType, decimal amount)
    {
        if (paymentType == "credit_card")
        {
            // process credit card payment
        }
        else if (paymentType == "debit_card")
        {
            // process debit card payment
        }
        else if (paymentType == "bank_transfer")
        {
            // process bank transfer payment
        }
        else
        {
            throw new InvalidOperationException("Invalid payment type");
        }
    }
}
```
In the corrected implementation, the `PaymentProcessor` class processes a payment using the `IPaymentMethod` interface. This allows you to add new payment methods by creating a new class that implements the `IPaymentMethod` interface, without modifying the `PaymentProcessor` class. You can then use dependency injection to pass an instance of the desired payment method to the `PaymentProcessor` class, as in the following example:
```cs
// Corrected implementation
public interface IPaymentMethod
{
    void ProcessPayment(decimal amount);
}

public class CreditCardPayment : IPaymentMethod
{
    public void ProcessPayment(decimal amount)
    {
        // process credit card payment
    }
}

public class DebitCardPayment : IPaymentMethod
{
    public void ProcessPayment(decimal amount)
    {
        // process debit card payment
    }
}

public class BankTransferPayment : IPaymentMethod
{
    public void ProcessPayment(decimal amount)
    {
        // process bank transfer payment
    }
}

public class PaymentProcessor
{
    private IPaymentMethod paymentMethod;

    public PaymentProcessor(IPaymentMethod paymentMethod)
    {
        this.paymentMethod = paymentMethod;
    }

    public void ProcessPayment(decimal amount)
    {
        paymentMethod.ProcessPayment(amount);
    }
}
```
