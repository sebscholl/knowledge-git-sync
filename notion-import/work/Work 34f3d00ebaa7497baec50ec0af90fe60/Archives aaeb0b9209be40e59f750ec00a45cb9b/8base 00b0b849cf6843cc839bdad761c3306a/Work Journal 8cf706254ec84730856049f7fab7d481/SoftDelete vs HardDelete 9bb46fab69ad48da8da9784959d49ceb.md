# SoftDelete vs HardDelete

Created: January 12, 2020 12:35 PM

(Strategy 1) - Table Level Settings

A table has a setting for Hard Delete Vs Soft Delete. At any point, the setting can be toggled on or off, however, changing the setting will result in irrecoverable data loss (destroy all deleted records).

We would restrict this to ONLY the *Administrator* role, as well as add some custom documentation about how the *Administrator* has specific special abilities... like destroying records.

If a table is set to soft delete, there will be a toggle in the Data Viewer that says "See Deleted Records". ANY ONE THAT HAS ACCESS TO THE ADMIN DATA VIEWER WILL HAVE ACCESS TO DESTROYING RECORDS ON A SOFT DELETE TABLE. However, this functionality will NOT be available via the API, for now.

(Strategy 2) - Delete vs. Destroy Mutations

We add a recordDelete and recordDestroy mutation to the API. Delete soft deletes the record, Destroy eliminates the record. In the roles and permissions section, we add a drop down to the Delete action column instead of a checkbox with the following options.

**Delete:**

- Off
- Soft Delete
- Hard Delete

Anyone with the permission, app user or team member, will be able to manage records accordingly via the API.

There will be a toggle in the Data Viewer that says "See Deleted Records". Only users with Hard Delete permission will see this toggle, and then be able to restore records. However, this functionality will NOT be available via the API, for now. Additionally, ANY MANDATORY RELATIONSHIPS WILL CASCADE THE DELETE/DESTROY OPERATION RUN ON THE PARENT WHEN THE FORCE FLAG IS SPECIFIED. 

(Strategy 3) - Destroy flag

Add a mutation argument top the recordDelete operation that is false by default, though when true runs a **destroy operation against the record and cascades to any mandatory relationships.**

There will be a toggle in the Data Viewer that says "See Deleted Records". Only *Administrators* with the table Delete permission will be able to view and hard delete records.

```jsx
mutation {
  somethingDelete(id: "lalalalala", destroy: true) {
    success
  }
}
```