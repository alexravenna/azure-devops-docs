<p></p>

### Events

| Event          | Event description    | Argument | Argument description     |
|----------------|----------------------|----------|--------------------------|
| `onFieldChanged` | Fired after a field has changed. If the field change ran rules that updated other fields, all these changes are part of a single event.          | ID       | The ID of the work item |
| `changedFields`  | Array with the reference name of all changed fields.       | ID         | The ID of the work item   |
| `onLoaded`       | Fired after the data gets loaded in the work item form, when the user opens a work item, or when the user navigates to another work item in the triage view.      | ID       | The ID of the work item |
| `onReset`        | Fired after the user undoes the changes to the work item.    | ID         | The ID of the work item   |
| `onRefreshed`    | Fired after the user refreshes the work item manually.       | ID       | The ID of the work item |
| `onSaved`        | Fired after a work item is saved. For work items in a dialog, you should target the `ms.vss-work-web.work-item-notifications` type to ensure the event fires since once the dialog closes, this contribution type gets unloaded. For more information, see [Listen for events](#listenforevents). | ID       | The ID of the work item  |
| `onUnloaded`     | Fired before the user closes the dialog, or before the user moves to another work item in the triage view.   | ID       | The ID of the work item  |
