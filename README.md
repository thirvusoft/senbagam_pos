<div align="center">
    <img src="https://frappecloud.com/files/pos.png" height="128">
    <h2>POS AWESOME</h2>
</div>

#### An open-source Point of Sale for [Erpnext](https://github.com/frappe/erpnext) using [Vue.js](https://github.com/vuejs/vue) and [Vuetify](https://github.com/vuetifyjs/vuetify)

---
### core code changes for serial no selct without batch no selection 
stock_controller.py line 88 - 93 command<br>
serial_no.py - line 390 - 394 command<br>
invoice.vue - line 1250 - 1261,481 - 505 command<br>
 
### Main Features

1. Supports Erpnext Version 12 & 13
2. User friendly and provides a good user experience and speed of use
3. The cashier has the option of either using list view or card view during sales transactions. Card view shows the images of the items
4. Supports enqueue invoice submission after printing the receipt for faster processing
5. Supports batch & serial numbering
6. Supports batch based pricing
7. Supports UOM specific barcode and pricing
8. Supports sales of scale (weighted) products
9. Ability to make returns from POS
10. Supports Making returns for either cash or customer credit
11. Supports using customer credit note for payment
12. Supports credit sales
13. Allows user to choose a due date for credit sales
14. Supports customer loyalty points
15. Shortcuts keys
16. Supports Customer Discount
17. Supports POS Offers
18. Auto apply batches for bundle items
19. Search and add items by Serial Number
20. Create Sales Order from POS directly
21. Supports template items with variants
22. Supports multiple languages
23. Supports Mpesa mobile payment
24. POS Coupons
25. Supports Referral Code
26. Supports Customer and Customer Group price list
27. Supports Sales Person
28. Supports Delivery Charges

---

### How to Install

#### Frappe Cloud:

One-click installing available if you are hosting on FC from [here](https://frappecloud.com/marketplace/apps/posawesome)

#### Self Hosting:

1. `bench get-app https://github.com/yrestom/POS-Awesome.git`
2. `bench setup requirements`
3. `bench build --app posawesome`
4. `bench restart`
5. `bench --site [your.site.name] install-app posawesome`
6. `bench --site [your.site.name] migrate`

---

### Support

#### Frappe Cloud:

If you are hosting on FC premium support is available [here](https://frappecloud.com/marketplace/apps/posawesome)

#### Self Hosting:

If you need premium support it is available [here](https://forms.clickup.com/2191574/f/22w6p-14180/8J92BNHRMKG5ZW2EPF)

#### Community Support:

Available in GitHub [discussions](https://github.com/yrestom/POS-Awesome/discussions)

---

### New Features and Bug report:

Please Create Github Issue from [here](https://github.com/yrestom/POS-Awesome/issues/new/choose) after checking the existing issues, and for paid features you can submit this [form](https://forms.clickup.com/2191574/f/22w6p-14740/NK7DUHU0CPM3HVXVDC)

---

### How To Use:

[POS Awesome Wiki](https://github.com/yrestom/POS-Awesome/wiki)

---

### Shortcuts:

- `CTRL or CMD + S` open payments
- `CTRL or CMD + X` submit payments
- `CTRL or CMD + D` remove first item from the top
- `CTRL or CMD + A` expand first item from the top
- `CTRL or CMD + E` focus on discount field

---

### Dependencies:

- [Frappe](https://github.com/frappe/frappe)
- [Erpnext](https://github.com/frappe/erpnext)
- [Vue.js](https://github.com/vuejs/vue)
- [Vuetify.js](https://github.com/vuetifyjs/vuetify)

---

### Contributing

Will using for this the same guidelines from Erpnext

1. [Issue Guidelines](https://github.com/frappe/erpnext/wiki/Issue-Guidelines)
2. [Pull Request Requirements](https://github.com/frappe/erpnext/wiki/Contribution-Guidelines)

---

### License

GNU/General Public License (see [license.txt](https://github.com/yrestom/POS-Awesome/blob/master/license.txt))

The POS Awesome code is licensed as GNU General Public License (v3)
