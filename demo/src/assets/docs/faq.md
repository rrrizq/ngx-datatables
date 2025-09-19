> Deprecation of "Angular way" usag> 'Warning: Unable to fully load <project> for sourcemap flattening; ENOENT: no such file or directory*'

This has been fixed in newer versions of `ngx-datatables`. Make sure you're using the latest version of the library.
This was done to address few issues:

1. The usage of `*ngFor` and setting AJAX callback's `data` property as empty, we're essentially tricking the library to consider "non-existent" data. (non-existent because AJAX callback is called with empty array and totalRecords* values don't match)

2. It breaks DT extensions that perform additional data processing like exporting tabular data to a PDF or CSV, etc.

We have introduced better ways to allow same level of control over rendering your data via [TemplateRef](https://rrrizq.github.io/ngx-datatables/#/advanced/using-template-ref) and [Pipes](https://rrrizq.github.io/ngx-datatables/#/advanced/using-pipe)

> Error encountered resolving symbol values statically.

Please update your `tsconfig.json` as shown below:

```json
{
  "compilerOptions": {
    ...
    "paths": {
      "@angular/*": [
        "../node_modules/@angular/*"
      ]
    }
  }
}
```

> Columns do not resize when using ColReorder extension

This is a known limitation when using ColReorder with Angular. If you encounter this issue, please check the GitHub repository for community solutions and workarounds. 

> Column data doesn't move with column header when re-ordering

This could be because you're using "Angular way" to display data. Check the documentation for proper data binding patterns when using column reordering features. 

> 'Warning: Unable to fully load <project> for sourcemap flattening; ENOENT: no such file or directory* '

This has been fixed in newer version of `ngx-datatables`. You can find latest releases for your project's Angular version on [Releases](https://github.com/rrrizq/ngx-datatables/releases) page.

> 'DataTables warning: table id=xx - Cannot reinitialise DataTable. For more information about this error, please see http://datatables.net/tn/3*'

This error occurs when you're trying to change `dtOptions` on a table which has been previously initialised by DataTables.
If you're using a shared table component, just call `destroy()` method on `ngOnDestroy` of the component.
If you're using DataTables v1.10.4 or later, you can add `destroy: true` to `dtOptions` when initialising the table to let the table be destroyed automatically when new changes arrive. 

> 'DataTables warning (table id = x): Requested unknown parameter y from the data source for row z* http://datatables.net/tn/4' or similar

This usually occurs when your `dtOptions` are configured incorrectly. Make sure your AJAX response matches to our AJAX example [here](http://localhost:4200/#/basic/with-ajax). 
We highly recommend checking out DataTables.net [documentation](https://datatables.net/manual/tech-notes/4) on this issue for more troubleshooting information. 

> Blank screen when using `visible: true` on TemplateRef or Pipes

