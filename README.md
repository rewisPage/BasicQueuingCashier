# 02 Laboratory Exercise 1: Basic Queuing Cashier

A dual-window Windows Forms application created in C# that simulates a real-time queue management system for a cashier service. The program allows customers to generate unique queue numbers while enabling a cashier station to monitor and serve incoming queue tokens in real time.

<img width="1032" height="441" alt="image" src="https://github.com/user-attachments/assets/7e351940-b276-4d27-84b3-6bb6f0323e6c" />


---

## Features

* **Auto-Generating Queue Numbers:** Generates incremental queue numbers starting from `P - 10001` upon button press.
* **Dual-Form Architecture:**
  * **`QueuingForm`:** Customer-facing interface to generate and view the latest assigned queue ticket.
  * **`CashierWindowQueueForm`:** Cashier-facing terminal displaying the active waiting list in FIFO (First-In, First-Out) sequence[cite: 1, 2].
* **Real-Time Sync (Challenge Exercise):** Implements a Windows Forms `Timer` running on a 1-second interval to automatically update the queue display without requiring manual refreshes.
* **Queue Servicing:** Features a `Next` action button to dequeue/serve the front student in the queue.
* **Dark Mode Interface:** Modern, high-contrast dark theme styling across all controls and forms.

---

## Technical Overview

* **Language:** C#
* **Framework:** .NET Framework (Windows Forms)[cite: 1, 2]
* **Key Data Structure:** `System.Collections.Generic.Queue<string>`
* **Display Mechanism:** `System.Windows.Forms.ListView`

---

## Class & Form Architecture

### 1. `CashierClass`
Acts as the central data model and state holder:
* `x` (`private int`): Counter starting at `10000`.
* `CashierQueue` (`public static Queue<string>`): Generic queue structure storing pending tokens in order.
* `getNumberInQueue` (`public static string`): Retains the latest generated token string.
* `CashierGeneratedNumber(string prefix)`: Increments `x` and appends it to the prefix (e.g., `P - 10001`).

### 2. `QueuingForm`
Contains the customer entry point:
* **`btnCashier`**: Generates a new sequence number using `CashierGeneratedNumber()`, displays it in `lblQueue`, and calls `CashierQueue.Enqueue()`.
* **`lblQueue`**: Displays the active issued number.

### 3. `CashierWindowQueueForm`
Contains the queue administration controls:
* **`listCashierQueue` (`ListView`)**: Displays the active list of tickets.
* **`btnRefresh`**: Manually calls `DisplayCashierQueue()` to re-render all elements from `CashierQueue`.
* **`btnNext`**: Calls `CashierQueue.Dequeue()` to serve and remove the front token.
* **`timer` (`Timer`)**: Ticks every 1000ms to keep the list refreshed automatically.

---

## Setup & Execution

1. Clone or download this project folder.
2. Open the solution file (`.sln`) in **Visual Studio 2015 or higher**.
3. Ensure the project structure contains:
   * `QueuingForm.cs` & `QueuingForm.Designer.cs`
   * `CashierWindowQueueForm.cs` & `CashierWindowQueueForm.Designer.cs`
   * `CashierClass.cs`
   * `Program.cs`
4. Build the solution (`Ctrl + Shift + B`).
5. Press `F5` to run the application.
