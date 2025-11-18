# Payment Approval API Story

## Purpose

This API helps managers quickly and accurately review and approve pending payments.

## Data Properties

* id – payment identifier
* amount – value
* currencyType – type of currency
* payee – entity to be paid
* invoice – invoice number to be paid
* comments – free-form notes
* requestor – entity/person requesting the payment
* reviewer – person reviewing the request for payment
* status – status of the record (pending, approved, denied, cancelled)
* dateDue – date the payment is due
* dateRequested – date the payment was requested
* dateReviewed – date the payment request was reviewed

## Resources

### home

Initial entry point for the API.

**Actions**

* showHome
* viewPayments

### payments

List of payment request records in the system.

**Actions**

* showHome
* viewPayments
* addPayment
* viewPayment
* viewFilteredPayments

### payment

Single payment request record.

**Actions**

* showHome
* viewPayments
* viewPayment
* updatePayment
* setPaymentStatus
* viewFilteredPayments

## Actions

* showHome

  * Input properties: none
  * Returns: home

* viewPayments

  * Input properties: none
  * Returns: payments

* addPayment

  * Input properties: id, amount, currencyType, payee, invoice, comments, requestor, status, dateDue, dateRequested (defaults to now)
  * Returns: payment

* updatePayment

  * Input properties: id, comments, status, dateDue, reviewer (optional), dateReviewed
  * Returns: payment

* viewPayment

  * Input properties: id
  * Returns: payment

* setPaymentStatus

  * Input properties: id, status, reviewer, dateReviewed
  * Returns: payment

* viewFilteredPayments

  * Input properties: status, dateDue, payee, requestor, reviewer (all optional)
  * Returns: payments

## Rules

* requiredAmount – Every payment must have an amount
* requiredCurrencyType – Every payment must specify a currency
* requiredPayee – Every payment must identify who receives the funds
* requiredRequestor – Every payment must identify who requested it
* requiredStatus – Every payment must have a status value
* requiredDateDue – Every payment must specify when it's due
* positiveAmount – Amount must be greater than zero
* validCurrencyType – Currency must be from an approved list (USD, EUR, etc.)
* validStatusValues – Status must be one of: pending, approved, denied, cancelled
* futureDateDue – Due date must be today or in the future
* reviewerRequiredForStatusChange – Changing status to approved/denied requires a reviewer
* dateReviewedRequiredWhenReviewed – If reviewer is set, dateReviewed must be set
* onlyPendingCanBeApproved – Only payments with status=pending can be approved
* noEditingAfterApproval – Approved or denied payments cannot be modified

## Validation Summary

Validation Summary: PASS

This API Story conforms to the Classic API Story Style and is ready for conversion to ALPS, OpenAPI, AsyncAPI, or prototype formats.

---

**Generated:** 2025-11-18  
**Domain:** Payment Approval  
**Version:** 1.0
