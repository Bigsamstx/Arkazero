# ArkaZero 🛡️ | The Self-Repaying Loan Simulator

> **"Don't fear debt. Make it pay you back."**

### 🏆 Submission for Arkadiko x Stacks Ecosystem Bounty

**ArkaZero** is a DeFi utility dashboard that helps users visualize and execute "Self-Repaying Loans." By calculating the delta between **Vault Debt Interest** and **Farming Yield**, ArkaZero proves to users that they can borrow USDA against their STX and use the yield to automatically pay off their loan over time.

---

## 🔗 Live Demo
**Try the app here:** [INSERT YOUR WEBSITE LINK HERE]

---

## 📉 The Problem
New users are often terrified of taking on debt in DeFi. They see "Liquidation Risk" and "Interest Rates" and get scared away. They lack the tools to model complex strategies where **Asset Yield > Borrow Cost**.

## 🚀 The Solution
**ArkaZero** provides a "Time-to-Freedom" visualization.
1.  **Simulate:** Input Collateral (STX) and desired LTV.
2.  **Strategize:** Select a Farming APY (e.g., STX-USDA LP).
3.  **Visualize:** The dashboard generates a real-time graph showing exactly **when** the yield will fully pay off the debt (e.g., *"Debt Free in 1.4 Years"*).

---

## 🛠️ Tech Stack

* **Frontend:** Vanilla JS + HTML5 (Lightweight, no build step required).
* **Styling:** Tailwind CSS (via CDN for rapid prototyping).
* **Icons:** Lucide-React.
* **Blockchain Logic:** Clarity (Smart Contract concepts for auto-repayment).

---

## ⚡ Quick Start (Run Locally)

This project is built as a lightweight "Vibecode" prototype. You do not need `npm install` to view the UI.

1.  **Clone or Download** this repository.
2.  Locate `arkazero.html`.
3.  **Double-click** to open it in your browser (Chrome/Brave recommended).
4.  Click **"Connect Wallet"** to simulate the Stacks authentication flow.
5.  Adjust the **APY Slider** to see the "Time to Freedom" update in real-time.

---

## 🧠 Smart Contract Logic (Concept)

ArkaZero is powered by an automation concept called `harvest-and-repay`. The following Clarity snippet demonstrates how the protocol would atomically claim farming rewards, swap them to USDA, and pay down the user's vault debt.

```clarity
;; ArkaZero Helper: Auto-Repay from Farm Yield
;; Contract: arkazero-automation.clar

(define-public (harvest-and-repay (vault-id uint))
    (begin
        ;; 1. Claim Rewards from Arkadiko Farm (DIKO)
        (let ((rewards (contract-call? 'ST2...arkadiko-farm-v1 claim-rewards)))
        
        ;; 2. Swap Rewards (DIKO -> USDA)
        ;; Uses Arkadiko Swap to convert volatile yield into stable debt repayment
        (let ((usda-gained (contract-call? 'ST2...arkadiko-swap swap-x-for-y rewards ...)))
        
        ;; 3. Repay Vault Debt using the swapped USDA
        ;; Reduces risk and increases health factor automatically
        (contract-call? 'ST2...arkadiko-vaults repay-usda-for-vault vault-id usda-gained)
        )
    )
)
