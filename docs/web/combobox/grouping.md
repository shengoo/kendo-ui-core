---
title: Grouping
page_title: Kendo UI ComboBox Grouping
description: This document provides information how to configure grouping in Kendo UI ComboBox, DropDownList, AutoComplete and MultiSelect
position: 3
---

# Grouping

Kendo UI AutoComplete, ComboBox, DropDownList and MultiSelect support binding to a grouped [datasource](http://docs.telerik.com/kendo-ui/framework/datasource/overview) since Q1 2015 (2015.1.318).
This functionality allows to display data items categorized by a specific model field. For more details about the data source grouping functionality please refer to
the [group documentation](http://docs.telerik.com/kendo-ui/api/javascript/data/datasource#configuration-group).

## Kendo UI ComboBox with remote transport and grouped data source

```html
<div class="demo-section k-header">
    <h4>Customers</h4>
    <input id="customers" style="width: 400px" />
</div>

<script>
    $(document).ready(function() {
        $("#customers").kendoComboBox({
            dataTextField: "ContactName",
            dataValueField: "CustomerID",
            height: 200,
            dataSource: {
                type: "odata",
                transport: {
                    read: "http://demos.telerik.com/kendo-ui/service/Northwind.svc/Customers"
                },
                group: { field: "Country" } //group the data by 'Country' field
            }
        });
    });
</script>
```

## How to configure

In order to display grouped items in the widget, you will need to group the data source component using its
[group configuration](http://docs.telerik.com/kendo-ui/api/javascript/data/datasource#configuration-group). Once the group option is defined,
widget will **automatically** display the suggestion items grouped.

## How to customize

Widget exposes [groupTemplate](http://docs.telerik.com/kendo-ui/api/javascript/ui/combobox#configuration-groupTemplate) and
[fixedGroupedTemplate](http://docs.telerik.com/kendo-ui/api/javascript/ui/combobox#configuration-fixedGroupTemplate) templates that
allows to configure rendering of the group titles.

### Customize the inline group title

To customize the inline group title displayed next to the suggestion item in the popup element, you will need to use the [groupTemplate](http://docs.telerik.com/kendo-ui/api/javascript/ui/combobox#configuration-groupTemplate)
option. It is rendered in the absolute positioned, right aligned group element displayed in every first element of each new group.

Parameter passed to the template is the group title value.

#### Define a custom group template

```html
<div class="demo-section k-header">
    <h4>Customers</h4>
    <input id="customers" style="width: 400px" />
</div>

<script>
    $(document).ready(function() {
        $("#customers").kendoComboBox({
            height: 200,
            groupTemplate: "<strong>#:data#</strong>", //`data` is the title of the group
            dataTextField: "ContactName",
            dataValueField: "CustomerID",
            dataSource: {
                type: "odata",
                transport: {
                    read: "http://demos.telerik.com/kendo-ui/service/Northwind.svc/Customers"
                },
                group: { field: "Country" } //group the data by 'Country' field
            }
        });
    });
</script>
```

### Customize the fixed group header

To customize the group title displayed in the fixed group header positioned on top of the list, you will need to use the [fixedGroupTemplate](http://docs.telerik.com/kendo-ui/api/javascript/ui/combobox#configuration-fixedGroupTemplate)
option. It shows the group title of the current visible group. That means that the value is updated dynamically on the scroll position of the grouped list.

Parameter passed to the template is the group title value.

#### Define a custom fixed group template

```html
<div class="demo-section k-header">
    <h4>Customers</h4>
    <input id="customers" style="width: 400px" />
</div>

<script>
    $(document).ready(function() {
        $("#customers").kendoComboBox({
            height: 200,
            fixedGroupedTemplate: "<strong>#:data#</strong>", //`data` is the title of the group
            dataTextField: "ContactName",
            dataValueField: "CustomerID",
            dataSource: {
                type: "odata",
                transport: {
                    read: "http://demos.telerik.com/kendo-ui/service/Northwind.svc/Customers"
                },
                group: { field: "Country" } //group the data by 'Country' field
            }
        });
    });
</script>
```
