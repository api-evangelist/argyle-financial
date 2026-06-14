# Argyle Financial — GraphQL Schema

Argyle is a consumer-permissioned employment and income data platform. Its REST API surfaces payroll-direct verification of employment (VOE), verification of income (VOI), combined VOIE, banking-direct verification of assets (VOA/VOAI), and document-processing flows. This conceptual GraphQL schema models the same domain — identity, employment, paystubs, shifts, gigs, banking, verifications, documents, and platform administration — as a unified graph for teams that prefer query-driven data access over resource-oriented REST calls.

## Domain Coverage

| Domain | Key Types |
|---|---|
| Users & Tokens | `ArgyleUser`, `UserToken` |
| Identity | `Identity`, `Address` |
| Accounts & Items | `Account`, `Item`, `ItemFilter` |
| Employment | `Employment` |
| Paystubs & Earnings | `Paystub`, `Earning`, `Deduction`, `TaxWithholding`, `PaystubConnection` |
| Shifts | `Shift`, `ShiftConnection`, `GeoPoint` |
| Gigs | `Gig`, `GigConnection` |
| Vehicles | `Vehicle` |
| Ratings | `Rating`, `RatingCategory` |
| Payroll Documents | `PayrollDocument` |
| Banking | `BankAccount`, `FinancialInstitution`, `DepositDestination`, `Transaction`, `TransactionConnection` |
| Verifications | `Verification`, `IncomeSnapshot`, `AssetSnapshot`, `AssetBreakdown`, `GseEligibility` |
| Reports | `Report`, `ReportSummary` |
| Invites | `Invite` |
| Uploads | `UserUpload` |
| Forms | `UserForm` |
| Receipts | `Receipt` |
| Pagination | `PageInfo` |
| Inputs | `CreateUserInput`, `UpdateUserInput`, `CreateItemFilterInput`, `UpdateItemFilterInput`, `CreateInviteInput`, `OrderVerificationInput`, `GenerateReportInput`, `InitiateUploadInput`, `UpdateDepositDestinationInput` |
| Enums | `EmploymentStatus`, `EmploymentType`, `PayCycle`, `GigType`, `GigStatus`, `DocumentType`, `DocumentStatus`, `VerificationStatus`, `VerificationType`, `AccountStatus`, `InviteStatus`, `InviteChannel`, `EarningType`, `DeductionType`, `ReportStatus`, `ReportFormat`, `ShiftStatus`, `BankAccountType`, `InstitutionType`, `UploadStatus`, `RatingSource`, `FormResponseStatus` |

## Schema File

`argyle-financial-schema.graphql`

## Representative Queries

### Fetch a user with their active employments and last three paystubs

```graphql
query UserVerificationProfile($userId: UUID!) {
  user(id: $userId) {
    id
    externalId
    identity {
      fullName
      email
      address {
        fullAddress
      }
    }
    employments(status: ACTIVE) {
      employerName
      jobTitle
      type
      hireDate
      payCycle
    }
    paystubs(limit: 3) {
      nodes {
        payDate
        grossPay
        netPay
        currency
        ytdGross
        earnings {
          type
          amount
        }
        deductions {
          type
          amount
        }
      }
    }
  }
}
```

### Pull gig income across multiple platforms for a date range

```graphql
query GigIncomeSummary($userId: UUID!, $from: Date!, $to: Date!) {
  gigs(userId: $userId, fromDate: $from, toDate: $to, limit: 500) {
    totalCount
    nodes {
      platform
      type
      startTime
      durationMinutes
      distanceMiles
      basePay
      tips
      bonuses
      totalPay
      currency
    }
  }
}
```

### Check verification status and GSE eligibility

```graphql
query VerificationStatus($verificationId: UUID!) {
  verification(id: $verificationId) {
    id
    type
    status
    completedAt
    incomeData {
      annualizedGross
      monthlyGross
      currency
      baseIncome
      variableIncome
    }
    gseEligibility {
      fannieMaeDay1Certainty
      freddieMacAim
      representationsAndWarranties
      certificationDate
    }
    report {
      status
      format
      downloadUrl
    }
  }
}
```

### Order a VOIE verification

```graphql
mutation OrderVOIE($userId: UUID!) {
  orderVerification(input: {
    userId: $userId
    type: VOIE
  }) {
    id
    status
    requestedAt
    expiresAt
  }
}
```

### List bank accounts with current balances

```graphql
query BankAssets($userId: UUID!) {
  bankAccounts(userId: $userId) {
    id
    accountType
    accountNumberLastFour
    currentBalance
    availableBalance
    currency
    institution {
      name
      type
    }
  }
}
```

## Enum Summary

- **EmploymentStatus**: `ACTIVE`, `TERMINATED`, `ON_LEAVE`, `PROBATIONARY`, `SEASONAL`, `UNKNOWN`
- **EmploymentType**: `FULL_TIME`, `PART_TIME`, `CONTRACT`, `SEASONAL`, `GIG`, `TEMPORARY`, `INTERNSHIP`
- **PayCycle**: `WEEKLY`, `BIWEEKLY`, `SEMI_MONTHLY`, `MONTHLY`, `DAILY`, `IRREGULAR`
- **VerificationType**: `VOE`, `VOI`, `VOIE`, `VOA`, `VOAI`
- **VerificationStatus**: `PENDING`, `IN_PROGRESS`, `COMPLETED`, `FAILED`, `EXPIRED`, `CANCELLED`
- **GigType**: `RIDE`, `DELIVERY`, `ERRAND`, `TASK`, `FREELANCE`, `RENTAL`, `OTHER`
- **DocumentType**: `W2`, `FORM_1099`, `FORM_1099_NEC`, `FORM_1099_K`, `PAYSTUB`, `BANK_STATEMENT`, `TAX_RETURN`, `OFFER_LETTER`, `OTHER`
- **EarningType**: `REGULAR`, `OVERTIME`, `BONUS`, `COMMISSION`, `TIP`, `REIMBURSEMENT`, `SEVERANCE`, `VACATION_PAYOUT`, `HOLIDAY`, `OTHER`
- **DeductionType**: `FEDERAL_TAX`, `STATE_TAX`, `LOCAL_TAX`, `SOCIAL_SECURITY`, `MEDICARE`, `HEALTH_INSURANCE`, `DENTAL_INSURANCE`, `VISION_INSURANCE`, `RETIREMENT_401K`, `FSA`, `HSA`, `LIFE_INSURANCE`, `GARNISHMENT`, `OTHER`
- **BankAccountType**: `CHECKING`, `SAVINGS`, `MONEY_MARKET`, `OTHER`
- **InviteChannel**: `EMAIL`, `SMS`
- **ReportFormat**: `PDF`, `JSON`

## Notes

- This is a conceptual schema derived from Argyle's public REST API surface. Argyle does not currently expose a native GraphQL endpoint.
- All monetary amounts use `Decimal` scalar to avoid floating-point precision issues; callers should treat them as strings when serializing.
- `PaystubConnection`, `ShiftConnection`, `GigConnection`, and `TransactionConnection` follow the Relay cursor-connection pattern with `PageInfo` for pagination.
- The `GseEligibility` type models Fannie Mae Day 1 Certainty and Freddie Mac AIM eligibility flags returned in Argyle's verification reports.
- `IncomeSnapshot` annualizes income from the paystub set used in a verification; `calculationBasis` indicates whether the figure is derived from YTD, trailing-twelve-months, or rolling-average logic.
