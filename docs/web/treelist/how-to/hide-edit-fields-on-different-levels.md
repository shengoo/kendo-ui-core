---
title: Hide edit fields on different levels
page_title: Hide edit fields on different levels
description: Hide edit fields on different levels
---

# Hide edit fields on different levels

The example below demonstrates how to hide editors for different columns on different levels.

#### Example:

```html
    <div id="treelist"></div>

    <style>
      .non-editable {
            visibility: hidden;
        }
    </style>

    <script>
      $(document).ready(function () {
        var crudServiceBaseUrl = "http://demos.telerik.com/kendo-ui/service";

        var dataSource = new kendo.data.TreeListDataSource({
          transport: {
            read:  {
              url: crudServiceBaseUrl + "/EmployeeDirectory/All",
              dataType: "jsonp"
            },
            update: {
              url: crudServiceBaseUrl + "/EmployeeDirectory/Update",
              dataType: "jsonp"
            },
            destroy: {
              url: crudServiceBaseUrl + "/EmployeeDirectory/Destroy",
              dataType: "jsonp"
            },
            create: {
              url: crudServiceBaseUrl + "/EmployeeDirectory/Create",
              dataType: "jsonp"
            },
            parameterMap: function(options, operation) {
              if (operation !== "read" && options.models) {
                return {models: kendo.stringify(options.models)};
              }
            }
          },
          batch: true,
          schema: {
            model: {
              id: "EmployeeId",
              fields: {
                EmployeeId: { type: "number", editable: false, nullable: false },
                parentId: { field: "ReportsTo", nullable: true },
                FirstName: { validation: { required: true } },
                LastName: { validation: { required: true } },
                HireDate: { type: "date" },
                Phone: { type: "string" },
                HireDate: { type: "date" },
                BirthDate: { type: "date" },
                Extension: { type: "number", validation: { min: 0, required: true } },
                Position: { type: "string" }
              },
              expanded: true
            }
          }
        });

        var hideEditorsForLevel = {
          0: ["Position", "HireDate", "Phone", "Extension"],
          1: ["Position"]
        };

        $("#treelist").kendoTreeList({
          dataSource: dataSource,
          toolbar: [ "create" ],
          editable: true,
          height: 540,
          edit: function(e) {
            // determine level from model
            var level = this.dataSource.level(e.model);

            // hide content in non-editable cells
            $(e.container).closest("tr")
              .find("[data-bind]").filter(function() {
                  var name = $(this).attr("name");
                  return $.inArray(name, hideEditorsForLevel[level]) > -1;
              }).closest("td>*").addClass("non-editable");
          },
          columns: [
            { field: "FirstName", expandable: true, title: "First Name", width: 220 },
            { field: "LastName", title: "Last Name", width: 100 },
            { field: "Position" },
            { field: "HireDate", title: "Hire Date", format: "{0:MMMM d, yyyy}" },
            { field: "Phone", title: "Phone" },
            { field: "Extension", title: "Ext", format: "{0:#}" },
            { title: "Edit", command: [ "edit", "destroy" ], width: 250,
             attributes: {
               style: "text-align: center;"
             }
            }
          ]
        });
      });
    </script>
```
