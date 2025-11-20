graph TD

    %% 01. INITIAL ONBOARDING & VERIFICATION
    subgraph 01_INITIAL_ONBOARDING
        A[Start: Family Application Received] --> B{Mandatory: Legal Verification Document?}
        B -- NO --> Z[Reject: Cannot Proceed]
        B -- YES --> C[Verify Family Size and Legal Status - Govt Document]
        C --> D[System Collects All Member Data and Health Background]
        D --> E[System Generates Unique Card Code NE-HOSP-00XX]
        E --> F[One-time Fee Payment 30000 IQD]
        F --> G[Family Sets Password]
        G --> H[System Generates QR or Barcode]
        H --> I[Account Created and Inactive]
    end

    %% 02. MONTHLY ACTIVATION & FINANCIAL SPLIT
    subgraph 02_MONTHLY_ACTIVATION
        I --> J{Access Activation Portal with Card Code and Password}
        J --> K{Choose Tier: Basic / Extend / Premium}
        K --> L[Monthly Fee Payment 30000 IQD Confirmed]
        L --> M[Financial Split Logic]
        M --> N[Debit: Hospital Fee Revenue]
        M --> O[Credit: Stored Balance for Future Liability]
        O --> P{Check Stored Balance Max Cap?}
        P -- OVER CAP --> Q[Apply Balance Cap and Notify User]
        P -- UNDER CAP --> R[Update Stored Balance]
        N --> S[Update Account Status and Benefits: Free Visits and SDUs]
        S --> T{Check Loyalty Consistency?}
        T -- YES --> U[Apply 3 Percent Loyalty Bonus]
        T -- NO --> U[Reset Strike or Loyalty]
        U --> V[End: Card Status Activated for 30-Day Period]
    end

    %% 03. SERVICE USAGE & BENEFIT LOGIC
    subgraph 03_SERVICE_USAGE
        V --> W[Member Seeks Service]
        W --> X{Service Type?}
        X -- Doctor Consultation --> Y{Check Pooled Free Visits Left?}
        Y -- YES --> Z1[Deduct 1 Free Visit from Pool]
        Y -- NO --> Z2[Bill Full Consultation Fee from Balance or Payment]
        X -- Basic Tier Service --> A1[Apply Tier Discount and Loyalty Bonus]
        X -- Non-Tier Service --> B1{Family Opts to Use SDU?}
        B1 -- YES --> C1[Deduct 1 SDU]
        C1 --> D1[Apply Tier Discount via SDU and Loyalty Bonus]
        B1 -- NO --> E1[Bill Full Price from Balance or Payment]
        Z1 --> F1[Record Transaction and Audit Trail]
        Z2 --> F1
        A1 --> F1
        D1 --> F1
        E1 --> F1
        F1 --> G1[Update Account: Balance, History, Free Visits, SDUs]
    end
