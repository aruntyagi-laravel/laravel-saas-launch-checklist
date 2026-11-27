# Laravel SaaS Launch Checklist

A practical checklist for founders and developers launching a SaaS product on Laravel. It's based on real MVP builds and rescues — use it to scope phase 1 and to catch the things that usually get missed before go-live.

Suggestions and pull requests are welcome.

---

## 1. Scope (before writing code)

- [ ] One core workflow customers will pay for, written down end to end
- [ ] A "not in phase 1" list shared with everyone
- [ ] Target customer size known (affects tenancy and roles)
- [ ] Success metric for the first 90 days

## 2. Tenancy

- [ ] Decision made: single database + `tenant_id` vs database-per-tenant
- [ ] Global scope (or package) applied to every tenant-owned model
- [ ] Tests that try to read another tenant's data — and fail
- [ ] Queued jobs carry the tenant ID and re-initialise context
- [ ] Cache keys and file paths prefixed per tenant

## 3. Accounts, teams and roles

- [ ] Email verification and password reset
- [ ] Owner can invite members; invites expire
- [ ] Roles kept simple in phase 1 (owner / admin / member)
- [ ] Authorization in Policies, not only in the UI
- [ ] Audit log for billing and permission changes

## 4. Billing

- [ ] Plans, trial length and grace period decided
- [ ] Laravel Cashier (Stripe) or Razorpay integration
- [ ] Local `subscriptions` table is the source of truth for access
- [ ] Webhooks: signature verification, idempotency, queued processing
- [ ] Upgrade / downgrade / cancellation rules tested
- [ ] Invoices with tax details (GST/VAT) where needed

## 5. Plan limits

- [ ] Limits (seats, projects, API calls) defined per plan
- [ ] Enforced in middleware/policies, with clear upgrade prompts

## 6. Admin panel

- [ ] Internal panel (e.g. Filament) to view customers, subscriptions and usage
- [ ] Impersonation for support, logged and restricted
- [ ] Ability to extend trials and issue refunds without touching the database

## 7. Background work

- [ ] Redis + Horizon (or SQS) for queues
- [ ] Emails, imports, exports and reports run as jobs
- [ ] `retry_after` > job `timeout`; jobs are idempotent
- [ ] Failed-job alerts go to a real person

## 8. Security

- [ ] Rate limiting on login, signup, password reset and API
- [ ] 2FA available (at least for owners)
- [ ] File uploads validated and stored privately where needed
- [ ] `composer audit` clean; dependencies up to date
- [ ] Secrets only in environment variables

## 9. Go-live

- [ ] Staging environment that mirrors production
- [ ] Automated backups **and** a tested restore
- [ ] Error tracking, uptime monitoring and log rotation
- [ ] Transactional email domain verified (SPF, DKIM, DMARC)
- [ ] Terms of service, privacy policy, data processing terms
- [ ] Analytics and Search Console on the marketing site

## 10. First 30 days after launch

- [ ] Weekly review of signups, activation and churn reasons
- [ ] Support inbox monitored daily
- [ ] Laravel and PHP version upgrade plan documented

---

## Related reading

- [Laravel production checklist](https://github.com/aruntyagi-laravel/laravel-production-checklist)
- [What to build in phase 1 of a SaaS MVP](https://aruntyagilaravel.substack.com/p/what-to-build-in-phase-1-of-a-saas)
- [Multi-tenant Laravel: single database or database-per-tenant?](https://aruntyagi-laravel.hashnode.dev/multi-tenant-laravel-single-database-or-database-per-tenant-how-i-decide)
- [Build SaaS with Laravel: complete guide (2026)](https://aruntyagi.com/blog/build-saas-with-laravel-complete-guide-2026)
- [Laravel SaaS MVP cost in India](https://aruntyagi.com/blog/laravel-saas-mvp-cost-india-2026)

## Author

Maintained by **Arun Tyagi**, freelance Laravel developer in Noida, India — [aruntyagi.com](https://aruntyagi.com).
Building a SaaS? See [Laravel SaaS development](https://aruntyagi.com/laravel-saas-development).

## License

MIT
