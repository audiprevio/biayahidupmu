![Group 1](https://github.com/audiprevio/week-7-audiprevio/assets/126348614/2a3787b5-607b-4968-8f6f-6f421eb5e494)

# [Biaya_Hidupmu - Financial Tracker that's for you, perhaps](https://biayahidupmu.netlify.app/)

### Note:

As of now Biaya_Hidupmu is only available in Bahasa Indonesia, you can use google translate feature on browsers to try to change the language.

## Project Overview

Biaya_Hidupmu (Your Cost of Living) is a free financial tracker application that helps users, especially Gen Z, manage their expenses effectively while giving them a good time (maybe). The application allows users to record their financial transactions and provides real-time insights into their total balance. The user-friendly interface and responsive design make it convenient for users to interact with the application.

## Functionality Details

### 1. Transaction Form

The application features a transaction form that allows users to input details for each transaction. The form includes the following fields:

- **Date**: Users can select the transaction date from a date picker.
- **Item**: Users can describe the transaction by providing a short description.
- **Nominal**: Users enter the transaction amount in Rupiah (Rp).
- **Tipe**: Users can select the transaction type from the dropdown, either "Cash In" or "Cash Out".


The backbone of the Event Listener - the button and listener:
```html
<form id="transactionForm">
  <!-- ... Other form elements ... -->
  <button type="submit">Catat Transaksi</button>
</form>
```
```TS
transactionForm?.addEventListener("submit", (event) => {
  event.preventDefault();
  // Retrieve form inputs and create a new transaction object
  // Add transaction card to the UI and save the transaction to LocalStorage
  // Update total balance after adding the new transaction
});
```

### 2. Displaying Total Balance
The application provides a section to display the total balance. The total balance is calculated by summing up all the "Cash In" transactions and subtracting the "Cash Out" transactions. The total balance is dynamically updated each time a new transaction is added or an existing transaction is deleted.

```HTML
<div id="totalBalanceContainer">
  <p id="totalBalance"></p>
  <p id="dynamicText"></p>
</div>
```

```TS
function displayTotalBalance(transactions: Transaction[]) {
  // Calculate total balance
  // Update totalBalanceElement with the new total balance
  
  // Add dynamic text based on the total balance
  // Use the dynamicTextElement to display messages based on the total balance
}

// Function to calculate the total balance
function calculateTotalBalance(transactions: Transaction[]): number {
  // Reduce the transactions to calculate the total balance
  return totalBalance;
}
```

### 3.Dynamic Text and Financial Status
Based on the total balance, the application dynamically generates a text element to indicate the user's financial status. The text element shows humorous and relatable messages based on the total balance range. For example, "Sultan" for very high balance, "Tjakep" for high balance, "GWS DAH" for very negative balance, and so on.
```HTML
<div id="totalBalanceContainer">
  <p id="totalBalance"></p>
  <p id="dynamicText"></p>
</div>
```

```TS
function displayTotalBalance(transactions: Transaction[]) {
function displayTotalBalance(transactions: Transaction[]) {
  // Calculate total balance
  const totalBalance = calculateTotalBalance(transactions);

  // Update totalBalanceElement with the new total balance
  const totalBalanceElement = document.getElementById("totalBalance");
  if (totalBalanceElement) {
    totalBalanceElement.innerText = `Saldo: Rp${totalBalance.toFixed(2)}`;
    
    // Change the text color of the total balance based on its value
    if (totalBalance < 0) {
      totalBalanceElement.style.color = "#cf0000"; // Red for negative balance
    } else if (totalBalance > 0.1) {
      totalBalanceElement.style.color = "#0016c2"; // Blue for positive balance greater than 0.1
    } else {
      totalBalanceElement.style.color = "initial"; // Reset to default color if balance is close to 0
    }
  }

  // Add dynamic text based on the total balance
  const dynamicTextElement = document.getElementById("dynamicText");
  if (dynamicTextElement) {
    if (totalBalance == 0) {
      dynamicTextElement.innerHTML = "<b>Status Keuanganmu: Belum Ada Data</b>";
    } else if (totalBalance > 10000000000) {
      dynamicTextElement.innerHTML = "<b>Status Keuanganmu:</b> <b class='positiveValue'>Sultan</b>";
    } else if (totalBalance > 1000000000) {
      dynamicTextElement.innerHTML = "<b>Status Keuanganmu:</b> <b class='positiveValue'>Ampun Gan</b>";
    } else if (totalBalance > 100000000) {
      dynamicTextElement.innerHTML = "<b>Status Keuanganmu:</b> <b class='positiveValue'>Gelo</b>";
// etc...
}
```

### 4. Transaction Cards
The application displays transaction details as cards on the page. Each card contains the transaction date, item description, transaction amount, and type. Transaction cards are color-coded based on the transaction type. "Cash In" transactions have a blue text, while "Cash Out" transactions have a red text.
```html
<div class="transaction-cards" id="transactionCards">
  <!-- Transaction cards will be added here dynamically using TypeScript -->
</div>
```

```TS
function addTransactionCard(transaction: Transaction) {
  // Create a new transaction card element
  // Set the card color based on the transaction type
  
  // Use the transaction data to fill in the card content
  
  // Add a delete button and attach a delete event listener
  
  // Add animation to the card when added to the UI

  // Append the card to the transactionCards element
}
```

### 5. Deleting Transactions
Users can delete a transaction by clicking the "Buang" button on the respective transaction card. When a transaction is deleted, the total balance is automatically updated, and the transaction card is removed from the display with a rotation animation.

```html
<div class="transaction-card">
  <!-- ... Transaction card content ... -->
  <button class="delete-btn">Buang</button>
</div>
```


```TS
function addTransactionCard(transaction: Transaction) {
  // ... Other code ...
  
  // Add a delete button and attach a delete event listener
  const deleteBtn = card.querySelector(".delete-btn") as HTMLButtonElement;
  deleteBtn.addEventListener("click", () => {
    // Delete the transaction from LocalStorage
    // Add rotation animation when deleting a transaction card
    // Update total balance after deleting the transaction
    // Remove the card from the UI after the animation is completed
  });
  
  // ... Other code ...
}
```

### 6. Dark Mode Toggle
Biaya HidupMu provides a default mode toggle button labeled "Klik untuk Ubah Mode." Users can click this button to switch between standard and focus modes. The application uses LocalStorage to remember the user's preferred theme even after the browser is closed or first launched.
```html
<button id="themeToggle" class="toggleFocus">
  Klik untuk Ubah Mode
</button>
```

```TS
const themeToggle = document.getElementById("themeToggle");

if (themeToggle) {
  themeToggle.addEventListener("click", () => {
    // Toggle dark mode by adding or removing the 'dark-mode' class on the body element
    // Toggle the button text based on the current theme
    // Save the theme preference to LocalStorage
  });
} else {
  console.error("themeToggle element not found!");
}

function setTheme(isDarkMode: boolean) {
  // Set the theme based on the isDarkMode value
}
```
### 7. DOM Manipulation in Summary

The Biaya_HidupMu application utilizes TypeScript to manipulate the Document Object Model (DOM) and handle various user interactions. The key functionalities involving DOM manipulation are as follows:

1. **Creating and Appending Transaction Cards:** The application dynamically creates and appends transaction cards based on user input. Each transaction card represents a financial transaction and displays details such as date, item, amount, and transaction type. Transaction cards are added to the page as div elements and are styled based on their transaction type.

2. **Updating Total Balance:** The total balance is updated in real-time as new transactions are added or existing ones are deleted. The application calculates the total balance by summing up the cash-in amounts and subtracting the cash-out amounts. The updated balance is then displayed on the page.

3. **Color-Coding of Transaction Cards:** Transaction cards are color-coded based on their transaction type. Cash-out transactions have a red background, while cash-in transactions have a blue background. The text color is adjusted accordingly for better visibility.

4. **Animation Effects:** The application applies animation effects to both transaction cards and total balance updates. When a new transaction card is added, it receives a bounce animation effect, making the interface more interactive and visually appealing. Additionally, when a transaction card is deleted, it rotates and scales down, creating a smooth removal animation.

5. **Dynamic Text Messages:** The application displays dynamic text messages based on the total balance range. These messages provide users with humorous and relatable feedback on their financial status. The messages change depending on whether the balance is positive, negative, or close to zero.

The TypeScript code handles various aspects of the application, such as event listeners for form submissions and interaction with the LocalStorage API to save and retrieve transactions. This ensures that the user's financial data is preserved even after reloading the page.

In conclusion, Biaya HidupMu offers an interactive and responsive financial tracking experience, allowing users to effectively manage their expenses. The combination of HTML, CSS, and TypeScript enables the application to provide a seamless and enjoyable user experience.


## Installation

1. Clone the repository to your local machine using `git clone <repository-url>`.
2. Change into the project directory using `cd <project-folder>`.

## Getting Started

1. Install dependencies by running `pnpm install`.
2. Run the TypeScript compiler in watch mode using `pnpm run watch`.

## How to Use

1. Open the `index.html` file in your browser.
2. Click the "Klik untuk Ubah Mode" button to toggle between standard and focus mode.
3. To add a new transaction, fill in the date, item, amount, and type (Cash In or Cash Out) in the form fields and click "Catat Transaksi".
4. Your transaction will be displayed as a card on the page.
5. To delete a transaction, click the "Buang" button on the respective transaction card.

## Contributing

Contributions are welcome! If you find any bugs or want to add new features, feel free to submit a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Credits

This project was built with love by Audi Previo. Special thanks to RevoU peeps, OpenAi for GPT coding ideas, and the world for giving me the problems that I want to solve for their valuable contributions.
