# Bank System Core (Smalltalk/Pharo)

## Overview
This project implements a banking core system using **Smalltalk (Pharo)**, adhering to strict **Object-Oriented Programming (OOP)** paradigms.

The goal was to design a polymorphic system where different account types handle transactions according to their specific business rules, utilizing inheritance and dynamic binding.

## Architecture & Class Hierarchy
The system is built around a central `Banco` class that manages a collection of abstract and concrete accounts.

### Class Structure
* **`Banco`**: Manages the lifecycle of accounts and aggregated metrics (total balance per client, debt analysis).
* **`Cuenta` (Abstract)**: Defines the common protocol (`depositar`, `extraer`, `saldo`).
  * **`CajaDeAhorro`**: Subclass that enforces a strict "no overdraft" rule. Withdrawals are rejected if funds are insufficient.
  * **`CuentaCorriente`**: Subclass that allows overdrafts up to a pre-defined limit (`limiteDescubierto`).

## Key OOP Concepts Applied
* **Polymorphism:** The method `extraerMonto: unMonto` is polymorphic.
    * In `CajaDeAhorro`, it checks `saldo >= unMonto`.
    * In `CuentaCorriente`, it checks against the overdraft limit.
    * The `Banco` class treats all accounts uniformly without needing to know their specific implementation.
  **Inheritance:** Common attributes (`numeroCuenta`, `dniTitular`, `saldo`) are defined in the parent class `Cuenta` to avoid code duplication.
* **Encapsulation:** All internal state is protected and accessed only through messages.
