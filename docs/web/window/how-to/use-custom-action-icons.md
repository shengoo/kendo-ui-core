---
title: Use custom action icons
page_title: Use custom action icons
description: Use custom action icons
---

# Use custom action icons

The example below demonstrates how to use custom icons for the Window's action buttons

#### Example:

```html
    <style>
      html
      {
        font: 12px sans-serif;
      }

      #splitter
      {
        border-width: 0;
        height: 100%;
      }

      #win
      {
        padding: 0;
        overflow: hidden;
      }
    </style>
    <div id="win">
      <div id="splitter">
        <div>left pane <br /><br />
          Please resize the Window and watch the Splitter resize automatically.</div>
        <div>right pane</div>
      </div>
    </div>
    <script>
      $("#win").kendoWindow({
        title: "Kendo UI Window",
        modal: true,
        width: 400,
        height: 250
      }).data("kendoWindow").center();

      $("#splitter").kendoSplitter({
        panes: [{},{}]
      });
    </script>
```